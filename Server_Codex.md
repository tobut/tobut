# VSCode Remote-SSH 使用 Codex：服务器 B 复用电脑 A 的 VPN

> **适用场景**：在 Windows 电脑 A 上运行 VPN，通过 VSCode Remote-SSH 开发 Linux 服务器 B 上的项目；希望 **Codex 在 B 上运行，但不在 B 上安装 VPN**。
>
> **方案**：SSH 反向端口转发 + VSCode 远程代理设置 + Codex 专用代理配置。以下是本次已成功使用的配置。

## 1. 环境与工作原理

| 项目 | 地址 / 配置 |
| --- | --- |
| 电脑 A（Windows） | `10.96.113.54`；VPN 混合代理为 `127.0.0.1:7369` |
| 服务器 B（Linux） | `10.96.71.58`；SSH 用户 `yagao`，端口 `1133` |
| SSH 私钥（A 上） | `C:\Users\admin\.ssh\keys\id_rsa_A6000` |
| B 上映射后的代理 | `127.0.0.1:17369` |

```text
B：Codex / VSCode 扩展
    ↓ 请求交给 http://127.0.0.1:17369
B：SSH 反向转发端口 17369
    ↓ 已建立的 SSH 连接
A：VPN 代理 127.0.0.1:7369
    ↓
OpenAI 服务
```

**要点**：B 只需连接自己本机的 `17369`，流量经 SSH 到 A 的 `7369`。无需在 B 安装 VPN，也无需把 A 的 VPN 代理开放给局域网。A 的 VPN 与 SSH 隧道必须保持运行。

## 2. 电脑 A：配置 SSH 反向转发

编辑 Windows 文件 `C:\Users\admin\.ssh\config`：

```sshconfig
Host 10.96.71.58
    HostName 10.96.71.58
    User yagao
    Port 1133
    IdentityFile C:/Users/admin/.ssh/keys/id_rsa_A6000

    RemoteForward 127.0.0.1:17369 127.0.0.1:7369
    ServerAliveInterval 60
    ServerAliveCountMax 3
```

- **`RemoteForward`**：让 B 的 `127.0.0.1:17369` 指向 A 的 `127.0.0.1:7369`，这是核心配置。
- **`ServerAliveInterval` / `ServerAliveCountMax`**：空闲时发送 SSH 心跳并检测失效；**不会自动重连**。

保存后，用 VSCode 的 **Remote-SSH** 重新连接 `10.96.71.58`，让配置生效。

## 3. 服务器 B：验证代理可达

在 VSCode **远程终端（B）** 依次执行：

```bash
# 验证 OpenAI API
curl -I -x http://127.0.0.1:17369 \
  https://api.openai.com/v1/models

# 验证 Codex 登录服务
curl -I -x http://127.0.0.1:17369 \
  https://auth.openai.com/oauth/token
```

本次已验证的响应：

| 接口 | 常见响应 | 含义 |
| --- | --- | --- |
| `api.openai.com/v1/models` | `HTTP 401` | 无 API Key，服务已响应；代理链路正常 |
| `auth.openai.com/oauth/token` | `200 Connection established`，随后 `HTTP 405` | HTTPS 隧道成功；接口不接受 `curl -I` 的 HEAD 请求 |

**注意**：这只证明 `curl` 经代理可以访问，**不代表 Codex 进程已经使用代理**。若看到 Snap 版 curl 的提示，通常与本次连通性验证无关。

## 4. 服务器 B：配置 Codex 代理（登录成功的关键）

在 B 的远程终端执行：

```bash
mkdir -p ~/.codex
nano ~/.codex/.env
```

填入以下内容（如文件已存在，请合并，不要覆盖其他配置）：

```dotenv
HTTP_PROXY=http://127.0.0.1:17369
HTTPS_PROXY=http://127.0.0.1:17369
ALL_PROXY=http://127.0.0.1:17369
NO_PROXY=localhost,127.0.0.1,::1

http_proxy=http://127.0.0.1:17369
https_proxy=http://127.0.0.1:17369
all_proxy=http://127.0.0.1:17369
no_proxy=localhost,127.0.0.1,::1
```

在 `nano` 中按 `Ctrl + O` → 回车保存，`Ctrl + X` 退出。

**注意**：
- 在 B 上填 `17369`，**不要**误填 A 的 `7369`。
- 即使访问 `https://` 网站，HTTP 代理地址仍使用 `http://127.0.0.1:17369`（通过 CONNECT 建立 HTTPS 通道）。
- `NO_PROXY` 与 VSCode 的 `http.noProxy` 属于不同配置，建议都保留。
- 若自定义了 `CODEX_HOME`，应检查 Codex 实际读取的 `.env` 位置。

然后**关闭并重新建立 VSCode Remote-SSH 会话**，确认 Codex 扩展安装、运行在预期的远程环境，打开 Codex 并选择 **Sign in with ChatGPT**。本次添加 `.env` 后已成功登录。

## 5. 服务器 B：配置 VSCode 远程代理 (不必要)

VSCode 已连接 B 时，按 `Ctrl + Shift + P` → **Preferences: Open Remote Settings (JSON)**。将以下字段**合并**到原有 JSON：

```json
{
    "http.useLocalProxyConfiguration": false,
    "http.proxy": "http://127.0.0.1:17369",
    "http.proxySupport": "on",
    "http.noProxy": [
        "localhost",
        "127.0.0.1",
        "::1"
    ]
}
```

**建议保留 `http.noProxy`**：让遵循 VSCode 此设置的请求在访问本机地址 `localhost`、`127.0.0.1`、`::1` 时直连，避免把本地服务流量送进代理。这些是**目标地址排除规则**，**不会因为代理服务器本身是 `127.0.0.1:17369`，就让访问 OpenAI 的请求绕过代理**。

> VSCode 的 `http.proxy` 不保证被 Codex 内部网络进程继承，因此还需要下一步。

## 6. 快速排错

| 症状 | 优先处理 |
| --- | --- |
| B 访问 `127.0.0.1:17369` 被拒绝 | 检查 A 的 VPN、SSH 是否重连、`RemoteForward` 是否生效、B 端口是否被占用 |
| `curl -x` 正常，但 `token_exchange_failed` | 检查 B 的 `~/.codex/.env`、代理端口与 Codex 实际运行位置；重新启动扩展/远程会话 |
| `Codex could not start its user interface` | 这是界面启动问题，不等于代理失败；查看 VSCode **Output → Codex** 日志，并检查扩展版本兼容性 |
| VPN / SSH 中断后 Codex 失去连接 | 恢复 A 的 VPN 并重新建立 SSH 连接；心跳配置不会自动重连 |
| 多个 SSH 连接抢占 B 的 `17369` | 使用下方的独立隧道方案，避免重复转发 |

**可选：独立 SSH 隧道。** 若 VSCode 多条 SSH 连接争用相同端口，先从 SSH config 中注释 `RemoteForward`，再在 **A 的 PowerShell** 运行并保持窗口打开：

```powershell
ssh -N -o ExitOnForwardFailure=yes -R 127.0.0.1:17369:127.0.0.1:7369 10.96.71.58
```

此时用 VSCode 正常连接 B；独立 SSH 进程负责隧道，不要再由 VSCode 重复占用 `17369`。

## 7. 最简复用清单

- [ ] A 的 VPN 代理运行于 `127.0.0.1:7369`
- [ ] A 的 SSH config 配置 `RemoteForward 127.0.0.1:17369 127.0.0.1:7369`
- [ ] VSCode Remote-SSH 重新连接 B
- [ ] B 的 `~/.codex/.env` 已配置代理与 `NO_PROXY`
- [ ] 重启远程会话，使用 Codex 登录并测试项目

**一句话总结**：通过 `RemoteForward` 把 **A 的 VPN 代理映射到 B 的本机 17369**，再分别告诉 **VSCode** 和 **Codex** 使用它；本机地址通过 `http.noProxy` / `NO_PROXY` 保持直连。

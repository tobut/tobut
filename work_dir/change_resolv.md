# 修改resolv.conf指南

## 位置
```bash
/etc/resolv.conf
```

## 保存备份
cp /etc/resolv.conf /etc/resolv_bak.conf

## 使用vim编辑
```bash
vim /etc/resolv.conf
```

## 忽略警告
```bash
(E)dit anyway
```

## 删除当前光标处的字符指令
```bash
x
```

## 在当前光标处插入字符指令
```bash
i
```

## 保存并退出指令
```bash
:wq
```

## 修改内容
将内容修改为：
```bash
114.114.114.114
```
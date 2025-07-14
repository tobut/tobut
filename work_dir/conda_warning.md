# conda problem

## 清理损坏包
遇到问题：
```
WARNING conda.gateways.disk.delete:unlink_or_rename_to_trash(140): Could not remove or rename 
```
通过清理破损包进行处理
```bash
conda clean --packages --tarballs
```
清理后更新
```bash
conda update --all
```

## Powershell 无法启动conda环境
以管理员身份运行
```
Set-ExecutionPolicy RemoteSigned
```

# scp命令
## scp从本地传输到服务器
传输文件
```bash
scp /path/to/local/file user@remote:/path/to/destination
```
传输文件夹
```bash
scp -r /path/to/local/folder user@remote:/path/to/destination
```

## scp从服务器传输到本地
传输文件
```bash
scp user@remote:/path/to/remote/file /path/to/destination
```
传输文件夹
```bash
scp -r user@remote:/path/to/destination /path/to/local/folder
```

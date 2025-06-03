# 创建新用户指南

## 获取权限
```bash
sudo su
```

## 创建新用户（包含家目录）
```bash
useradd -m new_user_name
```

## 为新用户设置密码
```bash
passwd new_user_name
```

## 指定新用户的解释程序为bash
```bash
usermod -s /bin/bash new_user_name
```

## 指定新用户的用户主目录
```bash
usermod -d /home/new_user_name new_user_name
```

## 将新用户添加到sudo列表
```bash
usermod -a -G sudo new_user_name
```

## 查看sudo用户列表
```bash
cat /etc/passwd
```

## 查看用户列表
```bash
sudo cat /etc/sudoers
```

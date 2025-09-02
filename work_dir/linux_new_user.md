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

## 创建远程密钥
```bash
sudo apt-get install openssh-server
```
```bash
ssh-keygen
```
```bash
cat ~/.ssh/id_rsa.pub >> ~/.ssh/authorized_keys
```
```bash
chmod 700 ~/.ssh
```
```bash
chmod 600 ~/.ssh/authorized_keys
```
```bash
cp ~/.ssh/id_rsa ../Downloads
```

参考链接：[https://blog.csdn.net/tyustli/article/details/122222605](https://blog.csdn.net/tyustli/article/details/122222605)

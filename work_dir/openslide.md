# openslide安装指南


## 安装过程
### 安装openslide-tools
```bash
apt-get install openslide-tools
```
### 安装python-openslide
```bash
apt-get install python-openslide
```

### 安装openslide-python
```bash
pip install openslide-python
```


## 链接问题
遇到如下问题：
```
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
ImportError: /lib/x86_64-linux-gnu/libgobject-2.0.so.0: undefined symbol: ffi_type_uint32, version LIBFFI_BASE_7.0
```
有的时候需要：
```bash
export LD_PRELOAD=/usr/lib/x86_64-linux-gnu/libffi.so.7
```
现在可以正常调用openslide



## 当apt无法正常使用时，使用如下方式换成国内源
### 保存备份
```bash
cp /etc/apt/sources.list /etc/apt/sources.list.bak
```

### 开始编辑
```bash
vim /etc/apt/sources.list
```

### 编辑指令
#### 删除当前光标到最后的所有字符
```bash
dG
```
#### 鼠标粘贴新链接文本

#### 保存退出
```bash
:wq
```
#### 保存后更新
```bash
apt-get update
```

```
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic main restricted universe multiverse
deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic main restricted universe multiverse
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic-updates main restricted universe multiverse
deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic-updates main restricted universe multiverse
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic-backports main restricted universe multiverse
deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic-backports main restricted universe multiverse
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic-security main restricted universe multiverse
deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic-security main restricted universe multiverse
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic-proposed main restricted universe multiverse
deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic-proposed main restricted universe multiverse

deb http://mirrors.aliyun.com/ubuntu/ bionic main restricted universe multiverse
deb http://mirrors.aliyun.com/ubuntu/ bionic-security main restricted universe multiverse
deb http://mirrors.aliyun.com/ubuntu/ bionic-updates main restricted universe multiverse
deb http://mirrors.aliyun.com/ubuntu/ bionic-proposed main restricted universe multiverse
deb http://mirrors.aliyun.com/ubuntu/ bionic-backports main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ bionic main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ bionic-security main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ bionic-updates main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ bionic-proposed main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ bionic-backports main restricted universe multiverse 
```
## apt-get Worning
解决警告：'Key is stored in legacy trusted.gpg keyring'
'''bash
sudo cp /etc/apt/trusted.gpg /etc/apt/trusted.gpg.d
'''

## 参考博客链接
安装openslide：[https://blog.csdn.net/qq_40678911/article/details/122367158#:~:text=Unable%20to](https://blog.csdn.net/qq_40678911/article/details/122367158#:~:text=Unable%20to) <br/>
vim指令大全：[https://zhuanlan.zhihu.com/p/61515833](https://zhuanlan.zhihu.com/p/61515833)
apt-get更换国内源出现Err：[https://blog.csdn.net/weixin_45784720/article/details/119298722](https://blog.csdn.net/weixin_45784720/article/details/119298722)

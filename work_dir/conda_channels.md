# conda配置清华源

## 查看当前源
```bash
conda config --show channels
```

## 删除添加源，回复默认源
```bash
conda config --remove-key channels
```

## 添加清华镜像源
```bash
#添加镜像源
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/main
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/r
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/pro
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/msys2
```

## 终端显示包从哪个channel下载，以及下载地址是什么
```bash
conda config --set show_channel_urls yes
```

## pip从特定源安装库的方法
```bash
pip install some-package -i https://pypi.tuna.tsinghua.edu.cn/simple
```

## 附带国内常用源
```
清华大学开源软件镜像站：https://pypi.tuna.tsinghua.edu.cn/simple
阿里云开源镜像站：https://mirrors.aliyun.com/pypi/simple/
豆瓣：https://pypi.douban.com/simple/
中国科技大学 https://pypi.mirrors.ustc.edu.cn/simple/
```

## 本篇参考CSDN：
网址链接：[CSDN](https://blog.csdn.net/weixin_44914727/article/details/130513081)
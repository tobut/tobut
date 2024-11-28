# opencv问题汇总

## 链接问题
遇到某些文件无法打开如下：
```
File "/usr/local/lib/python3.6/dist-packages/cv2/__init__.py", line 8, in <module>
    from .cv2 import *
ImportError: libGL.so.1: cannot open shared object file: No such file or directory
```

安装库即可解决
```bash
pip install opencv-python-headless
```

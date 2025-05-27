# nvidia-smi正常运行，但是nvcc -V失效

## 查看cuda目录下是否有nvcc
'''bash
cd /usr/local/cuda/bin
'''

## 如果有nvcc，直接将cuda路径加入系统路径
'''bash
vim ~/.bashrc
'''

## 添加以下两行
在/.bashrc中配置LD_LIBRARY_PATH路径、配置PATH路径，完整配置如下:
'''bash
export LD_LIBRARY_PATH=/usr/local/cuda/lib
export PATH=$PATH:/usr/local/cuda/bin
'''

## 更新配置文件
'''bash
source ~/.bashrc
'''

## 再次执行nvcc -V查看对应cuda版本
'''bash
nvcc -V
'''

# 关于两个CUDA版本的解释：
使用nvidia-smi命令查看CUDA版本为11.4，nvcc -V命令查看CUDA版本为11.1。以nvcc -V版本为准。
nvidia-smi对应的时driver api，nvcc -V对应的是runtime api。

# 参考文件
[https://blog.csdn.net/weixin_44750512/article/details/123156020](https://blog.csdn.net/weixin_44750512/article/details/123156020)

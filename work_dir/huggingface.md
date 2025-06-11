# 安装官方命令行工具
```cmd
pip install -U huggingface_hub
```

# 使用token登陆账户
```cmd
huggingface-cli login
```
然后输入token，回车，y，回车

# 使用命令行进行下载
```cmd
huggingface-cli download --resume-download meta-llama/Llama-2-13b-chat-hf
```

```cmd
huggingface-cli download --resume-download meta-llama/Llama-2-13b-chat-hf --local-dir Llama-2-13b-chat-hf
```


##参考文件
[https://blog.csdn.net/lanlinjnc/article/details/136709225](https://blog.csdn.net/lanlinjnc/article/details/136709225)

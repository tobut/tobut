# pytorch安装指南与使用问题

## pytorch安装指南官网地址

### 最新地址
[https://pytorch.org/get-started/locally/](https://pytorch.org/get-started/locally/)


### 旧版本地址
[https://pytorch.org/get-started/previous-versions/](https://pytorch.org/get-started/previous-versions/)


## pytorch problems

### _LinearWithBias
在torch>1.10版本之后以下指令失效
```python
from torch.nn.modules.linear import _LinearWithBias
```

应修改为如下方式
```python
from torch.nn.modules.linear import NonDynamicallyQuantizableLinear as _LinearWithBias
```


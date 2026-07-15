# git稀疏拉取
## 初始稀疏化克隆
```bash
git clone --filter=blob:none --sparse <repository_url>
```
```bash
cd <repository_name>
```

## 稀疏化下载
```bash
git sparse-checkout set <file_path>
```

## 稀疏化上传
```bash
git sparse-checkout add <file_path>
```

示例
```bash
git clone --filter=blob:none --sparse https://github.com/bytedance/deer-flow.git
cd .\deer-flow\
git sparse-checkout set skills/public/systematic-literature-review
```

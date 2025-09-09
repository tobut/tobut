# zip命令
```bash
zip [options] output.zip file1 file2 ...
```
output.zip：生成的压缩文件名。
file1 file2 ...：要压缩的文件或目录。

## 常用指令
压缩文件夹
```bash
zip -r folder.zip folder
```

压缩多个文件
```bash
zip folder.zip file1 file2 file3
```

## 详细参数
-r：递归压缩目录及其子目录中的所有文件。
-e：为压缩文件设置密码保护。
-q：静默模式，不显示压缩过程。
-v：显示详细的压缩过程。
-x：排除某些文件或目录，不进行压缩。
-m：压缩后删除原始文件。
-0 到 -9：指定压缩级别，-0 表示存储不压缩，-9 表示最高压缩率，默认是 -6。


# unzip命令
```bash
unzip [options] folder.zip
```

## 常用指令
直接解压缩
```bash
unzip folder.zip
```

静默解压缩到指定文件夹
```bash
unzip -q folder.zip path/to/target/folder
```

## 详细参数
-d <directory>：将解压缩的文件放入指定的目录。
-q: 静默状态，不显示输出
-l: 列出 .zip 文件中的内容，但不解压。
-v: 显示详细信息，包括 .zip 文件的结构和压缩率等信息。
-t: 测试 .zip 文件的完整性，但不解压。
-n: 解压时不覆盖已存在的文件。
-o: 解压时覆盖已存在的文件，而不提示。
-x <pattern>：解压时排除指定的文件或目录。
-j: 解压时不保留目录结构，将所有文件解压到当前目录中。

# 参考链接
[https://www.runoob.com/linux/linux-comm-zip.html](https://www.runoob.com/linux/linux-comm-zip.html)
[https://www.runoob.com/linux/linux-comm-unzip.html](https://www.runoob.com/linux/linux-comm-unzip.html)

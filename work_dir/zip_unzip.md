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


# tar命令
-c: 建立压缩档案
-x：解压
-t：查看内容
-r：向压缩归档文件末尾追加文件
-u：更新原压缩包中的文件

这五个是独立的命令，压缩解压都要用到其中一个，可以和别的命令连用但只能用其中一个。下面的参数是根据需要在压缩或解压档案时可选的。

-z：有gzip属性的
-j：有bz2属性的
-Z：有compress属性的
-v：显示所有过程
-O：将文件解开到标准输出

下面的参数-f是必须的

-f: 使用档案名字，切记，这个参数是最后一个参数，后面只能接档案名。

## 常用指令
```bash
tar -cf all.tar *.jpg
```
这条命令是将所有.jpg的文件打成一个名为all.tar的包。-c是表示产生新的包，-f指定包的文件名。

```bash
tar -rf all.tar *.gif
```
这条命令是将所有.gif的文件增加到all.tar的包里面去。-r是表示增加文件的意思。

```bash
tar -uf all.tar logo.gif
```
这条命令是更新原来tar包all.tar中logo.gif文件，-u是表示更新文件的意思。

```bash
tar -tf all.tar
```
这条命令是列出all.tar包中所有文件，-t是列出文件的意思

```bash
tar -xf all.tar
```
这条命令是解出all.tar包中所有文件，-x是解开的意思


# tar压缩
```bash
tar –cvf jpg.tar *.jpg
```
将目录里所有jpg文件打包成tar.jpg

```bash
tar –czf jpg.tar.gz *.jpg
```
将目录里所有jpg文件打包成jpg.tar后，并且将其用gzip压缩，生成一个gzip压缩过的包，命名为jpg.tar.gz
```bash
tar –cjf jpg.tar.bz2 *.jpg
```
将目录里所有jpg文件打包成jpg.tar后，并且将其用bzip2压缩，生成一个bzip2压缩过的包，命名为jpg.tar.bz2

```bash
tar –cZf jpg.tar.Z *.jpg
```
将目录里所有jpg文件打包成jpg.tar后，并且将其用compress压缩，生成一个umcompress压缩过的包，命名为jpg.tar.Z

```bash
rar a jpg.rar *.jpg
```
rar格式的压缩，需要先下载rar for linux

```bash
zip jpg.zip *.jpg
```
zip格式的压缩，需要先下载zip for linux

# tar解压缩
```bash
tar –xvf file.tar
```
解压 tar包
```bash
tar -xzvf file.tar.gz
```
解压tar.gz

```bash
tar -xjvf file.tar.bz2
```
解压 tar.bz2

```bash
tar –xZvf file.tar.Z
```
解压tar.Z

```bash
unrar e file.rar
```
解压rar

```bash
unzip file.zip
```
解压zip

总结

*.tar 用 tar –xvf 解压
*.gz 用 gzip -d或者gunzip 解压
*.tar.gz和*.tgz 用 tar –xzf 解压
*.bz2 用 bzip2 -d或者用bunzip2 解压
*.tar.bz2用tar –xjf 解压
*.Z 用 uncompress 解压
*.tar.Z 用tar –xZf 解压
*.rar 用 unrar e解压
*.zip 用 unzip 解压

# 参考链接
[https://www.runoob.com/linux/linux-comm-zip.html](https://www.runoob.com/linux/linux-comm-zip.html)
[https://www.runoob.com/linux/linux-comm-unzip.html](https://www.runoob.com/linux/linux-comm-unzip.html)
[https://blog.csdn.net/imyang2007/article/details/7634470](https://blog.csdn.net/imyang2007/article/details/7634470)

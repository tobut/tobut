## TMI模板报错

### ieeeecolor问题
```bash
You have requested document class ieeecolor
```
修改方法，到ieeecolor.cls中将\ProvidesClass{IEEEtran}改成\ProvidesClass{ieeecolor}

#### 参考教程
[https://blog.csdn.net/qq_43037367/article/details/146552313](https://blog.csdn.net/qq_43037367/article/details/146552313)

### 正文意外变成蓝色
修改方法，将一下内容粘贴到\documentclass[journal,twoside,web]{ieeecolor}与\usepackage{...}之间即可。
```bash
% Fix ieeecolor caption
\usepackage{etoolbox}
\makeatletter
\@ifundefined{color@begingroup}%
{\let\color@begingroup\relax
\let\color@endgroup\relax}{}%
\def\fix@ieeecolor@hbox#1{%
 \hbox{\color@begingroup#1\color@endgroup}}
\patchcmd\@makecaption{\hbox}{\fix@ieeecolor@hbox}{}{\FAILED}
\patchcmd\@makecaption{\hbox}{\fix@ieeecolor@hbox}{}{\FAILED}
```

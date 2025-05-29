

## 安装教程
[https://blog.csdn.net/Luan__Yu/article/details/143562703](https://blog.csdn.net/Luan__Yu/article/details/143562703)

## 配置vscode

'''bash
{
    //------------------------------LaTeX 配置----------------------------------
    // 设置是否自动编译
    "latex-workshop.latex.autoBuild.run": "never",
    //右键菜单
    "latex-workshop.showContextMenu": true,
    //从使用的包中自动补全命令和环境
    "latex-workshop.intellisense.package.enabled": true,
    //编译出错时设置是否弹出气泡设置
    "latex-workshop.message.error.show": false,
    "latex-workshop.message.warning.show": false,
    // 编译工具和命令
    "latex-workshop.latex.tools": [
        {
            "name": "xelatex",
            "command": "xelatex",
            "args": [
                "-synctex=1",
                "-interaction=nonstopmode",
                "-file-line-error",
                "%DOCFILE%"
            ]
        },
        {
            "name": "pdflatex",
            "command": "pdflatex",
            "args": [
                "-synctex=1",
                "-interaction=nonstopmode",
                "-file-line-error",
                "%DOCFILE%"
            ]
        },
        {
            "name": "latexmk",
            "command": "latexmk",
            "args": [
                "-synctex=1",
                "-interaction=nonstopmode",
                "-file-line-error",
                "-pdf",
                "-outdir=%OUTDIR%",
                "%DOC%"
            ],
            "env": {}
        },
        {
            "name": "lualatex",
            "command": "lualatex",
            "args": [
                "-synctex=1",
                "-interaction=nonstopmode",
                "-file-line-error",
                "-shell-escape", //这个命令行在网上的Latex Workshop设置里一般没有，所以直接recipe会报错
                "%DOCFILE%"
            ]
        },
        {
            "name": "bibtex",
            "command": "bibtex",
            "args": [
                "%DOCFILE%"
            ]
        },
        {
            "name": "biber",
            "command": "biber",
            "args": [
                "%DOCFILE%"
            ]
        }
    ],
    // 用于配置编译链
    "latex-workshop.latex.recipes": [
        {
            "name": "xelatex -> bibtex -> xelatex*2",
            "tools": [
                "xelatex",
                "bibtex",
                "xelatex",
                "xelatex"
            ]
        },
        {
            "name": "XeLaTeX",
            "tools": [
                "xelatex"
            ]
        },
        {
            "name": "PDFLaTeX",
            "tools": [
                "pdflatex"
            ]
        },
        // {
        //     "name": "LuaLaTeX",
        //     "tools": [
        //         "lualatex"
        //     ]
        // },
        // {
        //     "name": "BibTeX",
        //     "tools": [
        //         "bibtex"
        //     ]
        // },
        // {
        //     "name": "LaTeXmk",
        //     "tools": [
        //         "latexmk"
        //     ]
        // },
        {
            "name": "xelatex -> biber -> xelatex*2",
            "tools": [
                "xelatex",
                "biber",
                "xelatex",
                "xelatex"
            ]
        },
        {
            "name": "pdflatex -> bibtex -> pdflatex*2",
            "tools": [
                "pdflatex",
                "bibtex",
                "pdflatex",
                "pdflatex"
            ]
        },
        // {
        //     "name": "pdflatex -> biber -> pdflatex*2",
        //     "tools": [
        //         "pdflatex",
        //         "biber",
        //         "pdflatex",
        //         "pdflatex"
        //     ]
        // }
    ],
    
    //文件清理。此属性必须是字符串数组
    "latex-workshop.latex.clean.fileTypes": 
    [
        "*.aux",//包含有关文档交叉引用、标签和参考文献等信息
        "*.bbl",//用于管理文献引用和参考文献列表
        "*.blg",
        "*.idx",
        "*.ind",
        "*.lof",//插图目录
        "*.lot",
        "*.out",
        "*.toc",//目录
        "*.acn",
        "*.acr",
        "*.alg",
        "*.glg",
        "*.glo",
        "*.gls",
        "*.ist",
        "*.fls",
        "*.log",
        "*.fdb_latexmk",
    ],
//设置为onFaild 在构建失败后清除辅助文件
    "latex-workshop.latex.autoClean.run": "onFailed",
    // 使用上次的recipe编译组合
    "latex-workshop.latex.recipe.default": "lastUsed",
    //使用 SumatraPDF 预览编译好的PDF文件
    // 设置VScode内部查看生成的pdf文件
    "latex-workshop.view.pdf.viewer": "tab",
    // PDF查看器用于在\ref上的[View on PDF]链接
    "latex-workshop.view.pdf.ref.viewer": "auto",
    "latex-workshop.synctex.indicator":"circle",//正向搜索显示
    "latex-workshop.view.pdf.internal.synctex.keybinding": "double-click", //双击反向搜索
    "editor.wordWrap": "on",
    "editor.renderControlCharacters": false,
    "security.workspace.trust.untrustedFiles": "newWindow", // 
    "files.autoSave": "afterDelay",// 自动保存
 }
'''

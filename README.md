# NOTE_Microwave
LaTeX Note of Microwave, EM Field and Antenna

## 关于笔记内容
前4章和后3章主要来自本科课程《微波技术基础》和《天线原理》的自学整理，对应教材为梁昌洪的《简明微波》和魏文元的《天线原理》。

之后会在学习 *Microwave Engineering* by *David M. Pozar* 和 *RF Circuit Design* by *Richard Chi-Hsi Li* 后陆续补充尚未完成的内容。
## 关于工程树结构
这是一个使用VS Code扩展LaTeX Workshop开发的LaTeX工程。
- `./.vscode`是VS Code工作区配置文件所在目录，其中的`characters.code-snippets`是用户自定义的局部代码片段。
- `./build`是扩展配置中`"latex-workshop.latex.outDir"`一项所指定的工程输出目录。包含了中间件和PDF输出。
- `./figure`是手动存放所引用的图片的目录。
- TeX源文件全部位于根目录下。其中`nexus.sty`是开源的LaTeX Style库文件。
## 如何编译此工程
先安装TexLive2021及以上版本。然后安装VS Code和扩展LaTeX Workshop，将以下JSON设置粘贴到VS Code工作区或全局用户设置中：

```json
    "latex-workshop.latex.outDir": "%DIR%/build",
    "latex-workshop.latex.tools": [
        {
            "name": "xelatex",
            "command": "xelatex",
            "args": [
                "-synctex=1",
                "-interaction=nonstopmode",
                "-file-line-error",
                "-pdf",
                "--output-directory=%OUTDIR%",
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
            "name": "makeindex",
            "command": "makeindex",
            "args": [
                "%DOCFILE%.nlo",
                "-s",
                "nomencl.ist",
                "-o",
                "%DOCFILE%.nls"
            ]
        },
        {
            "name": "biber",
            "command": "biber",
            "args": [
                "%DOCFILE%"
            ]
        },
        {
            "name": "bibtex",
            "command": "bibtex",
            "args": [
                "%DOCFILE%"
            ]
        }
    ],
    "latex-workshop.latex.recipes": [
        {
            "name": "xelatex🔃",
            "tools": [
                "xelatex"
            ]
        },
        {
            "name": "xe->mkind->bib->xe*2🔃",
            "tools": [
                "xelatex",
                "makeindex",
                "biber",
                "xelatex",
                "xelatex"
            ]
        },
        {
            "name": "pdf->mkind->bib->pdf*2🔃",
            "tools": [
                "pdflatex",
                "makeindex",
                "biber",
                "pdflatex",
                "pdflatex"
            ]
        },
        {
            "name": "xe->bib->xe->xe🔃",
            "tools": [
                "xelatex",
                "bibtex",
                "xelatex",
                "xelatex"
            ]
        },
        {
            "name": "biber🔃",
            "tools": [
                "biber"
            ]
        },
        {
            "name": "pdflatex🔃",
            "tools": [
                "pdflatex"
            ]
        },
        {
            "name": "pdf->bib->pdf->pdf🔃",
            "tools": [
                "pdflatex",
                "bibtex",
                "pdflatex",
                "pdflatex"
            ]
        },
        {
            "name": "BibTeX🔃",
            "tools": [
                "bibtex"
            ]
        }
    ],
    "latex-workshop.view.pdf.viewer": "external",
    "latex-workshop.view.pdf.ref.viewer":"external", 
    "latex-workshop.showContextMenu":true,
    "latex-workshop.view.pdf.external.viewer.command": "C:/Program Files/SumatraPDF/SumatraPDF.exe", 
    "latex-workshop.view.pdf.external.viewer.args": [
        "%PDF%"
    ],
    "latex-workshop.view.pdf.external.synctex.command": "C:/Program Files/SumatraPDF/SumatraPDF.exe", 
    "latex-workshop.view.pdf.external.synctex.args": [
        "-forward-search",
        "%TEX%",
        "%LINE%",
        "%PDF%"
    ],
    "latex-workshop.latex.recipe.default": "lastUsed",
    "latex-workshop.synctex.synctexjs.enabled": false,
    "latex-workshop.synctex.afterBuild.enabled": true,
```
注意，这份配置中包含了联动 *SumatraPDF* 实现正向搜索的功能，这不是必须的，如果需要，请更改`SumatraPDF.exe`的路径。

程序入口在`Microwave.tex`中。按F5编译。如果您没有为所有用户安装PingFang SC Regular字体，编译会因为找不到字体文件报错。您也可以选择删除这一行

```latex
\setCJKmainfont{PingFang Regular.ttf} %设置 CJK 主字体为 PingFang Regular （苹方）
```
这意味着将使用ctex默认的字体（通常为simsun）。

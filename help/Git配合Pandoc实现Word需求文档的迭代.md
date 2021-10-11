目录

    1 方案简介
        [1.1 背景](#1.1 背景)
        1.2 Pandoc
        1.3 解决方案
    2 Pandoc安装
        2.1 Windows版本安装
        2.2 macOS版本安装
    3 Pandoc设置
    4 提交脚本安装

# 1 方案简介
## 1.1 背景

    Git在提交Word时，对于Word的变动显示并不友好
    在查看历史版本或者远端仓库时，Word文档的显示可能为“二进制文件不可显示”，根本无法查看变动
    Git对Word的支持并不完善

## 1.2 Pandoc

    Pandoc可以将Word文档转换成其他类型的文档
    支持的文档类型：
        HTML formats：XHTML, HTML5, and HTML slide shows using Slidy, reveal.js, Slideous, S5, or DZSlides
        Word processor formats：Microsoft Word docx, OpenOffice/LibreOffice ODT, OpenDocument XML, Microsoft PowerPoint
        Ebooks：EPUB version 2 or 3, FictionBook2
        Documentation formats：DocBook version 4 or 5, TEI Simple, GNU TexInfo, roff man, roff ms, Haddock markup
        Archival formats：JATS
        Page layout formats：InDesign ICML
        Outline formats：OMPL
        TeX formats：LaTeX, ConTeXt, LaTeX Beamer slides
        PDF：via pdflatex, xelatex, lualatex, pdfroff, wkhtml2pdf, prince, or weasyprint
        Lightweight markup formats：Markdown (including CommonMark and GitHub-flavored Markdown), reStructuredText, AsciiDoc, Emacs Org-Mode, Emacs Muse, Textile, txt2tags, MediaWiki markup, DokuWiki markup, TikiWiki markup, TWiki markup, Vimwiki markup, and ZimWiki markup
        Interactive notebook formats：Jupyter notebook (ipynb)

## 1.3 解决方案

    在提交Word时，在本地将Word由Pandoc转换成Markdown格式的文档
    Git在远端查看变动时，就能够通过自动生成的Markdown文件查看变动

2 Pandoc安装
2.1 Windows版本安装

    通过Pandoc官网下载Windows版本安装包
    执行安装包，安装

2.2 macOS版本安装

    打开"终端"
    使用Homebrew进行安装：

brew install pandoc
3 Pandoc设置

    设置全局配置文件gitconfig(Windows下路径"c:\Documents and Settings\user\.gitconfig"或者macOS下路径"~/.gitconfig")，在文件末尾添加如下信息：

[diff "pandoc"]
   textconv=pandoc --to=markdown
   prompt = false
[alias]
   wdiff = diff --word-diff=color --unified=1

    在项目根目录下添加或者编辑文件.gitattributes，在文件中加入如下信息:

*.docx diff=pandoc

    至此，git在进行文件对比时优先将Word文件转换为md文件然后进行对比

4 提交脚本安装

    将plugin目录下的post-commit(
    pre-commit-git-diff-docx.sh改成pre-commit)和pre-commit(post-commit-git-diff-docx.sh改成post-commit)两个文件复制到项目根目录下的.git\hooks下（macOS为.git/hooks）

附：

    集成docx文件diff程序

作者：背包客要背包
链接：https://www.jianshu.com/p/fb72861ed7a5
来源：简书
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。
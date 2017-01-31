# 编辑、预览和发布

## bookdown源码组成

bookdown的源文件由下列格式组成
- .rmd
- .yml

### .rmd文件

rmd为章节的源文件。主要包括
- index.rmd 
- 其他章节的rmd

index.rmd相当于是主页文件，bookdown在渲染的时候将index放在最前面，其他章节则默认按照数字编号排列。
因此一般章节的命名为:01-a,02-aa,...。 如果不想按照数字排列，则需要新建`_bookdown.yml`文件来指定渲染顺序
参考第\@ref(yml)小节。

index.rmd的开始可以放YMAL的数据，以`---`开始和结束。比如说

```
--- 
title: "Advanced R Solutions"   <!-- 标题. -->
author: "Malte Grosser & Henning Bumann" <!-- 作者. -->
date: "2017-01-30"   <!-- 日期. -->
knit: "bookdown::render_book" 
site: bookdown::bookdown_site <!--  RStudio will be able to discover the directory as a book source directory，在Rstudio打开project就能build了. -->
output: <!---输出格式，也可以新建一个.output.yml在.yml里设置--->
  bookdown::gitbook:
    config:
      toc:
          collapse: section
          scroll_highlight: yes
          before: null
          after: null
      edit: https://github.com/Tazinho/Advanced-R-Solutions/edit/master/%s
documentclass: book
bibliography: [packages.bib] <!--bib文件的名字. -->
biblio-style: apalike <!--文献显示的格式. -->
link-citations: yes
github-repo: Tazinho/Advanced-R-Solutions <!--github仓库的网址 -->
before_chapter_script: ["before_chapter_script_1.R"]
description: "Solutions to the exercises in Hadley Wickham's book Advanced R."
cover-image: images/advrs_cover.png   <!--封皮图像-->
---
```

### .yml {#yml}

- _bookdown.yml (可选)
- 


_bookdown.yml里的`rmd_files`可以指定渲染的顺序，比如：
```
rmd_files: ["index.RMD", "01-install_bookdown.Rmd", "03-edit-preview-publish.Rmd","02-test_syntax.rmd"]
```

_bookdown.yml还可以包含其他信息，比如
```
book_filename: "my-book.Rmd"
repo: https://github.com/rstudio/bookdown/
before_chapter_script: ["script1.R", "script2.R"]
after_chapter_script: "script3.R"
edit: https://github.com/rstudio/bookdown-demo/edit/master/%s
output_dir: "book-output" # 渲染后的目录名字
clean: ["my-book.bbl", "R-packages.bib"]
language:
  label:
    fig: "FIGURE "
    tab: "TABLE "
  ui:
    edit: "Edit"
    chapter_name: "Chapter "
```
含义可以参考：[bookdown书籍](https://bookdown.org/yihui/bookdown/configuration.html#configuration)

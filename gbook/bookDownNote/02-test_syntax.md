# 语法

## Markdown syntax
### Inline formatting

-斜体 _italic_   ` _italic_`

-黑体  *bold*    `*bold*`

-下标左右两边用`~`隔开，比如H~2~SO~4~, `H~2~SO~4~`

-上标两边用`^`隔开，比如c10^-1^, `c10^-1^`

-脚注用`^[]`表示，比如 hello^[this is a footnote.], `hello^[this is a footnote.]`








### Block-level elements

- one item
- one item
  - one item
  - one item
  
1. first
2. second



Blockquotes

> balabalabala
>
> --- Mark Twain


### math expresions


```
$$ \begin{array}{cc}
x_{11} & x_{12} \\
x_{21} & x_{22} 
\end{array}
$$
```
$$ \begin{array}{cc}
x_{11} & x_{12} \\
x_{21} & x_{22} 
\end{array}
$$



## Markdown extensions by bookdown

### number and reference equations

带标签和编号的公式

```
\begin{equation}
a = 3 
(\#eq:a)
\end{equation}
```
编译后:
\begin{equation}
a = 3 
(\#eq:a)
\end{equation}

引用`\@ref(eq:a)`
As shown in Eq.\@ref(eq:a)


不带编号和标签的公式
```
\begin{equation*}
a = 3 
\end{equation*}
```

\begin{equation*}
a = 3 
\end{equation*}



公式对齐`align`
```
\begin{align}
a & =3 \notag\\
b & =  \sqrt{2}
(\#eq:align)
\end{align}
```

\begin{align}
a & =3 \notag\\
b & =  \sqrt{2}
(\#eq:align)
\end{align}


利用`split` 将一个公式分成几行
```
\begin{equation}
\begin{split}
a &= 3 + 3 \\
& =6 
\end{split}
(\#eq:var-beta)
\end{equation}
```

\begin{equation}
\begin{split}
a &= 3 + 3 \\
& =6 
\end{split}
(\#eq:var-beta)
\end{equation}

### Theorems and proofs

定理

````markdown
```{theorem,thmtest, name = "my theorem"}
Here is my theorem.
```
````
编译后为：
\BeginKnitrBlock{theorem}\iffalse{-91-109-121-32-116-104-101-111-114-101-109-93-}\fi<div class="theorem"><span class="theorem" id="thm:thmtest"><strong>(\#thm:thmtest) \iffalse (my theorem) \fi </strong></span>Here is my theorem.</div>\EndKnitrBlock{theorem}

引用定理
```
cite Theorem.\@ref(thm:thmtest)
```
cite Theorem.\@ref(thm:thmtest)

lemma、definition、corollary、proposition、example都一样，引用的时候缩写分别为thm、lem、def、cor、prp、ex
\BeginKnitrBlock{lemma}<div class="lemma"><span class="lemma" id="lem:unnamed-chunk-1"><strong>(\#lem:unnamed-chunk-1)</strong></span>Here is my lemma.</div>\EndKnitrBlock{lemma}

\BeginKnitrBlock{definition}<div class="definition"><span class="definition" id="def:unnamed-chunk-2"><strong>(\#def:unnamed-chunk-2)</strong></span>Here is my definition.</div>\EndKnitrBlock{definition}

\BeginKnitrBlock{corollary}<div class="corollary"><span class="corollary" id="cor:unnamed-chunk-3"><strong>(\#cor:unnamed-chunk-3)</strong></span>Here is my corollary.</div>\EndKnitrBlock{corollary}

\BeginKnitrBlock{proposition}<div class="proposition"><span class="proposition" id="prp:unnamed-chunk-4"><strong>(\#prp:unnamed-chunk-4)</strong></span>Here is my proposition.</div>\EndKnitrBlock{proposition}

\BeginKnitrBlock{example}<div class="example"><span class="example" id="ex:unnamed-chunk-5"><strong>(\#ex:unnamed-chunk-5)</strong></span>Here is my example.</div>\EndKnitrBlock{example}

### Text references

没弄明白

(ref:foo) Define a text referene


`(ref:foo)`

## Figures


```r
knitr::include_graphics(rep("images/knit-logo.png", 2))
```

![](images/knit-logo.png)<!-- -->![](images/knit-logo.png)<!-- -->

````markdown
```{r knitr-logo, out.width='32.8%', fig.show='hold', fig.cap='Three knitr logos included in the document from an external PNG image file.'}
knitr::include_graphics(rep('images/knit-logo.png', 3))
```
````


```r
knitr::include_graphics(rep('images/knit-logo.png', 3))
```

<div class="figure">
<img src="images/knit-logo.png" alt="Three knitr logos included in the document from an external PNG image file." width="32.8%" /><img src="images/knit-logo.png" alt="Three knitr logos included in the document from an external PNG image file." width="32.8%" /><img src="images/knit-logo.png" alt="Three knitr logos included in the document from an external PNG image file." width="32.8%" />
<p class="caption">(\#fig:knitr-logo)Three knitr logos included in the document from an external PNG image file.</p>
</div>

## Citations {#citations}

假设bib文件为ref.bib，引用文献的key为xie2016bookdown，则首先需要在index.RMD里的开头部分加上

```
---
title: "BookDown Test"
bibliography: [ref.bib] 
biblio-style: apalike  
link-citations: yes
---
```
然后引用`@xie2016bookdown`或者`[@xie2016bookdown]`，最后一个RMD文件里放文献列表
```markdown
`r if (knitr:::is_html_output()) '# References {-}'`
```


see: @xie2016bookdown 2.8 
 

## Cross-references
比如要引用某一小节，首先在小节标题后面加上`{#id}`，然后引用的时候`\@ref(id)`
如果自己没有分配id，pandoc会默认分配id: *id和标题一样，只不过空格用`-`代替,而且标题中的大小全部换成小写了*。

效果：第\@ref(install-bookdown)章、第\@ref(citations)节、第\@ref(theorems-and-proofs)


<font color=#0099ff size=7 face="黑体">注意：id里不能含有下划线</font>

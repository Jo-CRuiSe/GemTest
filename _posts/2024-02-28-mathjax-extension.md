---
title: MathJax 支持 Packages 扩展
author: jo
date: 2024-02-26 20:00:00 +0800
categories: [Blogging, Tutorial]
tags: [typography]
pin: true
math: true
---
<p style="display: flex;align-items: center; justify-content: center">$ \{x\in\mathbb R: x^2-x+1 \lt 0 \}$</p>

## 使用方法

### 开启MathJax中自带的库

在`_config`中开启相应package来支持相应语法：

```yml
textcomp: true # the option for textcomp package
```

效果如下：

 当前室内温度25$$ \textdegree C$$

启用`mhchem`来支持化学方程式：


$$\ce{2K(s) + 2H2O(l)=2K+(aq) +2OH- (aq) +2H2(g)}\quad \Delta_rG^\ominus  _{m,298\ce{K}}=-404.82 \ce{kJ/mol} $$

MathJax 中支持的 TeX/LaTeX 命令：https://docs.mathjax.org/en/v3.2-latest/input/tex/macros/index.html

### 定义MathJax中不支持的符号

例如，MathJax目前不支持二重环路积分符号，我们可以自己定义

#### 在`_config`中设置宏

>这种方法会对所有文章生效
{: .prompt-tip}

```yml
macros:  # Before the colon is the formula name, and after the colon is the implementation method. Please pay attention to the format and use \\\\ instead of \
```

`macros`用来自定义需要的符号，例如使用`\oiint`来定义二重环路积分

```yml
macros:
	ooint: "{\\\\bigcirc}\\\\kern-11.5pt{\\\\int}\\\\kern-6.5pt{\\\\int}"
```

配置好后，可以直接在文章中使用

```latex
$$\ooint$$
```

效果如下：

$$\ooint_{S^{+}} \overrightarrow{F} \cdot d\overrightarrow{S} = \iiint\limits_{\Sigma}^{} div \overrightarrow{F} dV $$

>值得注意的是通过以上尺寸来定义的方法对行间和行内公式可能并不通用。演示的符号在行间公式中显示正常，而在行内公式中显示异常。
{: .prompt-danger}

#### 在文章中设置宏

>这种方法仅对当前文章生效，其他文章及主页等不生效
{: .prompt-tip}

需要在`_config`文件中开启`newcommand`

```yml
newcommand: true # the option for newcommand package
```

在文章的正文部分使用（定义后不会被显示，使用时才显示）

```latex
$$\def\rr{\bf R}$$
```

$$\def\rr{\bf R}$$

$$\rr$$

>如果需要使用{% raw %} `{{` {% endraw %}请到`_config`中定义，因为会和Jekyll语法冲突
{: .prompt-warning}

## 注意事项

当公式在第一行作为行间公式时，请使用`<p></p>`标签包裹，并设置样式，否则在首页摘要不能被正确渲染

```html
<p style="display: flex;align-items: center; justify-content: center">$ \{x\in\mathbb R: x^2-x+1 \lt 0 \}$</p>
```


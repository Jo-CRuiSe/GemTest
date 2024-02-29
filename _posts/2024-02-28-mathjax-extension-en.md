---
title: MathJax supports Packages extension
author: jo
date: 2024-02-29 19:00:00 +0800
categories: [Blogging, Tutorial]
tags: [typography]
pin: true
math: true
---
<p style="display: flex;align-items: center; justify-content: center">$ \{x\in\mathbb R: x^2-x+1 \lt 0 \}$</p>

## Usage

### Turn on the specific library of MathJax

Enable the corresponding package in `_config` to support the corresponding syntax:

```yml
textcomp: true # the option for textcomp package
```

The effect is as follows:

Current indoor temperature is 77$$ \textdegree F$$

Enable `mhchem` to support chemical equations:


$$\ce{2K(s) + 2H2O(l)=2K+(aq) +2OH- (aq) +2H2(g)}\quad \Delta_rG^\ominus  _{m,298\ce{K}}=-404.82 \ce{kJ/mol} $$

Supported TeX/LaTeX commands in MathJax：https://docs.mathjax.org/en/v3.2-latest/input/tex/macros/index.html

### Define unsupported symbols in MathJax

For example, MathJax currently does not support the double loop integral symbol. We can define it ourselves.

#### Set macros in `_config`

>This method will take effect on all articles
{: .prompt-tip}

```yml
macros:  # Before the colon is the formula name, and after the colon is the implementation method. Please pay attention to the format and use \\\\ instead of \
```

`macros` is used to customize the required symbols, for example, use `\oiint` to define a double loop integral

```yml
macros:
	ooint: "{\\\\bigcirc}\\\\kern-11.5pt{\\\\int}\\\\kern-6.5pt{\\\\int}"
```

After configuration, you can use it directly in the article

```latex
$$\ooint$$
```

#### Set macros in articles

>This method only takes effect for the current article, and does not take effect for other articles and homepage.
{: .prompt-tip}

You need to enable `newcommand` in `_config` file

```yml
newcommand: true # the option for newcommand package
```

Use Latex syntax definition in the body part of the article (it will not be displayed after definition, it will be displayed only when used)

```latex
$$\def\rr{\bf R}$$
```

$$\def\rr{\bf R}$$

$$\rr$$

>If you need to use `{{`, please define it in `_config`, because it will conflict with Jekyll syntax
{: .prompt-warning}

## Precautions

When the formula is used as an inline formula on the first line, please use the `<p></p>` tag to wrap it and set the style, otherwise the summary on the homepage will not be rendered correctly.

```html
<p style="display: flex;align-items: center; justify-content: center">$ \{x\in\mathbb R: x^2-x+1 \lt 0 \}$</p>
```


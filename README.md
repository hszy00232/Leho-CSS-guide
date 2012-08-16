# 编写统一、符合习惯的CSS的约定

这篇文档是在现有的样式规范的基础上对于CSS的开发做了更为细化的约定，目的是想实现CSS代码的风格统一化，方便大家对于其他同学代码的维护。这个文档也借鉴了一些目前业界比较不错的CSS Guide。

欢迎大家在查阅此文档时提出新的想法，还请多多贡献。

## 目录

1. [约定原则](#general-principles)
2. [CSS组织](#css-organization)
3. [CSS注释](#css-comments)
4. [CSS格式](#css-anchor)
5. [CSS命名](#css-naming)
6. [CSS Hank](#css-hack)

<a name="general-principles"></a>
## 1.约定原则

> “作为成功的项目的一员，很重要的一点是意识到只为自己写代码是很糟糕的行为。如果将有成千上万人使用你的代码，
> 那么你需要编写最具明确性的代码，而不是以自我的喜好来彰显自己的智商。” - Idan Gazit

* 在任何代码库中，无论有多少人参与贡献代码，所以代码都应该如同一个人编写的一样
* 严格执行一致认可的风格
* 如有疑义，则使用现有的约定

<a name="css-organization"></a>
## 2.CSS组织

* 一个频道中页面往往大于2个，这时我们需要把频道中通用的CSS提成 `common.css` 文件，具体页面使用时 `@import common.css`
* 具体页面的CSS，建议按 ` 页面通用->具体业务->重置全站通用 ` 这样的顺序来组织页面的CSS

<a name="css-comments"></a>
## 3.CSS注释

* 3-1 CSS文件注释

```css
/*
Copyright (c) 2012, leho Inc. All rights reserved.
version: 1.0.0.0
*/
/**
* stylesheet for pagename
* Author     :Email
* created    :Date and Time
* updated    :Date and Time
* updated by :Email
*/
```

在这里 updated:Date and Time 和 updated by：Email是比较重要的。

* 3-2 CSS单行注释

将注释放在主题上方并独占一行，避免在行末旋转注释，控制每行长度在合理的范围内，比如80个字符，注释的大小写应当与普通句子相同，并且使用一致的文本缩进。

CSS注释示例：

```css
/* layout */
...

/* mod */
...

/* 重置通用模块 */
...
```

<a name="css-anchor"></a>

## 4.CSS格式

最终选择的代码风格必须保证：易于阅读，易于清晰地注释，最小化无意中引入错误的可能性，可生成有用的diff和blame。

* 4-1 声明写在一行,声明中“{”和“}”前后加空格,对于声明块的最后一个声明，始终保留结束的分号。

```css
.selector-1 { width:300px;height:200px;border:1px solid #ccc; }
```
* 4-2 对于多个选择器同时定义时，每个选择器占一行。

```css
.selector-2,
.selector-3,
.selector-4 { width:400px;height:100px;border:1px solid #ddd; }
```

* 4-3 声明顺序

样式声明的顺序应当遵守一个单一的原则。我的倾向是将相关的属性组合在一起，并且将对结构来说比较重要的属性,如：
定位或盒模型(width/height/padding/border/margin)、行、字体/字号/颜色、背景、CSS3效果等属性。

```css
.selector { position:relative;display:block;width:50%;height:100%;padding:10px;border:0;margin:10px;color:#fff;background:#000; }
```

按字母排序也非常流行，但是这种做法存在一个缺点，即会将相关的属性分开。例如定位偏移量会无法放在一起，盒模型相关的属性会四散分布在一个声明块中。

* 4-4 CSS3中逗号分隔的长属性值：

```css
.selector {
    box-shadow:
        1px 1px 1px #000,
        2px 2px 1px #ccc inset;
    background-image:
        linear-gradient(#fff,#ccc),
        linear-gradient(#f3c,#4ec);
}
```

* 4-5 CSS3兼容书写形式和对齐方式：

```css
.selector {
    -webkit-box-shadow: 0px 0px 5px rgba(200,200,200,0.8);
       -moz-box-shadow: 0px 0px 5px rgba(200,200,200,0.8);
        -ms-box-shadow: 0px 0px 5px rgba(200,200,200,0.8);
         -0-box-shadow: 0px 0px 5px rgba(200,200,200,0.8);
            box-shadow: 0px 0px 5px rgba(200,200,200,0.8);
}
```

* 4-6 每个声明集之间保留一个空行。
* 4-7 CSS的颜色值使用十六进制值(rgba格式除外),使用小写，可以使用缩写时必须使用缩写。如 `#aaa`
* 4-8 单引号或双引号的选择保持一致。推荐使用双引号，如 `content:""`
* 4-9 对于选择器中的属性值也加上引号，如 `input[type="checkbox"]`
* 4-10 在允许的情况下，下要给0加上单位，如 `margin:0;`


<a name="css-naming"></a>
## 5.CSS命名

* 5-1 命名不要用缩写，除一些公认的缩写外，单词间用"-"做为连接符
* 5-2 ID一般不推荐使用，如果用到的情况，需保证命名的唯一
* 5-3 Class用来标识某一类型的对象，出于模块化代码的考虑，命名最好使用前缀和名字组成，前缀最好是频道。如：`.myhome-top`,`.app-share-bd` 等。
* 5-4 命名示例：

```css
/* Not recommended */
.mod .hd { ... }
.mod .bd { ... }
.mod .ft { ... }

/* recommended */
.mod .mod-hd { ... }
.mod .mod-bd { ... }
.mod .mod-ft { ... }
```
* 5-5 全站中按钮Class都须以 `btn-` 为前缀，由前缀+动作[+描述]构成。如 `btn-reg`,`btn-follow`,`btn-follow-add` 等
* 5-6 全站中图标Class都须以 `ico-` 为前缀，由前缀+描述构成。如 `ico-qq` 等
* 5-7 推荐缩写
<table>
<tr><td>表示状态</td><td>.on,.active,.selected</td></tr>
<tr><td>表示位置</td><td>.first,.last,.main,.side</td></tr>
<tr><td>表示结构</td><td>.hd,.bd,.ft,.col,.section</td></tr>
<tr><td>通用元素</td><td>.tb,.nav,.list,.item,.tag,.pic,.info</td></tr>
</table>


<a name="css-hack"></a>
## 6.避免滥用CSS Hack

推荐使用下页的：
区别属性：
<table>
<tr><td>IE6</td><td>_property:value</td></tr>
<tr><td>IE6/7</td><td>*property:value</td></tr>
<tr><td>IE6/7/8/9</td><td>property:value\9</td></tr>
</table>
区别规则：
<table>
<tr><td>IE6</td><td>* html selector{ ... }</td></tr>
<tr><td>IE7</td><td>*:first-child+html selector{ ... }</td></tr>
<tr><td>非IE6</td><td>html>body selector{ ... }</td></tr>
<tr>
    <td>firefox only</td>
    <td>@-moz-document url-prefix(){ ... }</td>
  </tr>
  <tr>
    <td>saf3+/chrome1+</td>
    <td>@media all and (-webkit-min-device-pixel-ratio:0){ ... }</td>
  </tr>
  <tr>
    <td>opera only</td>
    <td>@media all and (-webkit-min-device-pixel-ratio:10000),not all and (-webkit-min-device-pixel-ratio:0){ ... }</td>
  </tr>
  <tr>
    <td>iPhone/mobile webkit</td>
    <td>@media screen and (max-device-width: 480px){ ... }</td>
  </tr>
</table>
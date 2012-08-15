## 编写统一、符合习惯的CSS的约定

这篇文档是在现有的样式规范的基础上对于CSS的开发做了更为细化的约定，目的是想实现CSS代码的风格统一化，方便大家对于其他同学代码的维护。这个文档也借鉴了一些目前业界比较不错的CSS Guide。

欢迎大家在查阅此文档时提出新的想法，还请多多贡献。

### 目录

1. [约定原则](#general-principles)
2. [注释](#comments)

<a name="general-principles"></a>
### 1.约定原则

> “作为成功的项目的一员，很重要的一点是意识到只为自己写代码是很糟糕的行为。如果将有成千上万人使用你的代码，
> 那么你需要编写最具明确性的代码，而不是以自我的喜好来彰显自己的智商。” - Idan Gazit

* 在任何代码库中，无论有多少人参与贡献代码，所以代码都应该如同一个人编写的一样
* 严格执行一致认可的风格
* 如有疑义，则使用现有的约定

<a name="comments"></a>
### 2.样式文件整理

* 一个频道中页面往往大于2个，这时我们需要把频道中通用的样式提成 `common.css` 文件，具体页面使用时 `@import common.css`
* 具体页面的样式，建议按 页面的通用样式->页面模块的样式->重置通用模块样式 这样的顺序来组织页面的样式





### 1.CSS浏览器支持标准 ###

<table>
<tr><td></td><td>WinXP</td><td>Win7</td><td>OS X</td></tr>
<tr><td>IE8+</td><td>A</td><td>A</td><td></td></tr>
<tr><td>IE7/IE6</td><td>B</td><td>B</td><td></td></tr>
<tr><td>Chrom14+</td><td>A</td><td>A</td><td>A</td></tr>
<tr><td>FireFox9+</td><td>A</td><td>A</td><td>A</td></tr>
<tr><td>Safari</td><td>B</td><td>B</td><td>B</td></tr>
<tr><td>Opera</td><td>C</td><td>C</td><td>C</td></tr>
</table>

+ A级－交互和视觉完全符全设计的要求</li>
+ B级－视觉上允许有所差异，但不破坏页面的整体效果</li>
+ C级－可忽略设计上的细节，但不防碍使用</li>

### 2.避免滥用CSS Hack ###

推荐使用下页的：
区别属性：
<table>
  <tr>
    <td>IE6</td>
    <td>_property:value</td>
  </tr>
  <tr>
    <td>IE6/7</td>
    <td>*property:value</td>
  </tr>
  <tr>
    <td>IE6/7/8/9</td>
    <td>property:value\9</td>
  </tr>
</table>
区别规则：
<table>
  <tr>
    <td>IE6</td>
    <td>* html selector{ ... }</td>
  </tr>
  <tr>
    <td>IE7</td>
    <td>*:first-child+html selector{ ... }</td>
  </tr>
  <tr>
    <td>非IE6</td>
    <td>html>body selector{ ... }</td>
  </tr>
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
# 编写统一、符合习惯的CSS的约定

这篇文档是在现有的样式规范的基础上对于CSS的开发做了更为细化的约定，目的是想实现CSS代码的风格统一化，方便大家对于其他同学代码的维护。这个文档也借鉴了一些目前业界比较不错的CSS Guide。

欢迎大家在查阅此文档时提出新的想法，还请多多贡献。

## 目录

1. [约定原则](#general-principles)
2. [CSS组织](#css-organization)
3. [CSS注释](#css-comments)
4. [CSS格式](#css-anchor)

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
* 具体页面的CSS，建议按 ` 页面通用->页面主题->重置全站通用模块 ` 这样的顺序来组织页面的CSS

<a name="css-comments"></a>
## 3.CSS注释

* 将注释放在主题上方并独占一行
* 避免在行末旋转注释
* 控制每行长度在合理的范围内，比如80个字符。
* 使用注释从字面上将CSS代码分隔为独立的部分。
* 注释的大小写应当与普通句子相同，并且使用一致的文本缩进。

### CSS注释示例：

```css
/* 基本注释 */

/* 引导页-添加兴趣 */
.panel-guide .guide-sort .guide-sort-name { ... }
.panel-guide .sort-1 .guide-sort-name { ... }
.panel-guide .sort-2 .guide-sort-name { ... }
.panel-guide .sort-3 .guide-sort-name { ... }
.panel-guide .sort-4 .guide-sort-name { ... }
...
```

<a name="css-anchor"></a>
## 4.CSS格式

最终选择的代码风格必须保证：易于阅读，易于清晰地注释，最小化无意中引入错误的可能性，可生成有用的diff和blame。

1. 声明写在一行
2. 声明中“{”和“}”前后加空格
3. 对于声明块的最后一个声明，始终保留结束的分号。
4. 每个声明集之间保留一个空行。
5. 对于多个选择器同时定义时，每个选择器占一行。

```css
.selector-1 { width:300px;height:200px;border:1px solid #ccc; }
.selector-2,
.selector-3,
.selector-4 { width:400px;height:100px;border:1px solid #ddd; }
```

### 声明顺序

样式声明的顺序应当遵守一个单一的原则。我的倾向是将相关的属性组合在一起，并且将对结构来说比较重要的属性（如定位或者盒模型） 放在前面，先于排版、背景及颜色等属性。

```css
.selector { position:relative;display:block;width:50%;height:100%;padding:10px;border:0;margin:10px;color:#fff;background:#000; }
```

按字母排序也非常流行，但是这种做法存在一个缺点，即会将相关的属性分开。例如定位偏移量会无法放在一起，盒模型相关的属性会四散分布在一个声明块中。


### 例外及细微偏移原则的情况

对于CSS3这种属性值比较长的情况，可以放在多行中，冒号后加空格，有助于提高可读性，并易于生成有效的diff。

CSS3中逗号分隔的长属性值：

```css
.selector {
    box-shadow:
        1px 1px 1px #000，
        2px 2px 1px #ccc inset;
    background-image:
        linear-gradient(#fff,#ccc),
        linear-gradient(#f3c,#4ec);
}
```

CSS3兼容书写形式和对齐方式：

```css
.selector {
    -webkit-box-shadow: 0px 0px 5px rgba(200,200,200,0.8);
       -moz-box-shadow: 0px 0px 5px rgba(200,200,200,0.8);
        -ms-box-shadow: 0px 0px 5px rgba(200,200,200,0.8);
         -0-box-shadow: 0px 0px 5px rgba(200,200,200,0.8);
            box-shadow: 0px 0px 5px rgba(200,200,200,0.8);
}
```


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
编写统一、符合习惯的CSS的约定
======================

这篇文档是在现有的样式规范的基础上对于CSS的开发做了更为细化的约定，目的是想实现CSS代码的风格统一化，方便大家对于其他同学代码的维护。这个文档也借鉴了一些目前业界比较不错的CSS Guide。

欢迎大家在查阅此文档时提出新的想法，还请多多贡献。


## 1.CSS浏览器支持标准 ##
<table>
  <tr>
    <th></th>
    <th>WinXP</th>
    <th>Win7</th>
    <th>OS X</th>
  </tr>
  <tr>
    <th>IE9</th>
    <td>B</td>
    <td>B</td>
    <td></td>
  </tr>
  <tr>
    <th>IE8</th>
    <td>A</td>
    <td>A</td>
    <td></td>
  </tr>
  <tr>
    <th>IE7</th>
    <td>B</td>
    <td>B</td>
    <td></td>
  </tr>
  <tr>
    <th>IE6</th>
    <td>B</td>
    <td>B</td>
    <td></td>
  </tr>
  <tr>
    <th>Chrom16</th>
    <td>A</td>
    <td>A</td>
    <td>A</td>
  </tr>
  <tr>
    <th>Chrom14</th>
    <td>A</td>
    <td>A</td>
    <td>A</td>
  </tr>
  <tr>
    <th>FireFox10</th>
    <td>A</td>
    <td>A</td>
    <td>A</td>
  </tr>
  <tr>
    <th>FireFox9</th>
    <td>A</td>
    <td>A</td>
    <td>A</td>
  </tr>
  <tr>
    <th>Safari</th>
    <td>B</td>
    <td>B</td>
    <td>B</td>
  </tr>
  <tr>
    <th>Opera</th>
    <td>C</td>
    <td>C</td>
    <td>C</td>
  </tr>
</table>
+ A级－交互和视觉完全符全设计的要求</li>
+ B级－视觉上允许有所差异，但不破坏页面的整体效果</li>
+ C级－可忽略设计上的细节，但不防碍使用</li>

======================
## 2.避免滥用CSS Hack ##

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
## CSS实现彩色图片转换成黑白图片

### CSS3 filter

通过CSS3的来减少图片的饱和度很简单，下面我们给需要变黑白的图片添加一个class `.desaturate`，接下来使用CSS3的fiter：

        img.desaturate{
                -webkit-filter: grayscale(100%);
                   -moz-filter: grayscale(100%);
                    -ms-filter: grayscale(100%);
                     -o-filter: grayscale(100%);
                        filter: grayscale(100%);
        }
        
HTML结构：

        <img src="***.png" class="desaturate"/>
        

### 添加一个SVG filter

通过CSS3实现的filter效果只在Chrome19.0+,Safari6.0+,Firefox15.0+,IE10.0得到支持，为了兼容Firefox，Opera浏览器我们采用SVG filter来实现。

首页创建一个名称为desaturate.svg的文档，文档内容如下：

        <svg version="1.1" xmlns="http://www.w3.org/2000/svg">
                <filter id="greyscale">
                        <feColorMatrix type="matrix" 
                                values="0.3333 0.3333 0.333 0 0
                                        0.3333 0.3333 0.333 0 0
                                        0.3333 0.3333 0.333 0 0
                                        0 0 0 1 0"/>
                </filter>
        </svg>
        
滤镜使用一个数值矩阵表示如何改变图像的颜色。行数29，30，31，32表明如何改变图像的红、绿、蓝、α(透明度)通道，这4行中的每一行给出了红、绿、蓝、α的比例和一个校正值。

以第29行为例，它表明当前像素点的红色的比例为33.33%，绿色的比例为33.33%，蓝色的比例为33.33%，没有透明度，不使用校正值，把这些因素混合到一起，将成为这个像素点红色部分新的值。第30行代码为绿色部分新的值，第31行代码为蓝色部分新的值，第32行保持原来的透明度不变。这一滤镜的结果将图像由彩色改为黑白色。
        
扩展之后的CSS filter为:

        img.desaturate{
                -webkit-filter: grayscale(100%);
                   -moz-filter: grayscale(100%);
                    -ms-filter: grayscale(100%);
                     -o-filter: grayscale(100%);
                        filter: grayscale(100%);
                        filter: url(desaturate.svg#greyscale);
        }

### 增加对IE的支持

到目前为止，我们的代码支持了所有的高端浏览器，接下来只需要添加`filter:gray;`就可以兼容IE6-9了。

扩展之后的CSS filter为：
        img.desaturate{
                -webkit-filter: grayscale(100%);
                   -moz-filter: grayscale(100%);
                    -ms-filter: grayscale(100%);
                     -o-filter: grayscale(100%);
                        filter: grayscale(100%);
                        filter: url(desaturate.svg#greyscale);
                        filter: gray;
        }
        
如果想兼容老版的Webkit，需要在最后添加`-webkit-filter:grayscale(1);`,最终代码为：

        img.desaturate{
                -webkit-filter: grayscale(100%);
                   -moz-filter: grayscale(100%);
                    -ms-filter: grayscale(100%);
                     -o-filter: grayscale(100%);
                        filter: grayscale(100%);
                        filter: url(desaturate.svg#greyscale);
                        filter: gray;
                -webkit-filter: grayscale(1);
        }
        
### 扩展应用：实现整个页面变灰效果

        html{
                -webkit-filter: grayscale(100%);
                   -moz-filter: grayscale(100%);
                    -ms-filter: grayscale(100%);
                     -o-filter: grayscale(100%);
                        filter: grayscale(100%);
                        filter: url(desaturate.svg#greyscale);
                        filter: gray;
                        /* filter:progid:DXImageTransform.Microsoft.BasicImage(grayscale=1); 可被filter:gray替换 */
                -webkit-filter: grayscale(1);
        }
        
        
### 参考内容：

* [http://demosthenes.info/blog/532/Convert-Images-To-Black-And-White-With-CSS]
* [http://www.cnblogs.com/rubylouvre/archive/2012/08/13/2636796.html]
* [http://caniuse.com/#search=filter]
* [http://www.yesky.com/240/180240_4.shtml]
## CSS实现彩色图片转换成黑白图片

### CSS3灰度级滤镜

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

### 添加一个SVG的滤镜效果



该属性定义行内元素的基线相对于该元素所在行的基线的垂直对齐。允许指定负长度值和百分比值。这会使元素降低而不是升高。在表单元格中，这个属性会设置单元格框中的单元格内容的对齐方式。




IE本身有提供了原生的支持: `clipboardData` 和 `setData`。Firefox 等都没有，因此利用 flash 来做跨浏览器支持。

使用 ZeroClipboard 是目前最好的解决方式(需要在服务器上运行):  

        // 初始化一个复制程序
     var clip = new ZeroClipboard.Client(),
        doc = document,
        tip = doc.getElementById('tip'),
        text = doc.getElementById('text');
        
    // 把要复制的值初化为空
    clip.setText( '' );
    // 设置 flash 的鼠标手形
    clip.setHandCursor( true );
            
    // 监听复制完毕事件
    clip.addEventListener( 'complete', function(client, text) {
            tip.innerHTML = 'copied…';
            tip.style.display = 'inline';
            setTimeout(function(){
                tip.style.display = 'none';
            }, 1000);
    } );
    
    // 当鼠标点击按钮时，设置要复制出来的值 
    clip.addEventListener( 'mouseDown', function(client) { 
            clip.setText( text.value );
    } );
    
    // 把复制程序定位到某个具体的位置
    clip.glue( 'button' );
    
更多关于 `ZeroClipboard` 的内容：[http://code.google.com/p/zeroclipboard/]();
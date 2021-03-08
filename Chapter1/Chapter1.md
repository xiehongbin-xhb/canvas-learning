# 第一章 基础知识
## 1.1 canvas元素
### 1.1.1 canvas元素大小/ 绘图表面大小 
在默认情况下，浏览器所创建的canvas元素是300像素宽，150像素高。可以通过指定width和height属性而修改canvas元素的大小
还可以通过css属性来改变canvas元素的大小

canvas实际上有两套尺寸，一个是元素本身的大小，一个是元素绘图表面的大小。
如果是通过css来设定canvas元素的大小，那么只会改变元素本身的大小，而不会影响到绘图表面。
当canvas元素大小不符合其绘图表面的大小时，浏览器就会对绘图表面进行缩放，使其符合元素的大小。

结论：
通过width和height属性而非CSS属性来修改canvas元素的大小 是更好的办法。
如果使用css元素修改元素的大小，同时又没有指定canvas元素的width和height属性，那么当元素大小与canvas绘图表面大小不相符时，浏览器会对绘图表面进行缩放。

### 1.1.2 canvas元素的API
canvas元素只提供了两个属性和三个方法
#### 属性
**width**
canvas元素绘图表面的宽度，默认情况下浏览器会将canvas元素的大小设定成与绘图表面大小一致，如果在css中覆写了元素的大小，那么浏览器则会将绘图表面进行缩放，使之更符合元素尺寸；默认值是300。
**height**
canvas元素绘图表面的高度。
#### 方法
**getContext** 
返回与该canvas元素相关的绘图环境对象，每个canvas元素均有一个这样的环境对象，而且每个环境对象均与一个canvas元素相关联
**toDataURL(type, quality)**
返回一个数据地址，可以将它设定成img元素的属性值。第一个参数指定了图像的类型，例如image/jpeg，如果不指定第一个参数，则默认为image/png；第二个参数必须是0-1.0之间的double值，表示图像的显示质量
**toBlob(callback, type, args..)**
创建一个用于表示此canvas元素图像文件的blob。第一个参数是一个回调函数，浏览器会以一个指向blob的引用为参数，去调用该回调函数，
第二个参数以“image/png”这样的方式来指定图像的类型，如果不指定，则默认使用image/png类型。最后一个参数必须是0-1.0之间的double值，表示图像的显示质量。

## 1.2 Canvas绘图环境
先通过getElementById获取到这个canvas所对应的DOM元素，再通过getContext('2d')获取到这个canvas所对应的2d绘图环境
### 1.2.1 2d绘图环境
2d绘图环境包含的属性
- canvas 执行该绘图环境所属的canvas对象，该属性最常用的用途是通过它来获取canvas的宽度和高度，分别调用context.canvas.width 或者 context.canvas.height来获取
- fillstyle 指定该绘图环境在后续的图形填充操作中所有使用的颜色，渐变色或图案
- strokeStyle 指定了对路径进行描边时所用的绘制风格，可设定为某个颜色，渐变色或图案

- font 设在调用该绘图环境的fillText或者strokeText时，所使用的字型
- textAlign 决定了以fillText或者strokeText方法进行绘制时，所画文本的水平对齐方式
- textBaseline 决定了以fillText或者strokeText方法进行绘制时，所画文本的垂直对齐方式

- lineCap 该值告诉浏览器如何绘制线段的断点，可选值为 butt,round,square，默认值是butt
- lineWidth 该值决定了在canvas之后绘制线段的屏幕像素宽度
- lineJoin 告诉浏览器在两条线段相交时如何绘制焦点，可取值时bevel，round，miter，默认是miter
- miterLimit 告诉浏览器如何绘制miter形式的线段焦点

- shadowBlur 该值决定了浏览器如何延申阴影效果，值越高，阴影效果就延伸得越远。
- shadowColor 该值告诉浏览器使用何种颜色来绘制阴影，通过使用半透明色来作为该属性的值
- shadowOffsetX 以像素为单位，指定阴影效果在水平方向的偏移量
- shadowOffsetY 以像素为单位，指定阴影效果在垂直方向的偏移量

- globalAlpha 全局透明度设置，取0 - 1之间的值。浏览器绘制时会将每个像素的alpha值与该值相乘，绘制图像时也如此
- globalCompsiteOperation 该值决定了浏览器将某个物体绘制在其他物体之上时，所采用的绘制方式

### 1.2.2 canvas状态的保存和恢复

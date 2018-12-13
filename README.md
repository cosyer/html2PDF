# html转成pdf下载（html2canvas 和 jsPDF）

## html2canvas

### 简介

我们可以直接在浏览器端使用html2canvas，对整个或局部页面(一般为body)进行截图。但这并不是真的截图，而是通过遍历页面DOM结构，收集所有元素信息及相应样式，渲染出canvas image。

由于html2canvas只能将它能处理的生成canvas image，因此渲染出来的结果并不是100%与原来一致。但它不需要服务器参与，整个图片都由客户端浏览器生成，使用很方便。

### 使用

使用的API也很简洁，下面代码可以将某个元素渲染成canvas：

```javascript
html2canvas(element, {
    onrendered: function(canvas) {
        // canvas is the final rendered <canvas> element
    }
});
```

## jsPDF

jsPDF库可以用于浏览器端生成PDF。

### 文字生成PDF

使用方法如下：

```javascript
// 默认a4大小，竖直方向，mm单位的PDF
var doc = new jsPDF();

// 添加文本‘Hello World’
doc.text('Hello World', 10, 10);
doc.save('a4.pdf');
```

### 图片生成PDF

使用方法如下：

```javascript
// 三个参数，第一个方向，第二个单位，第三个尺寸格式
var doc = new jsPDF('landscape','pt',[205, 115])

// 将图片转化为dataUrl
var imageData = ‘data:image/png;base64,...’;

doc.addImage(imageData, 'PNG', 0, 0, 205, 115);
doc.save('a4.pdf');
```

### 文字与图片生成PDF

```javascript
// 三个参数，第一个方向，第二个尺寸，第三个尺寸格式
var doc = new jsPDF('landscape','pt',[205, 155])

// 将图片转化为dataUrl
var imageData = ‘data:image/png;base64,iVBORw0KGgo...’;

//设置字体大小
doc.setFontSize(20);

//10,20这两参数控制文字距离左边，与上边的距离
doc.text('Stone', 10, 20);

// 0, 40, 控制文字距离左边，与上边的距离
doc.addImage(imageData, 'PNG', 0, 40, 205, 115);
doc.save('a4.pdf')
```

### 多页的处理
可参考 https://www.cnblogs.com/yizhilin/p/8603879.html

- 去除body`overflow:hidden`,

- 设置html2canvas允许跨域：allowTaint: true

- 设置高度：height: $("#xxx").outerHeight()
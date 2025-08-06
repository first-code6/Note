# 不同单位的CSS运算 calc

在需要对其时有时需要vw单位的样式减去px单位

CSS的使用:

```css
width = calc(100vw - 254px)
```

React的使用:

```js
sx={{ width: "calc(100vw - 254px)" }}
```

# 将鼠标放到某个标签的时候，鼠标变成指定样式

需添加一个Cursor的css样式即可：<https://blog.csdn.net/wlijun_0808/article/details/125091394>

```html
<p>请把鼠标移动到单词上，可以看到鼠标指针发生变化：</p>
<span style="cursor:auto">Auto</span>             <!--默认，浏览器设置的光标-->
<br/>
<span style="cursor:crosshair">Crosshair</span>   <!--光标呈现为十字线-->
<br/>
<span style="cursor:default">Default</span>       <!--默认光标（通常是一个箭头）-->
<br/>
<span style="cursor:pointer">Pointer</span>       <!--光标呈现为手形-->
<br />
<span style="cursor:move">Move</span>
<br/>
<span style="cursor:e-resize">e-resize</span>
<br />
<span style="cursor:ne-resize">ne-resize</span>
<br/>
<span style="cursor:nw-resize">nw-resize</span>
<br/>
<span style="cursor:n-resize">n-resize</span>
<br/>
<span style="cursor:se-resize">se-resize</span>
<br/>
<span style="cursor:sw-resize">sw-resize</span>
<br/>
<span style="cursor:s-resize">s-resize</span>
<br/>
<span style="cursor:w-resize">w-resize</span>
<br/>
<span style="cursor:text">text</span>
<br/>
<span style="cursor:wait">wait</span>            <!--此光标指示程序正忙（通常是一只表或沙漏）-->
<br/>
<span style="cursor:help">help</span>            <!--此光标指示可用的帮助（通常是一个问号或一个气球）-->
```

# 删除inmput框type为number时右边的按钮

```css
input::-webkit-outer-spin-button, input::-webkit-inner-spin-button {
    -webkit-appearance: none;
}
 
input[type="number"] {
    -moz-appearance: textfield;
}
```

# 渐变色

# linear-gradient()

可以生成渐变颜色，例：

```css
background: linear-gradient(90deg, #e66465, #9198e5);
```

# 动画

# 定位

## 子元素为absoulte定位如何相对父元素进行定位

`将父元素postion设为"aboulte"或者"relative"即可，通常使用relative`

# 像素单位

1.  100vw,100vh 和 100%的区别

    100vw,100vh表示视窗大小，包括滚动条的大小，而100%则为可用大小，不包括滚动条的大小

# 鼠标穿透

1.在子元素覆盖住父元素时并且此时你想点击父元素下方的button的时候你会发现，button应为被子元素覆盖住无法点击

&#x9;使用 pointerEvents: "none",即可解决

```javascriptreact
sx={{
	pointerEvents: "none",
}}
```


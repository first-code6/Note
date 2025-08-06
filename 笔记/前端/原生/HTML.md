#### input标签只允许输入整数

###### 在原生HTML中
```html
<input 
	type="text" 
	oninput="this.value = this.value.replace(/^(0+)|[^\d]+/g,'');" 
/>
```

###### 在React中

在React中因为React中OnInput中不可以接收字符串所以
```jsx
<input
	type="text"
	OnInput = {(e) => {
		e.target.value = e.target.value.replace(/^(0+)|[^\d]+/g,'')
	}}
/>
```

#### 监听input元素按键

###### 在React中

```jsx
<input
	type="text"
	OnKeyDown={(e)=>{
		console.log(e.keyCode)
	}}
/>
```

| keyCode | 按键    |
| ------- | ----- |
| 13      | enter |

#### table合并单元格

*   **colspan**
    `colspan`是跨列的缩写，可以用于列与列之间的合并

```html
<td colspan = "2"></td>    // 表示合并两列
```

*   **rowspan**
    `rowspan`是跨行的缩写，可以用于行与行之间的合并

```html
<td rowspan = "2"></td>    // 表示合并两行
```

#### 保存格式base64编码的图片

前端先转化成blob格式，再使用a标签download即可

#### 拖拽方法使用addlistener响应会更快

网站：[Draggable objects](https://www.redblobgames.com/making-of/draggable/)


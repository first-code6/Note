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


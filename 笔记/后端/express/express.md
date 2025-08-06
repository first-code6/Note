# 安装

1.  首先创建一个express文件夹，随后在文件夹内输入`npm init`创建package.json文件夹
    注意：`entry point: (index.js)`命令，如果希望使用别的文件名可重新命名，如果本来就使用index.js则不用修改

2.  输入`npm install express`添加express

3.  添加index.js的js文件并编码完成Hello,world!

```js
const express = require('express')
const app = express()
const port = 3000

app.get('/', (req, res) => {
  res.send('Hello World!')
})

app.listen(port, () => {
  console.log(`Example app listening on port ${port}`)
})
```

# 在express中使用import

# req.query&#x20;

可获取 /user?id： 123中的参数，或者由axios传递的参数

```js
res.json(req.query)
```

# 跨域

```js
const express = require('express')
const cors = require('cors')
const app = express()
app.use(cors())
```

## 将组件暴露出来

```js
module.exports = { 组件名 }
```

# req.send

传送数据给前端

```js
res.send(data)   // 发送出data数据
```

# &#x20;req.json

将数据以json格式传递出来

```js
res.json(data)     // 发送出json格式的数据
```

# express导本地数据（函数）的导出与导入

1.exports
可通过exports将数据暴露出去再通过require获取数据，具体操作如下

```js
// 发送数据文件
const getName = () => {
    return 'Stark'
}
const data = 'Jim'

exports.Name = getName
exports.data = data


// 接收数据
const user = require('/user')

console.log(user.Name)
console.log(user.data)

// 解构接收数据
const {Name, data} = require('/user')
```

exports还有默认导出module.exports可以不解析直接使用

```js
// 导出数据
class User {
  constructor(name, age, email) {
    this.name = name;
    this.age = age;
    this.email = email;
  }

  getUserStats() {
    return `
      Name: ${this.name}
      Age: ${this.age}
      Email: ${this.email}
    `;
  }
}

module.exports = User;


// 接收数据
const User = require('./user');
const jim = new User('Jim', 37, 'jim@example.com');

console.log(jim.getUserStats());
```

# Router

创建一个router.js文件夹，名字随意

```js
// router.js 文件夹
const express = require('express')
const router = express.Router()

router.get('/', (req,res) => {
    res.send("this is router")
})

module.exports = router
```

使用Rouet文件夹

```js
const express = require('express')
const app = express()
const port = 3000

const router = require('./router/router')   // 导入Router文件夹

app.get('/', (req,res) => {
    res.send("Hello,World!")
})

app.use('/app', router)               // 使用Router

app.listen(port, ()=> {
    console.log('Example app listening on port ${port}')
})

```

# app.use

## 1.app.use(express.json())

在使用post传参给后端时，发现传入值为undefind，使用`app.use(express.json())`解决

```javascript
const express = require('express')
const cors = require('cors')
const app = express()

app.use(express.json())
```


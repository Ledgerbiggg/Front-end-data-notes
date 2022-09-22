# My SQL

## 主界面的组成部分

![页面组成部分](img/MySQL Workbench界面组成部分.jpg)



## 数据库的创建

![页面组成部分](img/数据库的创建.jpg)



## 创建数据表

![创建数据表](img/创建数据表.jpg)

```html

DataType数据类型:

·int 整数
·varchar(len)字符串
·tinyint(1)布尔值


字段的特殊标识:
·PK (Primary Key)主键、唯一标识
·NN (Not Null)值不允许为空
·uQ (Unique)值唯一
·Al (Autoincrement)值自动增长
·default 默认值
```
## 向表中写入数据

<img src='img/向表中写入数据.jpg'>

## 什么是SQL
```
什么是SQL

SQL(英文全称: Structured Query Language)是结构化查询语言，专门用来访问和处理数据库的编程语言。能够让我们以编程的形式，操作数据库里面的数据。
三个关键点:
1.SQL是一门数据库编程语言
2.使用SQL语言编写出来的代码，叫做SQL语句
3.SQL语言只能在关系型数据库中使用(例如MySQL、Oracle、SQL Server)。非关系型数据库(例如Mongodb)不支持SQL语言


SQL能做什么

从数据库中查询数据
向数据库中插入新的数据
更新数据库中的数据
从数据库删除数据
可以创建新数据库
可在数据库中创建新表
可在数据库中创建存储过程、视图
etc...

SQL的学习目标
重点掌握如何使用SQL从数据表中:
查询数据(select)、插入数据(insert into) 、更新数据(update) 、删除数(delete)
额外需要掌握的4种SQL语法:
where条件、and和or运算符、order by排序、count(*)函数

```
## 查询语句
```mysql
-- SELECT语句用于从表中查询数据。执行的结果被存储在一个结果表中(称为结果集)。语法格式如下:

-- 从FROM指定的【表中】，查询出【所有的】数据。*表示【所有列】
SELECT * FROM表名称
--从FROM指定的【表中】，查询出指定列名称(字段)的数据。
SELECT 列名称 FROM表名称

-- 通过*把user表中所有数据查出来
-- select * from users

-- 从users表中把username和password 对应数据查出来
-- select username,username from users

```
 ## 插入语句
 ```mysql
-- 向users 表中，插入一条username为tonystarkpassword 为098123的用户数据，示例如下:
insert into users (username,password)values('tony stark','098123')

 ```
 ## 修改语句
 ```mySQL
-- Update语句用于修改表中的数据。语法格式如下:
--语法解读:
--1.用UPDATE指定要更新哪个表中的数据
--2.用SET 指定列对应的新值
--3．用WHERE指定更新的条件
UPDATE表名称SET列名称=新值 WHERE列名称=某值

update users set password='888888' where id=4
-- 更新多个条件
update users set password='admin123' , status='0' where id=5

```
## 删除语法
```mySQL
-- 2.DELETE示例
-- 从users表中，删除id为4的用户，示例如下:
delete from users where id=4
```
## SQL的WHERE子句
```mysql
WHERE子句用于限定选择的标准。在SELECT、UPDATE、DELETE语句中，皆可使用WHERE子句来限定选择的标准。

1--查询语句中的WHERE条件
2 SELECT 列名称 FROM 表名称 WHERE 列 运算符 值
3 --更新语句中的wHERE条件
4 UPDATE 表名称 SET 列=新值 WHERE 列 运算符 值
5 --删除语句中的 wHERE条件
6 DELETE FROM 表名称 wHERE 列 运算符 值

2.可在 WHERE子句中使用的运算符
下面的运算符可在WHERE子句中使用，用来限定选择的标准:
```
操作符 | 描述
--- | ---
= | 等于
!= |不等于
> | 大于
< | 小于
>= | 大于等于
<= | 小于等于
BETWEEN | 在某个范围内
LIKE | 搜索某种模式

## SQL的AND和OR运算符
```
1.语法
AND和OR可在WHERE子语句中把两个或多个条件结合起来。
AND表示必须同时满足多个条件，相当于JavaScript 中的&&运算符，例如 if (a !== 10 && a !== 20)
OR表示只要满足任意一个条件即可，相当于JavaScript 中的Ⅱ运算符，例如if(a !== 10|| a !== 20)

```
## SQL的ORDER BY子句
```mysql
ORDER BY子句-升序排序
select * from users oreder by status DESC

ORDER BY子句-多重排序
对users 表中的数据，先按照 status 字段进行降序排序，再按照username的字母顺序，进行升序排序，示例如下:
select * from users oreder by status ASC,username DESC

tip:id是不变的值，如果中间有被删除的，id不会再连续
```
## SQL的COUNT(*)函数
```
1.语法
COUNT(*)函数用于返回查询结果的总数据条数,语法格式如下:
select count(*) from 表名字
2.使用AS为列设置别名
如果希望给查询出来的列名称设置别名，可以使用AS关键字，示例如下;
select count(*) as total from 表名字

```
## 在项目中操作数据库的步骤
```
1.安装操作MySQL数据库的第三方模块(mysql)
2.通过mysql模块连接到MySQL数据库
3.通过mysql模块执行SQL语句
```
## 安装与配置mysql模块
```
1.安装mysql模块
mysql模块是托管于npm 上的第三方模块。它提供了在Node.,js项目中连接和操作MySQL数据库的能力。
想要在项目中使用它，需要先运行如下命令，将mysql安装为项目的依赖包:
npm i mysql2

```
## 连接数据库与服务器
```js
//连接数据库
const mysql = require('mysql2');
const db = mysql.createPool({
    host: '127.0.0.1',
    user: 'root',
    password: 'admin123',
    database: 'my_database'
})
//判断数据库是否连接正常
db.query('SELECT 1', (err, results) => {
    if (err) return console.log(err.message);
    //打印出 [ { '1': 1 } ]就是表明数据库连接正常
    console.log(results);
})
```
## 使用mysql模块操作MySQL数据库
```js
// 1.查询数据
const sqlStr = 'select * from users'
db.query(sqlStr, (err, result) => {
    if (err) return console.log(err.message);
    //打印出 [ { '1': 1 } ]就是表明数据库连接正常
    console.log(result);
})

// 2.插入数据
const user = { username: 'zhangsan', password: '9999999' }
//？作为占位符
const addStr = 'insert into users (username,password) value(?,?)'
db.query(addStr, [user.username, user.password], (err, result) => {
    if (err) return console.log(err.message);
    //可以通过result.affectedRows查询是否插入成功
    if (result.affectedRows===1) {
        console.log('插入数据成功');
    }
})
//插入数据的简便方法
const user = { username: 'zhangsan', password: '9999999' }
//？作为占位符
const addStr = 'insert into users set ？'
db.query(addStr,user, (err, result) => {
    if (err) return console.log(err.message);
    //可以通过result.affectedRows查询是否插入成功
    if (result.affectedRows===1) {
        console.log('插入数据成功');
    }
})
//3.更新数据
const user3 = { username: 'yangyangyang', password: '6565656', id: 2 }
const addStr3 = 'update users set username=?,password=? where id=?'
db.query(addStr3, [user3.username, user3.password, user3.id], (err, result) => {
    if (err) return console.log(err.message);
    if (result.affectedRows === 1) {
        console.log('更新数据成功');
    }
})
//更新数据的简便方法
const user3 = { username: 'yangyangyang', password: '6565656', id: 2 }
const addStr3 = 'update users set ? where id=?'
db.query(addStr3, [user,user3.id], (err, result) => {
    if (err) return console.log(err.message);
    if (result.affectedRows === 1) {
        console.log('更新数据成功');
    }
})
//4.删除数据
const addStr5 = 'delete from users where id=?'
db.query(addStr5, 1, (err, result) => {
    if (err) return console.log(err.message);
    if (result.affectedRows === 1) {
        console.log('删除数据成功');
    }
})
//标记删除
// 使用DELETE语句，会把真正的把数据从表中删除掉。为了保险起见，推荐使用标记删除的形式，来模拟删除的动作。
// 所谓的标记删除，就是在表中设置类似于status这样的状态字段，来标记当前这条数据是否被删除。
// 当用户执行了删除的动作时，我们并没有执行DELETE语句把数据删除掉，而是执行了UPDATE语句，将这条数据对应的status字段标记为删除即可。

//标记删除例子
const delStr = 'update users set status=? where id=?'
db.query(delStr, [1, 2], (err, result) => {
    if (err) return console.log(err.message);
    if (result.affectedRows === 1) {
        console.log('删除数据成功');
    }
})
```
## Web开发模式
```html
1.服务端渲染的Web开发模式
服务端渲染的概念:服务器发送给客户端的HTML页面，是在服务器通过字符串的拼接，动态生成的。因此，客户端不需要使用Ajax这样的技术额外请求页面的数据。代码示例如下:
<script>
app.get('/index.html ', (req,res) =>{
// 1．要渲染的数据
const user = { name: 'zs ', age: 20 }
//2．服务器端通过字符串的拼接，动态生成HTML内容
const html = '<h1>姓名: ${user.name}，年龄: ${user.age}</h1>`
// 3．把生成成的页面内容响应给客户点。因此，客户端拿到的是带有真实数据的HTML页面res.send(htm1)
})
</script>

2.服务端渲染的优缺点
优点:
·前端耗时少。因为服务器端负责动态生成HTML内容，浏览器只需要直接渲染页面即可。尤其是移动端，更省电。
·有利于SEO。因为服务器端响应的是完整的HTML页面内容，所以爬虫更容易爬取获得信息，更有利于SEO.
缺点:
·占用服务器端资源。即服务器端完成HTML页面内容的拼接，如果请求较多，会对服务器造成一定的访问压力。
·不利于前后端分离，开发效率低。使用服务器端渲染，则无法进行分工合作，尤其对于前端复杂度高的项目，不利于项目高效开发。

3.前后端分离的Web开发模式
前后端分离的概念:前后端分离的开发模式，依赖于Ajax技术的广泛应用。简而言之，前后端分离的Web开发模式就是后端只负责提供API接口，前端使用Ajax调用接口的开发模式。

优点:
开发体验好。前端专注于UI页面的开发，后端专注于api的开发，且前端有更多的选择性。用户体验好。Ajax技术的广泛应用，极大的提高了用户的体验，可以轻松实现页面的局部刷新。
减轻了服务器端的渲染压力。因为页面最终是在每个用户的浏览器中生成的。

缺点:
不利于SEO。因为完整的HTML页面需要在客户端动态拼接完成，所以爬虫对无法爬取页面的有效信息。(解决方
案:利用Vue、React等前端框架的SSR(server side render)技术能够很好的解决SEO问题! )

```
## 如何选择Web开发模式
```
不谈业务场景而盲目选择使用何种开发模式都是耍流氓。
比如企业级网站，主要功能是展示而没有复杂的交互，并且需要良好的SEO，则这时我们就需要使用服务器端渲染;
而类似后台管理项目，交互性比较强，不需要考虑SEO，那么就可以使用前后端分离的开发模式。

另外，具体使用何种开发模式并不是绝对的，为了同时兼顾了首页的渲染速度和前后端分离的开发效率，一些网站采用首屏服务器端渲染＋其他页面前后端分离的开发模式。
```
## 身份认证
```
什么是身份认证
身份认证(Authentication)又称“身份验证”、“鉴权”，是指通过一定的手段，完成对用户身份的确认。

不同开发模式下的身份认证
对于服务端渲染和前后端分离这两种开发模式来说，分别有着不同的身份认证方案:
·服务端渲染推荐使用Session认证机制
·前后端分离推荐使用JWT认证机制

```
## Session认证机制
```
1.HTTP协议的无状态性
了解HTTP协议的无状态性是进一步学习Session认证机制的必要前提。
HTTP协议的无状态性，指的是客户端的每次HTTP请求都是独立的，连续多个请求之间没有直接的关系，服务器不会主动保留每次HTTP请求的状态。

2.如何突破HTTP无状态的限制
对于超市来说，为了方便收银员在进行结算时给VIP用户打折，超市可以为每个VIP用户发放会员卡。

注意:现实生活中的会员卡身份认证方式，在 Web开发中的专业术语叫做Cookie。

```

## 什么是Cookie
```
Cookie是存储在用户浏览器中的一段不超过4KB的字符串。它由一个名称(Name)、一个值(Value)和其它几个用于控制Cookie有效期、安全性、使用范围的可选属性组成。
不同域名下的Cookie 各自独立，每当客户端发起请求时，会自动把当前域名下所有未过期的Cookie一同发送到服务器。
Cookie的几大特性:
·自动发送
·域名独立
·过期时限
·4KB限制
```
## Cookie在身份认证中的作用
```
认证机制
客户端第一次请求服务器的时候，服务器通过响应头的形式，向客户端发送一个身份认证的Cookie，客户端会自动将Cookie保存在浏览器中。
随后，当客户端浏览器每次请求服务器的时候，浏览器会自动将身份认证相关的Cookie，通过请求头的形式发送给服务器，服务器即可验明客户端的身份。
```
[cookie](img/Cooki e.jpg)

## Cookie 不具有安全性
```
由于Cookie 是存储在浏览器中的，而且浏览器也提供了读写Cookie的API，因此Cookie很容易被伪造，不具有安全性。因此不建议服务器将重要的隐私数据，通过Cookie的形式发送给浏览器。
tip:千万不要用Cookie存放隐私数据，比如身份数据，密码。
```
## 提高身份认证的安全性
```
为了防止客户伪造会员卡，收银员在拿到客户出示的会员卡之后，可以在收银机上进行刷卡认证。只有收银机确认存在的会员卡，才能被正常使用。
这种“会员卡＋刷卡认证”的设计理念，就是Session认证机制的精髓。

```
## Session工作原理
[Session工作原理](img/Session%E5%B7%A5%E4%BD%9C%E5%8E%9F%E7%90%86.jpg)

## 在 Express中使用Session认证
```
2.配置express-session 中间件
express-session中间件安装成功后，需要通过app.use()来注册session中间件，示例代码如下:
```
## JWT认证机制
```
1.了解Session 认证的局限性
Session认证机制需要配合Cookie才能实现。由于Cookie默认不支持跨域访问，所以，当涉及到前端跨域请求后端接口的时候，需要做很多额外的配置。才能实现跨域 Session认证。
注意:
·当前端请求后端接口不存在跨域问题的时候，推荐使用Session身份认证机制。
·当前端需要跨域请求后端接口的时候，不推荐使用Session身份认证机制，推荐使用JWT认证机制。
```
## 3.JWT的工作原理
[JWT的工作原理](img/JWT%E5%8E%9F%E7%90%86.jpg)
```
总结:用户的信息通过Token字符串的形式，保存在客户端浏览器中。服务器通过还原Token字符串的形式来认证用户的身份。

4.JWT的组成部分
JWT通常由三部分组成，分别是 Header (头部)、Payload(有效荷载)、Signature (签名)。
三者之间使用英文的""分隔，格式如下:
Header.Payload.Signature

6.JWT的三个部分各自代表的含义
JWT的三个组成部分，从前到后分别是 Header、Payload、Signature。
其中:Payload部分才是真正的用户信息，它是用户信息经过加密之后生成的字符串。Header和Signature是安全性相关的部分，只是为了保证Token的安全性。

7.JWT的使用方式
客户端收到服务器该回的WT之后，通常会将它储存在localStorage或sessionStorage 中。
此后，客户端每次与服务器通信，都要带上这个WT的字符串，从而进行身份认证。推荐的做法是把JWT放在HTTP请求头的Authorization字段中，格式如下:

1.了解Session认证的局限性
Session认证机制需要配合Cookie 才能实现。由于Cookie默认不支持跨域访问，所以，当涉及到前端跨域请求后端接口的时候，需要做很多额外的配置，才能实现跨域Session认证。
注意:
当前端请求后端接口不存在跨域问题的时候，推荐使用Session身份认证机制。
当前端需要跨域请求后端接口的时候，不推荐使用Session身份认证机制，推荐使用JWT认证机制。

```
## 在Express中使用JWT
```html
1.安装JWT相关的包
运行如下命令，安装如下两个JWT相关的包:
jsonwebtoken用于生成JWT字符串
express-jwt用于将JWT字符串解析还原成JSON对象

2.导入JWT相关的包
使用require()函数，分别导入JWT相关的两个包:

3.定义secret密钥
为了保证WT字符串的安全性，防止JWT字符串在网络传输过程中被别人破解，我们需要专门定义一个用于加密和解密的secret密钥:
当生成WT字符串的时候，需要使用secret密钥对用户的信息进行加密，最终得到加密好的JWT字符串当把JWT字符串解析还原成JSON对象的时候，需要使用secret密钥进行解密

4.在登录成功后生成JWT字符串
调用jsonwebtoken包提供的sign()方法，将用户的信息加密成JWT字符串，响应给客户端:

5.将JWT字符串还原为JSON对象
客户端每次在访问那些有权限接口的时候，都需要主动通过请求头中的Authorization字段，将Token字符串发送到服务器进行身份认证。
此时，服务器可以通过express-jwt这个中间件，自动将客户端发送过来的Token解析还原成JSON对象:

7.捕获解析JWT失败后产生的错误
当使用express-jwt解析Token字符串时，如果客户端发送过来的Token字符串过期或不合法，会产生一个解析失败的错误，影响项目的正常运行。我们可以通过Express的错误中间件，捕获这个错误并进行相关的处理，示例代码如下:

<script>
    // 导入 express 模块
const express = require('express')
// 创建 express 的服务器实例
const app = express()

// TODO_01：安装并导入 JWT 相关的两个包，分别是 jsonwebtoken 和 express-jwt
const jwt = require('jsonwebtoken')
const expressJWT = require('express-jwt')

// 允许跨域资源共享
const cors = require('cors')
app.use(cors())

// 解析 post 表单数据的中间件
const bodyParser = require('body-parser')
app.use(bodyParser.urlencoded({ extended: false }))

// TODO_02：定义 secret 密钥，建议将密钥命名为 secretKey
const secretKey = 'itheima No1 ^_^'

// TODO_04：注册将 JWT 字符串解析还原成 JSON 对象的中间件
// 注意：只要配置成功了 express-jwt 这个中间件，就可以把解析出来的用户信息，挂载到 req.user 属性上
app.use(expressJWT.expressjwt({ secret: secretKey, algorithms: ['HS256'] }).unless({ path: [/^\/api\//] }))//新版写法


// 登录接口
app.post('/api/login', function (req, res) {
  // 将 req.body 请求体中的数据，转存为 userinfo 常量
  const userinfo = req.body
  // 登录失败
  if (userinfo.username !== 'admin' || userinfo.password !== '000000') {
    return res.send({
      status: 400,
      message: '登录失败！',
    })
  }
  // 登录成功
  // TODO_03：在登录成功之后，调用 jwt.sign() 方法生成 JWT 字符串。并通过 token 属性发送给客户端
  // 参数1：用户的信息对象
  // 参数2：加密的秘钥
  // 参数3：配置对象，可以配置当前 token 的有效期
  // 记住：千万不要把密码加密到 token 字符中
  const tokenStr = jwt.sign({ username: userinfo.username }, secretKey, { expiresIn: '1s' })
  res.send({
    status: 200,
    message: '登录成功！',
    token: tokenStr, // 要发送给客户端的 token 字符串
  })
})

// 这是一个有权限的 API 接口
app.get('/admin/getinfo', function (req, res) {
  // TODO_05：使用 req.user 获取用户信息，并使用 data 属性将用户信息发送给客户端
  console.log(req.auth)
  res.send({
    status: 200,
    message: '获取用户信息成功！',
    data: req.auth, // 要发送给客户端的用户信息
  })
})

// TODO_06：使用全局错误处理中间件，捕获解析 JWT 失败后产生的错误
app.use((err, req, res, next) => {
  // 这次错误是由 token 解析失败导致的
  if (err.name === 'UnauthorizedError') {
    return res.send({
      status: 401,
      message: '无效的token',
    })
  }
  res.send({
    status: 500,
    message: '未知的错误',
  })
})

// 调用 app.listen 方法，指定端口号并启动web服务器
app.listen(8888, function () {
  console.log('Express server running at http://127.0.0.1:8888')
})
</script>
tips:请求用户名时，要在请求头里面加入{Authorization:Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6IkxlZGdlciIsImlhdCI6MTY2MzgzOTY1OCwiZXhwIjoxNjYzODYxMjU4fQ.QiZ4cr7ZXGY5SOOmfAeHPLGLbwPivZcEy17G-jRUojU}
Bearer一定要加

```



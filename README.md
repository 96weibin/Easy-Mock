# Easy-Mock

Easy mock 可视化的数据伪造  拦截前端ajax，返回伪造的服务器返回数据  使得在后端没有开发完的时候    前端  可以模拟链接服务器的情况

## First先了解一下  mock.js

### 1.安装

```nodejs
npm install mockjs
```

### 2使用

```js
var Mock = require('mockjs')
var data = Mock.mock({
  'name|rule':value,
  ............
})
```

### 语法规范

- 数据模板定义规范

#### 模板

```js
'name|rule':value
/**
 *name 属性名
 *rule 生成规则
 *value 属性值
 */
```

#### 例子

```js
  //属性值是字符串
  'name|min-max':string   //重复string 重复次数大于 min 小于 max
  'name | count':string   //重复count 次

  //属性值是数字
  'name | +1':number // 属性值自动加一
  'name|min - max':number //生成一个 大于min小于max 的整数 ，  number仅用来 确定类型
  'name|min-max.dmin-dmax':number   //生成浮点数，min<整数部分<max  小数部分 保留  dmin 到 dmax 位

  //属性值是布尔类型
  'name|1':boolean  //随机生成一个布尔值
  'name|min-max':value  //随机生成value和!value 概率分别为  min/(min+max) 与 max/(min+max)

  //属性值是对象
  'name|count':object //从object随机选取count个属性
  'name-min-max':object //从object种随机取出 min 到 max 个属性
  //属性值是数组
  'name|1':array  //从array中随机选1个
  'name|+1':array //从array中顺序选取1个
  'name|min-max':array  //重复array   min 到 max 次
  'name|count':array//重复count次

  //属性值是函数
  'name':function //取函数执行后的返回值，函数的上下文 是  name所在的对象

  //属性值是正则表达式
  'name':regexp //生成随机的符合正则的字符串
```

- 数据占位符定规范

链接 <https://github.com/nuysoft/Mock/wiki/Syntax-Specification>   没看懂这玩应有啥用

```js
  //@后面接的就是占位符   他是 Mock。random的方法
  Mock.mock({
    name:{
      first:'@first',
      middle:'@First',
    }
  })
```

### Mock.mock()

### 支持的参数有如下

1. *rurl* 可选 标识要拦截的url  可以是 字符串或正则;

2. *rtype* 可选 标识需要拦截的ajax请求类型 GET等

3. *template* 可选 模板  数据模板，占位符模板

4. *function(options)* 可选 表示用于生成响应式数据的函数

  ->>options   rul type body  通过模拟 XMLHttpRequest行为拦截的ajax

### Mock.mock()参数组合

**Mock.mock(rurl?,rtype?,template|function(options))**参数之间可选 根据需求

### Mock.setup()

指定被拦截的ajax请求的响应时间

```js
  Mock.setup({
    timeout:'200-600' //也可以是固定的数字
  })
```

### Mock.Random

Mock.Random是一个工具类用于生成各种随机数据

### Mock.valid()

#### 校验data是否与 template匹配

```js
  Mock.valid(template,data)
```

*template* 必选 表示数据模板，可以是对象或是字符串

*data*  必选  表示真实数据

#### ej

```js
  var template = {
    name:'value1'
  }
  var data = {
    name:'value2
  }
  Mock.valid(template, data)
```

### Mock.toJSONSchema()

  **Mock.toJSONSchema(template)**把mock.js风格的数据模板转换成 JSON Schema   根据我查了查资料发现  这个json schema  好像是  规范化的  json   便于复用

## EasyMock

1. 点击蓝色加号创建项目

2. 再点击创建接口  就可以创建接口
  --->在里面输入 em.demo.all就可以 得到基本包括所有情况的例子了，这时候  只要根据 Mock.js 语法 和自己的需要更改  demo即可

## Easy Mock CLI

  基于Easy Mock快速生成 api.js的命令行工具

### 安装CLI

```node
  npm install -g easy-mock-cli

  npm install -S easy-mock-cli
```


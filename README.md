# Getting Start

这里是sletjs自动挂载路由的基础示例

## 安装slet模块

```
$ npm i -S slet
```

## 从app.js开始

```
'use strict';

const Slet = require('slet');
const app = new Slet({
    root: __dirname,
    debug: true
});

app.start(3000) 
```

## 创建controllers目录

根据slet默认配置，默认如果有controllers目录，则自动将该目录挂载为路由模块。

如果想定制，可以修改配置项automount.path

```
'use strict';

const Slet = require('slet');
const app = new Slet({
    root: __dirname,
    debug: true,
    "automount": {
        "path": "controllers",
        "option": {
            "recurse": true
        }
    }
});

app.start(3000) 
```

## 编写带有path的controller

由于自动挂载路由，所以没地方指定path，所以path必须出现在controller里

在controller里配置path有2种办法

- this.path = "/"
- MyBasicController.path = "/2"

下面分别给出示例

### 编写basicctrl.js

编写controllers/basicctrl.js

```
'use strict';

const BasicController = require('slet').BasicController

module.exports = class MyBasicController extends BasicController {
  constructor(app, ctx, next) {
    super(app, ctx, next)
    this.path = "/"
  }
  
  get() { 
    let a = this.query.a
    // this.renderType='view'
    return {
      a: 'this is a',
      b: {
        c: 'ssddssdd a= ' + a
      }
    }
  } 
}

```

和example-basic版本的basicctrl.js只有一行不一样的，即

```
this.path = "/"
```

只要是koa-router支持的path，这里都可以写。

### 编写basicctrl2.js

编写controllers/basicctrl2.js

```
'use strict';

const BasicController = require('slet').BasicController

class MyBasicController extends BasicController {
  constructor(app, ctx, next) {
    super(app, ctx, next)
  }
  
  get() { 
    let a = this.query.a
    // this.renderType='view'
    return {
      a: 'this is a',
      b: {
        c: 'ssddssdd a= ' + a
      }
    }
  } 
}

MyBasicController.path = "/2"

module.exports = MyBasicController

```

这是另外一种配置path的方法，通过static属性来配置。

## 启动server

最后，执行app.js，启动server

```
$ node app.js
```

## 查验结果

在浏览器中打开 

- http://127.0.0.1:3000/?a=2
- http://127.0.0.1:3000/2?a=2

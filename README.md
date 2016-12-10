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

## 编写basicctrl.js

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
    var a = this.query.a
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

## 启动server

最后，执行app.js，启动server

```
$ node app.js
```

## 查验结果

在浏览器中打开 http://127.0.0.1:3000/?a=2

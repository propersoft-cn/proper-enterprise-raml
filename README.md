Proper Enterprise Raml
=====================

路径规范
----------
业务部分文件路径按照 类别 -> 模块 -> raml 层次划分路径结构（一定是两层结构）。模块调用其它模块的文档时，采用相对路径的方式引用
```
app                         //公共资源
  securitySchemas
  schemas
platform                    //平台业务
  permission                //权限模块
    types                   //数据结构的公共属性，没有此文件夹可省略下同
    securitySchemas         //api访问的安全机制的公共属性
    ressourceTypes          //模块资源的公共属性
    raits                   //方法的公共属性
    schemas                 //请求参数或者响应结构的公共属性
    api.raml                //模块的raml设计文档
  workflow                  //流程模块
hr                          //人力资源
  leave                     //请假
  attendance                //考勤
```

文档规范
----------
-版本统一使用RAML 1.0
-title为模块名称
-baseUri内路径从类别开始(例：/hr/leave)，和路径保持一致
-公共属性必须定义到指定文件夹内，raml文档使用相对路径引用公共属性

版本号规范
---------
- 版本号采用三位数字（1.1522.49）
- 版本号第一位表示重大更新
- 版本号第二位表示每次需求变更，版本号生成后，要把版本号记录到需求文档上，方便下次查找
- 版本号第三位表示bug等非需求修改
- 前台、后台、raml工程版本号要保持一致，方便三个工程对应。例如第一次需求变更版本号为1.1.0，只修改了前台工程，则前台工程版本号为1.1.0，后台和raml未修改依然为原版本号；第二次需求变更版本号为1.2.0，修改了前台和后台工程，则前台和后台工程版本号变为1.2.0，此处后台工程跳过一个版本直接更新成最新版本

### RAML编写
- RAML 1.0版本不支持多继承，在modules文件夹内新添加模块raml文档时需注意嵌套继承

### Build Steps
```
$ npm install github:cybertk/abao
$ node_modules/abao/bin/abao api.raml --server https://server.propersoft.cn/ihos/api
```

### Transform to HTML
```
$ npm i -g raml2html
$ raml2html api.raml > api.html
```

### API发版
- 连接到npm私服
```
$ npm config set registry http://nexus.propersoft.cn:8081/repository/npm-internal/
$ npm login --registry http://nexus.propersoft.cn:8081/repository/npm-internal/
```
- 执行发版命令
```
$ npm publish
```

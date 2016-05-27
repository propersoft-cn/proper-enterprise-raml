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
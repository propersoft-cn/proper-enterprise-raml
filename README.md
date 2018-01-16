Proper Enterprise Raml
=====================
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

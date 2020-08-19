# Week 19 学习总结
## 工具链——组合工具
- 初始化项目
- 初始化 generator
- 初始化 npm
- 初始化 mocha
## 发布系统——实现一个线上服务
### 安装 Express
在 publish 文件夹中添加 server 文件夹
```js
mkdir server
```
初始化 npm
```js
npm init
```
安装 express
```js
npm install express --save
```
### 启动服务
在 server 文件夹中添加一个文件：
```js
cd. > index.js
``` 
在 index.js 文件中添加如下配置：
```js
const express = require('express')
const app = express()
const port = 3000

app.get('/', (req, res) => {
  res.send('Hello World!')
})

app.listen(port, () => {
  console.log(`Example app listening at http://localhost:${port}`)
})
```
### 使用 express-generator 创建应用
安装并启动 express-generator
```js
npm install -g express-generator
express
```
安装依赖
```js
npm install
```
启动项目
```js
npm start
```
这样我们的 server 就搭建好了。

在 server 文件夹中创建 publish-server 文件夹（这里没有什么用）
```js
mkdir publish-server
```
构建一个没有 view 的 express 应用
```js
npx express-generator --no-view
```
安装依赖
```js
npm install
```
### 上传流式文件
在 server 文件夹中创建 publish-tool 文件夹
```js
mkdir publish-tool
```
安装依赖
```js
npm install
```
在 publish-tool 文件夹中添加 publish.js 文件并添加如下内容，这样就可以流式上传图片了：
```js
const http = require('http');
const fs = require('fs');

let filename = './cat.jpg';

fs.stat(filename, (error, stat) => {
    const options = {
        host: 'localhost',
        port: 8081,
        path: '/?filename=cat.jpg',
        method: 'POST',
        headers: {
            'Content-Type': 'application/octet-steam',
            'Content-Length': stat.size
        }
    }

    const req = http.request(options, (res) => {
        console.log(`STATUS: ${res.statusCode}`);
        console.log(`HEADERS: ${JSON.stringify(res.headers)}`);
    });

    req.on('error', (e) => {
        console.error(`problem with request: ${e.message}`);
    });

    // Write data to request body
    let readStream = fs.createReadStream('./cat.jpg');
    readStream.pipe(req);
    readStream.on('end', () => {
        req.end();
    });
});
```
### 接收流式文件
创建一个 名为 publish-server-vanilla 文件夹，创建一个 index.js 文件并添加内容：
```js
const http = require('http');
const fs = require('fs');

const server = http.createServer((req, res) => {
    let matched = req.url.match(/filename=([^$]+)/);
    let filename = matched && matched[1];
    console.log(filename);
    if (!filename) return;
    let writeStream = fs.createWriteStream('../server/public/' + filename);
    req.pipe(writeStream);
    req.on('end', () => {
        res.writeHead(200, {
            'content-Type': 'text/plain'
        });
        res.end('okay');
    });
});

server.listen(8081);
```
### 压缩并上传文件
在 publish-tool 项目中安装 archive 依赖
```js
npm install archiver
```
修改 publish.js 文件
```js
const http = require('http');
const fs = require('fs');
let archiver = require('archiver');
let packName = './package';

const options = {
    host: 'localhost',
    port: 8081,
    path: '/?filename=' + 'package.zip',
    method: 'POST',
    headers: {
        'Content-Type': 'application/octet-steam'
    }
}

const req = http.request(options, (res) => {
    console.log(`STATUS: ${res.statusCode}`);
    console.log(`HEADERS: ${JSON.stringify(res.headers)}`);
});

req.on('error', (e) => {
    console.error(`problem with request: ${e.message}`);
});

var archive = archiver('zip', {
    zlib: { level: 9 } // Sets the compression level.
});

archive.directory(packName, false)

archive.pipe(req);

archive.finalize();

archive.on('end', () => {
    req.end();
});
```
### 解压文件
在 publish-server-vanilla 项目中安装 unzipper 依赖
```js
npm install unzipper
```
修改 publish-server-vanilla 项目中的 index.js 文件
```js
const http = require('http');
const fs = require('fs');
const unzip = require('unzipper');

const server = http.createServer((req, res) => {
    
    let writeStream = unzip.Extract({path: '../server/public/'});
    req.pipe(writeStream);
    /*req.on('data', trunk => {
        writeStream.write(trunk);
    });
    req.on('end', trunk => {
        writeStream.end(trunk);
    });*/
    req.on('end', () => {
        res.writeHead(200, {
            'content-Type': 'text/plain'
        });
        res.end('okay');
    });
});

server.listen(8081);
```
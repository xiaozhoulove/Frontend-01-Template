# Week 20 学习总结
## Oauth
- 理解Oauth 流程 了解鉴权实现及其原理 预想可以用来应用到公司的管理系统
- 可以通过node的exec使用open + url的方式直接调起浏览器
## Publish
- 由tool唤起浏览器白屏页面进行Oauth授权
- 授权过后跳转server 并带着token返回到publish tool的白屏界面
- 在此之后就可以进行一些发布的操作了 白屏页面可以自定义自己的配置 上传要发布的文件 选择发布位置等操作

## PhantomJS
### 简介
PhantomJS 是一个命令行工具，类似于 node

### 安装
将下载到的文件 phantomjs 安装到 PATH 中的某个位置

### 使用
新建 hello.js 文件，加入以下代码
```js
var page = require("webpage").create();
page.open("http://baidu.com", function (status) {
  console.log("Status: " + status);
  if (status === "success") {
    page.render("./baidu.png"); // 将http://baidu.com生成一个baidu.png图片
  }
  phantom.exit();
});
```
```js
phantomjs hello.js
```
生成http://localhost:8000/页面节点
```js
var page = require("webpage").create();
page.open("http://localhost:8000/", function (status) {
  console.log("Status: " + status);
  if (status === "success") {
    var body = page.evaluate(function () {
      var toString = function (pad, element) {
        var children = element.childNodes;
        var childrenString = "";
        for (var i = 0; i < children.length; i++) {
          childrenString += toString("    " + pad, children[i] + "\n");
        }
        var name;
        if (element.nodeType === Node.TEXT_NODE) {
          name = "#text " + JSON.stringify(element.textContent);
        }
        if (element.nodeType === Node.ELEMENT_NODE) {
          name = element.tagName;
        }
        return pad + name + (childrenString ? "\n" + childrenString : "");
      };
      return toString("", document.body);
    });
    console.log(body);
  }
  phantom.exit();
});
```
## GitHub Oauth
### 获取 code
```js
var url = `https://github.com/login/oauth/authorize?client_id=${client_id}&redirect_uri=${encodeURIComponent(
  "http://localhost:8000"
)}&user=read:%3Auser&state=123abc`;
```
### 获取 access_token
```js
const code = "your code";
const state = "123abc";
const client_secret = "your client_secret";
const client_id = "your client_id";
const redirect_uri = encodeURIComponent("http://localhost:8000");
const params = `code=${code}&state=${state}&client_secret=${client_secret}&client_id=${client_id}&redirect_uri=${redirect_uri}`;
const request_url = `https://github.com/login/oauth/access_token?${params}`;

function request(url, method, config) {
  var xmlhttp;
  if (window.XMLHttpRequest) {
    //  IE7+, Firefox, Chrome, Opera, Safari 浏览器执行代码
    xmlhttp = new XMLHttpRequest();
  } else {
    // IE6, IE5 浏览器执行代码
    xmlhttp = new ActiveXObject("Microsoft.XMLHTTP");
  }
  xmlhttp.onreadystatechange = function () {
    if (xmlhttp.readyState == 4 && xmlhttp.status == 200) {
      console.log("===响应===", xmlhttp.responseText);
    }
  };

  xmlhttp.open(method, url, true);
  xmlhttp.setRequestHeader("Authorization", "");
  xmlhttp.send();
}

request("request_url", "POST");
```
### 获取用户信息
```js
function request(url, method) {
  var xmlhttp;
  if (window.XMLHttpRequest) {
    //  IE7+, Firefox, Chrome, Opera, Safari 浏览器执行代码
    xmlhttp = new XMLHttpRequest();
  } else {
    // IE6, IE5 浏览器执行代码
    xmlhttp = new ActiveXObject("Microsoft.XMLHTTP");
  }
  xmlhttp.onreadystatechange = function () {
    if (xmlhttp.readyState == 4 && xmlhttp.status == 200) {
      console.log("===响应===", xmlhttp.responseText);
    }
  };

  xmlhttp.open(method, url, true);
  xmlhttp.setRequestHeader(
    "Authorization",
    "token d00bdd5d3f1605db80460a0747f07284850d1e40"
  );
  xmlhttp.send();
}

request("https://api.github.com/user", "GET");
```
# Week 18 学习总结
## Dev工具
- Server
    - build: webpack babel vue jsx postcss……
    - watch: fsevent
    - mock: ……
    - http: websocket
- Client
    - debugger: vscode devtool
    - source map
## 测试工具
### Mocha
1. 搭建项目
```js
npm init
```
2. 安装 Mocha
```js
npm install --save-dev mocha
```
3. 创建目录
```js
├───test/
    ├───src/
    │   └───add.js
    └───test/
        └───add.test.js
```
4. 添加测试用例
```js
var assert = require('assert');
var add = require('../src/add.js');
describe('add', function () {
    it('should return -1 when the value is not present', function () {
      assert.equal(add.add(3, 4), 7);
    });
});
```
5. 在package.json 修改 scripts 配置
```js
"test": "mocha"
```
6. 兼容 ES6 module 语法
- 安装最新版本 nodejs

- 在 package.json 文件中添加如下代码：
```js
"type": "module"
```
### nyc
1. 安装 nyc
```js
npm install nyc
```
2. 在 package.json 中添加脚本
```js
"coverage": "nyc mocha"
```
4. 添加 .nycrc 文件
```js
{
    "all": true,
    "include": [
        "dist/*.js"
    ]
}
```
3. 安装 webpack
```js
npm install --save-dev webpack
```
4. 安装 babel
```js
npm install --save-dev babel-loader @babel/core @babel/preset-env
```
5. 添加 .babelrc 文件
```js
{
    "presets": ["@babel/preset-env"]
}
```
6. 添加 package.json scripts 配置
```js
"coverage": "nyc mocha"
```
### ava
1. 安装
```js
npm install --save-dev ava
npm install --save-dev @babel/register
npm install --save-dev @ava/babel
```
2. 修改 add.test.js 文件
```js
let mod = require('../src/add.js');
let test = require('ava');

test('foo', t => {
    if (mod.add(3, 4), 7) {
        t.pass();
    }
});
```
3. 在 package.json 文件中添加 ava 配置
```js
"ava": {
    "files": [
      "test/*.js"
    ],
    "require": [
      "@babel/register"
    ],
    "babel": {
      "testOptions": {
        "babelrc": true
      }
    }
  }
```
4. 修改 .nycrc 文件
```js
{
    "all": true,
    "include": [
        "src/*.js"
    ]
}
```
5. 修改 package.json 文件中的 scripts 配置
```js
"test": "ava",
"coverage": "nyc ava"
```
### istanbuljs 插件
1. 安装
```js
npm install --save-dev @istanbuljs/nyc-config-babel
npm install --save-dev babel-plugin-istanbul
```
2. 在 .nycrc 文件中新增如下选项
```js
"extends": "@istanbuljs/nyc-config-babel"
```
3. 在 .babelrc 文件中添加如下配置
```js
"plugins": ["babel-plugin-istanbul"]
```
4. 修改 add.test.js 文件
```js
import { add } from '../src/add.js';
import assert from 'assert';

it('add(3, 4) should be 7', () => {
    assert.equal(add(3, 4), 7);
});
```
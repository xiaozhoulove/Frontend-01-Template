# Week 17 学习总结
## 工具链
### 工具
- 基础工具

  - nvm
  - node
  - npm
- 初始化

  - yeoman
  - vue-cli
  - create-react-app
- 开发/调试

  - dev-tool / chrome
  - webpack-dev-server
  - mock
  - wireshark
  - charles
  - vite
- 测试

  - mocha
  - jest
- 发布

  - lint
  - jenkis

## 在没有函数名字的函数里面实现递归 anonymous recursion
```js
let y = g => 
    (f => f(f))(
      self =>
        g( (...args) => self(self).apply(this, args) )
    )

    
let f = y(self => {
  return n => n > 0 ? self(n - 1) + n : 0
})

f(100)
```
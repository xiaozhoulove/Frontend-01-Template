# Week 05 学习总结
## 浏览器工作原理——总论与HTTP协议
- URL=(HTTP)=>HTML=(parse)=>DOM=(css computing)=>DOM with CSS=(layout)=>DOM with position=(render)=>Bitmap

### ISO-OSI七层网络模型



### TCP与IP的一些基础知识
- 流
- 端口
- require('net');
- 包
- IP地址
- libnet/libpcap

### HTTP
- Request
- Response

## JavaScript里的结构化程序设计的基础设施

### JS执行粒度
- JS Context => Realm
- 宏任务
- 微任务（Promise）
- 函数调用（Execution Context）
- 语句/声明
- 表达式
- 直接量/变量/this ...
- 函数调用（Execution Context）
- code evaluation state——代码执行位置 async generate
- Function
- Script or Module
- Generator
- Realm
- LexicalEnvironment——词法环境
- this
- new.target
- super
- 变量
- VariableEnvironment——变量环境
- 历史遗留的包袱，仅仅用于处理var声明
- Environment Record
- Declarative Environment Records
    - Function Environment Records(Function - Closure)
    - module Environment Records
- Global Environment Records
- Object Environment Records
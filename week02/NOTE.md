# Week 02 学习总结
## 编程语言通识：
- 了解了形式语言和非形式语言
- 了解了什么是产生式：将源程序经过词法分析和语法分析后得到的一系列符合文法规则的语句
- 知道了市面上的那些语言，有强类型和弱类型语言、有动态和静态语言。

## 巴科斯范式：
- (Backus Normal Form, 简称BNF)

- 是一种用于表示上下文无关文法的语言, 上下文无关文法描述了一类形式语言.
- 尽管巴科斯范式也能表示一部分自然语言的语法, 它还是更广泛的用于程序设计语言, 指令集, 通信协议的语法表示中

### 介绍
- BNF 规定是推到规则(产生式)的集合, 写为:

- <符号>::=<使用符号的表达式>

- 这里的<符号>是非终结符, 而表达式由一个符号序列, 或勇表示选择的竖杠 '|'分隔的多个符号序列构成, 每个符号序列整体都是左端的符号的一种可能的替代. 从未在末端出现的符号叫做终结符

### 产生式(BNF - 巴科斯范式)
- 用尖括号括起来的名称来表示语法结构名
- 语法结构分成基础结构和需要用其他语法结构定义的复用结构
- 基础结构称终结符
- 复合结构称非终结符
- 引号和中间的字符表示终结符
- 可以有括号
- *表示重复多次
- | 表示或
- 表示至少一次
- 四则运算:
    - 1 + 2 * 3
- 终结符:
    - Number
    - +-*/
- 非终结符
    - MulitiplicativeExpression
    - AddtiveExpression

## 动态与静态：
### 动态

- 在用户的设备/在线服务器上
- 产品实际运行时
- runtime
### 静态

- 在程序员的设备上
- 产品开发时
- compiletime (编译时)

## 类型系统：
- 动态类型系统与静态类型系统
- 强类型与弱类型
    - String + Number
    - String == Boolean
- 复合类型
    - 结构体
    - 函数签名
- 子类型
    - 逆变/协变

## 词法和类型：
- InputElement
    - WhiteSpace
    - LineTerminator
    - Comment
    - Token
        - Punctuator
        - IdentifierName
            - Keywords
            - Identifier
            - Future reserved Keywords: enum
        - Literal
            - Number
            - String
            - Boolean
            - Null
            - Undefined
            - Object
            - Symbol
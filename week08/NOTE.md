# Week 08 学习总结
## 重学CSS选择器
### 1、选择器语法

- 简单选择器
    - div svg | a (namespace?)
    - .class
    - #id
    - [attr=value] （~ | ）（[arrt]）
    - :hover
    - ::before
- 复合选择器(与的关系)
    - <简单选择器><简单选择器><简单选择器>
    - * 或者div必须写在最前面
- 复杂选择器
    - <复合选择器><复合选择器> 子孙关系
    - <复合选择器>">"<复合选择器> 父子关系
    - <复合选择器>"~"<复合选择器> sibling
    - <复合选择器>"+"<复合选择器> sibling
    - <复合选择器>"||"<复合选择器> leve4，兼容性不好
- 选择器列表
    - 使用“，”分隔
### 2、选择器优先级

##### 通配选择符（universal selector）（*）关系选择符（combinators）（+, >, ~, ' ', ||）和 否定伪类（negation pseudo-class）（:not()）对优先级没有影响。（但是，在 :not() 内部声明的选择器会影响优先级）。

- 简单选择器计数
- 伪类
    - 链接/行为
        - :any-link
        - :link :visited
        - :hover
        - :active
        - :focus
        - :target
    - 树结构
        - :empty 没有子元素
        - :nth-child()
        - :nth-last-child()
        - :first-child :last-child :only-child
    - 逻辑型
        - :not伪类
        - :where :has
- 伪元素
    - ::before
    - ::after
    - ::first-line 选中已有内容的第一行（第一行与回车没有关系，只是显示）
        - font系列
        - color系列
        - background系列
        - word-spacing
        - letter-spacing
        - text-decorating
        - text-transform
        - line-height
    - ::first-letter
        - font系列
        - color系列
        - background系列
        - word-spacing
        - letter-spacing
        - text-decorating
        - text-transform
        - line-height
        - float
        - vertical-align
        - 盒模型系列：margin、padding、border
##### 为什么first-letter可以设置display:float之类的，而first-line不行？
##### 选中的first-line如果加上float属性会脱离文档流，font属性作用于文字而非box上。

## 重学CSS排版
### 1、盒（Box）

- 标签 元素 盒

    - CSS选择器选中的时元素

    - CSS选择器选中的元素，在排版时可能会产生多个盒

    - 排版盒渲染的基本单位时盒

### 2、盒模型

- content
- padding
- border
- margin
- box-sizing
- content-box
- border-box = content-box + border + padding
### 3、正常流（Normal Flow）

- 从写字的角度考虑排版
    - 从左到右书写
    - 同一行写的文字都是对齐的
    - 一行写满了，就换到下一行
- 正常流排版
    - 收集盒进行
    - 计算盒子行中的排布
    - 计算行的排布
- 排版元素
    - 正常文字
    - inline-box元素，有自己的宽盒高属性（IFC）
    - block-box元素，占一整行 （BFC: Block formatting context）
### 4、正常流的行模型

- baseline基线

- 一个inline-box里面没有内容，它的基线在盒子底部

- inline-box元素本身的height可能会超过line-height，vertical-align属性就会保证行内最高的元素对齐方式正确

- 建议：inline-box元素的vertical-laign属性只使用：top、middle、bottom

### 5、float与clear

- clear属性可以用于清除浮动

- float元素可以添加clear属性达到换行的目的

- float元素也可以添加margin属性

- inline-block元素之间会有空白，来自于html标签间的换行符

### 6、BFC

- 对边距留白margin的影响

- 正常流的margin可以复用

- 正常流中间嵌套一个新元素

    - 容器触发条件：
        - overflow:hidden（overflow:visible无影响，称之为BFC的合并）
        - display:inline-block
        - margin-top的效果
        - 其他正常流元素
- BFC 与float之间相互作用

### 7、Flex排版

- 收集盒进行
- 计算盒再主轴方向的排布
- 计算盒再交叉轴方向的排布
- component
    - flex-grow
    - flex-basis
    - flex-shrink
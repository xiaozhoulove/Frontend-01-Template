# Week 13 学习总结
## 组件化基础
### 对象与组件
- 对象
- Properties
- Methods
- Inherit
- 组件
    - Properties
    - Methods
    - Inherit
    - Attribute
    - Config & State
    - Event
    - Lifecycle
    - Children
### Component
- End User Input
    - State
    - Children
- Component User's Markup Code
    - atrribute
- Component User's JS Code
    - Method
    - Property
    - Event
### Attribute
- Attribute 强调描述性
- Property 强调从属关系
### 如何设计组件状态
Markup set	JS set	JS Change	User Input Chage	
X	√	√	？	poperty
√	√	√	？	attribute
X	X	X	√	state
X	√	X	X	config
### Lifecycle
- created
    - mount
        - mount
        - mount
        - unmount
    - js change/set
        - render/update
    - user input
        - render/update
- destroyed
### Children
- Content型
- Template型
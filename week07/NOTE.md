# Week 07 学习总结
## CSS脑图
### CSS
- at rules
- - @charset ： https://www.w3.org/TR/css-syntax-3/
- - @import ：https://www.w3.org/TR/css-cascade-4/
- - @media ：https://www.w3.org/TR/css3-conditional/
- - @page ： https://www.w3.org/TR/css-page-3/
- - @counter-style ：https://www.w3.org/TR/css-counter-styles-3
- - @keyframes ：https://www.w3.org/TR/css-animations-1/
- - @fontface ：https://www.w3.org/TR/css-fonts-3/
- - @supports ：https://www.w3.org/TR/css3-conditional/
- - @namespace ：https://www.w3.org/TR/css-namespaces-3/
- rule
- - Selector
- - - selector_group
- - - combinator
- - - simple_selector
    - - - type
    - - - .
    - - - []
    - - - :
    - - - ::
- - Declaration
- - - Key
    - - - property
    - - - variable
- - - Value
## BFC（Block Formatting Context，块格式化上下文）
### 含义：块格式化上下文是Web页面的可视CSS渲染的一部分，是块盒子的布局过程发生的区域，也是浮动元素与其他元素交互的区域
### 发生场景：
- 根元素()
- 浮动元素（元素的 float 不是 none）
- 绝对定位元素（元素的 position 为 absolute 或 fixed）
- 行内块元素（元素的 display 为 inline-block）
- 表格单元格（元素的 display为 table-cell，HTML表格单元格默认为该值）
- 表格标题（元素的 display 为 table-caption，HTML表格标题默认为该值）
- 匿名表格单元格元素（元素的 display为 table、table-row、 table-row-group、table-header-group、table-footer-group（分别是HTML table、row、tbody、thead、tfoot的默认属- 性）或 inline-table）
- overflow 值不为 visible 的块元素
- display 值为 flow-root 的元素
- contain 值为 layout、content或 paint 的元素
- 弹性元素（display为 flex 或 inline-flex元素的直接子元素）
- 网格元素（display为 grid 或 inline-grid 元素的直接子元素）
- 多列容器（元素的 column-count 或 column-width 不为 auto，包括 column-count 为 1）
- column-span 为 all 的元素始终会创建一个新的BFC，即使该元素没有包裹在一个多列容器中（标准变更，Chrome bug）
### 浮动定位和清除浮动只会发生在一个BFC内，不会影响其他的BFC
### 外边距重叠也只会发生在同一个BFC内
# 写一个正则表达式 匹配所有 Number 直接量
整型直接量：

概念
一个数字序列表示一个十进制整数

对应正则
/^-?[0-9]\d*$/

十六进制直接量：

概念
以 0x或 0X为前缀，其后跟随十六进制数串的直接量

对应正则
/(0x)?[0-9a-fA-F]+/

八进制直接量：

概念：
八进制直接量以数字0开始， 其后跟随一个由0~7（包括0和7）之间的数字组成的序列

注意： 由于某些JavaScript的实现支持八进制直接量， 而有些不支持， 因此最好不要使用以0为前缀的整型直接量，毕竟我们无法得知当前JavaScript的实现是否支持八进制的解析。

在ES6的严格模式下， 八进制直接量是明令禁止的

对应正则
/0?[0-7]*/

浮点型直接量：

概念
浮点型直接量可以含有小数点，采用的是传统的实数写法。
一个实数由整数部分、小数点和小数部分组成

对应正则
/^-?([1-9]\d*\.\d*|0\.\d*[1-9]\d*|0?\.0+|0)$/

匹配所有Number直接量的正则：

/^-?[0-9]\d*$|(0x)?[0-9a-fA-F]+|0?[0-7]*|^-?([1-9]\d*\.\d*|0\.\d*[1-9]\d*|0?\.0+|0)$/

# 写一个 UTF-8 Encoding 的函数
function UTF8Encoding(str) {
  const code = encodeURIComponent(str)
  const bytes = []

  for (let i = 0; i < code.length; i++) {
    const c = code.charAt(i)
    if (c === '%') {
      const hex = code.charAt(i + 1) + code.charAt(i + 2)
      const hexVal = parseInt(hex, 16)
      bytes.push(hexVal)
      i += 2
    } else {
      bytes.push(c.charCodeAt(0))
    }
  }
  return bytes
}

# 写一个正则表达式，匹配所有的字符串直接量，单引号和双引号
/[\u0021-\u007E]{6,16}|[\x21-\x7E]{6,16}|(['"])(?:(?!\1).)*?\1/g
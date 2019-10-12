---
title: Babel的简单了解
date: 2019-10-12 10:48:50
tags:
---
在了解Babel之前我们有必要了解下AST， 什么是AST呢？

### AST(抽象语法树)
```
function square(n) {
  return n * n;
}
```
如上代码可以被表示如下的一棵树:
```
- FunctionDeclaration:
  - id:
    - Identifier:
      - name: square
  - params [1]
    - Identifier
      - name: n
  - body:
    - BlockStatement
      - body [1]
        - ReturnStatement
          - argument
            - BinaryExpression
              - operator: *
              - left
                - Identifier
                  - name: n
              - right
                - Identifier
                  - name: n
```
<!--more-->
或是如下所示的 JavaScript Object（对象）:
```
{
  type: "FunctionDeclaration",
  id: {
    type: "Identifier",
    name: "square"
  },
  params: [{
    type: "Identifier",
    name: "n"
  }],
  body: {
    type: "BlockStatement",
    body: [{
      type: "ReturnStatement",
      argument: {
        type: "BinaryExpression",
        operator: "*",
        left: {
          type: "Identifier",
          name: "n"
        },
        right: {
          type: "Identifier",
          name: "n"
        }
      }
    }]
  }
}
```
AST每一层的结构如下：

```
// 外层 节点（Node）
{
  type: "FunctionDeclaration",
  id: {...},
  params: [...],
  body: {...}
}

// 中层 节点（Node）
{
  type: "Identifier",
  name: ...
}

// 里层 节点（Node）
{
  type: "BinaryExpression",
  operator: ...,
  left: {...},
  right: {...}
}

// 每一层都有如下节点
interface Node {
  type: string;
}
每一个节点都会有 start，end，loc 这几个属性。用于描述该节点在原始代码中的位置。
```
### Babel原理
 Babel解析成AST，然后插件更改AST，最后由Babel输出代码
### Babel的三个主要处理步骤  
解析（parse），转换（transform），生成（generate）。
> 具体参考：https://github.com/jamiebuilds/babel-handbook/blob/master/translations/zh-Hans/plugin-handbook.md

### Babel介绍
babel是一个 JavaScript 编译器，主要用于将 ES5+ 版本的代码转换为向后兼容的js 语法(eg: es6->es5)，以便能够运行在当前和旧版本的浏览器或其他环境中  
例如：
```
// Babel 输入： ES6 箭头函数
[1, 2, 3].map((n) => n + 1);

// Babel 输出： ES5 普通函数
[1, 2, 3].map(function(n) {
  return n + 1;
});
```
> 参考-手写一个babel插件：https://juejin.im/post/5a9315e46fb9a0633a711f25

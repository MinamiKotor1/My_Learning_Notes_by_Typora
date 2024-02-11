# null、undefined和bool

### 1 null和undefined

##### 1) 概述

```javascript
var a = undefined;
// 或者
var a = null;
```

实际上这两种写法几乎等价

> [!Tip]
>
> 在`if`语句中，它们都会被自动转为`false`，相等运算符（`==`）甚至直接报告两者相等

+ 1995年 JavaScript 诞生时，最初像 Java 一样，只设置了`null`表示"无"。根据 C 语言的传统，`null`可以自动转为`0`

+ 但是，JavaScript 的设计者 Brendan Eich，觉得这样做还不够。首先，第一版的 JavaScript 里面，`null`就像在 Java 里一样，被当成一个对象，Brendan Eich 觉得表示“无”的值最好不是对象。其次，那时的 JavaScript 不包括错误处理机制，Brendan Eich 觉得，如果`null`自动转为0，很不容易发现错误

  因此，他又设计了一个`undefined`。区别是这样的：

  **`null`是一个表示“空”的对象，转为数值时为`0`；`undefined`是一个表示"此处无定义"的原始值，转为数值时为`NaN`。**

```javascript
Number(null) // 0
5 + null // 5

Number(undefined) // NaN
5 + undefined // NaN
```

##### 2) 用法和含义

`null`表示该处值为空。如，某个函数接受引擎抛出的错误作为参数，如果运行过程中未出错，那么这个参数就会传入`null`，表示未发生错误

`undefined`表示“未定义”

```javascript
// 变量声明了，但没有赋值
var i;
i // undefined

// 调用函数时，应该提供的参数没有提供，该参数等于 undefined
function f(x) {
  return x;
}
f() // undefined

// 对象没有赋值的属性
var  o = new Object();
o.p // undefined

// 函数没有返回值时，默认返回 undefined
function f() {}
f() // undefined
```

### 2 布尔值

真：`true`

假：`false`

> [!Note]
>
> 会返回布尔值的运算：
>
> - 前置逻辑运算符： `!` (Not)
> - 相等运算符：`===`，`!==`，`==`，`!=`
> - 比较运算符：`>`，`>=`，`<`，`<=`

如果 JavaScript 预期某个位置应该是布尔值，会将该位置上现有的值自动转为布尔值。转换规则是除了下面六个值被转为`false`，其他值都视为`true`

> [!Note]
>
> - `undefined`
> - `null`
> - `false`
> - `0`
> - `NaN`
> - `""`或`''`（空字符串）

```javascript
if ('') {
  console.log('true');
}
// 没有任何输出（''被转换为flase）
```
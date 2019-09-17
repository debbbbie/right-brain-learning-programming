---
tags | JavaScript, ES, ES2019
记忆类型 | 故事定桩法
date | 2019/09/17
---

# ES2019 新特性 右脑快速记忆

## 右脑快速记忆
---

### 需要记忆的关键词


> `flat`, 
> `9`, 
> `fromEntry`, 
> 
> `trim`, 
> `description`, 
> `catch`, 
> 
> `uni`-`stringify`-`superset`


### 故事联想法记忆

> `胖舅`来自`银川`,
> 
> 依稀`记得`他的`只言片语`：
> 
> `杰森`、`优尼`，你们2人`去死`  (json uni-2s)



### 编码表

|记忆内容|编码|备注|
|  ----  | ---- |---- |
flat |胖 |fat
9  |舅 | ES2019
fromEntry |来自银川 | Entry谐音银川
catch|记得|可选的 catch 绑定
trim description|只言片语 |  给描述去空格|
json |杰森
uni |优尼 | unicode
2S |去死 | stringify & superset

## ES2019 新特性内容
---

### 可选的 `catch` 绑定
可以不给 catch 传参数
```javascript
catch (err) { /*...*/ } // before
// =>
catch { /*...*/ }       // now
```

当我们不关心错误内容或是预知的错误时，可以用这个新特性。

### `JSON.superset`

新增支持转义 **行分隔符** (`\u2028`) 和**段落分隔符** (`\u2029`) 字符

```js
const PS = eval("'\u2029'"); // ES2019 之前报错 SyntaxError: Invalid or unexpected token
```

### `Symbol#description`

用来获取 Symbol 类型数据的描述信息（description）。

```js
Symbol('debbbbie').description; // "debbbbie"
Symbol.iterator.description;    // "Symbol.iterator"
```

### `Function#toString`

函数toString() 方法，将准确返回原有内容，包括空格和注释等

```js
let fn = function(){
    // do something
    console.log('debbbbie')
}
fn.toString();
/**
"function(){
    // do something
    console.log('debbbbie')
}"
*/
```

### `Object.fromEntries`

用于将键值对列表转换为对象

```js
// Array => Object
const arr = [ ['name', 'debbbbie'], ['age', 18] ];
Object.fromEntries(arr); // {name: "debbbbie", age: 18}

// Map => Object
const map = new Map( [ ['name', 'debbbbie'], ['age', 18] ] )
Object.fromEntries(map); // {name: "debbbbie", age: 18}
```
### 更友好的 `JSON.stringify`

对于一些超出范围的 Unicode 字符串，为其输出转义序列，使其成为有效 Unicode 字符串

```js
// Non-BMP characters still serialize to surrogate pairs.
JSON.stringify('𝌆')            // → '"𝌆"'
JSON.stringify('\uD834\uDF06')  // → '"𝌆"'

// Unpaired surrogate code units will serialize to escape sequences.
JSON.stringify('\uDF06\uD834')  // → '"\\udf06\\ud834"'
JSON.stringify('\uDEAD')        // → '"\\udead"'
```

### `String#trim`
`trimStart()` / `trimEnd()` 移除 开头 / 结尾 的空白字符，返回新字符串

`trimLeft()` / `trimRight()` 是他们的别名。

```js
let name = "\t   Hello debbbbie   \n";
name.trimStart(); // "Hello debbbbie!   \n";
name.trimEnd();   // "\t   Hello debbbbie";
```


### `Array#flat`

`Array#flat` 将一个数组打平。
默认只打平第一层数据，如果需要更多层，需要显示传入参数

```js
[1, 2, [[3]] ].flat(); // [1, 2, [3]]
[1, 2, [1, [2, [3]]] ].flat(2); // [1, 2, 1, 2, [3]]
```

官方还增加了` Array#flatMap` 方法，其实就是 `flat` 和 `map` 一起组合操作：

```js
[1, 3, 5].map(x => [x * x]);     // [[1],[9],[25]]

[1, 3, 5].flatMap(x => [x * x]); // [1,9,25]
```

## 参考链接
- https://segmentfault.com/a/1190000020255895
- https://blog.logrocket.com/5-es2019-features-you-can-use-today/

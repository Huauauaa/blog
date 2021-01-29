---
title: Which is Better
date: '2021-01-04'
description: 'difference of JavaScript API'
---

## parseInt vs Number

<a href="https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/parseInt" target="_blank">parseInt</a>

**Always specify a radix to avoid this unreliable behavior.**

```js
window.parseInt === Number.parseInt; // true
window.parseFloat === Number.parseFloat; // true
```

#### 注意

```js
parseInt('6.022e2', 10); //  6
parseInt(' 6.022e2', 10); //  6
parseInt(6.022e2, 10); // 602
Number('6.022e2'); //  602.2
parseInt('62a.02', 10); //  62
Number('62a.02'); // NaN
parseInt('0e0', 16); // 224
parseInt('123_456'); // 123
parseInt(123_456); // 123456
```

## indexOf vs includes

<a href="https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/indexOf" target="_blank">indexOf</a>

#### 缺点

- 不够语义化
- 它内部使用严格相等运算符（===）进行判断，这会导致对 NaN 的误判。

```javascript
[NaN].indexOf(NaN); // -1
[NaN].includes(NaN); // true
```

## toFixed

<a href="https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Number/toFixed" target="_blank">toFixed</a>

```js
(0.105).toFixed(2); // "0.10"
(0.105).toPrecision(2); // "0.10"
```

## forEach map reduce

### [forEach](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/forEach)

注意： 除了抛出异常以外，没有办法中止或跳出 forEach() 循环。如果你需要中止或跳出循环，forEach() 方法不是应当使用的工具

## innerText vs innerHTML vs textContent

recommend: `textContent`, but it depends

```html
<div><</div>
<section>
  hello
  <div style="display: none;">hidden message</div>
</section>
<script>
  const $ = (selector) => document.querySelector(selector);
  console.log($('div').innerHTML); // &lt;
  console.log($('div').innerText); // <
  console.log($('div').textContent); // <
  console.log($('section').innerHTML); // hello <div style="display: none;">hidden message<div>
  console.log($('section').innerText); // hello
  console.log($('section').textContent); // hello hidden message
</script>
```

## childNodes vs children

recommend: `children`

```html
<ul>
  <li>1</li>
  <li>2</li>
  <li>3</li>
  <li>4</li>
</ul>
<script>
  const $ = (selector) => document.querySelector(selector);
  console.log($('ul').childNodes.length); // 9
  console.log($('ul').children.length); // 4
</script>
```

## nextSibling vs nextElementSibling

recommend: `nextElementSibling`

```html
<ul>
  <li>1</li>
  <li>2</li>
  <li>3</li>
  <li>4</li>
</ul>
<script>
  const $ = (selector) => document.querySelector(selector);
  console.log('nextSibling', $('ul :nth-child(4)').nextSibling);
  console.log('nextElementSibling', $('ul :nth-child(4)').nextElementSibling);
</script>
```

## line-height

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <meta http-equiv="X-UA-Compatible" content="ie=edge" />
    <title>line-height demo</title>
    <style>
      .green {
        line-height: 1.1;
        border: solid limegreen;
      }

      .red {
        line-height: 1.1em;
        border: solid red;
      }

      h1 {
        font-size: 30px;
      }

      .box {
        width: 18em;
        display: inline-block;
        vertical-align: top;
        font-size: 15px;
      }
    </style>
  </head>
  <body>
    <!-- 这个示例说明了为什么给 line-height 赋值时使用 <数字> 值比使用 <长度> 更好 -->
    <div class="box green">
      <h1>Avoid unexpected results by using unitless line-height.</h1>
      length and percentage line-heights have poor inheritance behavior ...
    </div>

    <div class="box red">
      <h1>Avoid unexpected results by using unitless line-height.</h1>
      length and percentage line-heights have poor inheritance behavior ...
    </div>
  </body>
</html>
```

## isNaN vs Number.isNaN

recommend: `Number.isNaN`

### polyfill

```js
var isNaN = function (value) {
  var n = Number(value);
  return n !== n;
};
```

## subStr vs substring

<a href="https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/String/substring" target="_blank">String.prototype.substring()</a>

> substring() 方法返回一个字符串在开始索引到结束索引之间的一个子集, 或从开始索引直到字符串的末尾的一个子集. all lower case

### string.prototype.substr()

> substr() 方法返回一个字符串中从指定位置开始到指定字符数的字符.

**!!不建议使用**

## dataType

```js
const getType = (v) => Object.prototype.toString.call(v);

const type = (v) =>
  v === undefined ? 'Undefined' : v === null ? 'Null' : v.constructor.name;

console.log(getType(), type());
console.log(getType(null), type(null));
console.log(getType(1), type(1));
console.log(getType(false), type(false));
console.log(getType('foo'), type('foo'));
console.log(getType(Symbol('bar')), type(Symbol('bar')));
console.log(getType(new Object()), type(new Object()));
console.log(getType(1n), type(1n));
console.log(getType(getType), type(getType));
console.log(getType([1]), type([1]));
console.log(getType(new Date()), type(new Date()));
```

**To Be Continued...**

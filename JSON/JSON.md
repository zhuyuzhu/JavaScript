# JSON

**JSON** 是一种语法（JavaScript Object Notation），用来序列化对象、数组、数值、字符串、布尔值和null。

> ```
> JSON = null
>     or true or false
>     or JSONNumber
>     or JSONString
>     or JSONObject
>     or JSONArray
> ```

它基于 JavaScript 语法，但与之不同：**JavaScript不是JSON，JSON也不是JavaScript**。

### 一、JSON传值分类：

##### 1、null

NaN 、Infinity、null都被当做null来处理。

##### 2、布尔值

true、false，会被转为字符串

##### 3、数字

数字，禁止出现前导零，如果有小数点，后面必须至少跟一个数字。

默认将其他进制的数字，转换为10进制的数字。

##### 4、字符串

字符串，字符串必须用双引号，关于字符，禁止某些控制符，只有个别的一些字符可以别转义，比如：Unicode行分隔符（U+2028）**‘\2028’**   和端分隔符（U+2029）**'\2029'**

JSON只支持这些空白字符： 制表符（[U+0009](http://unicode-table.com/en/0009/)），换行（[U+00](http://unicode-table.com/en/0020/)0A），回车（[U+000D](http://unicode-table.com/en/000D/)）以及空格（[U+0020](http://unicode-table.com/en/0020/)）。

字符串会被处理为添加了双引号的字符串，比如字符串a，length是1，被处理为字符串"a"，length是3

##### 5、数组

对象和数组，属性名必须是双引号，最后一个属性不能有逗号。

**特点**：能识别的类型，会被JSON序列化，不能识别的值类型，会被处理为null。

示例：

```js
        let bool = [null, true, 2021, 'a']
        console.log(JSON.stringify(bool))
```

结果：`[null,true,2021,"a"]`

示例 ：

```js
        let bool = [NaN, Symbol(), function(){}, undefined, Infinity]
        console.log(JSON.stringify(bool))
```

结果 ：`[null,null,null,null,null]`

##### 6、对象

对象和数组，属性名必须是双引号，最后一个属性不能有逗号。

特点：无法识别的，不可遍历的，都会忽略。

```js
        let bool = {
            a: NaN,
            b: undefined,
            c: Infinity,
            d: Symbol(),
            e: null,
            f: function(){}
        }
        console.log(JSON.stringify(bool))
```

结果：`{"a":null,"c":null,"e":null}`

### 二、JSON的方法

##### 1、JSON.stringify

`JSON.stringify()` 方法将一个 JavaScript 对象或值转换为 JSON 字符串，如果指定了一个 replacer 函数，则可以选择性地替换值，或者指定的 replacer 是数组，则可选择性地仅包含数组指定的属性。

```
JSON.stringify(value[, replacer [, space]])
```

**返回值：一个表示给定值的JSON字符串。**

| 值类型                 | JSON.stringify返回结果       |
| ---------------------- | ---------------------------- |
| null、NaN 、infinity   | 'null'                       |
| true                   | 'true'                       |
| 1                      | '1'                          |
| "a"                    | '"a"'  字符串"a"，值也改变了 |
| [1,"a",3]              | '[1,"a",3]'                  |
| {a: 1,b: "a",c: false} | '{"a":1,"b":"a","c":false}'  |
| 其他类型的值           | undefined                    |

##### `replacer` 

如果该参数是一个函数，则在序列化过程中，被序列化的值的每个属性都会经过该函数的转换和处理；如果该参数是一个数组，则只有包含在这个数组中的属性名才会被序列化到最终的 JSON 字符串中；如果该参数为 null 或者未提供，则对象所有的属性都会被序列化。

**如果replacer是数组**，指定对象的哪些值，会被JSON序列化。

```js
        let bool = {a: 1,b: "a",c: false};
        console.log(JSON.stringify(bool,  ["a", "c"]))
```

结果：

```json
{"a":1,"c":false}
```

**如果replacer是函数，**作为函数，它有两个参数，键（key）和值（value），它们都会被序列化。在开始时, `replacer` 函数会被传入一个空字符串作为 `key` 值，代表着要被 `stringify` 的这个对象。随后每个对象或数组上的属性会被依次传入。 

函数应当返回JSON字符串中的value, 如下所示:

- 如果返回一个 [`Number`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Number), 转换成相应的字符串作为属性值被添加入 JSON 字符串。
- 如果返回一个 [`String`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/String), 该字符串作为属性值被添加入 JSON 字符串。
- 如果返回一个 [`Boolean`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Boolean), "true" 或者 "false" 作为属性值被添加入 JSON 字符串。
- 如果返回任何其他对象，该对象递归地序列化成 JSON 字符串，对每个属性调用 replacer 方法。除非该对象是一个函数，这种情况将不会被序列化成 JSON 字符串。
- 如果返回 undefined，该属性值不会在 JSON 字符串中输出。

**注意:** 不能用 replacer 方法，从数组中移除值（values），如若返回 undefined 或者一个函数，将会被 null 取代。

示例：

```js
function replacer(key, value) {
  if (typeof value === "string") {
    return undefined;
  }
  return value;
}

var foo = {foundation: "Mozilla", model: "box", week: 45, transport: "car", month: 7};
var jsonString = JSON.stringify(foo, replacer);
```

JSON序列化结果为 `{"week":45,"month":7}`.



#### `JSON.stringify()`将值转换为相应的JSON格式：

- 转换值如果有 toJSON() 方法，该方法定义什么值将被序列化。**——有的数值有toJSON方法，比如Date对象的toJSON方法**
- 非数组对象的属性不能保证以特定的顺序出现在序列化后的字符串中。**——对象序列化后的顺序不能保证唯一**
- 布尔值、数字、字符串的包装对象在序列化过程中会自动转换成对应的原始值。**——包装类对象自动转换为原始值**
- `undefined`、任意的函数以及 symbol 值，在序列化过程中会被忽略（出现在非数组对象的属性值中时）或者被转换成 `null`（出现在数组中时）。——对象中会忽略；数组中会转换为null——**对象忽略undefined、symbol、函数；数组会转为null**
- 函数、undefined 被单独转换时，会返回 undefined，如`JSON.stringify(function(){})` or `JSON.stringify(undefined)`.**——为什么会返回undefined，是因为这个几个类型的值，不是JSON.stringify的可序列化的类型，如同其他的函数方法一样，返回值为undefined。**
- 对包含循环引用的对象（对象之间相互引用，形成无限循环）执行此方法，会抛出错误。**——异常之一，对象相互引用时，抛出异常**
- 所有以 symbol 为属性键的属性都会被完全忽略掉，即便 `replacer` 参数中强制指定包含了它们。**——replacer强制指定了symbol值，对象也会忽略该值**
- Date 日期调用了 toJSON() 将其转换为了 string 字符串（同Date.toISOString()），因此会被当做字符串处理。
- NaN 和 Infinity 格式的数值及 null 都会被当做 null。**——NaN、Infinity格式数值、null都被当做null**。**都属于JSON中null类型。不管是单独转换时，还是在对象或数组中进行转换时。**
- 其他类型的对象，包括 Map/Set/WeakMap/WeakSet，仅会序列化可枚举的属性。**——不可枚举的属性默认会被忽略，包括在对象中时**

示例：

```js
JSON.stringify({});                        // '{}'
JSON.stringify(true);                      // 'true'
JSON.stringify("foo");                     // '"foo"'
JSON.stringify([1, "false", false]);       // '[1,"false",false]'
JSON.stringify({ x: 5 });                  // '{"x":5}'

JSON.stringify({x: 5, y: 6});
// "{"x":5,"y":6}"

JSON.stringify([new Number(1), new String("false"), new Boolean(false)]);
// '[1,"false",false]'

JSON.stringify({x: undefined, y: Object, z: Symbol("")});
// '{}'

JSON.stringify([undefined, Object, Symbol("")]);
// '[null,null,null]'

JSON.stringify({[Symbol("foo")]: "foo"});
// '{}'

JSON.stringify({[Symbol.for("foo")]: "foo"}, [Symbol.for("foo")]);
// '{}'

JSON.stringify(
    {[Symbol.for("foo")]: "foo"},
    function (k, v) {
        if (typeof k === "symbol"){
            return "a symbol";
        }
    }
);


// undefined

// 不可枚举的属性默认会被忽略：
JSON.stringify(
    Object.create(
        null,
        {
            x: { value: 'x', enumerable: false },
            y: { value: 'y', enumerable: true }
        }
    )
);

// "{"y":"y"}"
```

#### 异常 （JSON序列化数据 ，会对数据进行一系列处理。但某些数据会导致JSON序列化时异常）

- 当对象循环引用时
- 当尝试去转换 [`BigInt`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/BigInt) 类型的值会抛出异常（BigInt值不能JSON序列化）

#### toJSON方法

如果一个被序列化的对象拥有 `toJSON` 方法，那么该 `toJSON` 方法就会覆盖该对象默认的序列化行为：**不是该对象被序列化，而是调用 `toJSON` 方法后的返回值会被序列化，**例如：

```js
var obj = {
  foo: 'foo',
  toJSON: function () {
    return 'bar';
  }
};
JSON.stringify(obj);      // '"bar"'
JSON.stringify({x: obj}); // '{"x":"bar"}'
```



##### 2、JSON.parse

**JSON.parse()** 方法用来解析JSON字符串，构造由字符串描述的JavaScript值或对象。提供可选的 **reviver** 函数用以在返回之前对所得到的对象执行变换(操作)。

```js
JSON.parse(text[, reviver])
```

示例：

```js
JSON.parse('{}');              // {}
JSON.parse('true');            // true
JSON.parse('"foo"');           // "foo"
JSON.parse('[1, 5, "false"]'); // [1, 5, "false"]
JSON.parse('null');            // null
```

使用reviver函数：

如果指定了 `reviver` 函数，则解析出的 JavaScript 值（解析值）会经过一次转换后才将被最终返回（返回值）。更具体点讲就是：解析值本身以及它所包含的所有属性，会按照一定的顺序（从最最里层的属性开始，一级级往外，最终到达顶层，也就是解析值本身）分别的去调用 `reviver` 函数，在调用过程中，当前属性所属的对象会作为 `this` 值，当前属性名和属性值会分别作为第一个和第二个参数传入 `reviver` 中。如果 `reviver` 返回 `undefined`，则当前属性会从所属对象中删除，如果返回了其他值，则返回的值会成为当前属性新的属性值。

当遍历到最顶层的值（解析值）时，传入 `reviver` 函数的参数会是空字符串 `""`（因为此时已经没有真正的属性）和当前的解析值（有可能已经被修改过了），当前的 `this` 值会是 `{"": 修改过的解析值}`，在编写 `reviver` 函数时，要注意到这个特例。（这个函数的遍历顺序依照：从最内层开始，按照层级顺序，依次向外遍历）

**示例 ：从外层进去，每次由内而外开始遍历。**

```js
        JSON.parse('{"a": 1, "b": 2,"c": {"c1": 4, "c2": {"c21": 6}}, "d":{}, "e": []}', function (k, v) {
            console.log(k); // 输出当前的属性名，从而得知遍历顺序是从内向外的，
            // 最后一个属性名会是个空字符串。
            return v; // 返回原始属性值，相当于没有传递 reviver 参数。
        });
```

输出 ：a、b、c1、c21、c2、c、d、e、“”

**关于异常 ：**

不正确的JSON格式的数据都会抛出异常。JSON对象 和JSON 数组最后都不能有逗号。



https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/JSON/parse



### 三、其他值中对JSON的实现：

#### Date.prototype.toJSON()

https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Date/toJSON

[`Date`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Date) 实例引用一个具体的时间点。 调用 `toJSON()` 返回一个 JSON 格式字符串(使用 [`toISOString()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Date/toISOString))，表示该日期对象的值。默认情况下，这个方法常用于 [JSON](https://developer.mozilla.org/zh-CN/docs/Glossary/JSON)序列化[`Date`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Date)对象。

**toISOString()** 方法返回一个 ISO（[ISO 8601 Extended Format](http://en.wikipedia.org/wiki/ISO_8601)）格式的字符串： **YYYY-MM-DDTHH:mm:ss.sssZ**。时区总是UTC（协调世界时），加一个后缀“Z”标识。兼容性IE9

```js
var date = new Date();
console.log(date); //Thu Nov 09 2017 18:54:04 GMT+0800 (中国标准时间)

var jsonDate = (date).toJSON();
console.log(jsonDate); //"2017-11-09T10:51:11.395Z"

var backToDate = new Date(jsonDate);
console.log(backToDate); //Thu Nov 09 2017 18:54:04 GMT+0800 (中国标准时间)
```

转换值如果有 toJSON() 方法，该方法定义什么值将被序列化。**——有的数值有toJSON方法，比如Date对象的toJSON方法**

示例：

```js
        let bool = new Date();
        console.log(bool);
        console.log(JSON.stringify(bool))
```

结果：

```
Tue Jan 05 2021 09:35:43 GMT+0800 (中国标准时间)
"2021-01-05T01:35:43.144Z"
```


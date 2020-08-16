## 十六章.数组相关API

- push() 、pop()、unshift()、shift()

```js
   
    let arr = [11,22,33,44];

    // 往数组后面添加数据
     arr.push(678);// 返回长度5 [11,22,33,44,678]
     arr.push(5,6);//[11,22,33,44,678,5,6]

    // 删除数组的最后一个数据
     arr.pop();//返回删除的8 [11,22,33,44,678,5]

    // 往数组前面添加数据
     arr.unshift(999);//返回数组长度7 [999, 11, 22, 33, 44, 678, 5]

    // 删除数组第一个数据
    arr.shift();

    console.log(arr);


    // console.log(arr.length);
    // arr[3] = 99;

    // arr.length = 2;
    /*arr.length = 10;

    console.log(arr);*/
```

## [pop/push, shift/unshift 方法](https://zh.javascript.info/array#poppushshiftunshift-fang-fa)

[队列（queue）](https://en.wikipedia.org/wiki/Queue_(abstract_data_type))是最常见的使用数组的方法之一。在计算机科学中，这表示支持两个操作的一个有序元素的集合：

- `push` 在末端添加一个元素.
- `shift` 取出队列首端的一个元素，整个队列往前移，这样原先排第二的元素现在排在了第一。

这两种操作数组都支持。

队列的应用在实践中经常会碰到。例如需要在屏幕上显示消息队列。

数组还有另一个用例，就是数据结构 [栈](https://en.wikipedia.org/wiki/Stack_(abstract_data_type))。

它支持两种操作：

- `push` 在末端添加一个元素.

- `pop` 从末端取出一个元素.

所以新元素的添加和取出都是从“末端”开始的。

栈通常被被形容成一叠卡片：要么在最上面添加卡片，要么从最上面拿走卡片：

对于栈来说，后放进去的内容是最先接收的，也叫做 LIFO（Last-In-First-Out），即后进先出法则。而与队列相对应的叫做 FIFO（First-In-First-Out），即先进先出。

JavaScript 中的数组既可以用作队列，也可以用作栈。它们允许你从首端/末端来添加/删除元素。这在计算机科学中，允许这样的操作的数据结构被称为 [双端队列（deque）](https://en.wikipedia.org/wiki/Double-ended_queue)。

**作用于数组末端的方法：**

- `pop`

    取出并返回数组的最后一个元素：`let fruits = ["Apple", "Orange", "Pear"];  alert( fruits.pop() ); // 移除 "Pear" 然后 alert 显示出来  alert( fruits ); // Apple, Orange`

- `push`

    在数组末端添加元素：
    
    ```js
    let fruits = ["Apple", "Orange"];  fruits.push("Pear");  
    alert( fruits ); // Apple, Orange, Pear`调用 `fruits.push(...)` 与 `fruits[fruits.length] = ...` 是一样的。
    ```

**作用于数组首端的方法：**

- `shift`

    取出数组的第一个元素并返回它：

    ```js
    let fruits = ["Apple", "Orange", "Pear"];  
    alert( fruits.shift() ); // 移除 Apple 然后 alert 显示出来  alert( fruits ); // Orange, Pear
    ```

- `unshift`

    在数组的首端添加元素：`let fruits = ["Orange", "Pear"];  fruits.unshift('Apple');  alert( fruits ); // Apple, Orange, Pear`

`push` 和 `unshift` 方法都可以一次添加多个元素：

```javascript
let fruits = ["Apple"];

fruits.push("Orange", "Peach");
fruits.unshift("Pineapple", "Lemon");

// ["Pineapple", "Lemon", "Apple", "Orange", "Peach"]
alert( fruits );
```

## [内部](https://zh.javascript.info/array#nei-bu)

数组是一种特殊的对象。使用方括号来访问属性 `arr[0]` 实际上是来自于对象的语法。它其实与 `obj[key]` 相同，其中 `arr` 是对象，而数字用作键（key）。

它们扩展了对象，提供了特殊的方法来处理有序的数据集合以及 `length` 属性。但从本质上讲，它仍然是一个对象。

记住，在 JavaScript 中只有 7 种基本类型。数组是一个对象，因此其行为也像一个对象。

例如，它是通过引用来复制的：

```javascript
let fruits = ["Banana"]

let arr = fruits; // 通过引用复制 (两个变量引用的是相同的数组)

alert( arr === fruits ); // true

arr.push("Pear"); // 通过引用修改数组

alert( fruits ); // Banana, Pear — 现在有 2 项了
```

……但是数组真正特殊的是它们的内部实现。JavaScript 引擎尝试把这些元素一个接一个地存储在连续的内存区域，就像本章的插图显示的一样，而且还有一些其它的优化，以使数组运行得非常快。

但是，如果我们不像“有序集合”那样使用数组，而是像常规对象那样使用数组，这些就都不生效了。

例如，从技术上讲，我们可以这样做:

```javascript
let fruits = []; // 创建一个数组

fruits[99999] = 5; // 分配索引远大于数组长度的属性

fruits.age = 25; // 创建一个具有任意名称的属性
```

这是可以的，因为数组是基于对象的。我们可以给它们添加任何属性。

但是 Javascript 引擎会发现，我们在像使用常规对象一样使用数组，那么针对数组的优化就不再适用了，然后对应的优化就会被关闭，这些优化所带来的优势也就荡然无存了。

数组误用的几种方式:

- 添加一个非数字的属性，比如 `arr.test = 5`。
- 制造空洞，比如：添加 `arr[0]`，然后添加 `arr[1000]` (它们中间什么都没有)。
- 以倒序填充数组，比如 `arr[1000]`，`arr[999]` 等等。

请将数组视为作用于 **有序数据** 的特殊结构。它们为此提供了特殊的方法。数组在 JavaScript 引擎内部是经过特殊调整的，使得更好地作用于连续的有序数据，所以请以正确的方式使用数组。如果你需要任意键值，那很有可能实际上你需要的是常规对象 `{}`。

## [性能](https://zh.javascript.info/array#xing-neng)

`push/pop` 方法运行的比较快，而 `shift/unshift` 比较慢。

<img src="C:/Users/%E7%AB%B9%E9%9D%92%E6%9A%AE%E9%9B%A8/AppData/Roaming/Typora/typora-user-images/1590118925865.png" alt="1590118925865" style="zoom: 67%;" />

为什么作用于数组的末端会比首端快呢？让我们看看在执行期间都发生了什么：

```javascript
fruits.shift(); // 从首端取出一个元素
```

只获取并移除数字 `0` 对应的元素是不够的。其它元素也需要被重新编号。

`shift` 操作必须做三件事:

1. 移除索引为 `0` 的元素。
2. 把所有的元素向左移动，把索引 `1` 改成 `0`，`2` 改成 `1` 以此类推，对其重新编号。
3. 更新 `length` 属性。

**数组里的元素越多，移动它们就要花越多的时间，也就意味着越多的内存操作。**

`unshift` 也是一样：为了在数组的首端添加元素，我们首先需要将现有的元素向右移动，增加它们的索引值。

那 `push/pop` 是什么样的呢？它们不需要移动任何东西。如果从末端移除一个元素，`pop` 方法只需要清理索引值并缩短 `length` 就可以了。

`pop` 操作的行为：

```javascript
fruits.pop(); // 从末端取走一个元素
```

<img src="C:/Users/%E7%AB%B9%E9%9D%92%E6%9A%AE%E9%9B%A8/AppData/Roaming/Typora/typora-user-images/1590118994268.png" alt="1590118994268" style="zoom:67%;" />

pop 方法不需要移动任何东西，因为其它元素都保留了各自的索引。这就是为什么 pop 会特别快。**

`push` 方法也是一样的。

## [循环](https://zh.javascript.info/array#xun-huan)

遍历数组最古老的方式就是 `for` 循环：

```javascript
let arr = ["Apple", "Orange", "Pear"];

for (let i = 0; i < arr.length; i++) {
  alert( arr[i] );
}
```

但对于数组来说还有另一种循环方式，`for..of`：

```javascript
let fruits = ["Apple", "Orange", "Plum"];

// 遍历数组元素
for (let fruit of fruits) {
  alert( fruit );
}
```

`for..of` 不能获取当前元素的索引，只是获取元素值，但大多数情况是够用的。而且这样写更短。

技术上来讲，因为数组也是对象，所以使用 `for..in` 也是可以的：

```javascript
let arr = ["Apple", "Orange", "Pear"];

for (let key in arr) {
  alert( arr[key] ); // Apple, Orange, Pear
}
```

但这其实是一个很不好的想法。会有一些潜在问题存在：

1. `for..in` 循环会遍历 **所有属性**，不仅仅是这些数字属性。

    在浏览器和其它环境中有一种称为“类数组”的对象，它们 **看似是数组**。也就是说，它们有 `length` 和索引属性，但是也可能有其它的非数字的属性和方法，这通常是我们不需要的。`for..in` 循环会把它们都列出来。所以如果我们需要处理类数组对象，这些“额外”的属性就会存在问题。

2. `for..in` 循环适用于普通对象，并且做了对应的优化。但是不适用于数组，因此速度要慢 10-100 倍。当然即使是这样也依然非常快。只有在遇到瓶颈时可能会有问题。但是我们仍然应该了解这其中的不同。

通常来说，我们不应该用 `for..in` 来处理数组。

## [关于 “length”](https://zh.javascript.info/array#guan-yu-length)

当我们修改数组的时候，`length` 属性会自动更新。准确来说，它实际上不是数组里元素的个数，而是最大的数字索引值加一。

例如，一个数组只有一个元素，但是这个元素的索引值很大，那么这个数组的 `length` 也会很大：

```javascript
let fruits = [];
fruits[123] = "Apple";

alert( fruits.length ); // 124
```

要知道的是我们通常不会这样使用数组。

`length` 属性的另一个有意思的点是它是可写的。

如果我们手动增加它，则不会发生任何有趣的事儿。但是如果我们减少它，数组就会被截断。该过程是不可逆的，下面是例子：

```javascript
let arr = [1, 2, 3, 4, 5];

arr.length = 2; // 截断到只剩 2 个元素
alert( arr ); // [1, 2]

arr.length = 5; // 又把 length 加回来
alert( arr[3] ); // undefined：被截断的那些数值并没有回来
```

所以，清空数组最简单的方法就是：`arr.length = 0;`。

## [new Array()](https://zh.javascript.info/array#new-array)

这是创建数组的另一种语法：

```javascript
let arr = new Array("Apple", "Pear", "etc");
```

它很少被使用，因为方括号 `[]` 更短更简洁。而且这种语法还存在一些诡异的特性。

如果使用单个参数（即数字）调用 `new Array`，那么它会创建一个 **指定了长度，却没有任何项** 的数组。

让我们看看如何搬起石头砸自己的脚:

```javascript
let arr = new Array(2); // 会创建一个 [2] 的数组吗？

alert( arr[0] ); // undefined！没有元素。

alert( arr.length ); // length 2
```

在上面的代码中，`new Array(number)` 创建的数组的所有元素都是 `undefined`。

为了避免这种乌龙事件，我们通常都是使用方括号的，除非我们清楚地知道自己正在做什么。

### 多维数组（了解）

数组里的项也可以是数组。我们可以将其用于多维数组，例如存储矩阵：

```javascript
let matrix = [
  [1, 2, 3],
  [4, 5, 6],
  [7, 8, 9]
];

alert( matrix[1][1] ); // 最中间的那个数 5
```

## toString

数组有自己的 `toString` 方法的实现，会返回以逗号隔开的元素列表。

例如：

```javascript
let arr = [1, 2, 3];

alert( arr ); // 1,2,3
alert( String(arr) === '1,2,3' ); // true
```

此外，我们试试运行一下这个：

```javascript
alert( [] + 1 ); // "1"
alert( [1] + 1 ); // "11"
alert( [1,2] + 1 ); // "1,21"
```

数组没有 `Symbol.toPrimitive`，也没有 `valueOf`，它们只能执行 `toString` 进行转换，所以这里 `[]` 就变成了一个空字符串，`[1]` 变成了 `"1"`，`[1,2]` 变成了 `"1,2"`。

当 `"+"` 运算符把一些项加到字符串后面时，加号后面的项也会被转换成字符串，所以下一步就会是这样：

```javascript
alert( "" + 1 ); // "1"
alert( "1" + 1 ); // "11"
alert( "1,2" + 1 ); // "1,21"
```

## [总结](https://zh.javascript.info/array#zong-jie)

数组是一种特殊的对象，适用于存储和管理有序的数据项。

- 声明:

    ```javascript
    // 方括号 (常见用法)
    let arr = [item1, item2...];
    
    // new Array (极其少见)
    let arr = new Array(item1, item2...);
    ```

    调用 `new Array(number)` 会创建一个给定长度的数组，但不含有任何项。

- `length` 属性是数组的长度，准确地说，它是数组最后一个数字索引值加一。它由数组方法自动调整。

- 如果我们手动缩短 `length`，那么数组就会被截断。

我们可以通过下列操作以双端队列的方式使用数组：

- `push(...items)` 在末端添加 `items` 项。
- `pop()` 从末端移除并返回该元素。
- `shift()` 从首端移除并返回该元素。
- `unshift(...items)` 从首端添加 `items` 项。

遍历数组的元素：

- `for (let i=0; i<arr.length; i++)` — 运行得最快，可兼容旧版本浏览器。
- `for (let item of arr)` — 现代语法，只能访问 items。
- `for (let i in arr)` — 永远不要用这个。

### [splice](https://zh.javascript.info/array-methods#splice)

如何从数组中删除元素？

数组是对象，所以我们可以尝试使用 `delete`：

```javascript
let arr = ["I", "go", "home"];

delete arr[1]; // remove "go"  返回true

alert( arr[1] ); // undefined

// now arr = ["I",  , "home"];
alert( arr.length ); // 3
```

元素被删除了，但数组仍然有 3 个元素，我们可以看到 `arr.length === 3`。

这很正常，因为 `delete obj.key` 是通过 `key` 来移除对应的值。对于对象来说是可以的。但是对于数组来说，我们通常希望剩下的元素能够移动并占据被释放的位置。我们希望得到一个更短的数组。

所以应该使用特殊的方法。

[arr.splice(str)](https://developer.mozilla.org/zh/docs/Web/JavaScript/Reference/Global_Objects/Array/splice) 方法可以说是处理数组的瑞士军刀。它可以做所有事情：添加，删除和插入元素。

语法是：

```js
arr.splice(index[, deleteCount, elem1, ..., elemN])
```

从 `index` 开始：删除 `deleteCount` 个元素并在当前位置插入 `elem1, ..., elemN`。最后返回已删除元素的数组。

让我们从删除开始：

```javascript
let arr = ["I", "study", "JavaScript"];

arr.splice(1, 1); // 从索引 1 开始删除 1 个元素

alert( arr ); // ["I", "JavaScript"]
```

简单，对吧？从索引 `1` 开始删除 `1` 个元素。

在下一个例子中，我们删除了 3 个元素，并用另外两个元素替换它们：

```javascript
 let arr = ["I", "study", "JavaScript", "right", "now"];

// remove 3 first elements and replace them with another
arr.splice(0, 3, "Let's", "dance");

alert( arr ) // now ["Let's", "dance", "right", "now"]
```

在这里我们可以看到 `splice` 返回了已删除元素的数组：

```javascript
                        let arr = ["I", "study", "JavaScript", "right", "now"];

// 删除前两个元素
let removed = arr.splice(0, 2);

alert( removed ); // "I", "study" <-- 被从数组中删除了的元素
```

我们可以将 `deleteCount` 设置为 `0`，`splice` 方法就能够插入元素而不用删除任何元素：

```javascript
let arr = ["I", "study", "JavaScript"];

// 从索引 2 开始
// 删除 0 个元素
// 然后插入 "complex" 和 "language"
arr.splice(2, 0, "complex", "language");

alert( arr ); // "I", "study", "complex", "language", "JavaScript"
```

**允许负向索引**

在这里和其他数组方法中，负向索引都是被允许的。它们从数组末尾计算位置，如下所示：

```javascript
let arr = [1, 2, 5];

// 从索引 -1（尾端前一位）
// 删除 0 个元素，
// 然后插入 3 和 4
arr.splice(-1, 0, 3, 4);

alert( arr ); // 1,2,3,4,5
```

### [slice](https://zh.javascript.info/array-methods#slice)

[arr.slice](https://developer.mozilla.org/zh/docs/Web/JavaScript/Reference/Global_Objects/Array/slice) 方法比 `arr.splice` 简单得多。

语法是：

- **arr.slice([start], [end])**

它会返回一个新数组，将所有从索引 `start` 到 `end`（不包括 `end`）的数组项复制到一个新的数组。`start` 和 `end` 都可以是负数，在这种情况下，从末尾计算索引。

它和字符串的 `str.slice` 方法有点像，就是把子字符串替换成子数组。

例如：

```javascript
let arr = ["t", "e", "s", "t"];

alert( arr.slice(1, 3) ); // e,s（复制从位置 1 到位置 3 的元素）

alert( arr.slice(-2) ); // s,t（复制从位置 -2 到尾端的元素）
```

我们也可以不带参数地调用它：`arr.slice()` 会创建一个 `arr` 的副本。其通常用于获取副本，以进行不影响原始数组的进一步转换。

### [concat](https://zh.javascript.info/array-methods#concat)

[arr.concat](https://developer.mozilla.org/zh/docs/Web/JavaScript/Reference/Global_Objects/Array/concat) 创建一个新数组，其中包含来自于其他数组和其他项的值。

语法：

- **arr.concat(arg1, arg2...)**
- 它接受任意数量的参数 — 数组或值都可以。


结果是一个包含来自于 `arr`，然后是 `arg1`，`arg2` 的元素的新数组。

如果参数 `argN` 是一个数组，那么其中的所有元素都会被复制。否则，将复制参数本身。

例如：

```javascript
let arr = [1, 2];

// create an array from: arr and [3,4]
alert( arr.concat([3, 4]) ); // 1,2,3,4

// create an array from: arr and [3,4] and [5,6]
alert( arr.concat([3, 4], [5, 6]) ); // 1,2,3,4,5,6

// create an array from: arr and [3,4], then add values 5 and 6
alert( arr.concat([3, 4], 5, 6) ); // 1,2,3,4,5,6
```

通常，它只复制数组中的元素。其他对象，即使它们看起来像数组一样，但仍然会被作为一个整体添加：

```javascript
let arr = [1, 2];

let arrayLike = {
  0: "something",
  length: 1
};

alert( arr.concat(arrayLike) ); // 1,2,[object Object]
```

……但是，如果类似数组的对象具有 `Symbol.isConcatSpreadable` 属性，那么它就会被 `concat` 当作一个数组来处理：此对象中的元素将被添加：

```javascript
let arr = [1, 2];

let arrayLike = {
  0: "something",
  1: "else",
  [Symbol.isConcatSpreadable]: true,
  length: 2
};

alert( arr.concat(arrayLike) ); // 1,2,something,else
```

## [遍历：forEach](https://zh.javascript.info/array-methods#bian-li-foreach)

[arr.forEach](https://developer.mozilla.org/zh/docs/Web/JavaScript/Reference/Global_Objects/Array/forEach) 方法允许为数组的每个元素都运行一个函数。

语法：

```javascript
arr.forEach(function(item, index, array) {
  // ... do something with item
});
```

例如，下面这个程序显示了数组的每个元素：

```javascript
// 对每个元素调用 alert
["Bilbo", "Gandalf", "Nazgul"].forEach(alert);
```

而这段代码更详细地介绍了它们在目标数组中的位置：

```javascript
["Bilbo", "Gandalf", "Nazgul"].forEach((item, index, array) => {
  alert(`${item} is at index ${index} in ${array}`);
});
```

该函数的结果（如果它有返回）会被抛弃和忽略。

## [在数组中搜索](https://zh.javascript.info/array-methods#zai-shu-zu-zhong-sou-suo)

现在，让我们介绍在数组中进行搜索的方法。

### [indexOf/lastIndexOf 和 includes](https://zh.javascript.info/array-methods#indexoflastindexof-he-includes)

[arr.indexOf](https://developer.mozilla.org/zh/docs/Web/JavaScript/Reference/Global_Objects/Array/indexOf)、[arr.lastIndexOf](https://developer.mozilla.org/zh/docs/Web/JavaScript/Reference/Global_Objects/Array/lastIndexOf) 和 [arr.includes](https://developer.mozilla.org/zh/docs/Web/JavaScript/Reference/Global_Objects/Array/includes) 方法与字符串操作具有相同的语法，并且作用基本上也与字符串的方法相同，只不过这里是对数组元素而不是字符进行操作：

- `arr.indexOf(item, from)` 从索引 `from` 开始搜索 `item`，如果找到则返回索引，否则返回 `-1`。
- `arr.lastIndexOf(item, from)` — 和上面相同，只是从右向左搜索。
- `arr.includes(item, from)` — 从索引 `from` 开始搜索 `item`，如果找到则返回 `true`（译注：如果没找到，则返回 `false`）。

例如：

```javascript
let arr = [1, 0, false];

alert( arr.indexOf(0) ); // 1
alert( arr.indexOf(false) ); // 2
alert( arr.indexOf(null) ); // -1

alert( arr.includes(1) ); // true
```

请注意，这些方法使用的是严格相等 `===` 比较。所以如果我们搜索 `false`，会精确到的确是 `false` 而不是数字 `0`。

如果我们想检查是否包含某个元素，并且不想知道确切的索引，那么 `arr.includes` 是首选。

此外，`includes` 的一个非常小的差别是它能正确处理`NaN`，而不像 `indexOf/lastIndexOf`：

```javascript
const arr = [NaN];
alert( arr.indexOf(NaN) ); // -1（应该为 0，但是严格相等 === equality 对 NaN 无效）
alert( arr.includes(NaN) );// true（这个结果是对的）
```

### [find 和 findIndex](https://zh.javascript.info/array-methods#find-he-findindex)

想象一下，我们有一个对象数组。我们如何找到具有特定条件的对象？

这时可以用 [arr.find](https://developer.mozilla.org/zh/docs/Web/JavaScript/Reference/Global_Objects/Array/find) 方法。

语法如下：

```javascript
let result = arr.find(function(item, index, array) {
  // 如果返回 true，则返回 item 并停止迭代
  // 对于 falsy 则返回 undefined
});
```

依次对数组中的每个元素调用该函数：

- `item` 是元素。
- `index` 是它的索引。
- `array` 是数组本身。

如果它返回 `true`，则搜索停止，并返回 `item`。如果没有搜索到，则返回 `undefined`。

例如，我们有一个存储用户的数组，每个用户都有 `id` 和 `name` 字段。让我们找到 `id == 1` 的那个用户：

```javascript
let users = [
  {id: 1, name: "John"},
  {id: 2, name: "Pete"},
  {id: 3, name: "Mary"}
];

let user = users.find(item => item.id == 1);

alert(user.name); // John
```

在现实生活中，对象数组是很常见的，所以 `find` 方法非常有用。

注意在这个例子中，我们传给了 `find` 一个单参数函数 `item => item.id == 1`。这很典型，并且 `find` 方法的其他参数很少使用。

[arr.findIndex](https://developer.mozilla.org/zh/docs/Web/JavaScript/Reference/Global_Objects/Array/findIndex) 方法（与 `arr.find` 方法）基本上是一样的，但它返回找到元素的索引，而不是元素本身。并且在未找到任何内容时返回 `-1`。

### [filter](https://zh.javascript.info/array-methods#filter)

`find` 方法搜索的是使函数返回 `true` 的第一个（单个）元素。

如果需要匹配的有很多，我们可以使用 [arr.filter(fn)](https://developer.mozilla.org/zh/docs/Web/JavaScript/Reference/Global_Objects/Array/filter)。

语法与 `find` 大致相同，但是 `filter` 返回的是所有匹配元素组成的数组：

```javascript
let results = arr.filter(function(item, index, array) {
  // 如果 true item 被 push 到 results，迭代继续
  // 如果什么都没找到，则返回空数组
});
```

例如：

```javascript
let users = [
  {id: 1, name: "John"},
  {id: 2, name: "Pete"},
  {id: 3, name: "Mary"}
];

// 返回前两个用户的数组
let someUsers = users.filter(item => item.id < 3);

alert(someUsers.length); // 2
```

## [转换数组](https://zh.javascript.info/array-methods#zhuan-huan-shu-zu)

让我们继续学习进行数组转换和重新排序的方法。

### [			map](https://zh.javascript.info/array-methods#map)

[arr.map](https://developer.mozilla.org/zh/docs/Web/JavaScript/Reference/Global_Objects/Array/map) 方法是最有用和经常使用的方法之一。

它对数组的每个元素都调用函数，并返回结果数组。

语法：

```javascript
let result = arr.map(function(item, index, array) {
  // 返回新值而不是当前元素
})
```

例如，在这里我们将每个元素转换为它的字符串长度：

```javascript
let lengths = ["Bilbo", "Gandalf", "Nazgul"].map(item => item.length);
alert(lengths); // 5,7,6
```

### [sort(fn)](https://zh.javascript.info/array-methods#sortfn)

[arr.sort](https://developer.mozilla.org/zh/docs/Web/JavaScript/Reference/Global_Objects/Array/sort) 方法对数组进行 **原位（in-place）** 排序，更改元素的顺序。(译注：原位是指在此数组内，而非生成一个新数组。)

它还返回排序后的数组，但是返回值通常会被忽略，因为修改了 `arr` 本身。

语法：

```javascript
let arr = [ 1, 2, 15 ];

// 该方法重新排列 arr 的内容
arr.sort();

alert( arr );  // 1, 15, 2
```

你有没有注意到结果有什么奇怪的地方？

顺序变成了 `1, 15, 2`。不对，但为什么呢？

**这些元素默认情况下被按字符串进行排序。**

从字面上看，所有元素都被转换为字符串，然后进行比较。对于字符串，按照词典顺序进行排序，实际上应该是 `"2" > "15"`。

要使用我们自己的排序顺序，我们需要提供一个函数作为 `arr.sort()` 的参数。

该函数应该比较两个任意值并返回：

```javascript
function compare(a, b) {
  if (a > b) return 1; // 如果第一个值比第二个值大
  if (a == b) return 0; // 如果两个值相等
  if (a < b) return -1; // 如果第一个值比第二个值小
}
```

例如，按数字进行排序：

```javascript
function compareNumeric(a, b) {
  if (a > b) return 1;
  if (a == b) return 0;
  if (a < b) return -1;
}

let arr = [ 1, 2, 15 ];

arr.sort(compareNumeric);

alert(arr);  // 1, 2, 15
```

现在结果符合预期了。

我们思考一下这儿发生了什么。`arr` 可以是由任何内容组成的数组，对吗？它可能包含数字、字符串、对象或其他任何内容。我们有一组 **一些元素**。要对其进行排序，我们需要一个 **排序函数** 来确认如何比较这些元素。默认是按字符串进行排序的。

`arr.sort(fn)` 方法实现了通用的排序算法。我们不需要关心它的内部工作原理（大多数情况下都是经过 [快速排序](https://en.wikipedia.org/wiki/Quicksort) 算法优化的）。它将遍历数组，使用提供的函数比较其元素并对其重新排序，我们所需要的就是提供执行比较的函数 `fn`。

顺便说一句，如果我们想知道要比较哪些元素 — 那么什么都不会阻止 alert 它们：

```javascript
[1, -2, 15, 2, 0, 8].sort(function(a, b) {
  alert( a + " <> " + b );
});
```

该算法可以在此过程中，将一个元素与多个其他元素进行比较，但是它会尝试进行尽可能少的比较。

**比较函数可以返回任何数字**

实际上，比较函数只需要返回一个正数表示“大于”，一个负数表示“小于”。

通过这个原理我们可以编写更短的函数：

```javascript
let arr = [ 1, 2, 15 ];

arr.sort(function(a, b) { return a - b; });

alert(arr);  // 1, 2, 15
```

**箭头函数最好**

这里使用箭头函数会更加简洁：

```javascript
arr.sort( (a, b) => a - b );
```

### [reverse](https://zh.javascript.info/array-methods#reverse)

[arr.reverse](https://developer.mozilla.org/zh/docs/Web/JavaScript/Reference/Global_Objects/Array/reverse) 方法用于颠倒 `arr` 中元素的顺序。

例如：

```javascript
let arr = [1, 2, 3, 4, 5];
arr.reverse();

alert( arr ); // 5,4,3,2,1
```

它也会返回颠倒后的数组 `arr`。

### [split 和 join](https://zh.javascript.info/array-methods#split-he-join)

举一个现实生活场景的例子。我们正在编写一个消息应用程序，并且该人员输入以逗号分隔的接收者列表：`John, Pete, Mary`。但对我们来说，名字数组比单个字符串舒适得多。怎么做才能获得这样的数组呢？

[str.split(delim)](https://developer.mozilla.org/zh/docs/Web/JavaScript/Reference/Global_Objects/String/split) 方法可以做到。它通过给定的分隔符 `delim` 将字符串分割成一个数组。

在下面的例子中，我们用“逗号后跟着一个空格”作为分隔符：

```javascript
let names = 'Bilbo, Gandalf, Nazgul';

let arr = names.split(', ');

for (let name of arr) {
  alert( `A message to ${name}.` ); // A message to Bilbo（和其他名字）
}
```

`split` 方法有一个可选的第二个数字参数 — 对数组长度的限制。如果提供了，那么额外的元素会被忽略。但实际上它很少使用：

```javascript
let arr = 'Bilbo, Gandalf, Nazgul, Saruman'.split(', ', 2);

alert(arr); // Bilbo, Gandalf
```

**拆分为字母**

调用带有空参数 `s` 的 `split(s)`，会将字符串拆分为字母数组：

```javascript
let str = "test";

alert( str.split('') ); // t,e,s,t
```

[arr.join(glue)](https://developer.mozilla.org/zh/docs/Web/JavaScript/Reference/Global_Objects/Array/join) 与 `split` 相反。它会在它们之间创建一串由 `glue` 粘合的 `arr` 项。

例如：

```javascript
let arr = ['Bilbo', 'Gandalf', 'Nazgul'];

let str = arr.join(';'); // 使用分号 ; 将数组粘合成字符串

alert( str ); // Bilbo;Gandalf;Nazgul
```

### [reduce/reduceRight](https://zh.javascript.info/array-methods#reducereduceright)

当我们需要遍历一个数组时 — 我们可以使用 `forEach`，`for` 或 `for..of`。

当我们需要遍历并返回每个元素的数据时 — 我们可以使用 `map`。

[arr.reduce](https://developer.mozilla.org/zh/docs/Web/JavaScript/Reference/Global_Objects/Array/reduce) 方法和 [arr.reduceRight](https://developer.mozilla.org/zh/docs/Web/JavaScript/Reference/Global_Objects/Array/reduceRight) 方法和上面的种类差不多，但稍微复杂一点。它们用于根据数组计算单个值。

语法是：

```javascript
let value = arr.reduce(function(accumulator, item, index, array) {
  // ...
}, [initial]);
```

该函数一个接一个地应用于所有数组元素，并将其结果“搬运（carry on）”到下一个调用。

参数：

- `accumulator` – 是上一个函数调用的结果，第一次等于 `initial`（如果提供了 `initial` 的话）。
- `item` — 当前的数组元素。
- `index` — 当前索引。
- `arr` — 数组本身。

应用函数时，上一个函数调用的结果将作为第一个参数传递给下一个函数。

因此，第一个参数本质上是累加器，用于存储所有先前执行的组合结果。最后，它成为 `reduce` 的结果。

听起来复杂吗？

掌握这个知识点的最简单的方法就是通过示例。

在这里，我们通过一行代码得到一个数组的总和：

```javascript
let arr = [1, 2, 3, 4, 5];

let result = arr.reduce((sum, current) => sum + current, 0);

alert(result); // 15
```

传递给 `reduce` 的函数仅使用了 2 个参数，通常这就足够了。

让我们看看细节，到底发生了什么。

1. 在第一次运行时，`sum` 的值为初始值 `initial`（`reduce` 的最后一个参数），等于 0，`current` 是第一个数组元素，等于 `1`。所以函数运行的结果是 `1`。
2. 在第二次运行时，`sum = 1`，我们将第二个数组元素（`2`）与其相加并返回。
3. 在第三次运行中，`sum = 3`，我们继续把下一个元素与其相加，以此类推……

计算流程：

![1590120758071](C:/Users/%E7%AB%B9%E9%9D%92%E6%9A%AE%E9%9B%A8/AppData/Roaming/Typora/typora-user-images/1590120758071.png)

或者以表格的形式表示，每一行代表的是对下一个数组元素的函数调用：

|             | `sum` | `current` | `result` |
| :---------- | :---- | :-------- | :------- |
| 第 1 次调用 | `0`   | `1`       | `1`      |
| 第 2 次调用 | `1`   | `2`       | `3`      |
| 第 3 次调用 | `3`   | `3`       | `6`      |
| 第 4 次调用 | `6`   | `4`       | `10`     |
| 第 5 次调用 | `10`  | `5`       | `15`     |

在这里，我们可以清楚地看到上一个调用的结果如何成为下一个调用的第一个参数。

我们也可以省略初始值：

```javascript
let arr = [1, 2, 3, 4, 5];

// 删除 reduce 的初始值（没有 0）
let result = arr.reduce((sum, current) => sum + current);

alert( result ); // 15
```

结果是一样的。这是因为如果没有初始值，那么 `reduce` 会将数组的第一个元素作为初始值，并从第二个元素开始迭代。

计算表与上面相同，只是去掉第一行。

但是这种使用需要非常小心。如果数组为空，那么在没有初始值的情况下调用 `reduce` 会导致错误。

例如：

```javascript
let arr = [];

// Error: Reduce of empty array with no initial value
// 如果初始值存在，则 reduce 将为空 arr 返回它（即这个初始值）。
arr.reduce((sum, current) => sum + current);
```

所以建议始终指定初始值。

[arr.reduceRight](https://developer.mozilla.org/zh/docs/Web/JavaScript/Reference/Global_Objects/Array/reduceRight) 和 [arr.reduce](https://developer.mozilla.org/zh/docs/Web/JavaScript/Reference/Global_Objects/Array/reduce) 方法的功能一样，只是遍历为从右到左。

## [Array.isArray](https://zh.javascript.info/array-methods#arrayisarray)

数组是基于对象的，不构成单独的语言类型。

所以 `typeof` 不能帮助从数组中区分出普通对象：

```javascript
alert(typeof {}); // object
alert(typeof []); // same
```

……但是数组经常被使用，因此有一种特殊的方法用于判断：[Array.isArray(value)](https://developer.mozilla.org/zh/docs/Web/JavaScript/Reference/Global_Objects/Array/isArray)。如果 `value` 是一个数组，则返回 `true`；否则返回 `false`。

```javascript
alert(Array.isArray({})); // false

alert(Array.isArray([])); // true
```

## [总结](https://zh.javascript.info/array-methods#zong-jie)

数组方法备忘单：

- 添加/删除元素：
    - `push(...items)` — 向尾端添加元素，
    - `pop()` — 从尾端提取一个元素，
    - `shift()` — 从首端提取一个元素，
    - `unshift(...items)` — 向首端添加元素，
    - `splice(pos, deleteCount, ...items)` — 从 `index` 开始删除 `deleteCount` 个元素，并在当前位置插入 `items`。
    - `slice(start, end)` — 创建一个新数组，将从位置 `start` 到位置 `end`（但不包括 `end`）的元素复制进去。
    - `concat(...items) — 返回一个新数组：复制当前数组的所有元素，并向其中添加 `items`。如果 `items` 中的任意一项是一个数组，那么就取其元素。
- 搜索元素：
    - `indexOf/lastIndexOf(item, pos)` — 从位置 `pos` 开始搜索 `item`，搜索到则返回该项的索引，否则返回 `-1`。
    - `includes(value)` — 如果数组有 `value`，则返回 `true`，否则返回 `false`。
    - `find/filter(func)` — 通过 `func` 过滤元素，返回使 `func` 返回 `true` 的第一个值/所有值。
    - `findIndex` 和 `find` 类似，但返回索引而不是值。
- 遍历元素：
    - `forEach(func)` — 对每个元素都调用 `func`，不返回任何内容。
- 转换数组：
    - `map(func)` — 根据对每个元素调用 `func` 的结果创建一个新数组。
    - `sort(func)` — 对数组进行原位（in-place）排序，然后返回它。
    - `reverse()` — 原位（in-place）反转数组，然后返回它。
    - `split/join` — 将字符串转换为数组并返回。
    - `reduce(func, initial)` — 通过对每个元素调用 `func` 计算数组上的单个值，并在调用之间传递中间结果。
- 其他：  – `Array.isArray(arr)` 检查 `arr` 是否是一个数组。

请注意，`sort`，`reverse` 和 `splice` 方法修改的是数组本身。

```html
<!DOCTYPE html>
<html lang="zh-cn">
<head>
  <meta charset="UTF-8">
  <title>Title</title>
  <style>
    *{
      margin:0;
      padding:0;
      font-family:"Microsoft Yahei";
      list-style: none;
      user-select: none;
    }
    #wrap{
      box-sizing: border-box;
      width: 960px;
      height: 630px;
      padding: 40px 30px;
      border: 1px solid #aaa;
      margin: 50px auto;
    }
    #wrap .goods{
      overflow: hidden;
      width: 100%;
    }
    #wrap .goods li{
      position: relative;
      box-sizing: border-box;
      float: left;
      width: 25%;
      height: 240px;
      padding: 10px 6px;
    }
    #wrap .goods li img{
      display: block;
    }
    #wrap .goods li p.price{
      position: absolute;
      bottom: 10px;
      right: 10px;
      width: 50px;
      height: 50px;
      background-image: url("./img/price.png");

      color: #fff;
      line-height: 50px;
      text-align: center;
      font-style: italic;
      font-size: 14px;
    }
    #wrap .goods li p.title{
      font-size: 12px;
      line-height: 30px;
    }
    #wrap .btn li{
      float: right;
      width: 90px;
      height: 40px;
      margin-top: 20px;
      margin-right: 10px;
      background-color: #f60;

      line-height: 40px;
      text-align: center;
      font-size: 12px;
      color: #fff;

      cursor: pointer;
    }
  </style>
</head>
<body>
  <div id="wrap">
    <ul class="goods">
      <!--<li>
        <img width="190" height="190" src="./img/xh_img1.jpg" alt="">
        <p class="price">￥<b>100</b></p>
        <p class="title">深红色经典玫瑰</p>
      </li>
      <li>
        <img width="190" height="190" src="./img/xh_img2.jpg" alt="">
        <p class="price">￥<b>97</b></p>
        <p class="title">甜美七分袖荷叶边条纹设</p>
      </li>
      <li>
        <img width="190" height="190" src="./img/xh_img3.jpg" alt="">
        <p class="price">￥<b>99.5</b></p>
        <p class="title">甜美七分袖荷叶边条纹设</p>
      </li>
      <li>
        <img width="190" height="190" src="./img/xh_img4.jpg" alt="">
        <p class="price">￥<b>215</b></p>
        <p class="title">甜美七分袖荷叶边条纹设</p>
      </li>
      <li>
        <img width="190" height="190" src="./img/xh_img5.jpg" alt="">
        <p class="price">￥<b>130</b></p>
        <p class="title">经典红色我的最爱</p>
      </li>
      <li>
        <img width="190" height="190" src="./img/xh_img6.jpg" alt="">
        <p class="price">￥<b>300</b></p>
        <p class="title">清淡优雅百年百合</p>
      </li>
      <li>
        <img width="190" height="190" src="./img/xh_img7.jpg" alt="">
        <p class="price">￥<b>700</b></p>
        <p class="title">紫色冷艳系列</p>
      </li>
      <li>
        <img width="190" height="190" src="./img/xh_img8.jpg" alt="">
        <p class="price">￥<b>500</b></p>
        <p class="title">粉色浪漫系列玫瑰</p>
      </li>-->
    </ul>
    <ul class="btn">
      <li>从高到低</li>
      <li>从低到高</li>
      <li>随机排序</li>
    </ul>
  </div>
  <script>

    (function(){
      /*需要从后台请求数据 */
      //先假装我们请求到了数据data
      let data = [
        {
          src : "./img/xh_img1.jpg",
          price : 100,
          title : "深红色经典玫瑰"
        },
        {
          src : "./img/xh_img2.jpg",
          price : 97,
          title : "甜美七分袖荷叶边条纹设"
        },
        {
          src : "./img/xh_img3.jpg",
          price : 99.5,
          title : "甜美七分袖荷叶边条纹设"
        },
        {
          src : "./img/xh_img4.jpg",
          price : 215,
          title : "甜美七分袖荷叶边条纹设"
        },
        {
          src : "./img/xh_img5.jpg",
          price : 130,
          title : "经典红色我的最爱"
        },
        {
          src : "./img/xh_img6.jpg",
          price : 300,
          title : "清淡优雅百年百合"
        },
        {
          src : "./img/xh_img7.jpg",
          price : 700,
          title : "紫色冷艳系列"
        },
        {
          src : "./img/xh_img8.jpg",
          price : 500,
          title : "粉色浪漫系列玫瑰"
        }
      ];

      //前端的数据处理
      let oGoodsUl = document.querySelector("#wrap .goods");
      let aBtnLi = document.querySelectorAll("#wrap .btn li");

      //遍历data生成所需要的前端标签结构
      init();
      function init(){
        let html = "";
        data.forEach(item=>{
          html += `<li>
            <img src="${item.src}" width="190" height="190" alt="">
            <p class="price">￥<b>${item.price}</b></p>
            <p class="title">${item.title}</p>
          </li>`;
        });
        oGoodsUl.innerHTML = html;
      }

      //点击事件的添加
      (function(){
        let fnArr = [
          (a,b)=>b.price-a.price,
          (a,b)=>a.price-b.price,
          (a,b)=>Math.random()-0.5
        ];
        aBtnLi.forEach((node,index)=>{
          // console.log(node);
          node.onclick = function(){
            //对data进行排序 --- 根据index来决定使用什么函数做排序
            data.sort(fnArr[index]);
            //重新渲染新的页面结构
            init();
          };
        });
      })();
      /*(function(){
        //从高到底
        aBtnLi[0].onclick = function(){
          //对data进行排序
          let fn = (a,b)=>b.price-a.price;
          data.sort(fn);
          //重新渲染新的页面结构
          init();
        };

        //从低到高
        aBtnLi[1].onclick = function(){
          //对data进行排序
          let fn = (a,b)=>a.price-b.price;
          data.sort(fn);
          //重新渲染新的页面结构
          init();
        };

        //随机排序
        aBtnLi[2].onclick = function(){
          //对data进行排序
          let fn = ()=>Math.random()-0.5;
          data.sort(fn);// -0.5 ~ 0.5
          //重新渲染新的页面结构
          init();
        };
      })();*/
      /*(function(){
        //从高到底
        aBtnLi[0].onclick = function(){
          //对data进行排序
          data.sort((a,b)=>b.price-a.price);
          //重新渲染新的页面结构
          init();
        };

        //从低到高
        aBtnLi[1].onclick = function(){
          //对data进行排序
          data.sort((a,b)=>a.price-b.price);
          //重新渲染新的页面结构
          init();
        };

        //随机排序
        aBtnLi[2].onclick = function(){
          //对data进行排序
          data.sort(()=>Math.random()-0.5);// -0.5 ~ 0.5
          //重新渲染新的页面结构
          init();
        };
      })();*/

    })();
  </script>
</body>
</html>
```


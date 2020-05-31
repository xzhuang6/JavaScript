- ## 第十七章.字符串相关API

字符串就很数熟知了，就不多赘余bb了，直接上代码啦~

```js
/*
    * string.length 得到字符串的长度
    * 只读，不可修改
    *
    * string[0] 可以下标取值
    * 只读，不可修改
    *
    * 低版本的IE不兼容 [] 下标取字符串的值
    * 所以一般情况下，我们想要取某个位置的字符使用：
    * charAt( index )
    *
    * */

    let str = "abc 皮卡同学";

    console.log( str.length ); //可以得到长度 8
    str.length = 3; //不能改变源字符串的长度 
    console.log(str);//abc 皮卡同学

    console.log(str[5]); //可以得到对应位置的字符串 卡
    str[5] = "摔"; //不可以改值
    console.log(str);  //abc 皮卡同学
    console.log( str.charAt(4) ); //皮
    console.log( str.charAt(6) ); //同
```

unicode 示例：

```javascript
alert( "\u00A9" ); // ©
alert( "\u{20331}" ); // 佫，罕见的中国象形文字（长 unicode）
alert( "\u{1F60D}" ); // 😍，笑脸符号（另一个长 unicode）
```

所有的特殊字符都以反斜杠字符 `\` 开始。它也被称为“转义字符”。

如果我们想要在字符串中插入一个引号，我们也会使用它。

例如：

```javascript
alert( 'I\'m the Walrus!' ); // I'm the Walrus!
```

正如你所看到的，我们必须在内部引号前加上反斜杠 `\'`，否则它将表示字符串结束。

- 补充

```js
/*
    * 任意的一个字符对应的都有一个数字编码
    *
    * str.charCodeAt( 下标 )
    *
    * String.fromCharCode(数字编码)
    *
    * */
    // let str = "123皮卡同学";
    // console.log( str.charCodeAt(4) );
    // console.log( String.fromCharCode(48) );

    let str = "竹青暮雨我爱你";

    let newStr = "";
    for (let i=0;i<str.length;i++){
      let code = str.charCodeAt(i) + 520;
      // console.log(code);
      // console.log(String.fromCharCode(code));
      newStr += String.fromCharCode(code);
    }
    console.log(newStr);//紁饚梶飰搙琹全
```

## [改变大小写](https://zh.javascript.info/string#gai-bian-da-xiao-xie)

[toLowerCase()](https://developer.mozilla.org/zh/docs/Web/JavaScript/Reference/Global_Objects/String/toLowerCase) 和 [toUpperCase()](https://developer.mozilla.org/zh/docs/Web/JavaScript/Reference/Global_Objects/String/toUpperCase) 方法可以改变大小写：

```javascript
alert( 'Interface'.toUpperCase() ); // INTERFACE
alert( 'Interface'.toLowerCase() ); // interface
```

或者我们想要使一个字符变成小写：

```javascript
alert( 'Interface'[0].toLowerCase() ); // 'i'
```

## [查找子字符串](https://zh.javascript.info/string#cha-zhao-zi-zi-fu-chuan)

- ### [str.indexOf](https://zh.javascript.info/string#strindexof)

第一个方法是 [str.indexOf(substr, pos)](https://developer.mozilla.org/zh/docs/Web/JavaScript/Reference/Global_Objects/String/indexOf)。

它从给定位置 `pos` 开始，在 `str` 中查找 `substr`，如果没有找到，则返回 `-1`，否则返回匹配成功的位置。

例如：

```javascript
let str = 'Widget with id';

alert( str.indexOf('Widget') ); // 0，因为 'Widget' 一开始就被找到
alert( str.indexOf('widget') ); // -1，没有找到，检索是大小写敏感的

alert( str.indexOf("id") ); // 1，"id" 在位置 1 处（……idget 和 id）
```

可选的第二个参数允许我们从给定的起始位置开始检索。

例如，`"id"` 第一次出现的位置是 `1`。查询下一个存在位置时，我们从 `2` 开始检索：

```javascript
let str = 'Widget with id';

alert( str.indexOf('id', 2) ) // 12
```

## [获取子字符串](https://zh.javascript.info/string#huo-qu-zi-zi-fu-chuan)

JavaScript 中有三种获取字符串的方法：`substring`、`substr` 和 `slice`。

`str.slice(start [, end])`

返回字符串从 `start` 到（但不包括）`end` 的部分。

例如：

```js
let str = "stringify";
alert( str.slice(0, 5) ); // 'strin'，从 0 到 5 的子字符串（不包括 5）
alert( str.slice(0, 1) ); // 's'，从 0 到 1，但不包括 1，所以只有在 0 处的字符
```

如果没有第二个参数，`slice` 会一直运行到字符串末尾：

```js
let str = "stringify";
alert( str.slice(2) ); // 从第二个位置直到结束
```

`start/end` 也有可能是负值。它们的意思是起始位置从字符串结尾计算：

```js
let str = "stringify";

// 从右边的第四个位置开始，在右边的第一个位置结束
alert( str.slice(-4, -1) ); // 'gif'
```

- **str.substring(start [, end])**

返回字符串在 `start` 和 `end` **之间** 的部分。

这与 `slice` 几乎相同，但它允许 `start` 大于 `end`。

例如：

```js
let str = "stringify";

// 这些对于 substring 是相同的
alert( str.substring(2, 6) ); // "ring"
alert( str.substring(6, 2) ); // "ring"

// ……但对 slice 是不同的：
alert( str.slice(2, 6) ); // "ring"（一样）
alert( str.slice(6, 2) ); // ""（空字符串）
```

不支持负参数（不像 slice），它们被视为 `0`。

- **str.substr(start [, length])**

返回字符串从 `start` 开始的给定 `length` 的部分。

与以前的方法相比，这个允许我们指定 `length` 而不是结束位置：

```js
let str = "stringify";
alert( str.substr(2, 4) ); // 'ring'，从位置 2 开始，获取 4 个字符
```

第一个参数可能是负数，从结尾算起：

```js
let str = "stringify";
alert( str.substr(-4, 2) ); // 'gi'，从第 4 位获取 2 个字符
```

回顾一下这些方法，以免混淆：

| 方法                    | 选择方式……                                            | 负值参数            |
| :---------------------- | :---------------------------------------------------- | :------------------ |
| `slice(start, end)`     | 从 `start` 到 `end`（不含 `end`）                     | 允许                |
| `substring(start, end)` | `start` 与 `end` 之间（包括 `start`，但不包括 `end`） | 负值代表 `0`        |
| `substr(start, length)` | 从 `start` 开始获取长为 `length` 的字符串             | 允许 `start` 为负数 |

还有其他几种有用的字符串方法：

- `str.trim()` —— 删除字符串前后的空格 (“trims”)。
- `str.repeat(n)` —— 重复字符串 `n` 次。
- …其他

- ## 案列

```html

<!DOCTYPE HTML>
<html>
<head>
  <meta charset="UTF-8">
  <title>Title</title>
  <meta name="keywords" content="关键词">
  <meta name="description" content="描述">
  <meta name="author" content="潭州教育-阿飞老师">
  <style>
    body{font-family: "Microsoft YaHei",serif;}
    body,dl,dd,p,h1,h2,h3,h4,h5,h6{margin:0;}
    ol,ul,li{margin:0;padding:0;list-style:none;}
    img{border:none;}

    #wrap{
      width: 640px;
      height: 315px;
      margin: 50px auto;
      border: 1px solid #bbb;
      border-radius: 5px;
    }
    #wrap .top{
      width: 600px;
      height: 40px;
      padding-top: 30px;
      margin: 0 auto;
    }
    #wrap .top input{
      margin:0 5px;
      outline: none;
    }
    #wrap .top input[type=text]{
      width: 180px;
      height: 36px;
      border:1px solid #bbb;
      text-indent: 5px;

    }
    #wrap .top input[type=button]{
      width: 50px;
      height: 40px;
    }
    #wrap .bottom{
      margin-top: 20px;
    }
    #wrap .bottom p{
      margin: 5px 0;
      font-size: 15px;
      text-indent: 2em;
      line-height: 25px;
    }
    #wrap .bottom p b{
      color: red;
    }

  </style>
</head>
<body>
  <div id="wrap">
    <div class="top">
      <input type="text" placeholder="搜索内容">
      <input type="button" value="搜索">
      <input type="text" placeholder="替换内容">
      <input type="button" value="替换">
      <input type="button" value="重置">
    </div>

    <div class="bottom">
      <p>张家界是湖南省辖地级市，原名大庸市，辖2个市辖区（永定区、武陵源区）、2个县（慈利县、桑植县）。位于湖南西北部，澧水中上游，属武陵山区腹地。[1] 张家界因旅游建市，是中国最重要的旅游城市之一，是湘鄂渝黔革命根据地的发源地和中心区域。</p>
      <p>1982年9月，张家界国家森林公园成为中国第一个国家森林公园。</p>
      <p>1988年8月，张家界武陵源风景名胜区被列入国家重点风景名胜区；1992年，由张家界国家森林公园等三大景区构成的武陵源风景名胜区被联合国教科文组织列入《世界自然遗产名录》；2004年2月，被列入全球首批《世界地质公园》；2007年，被列入中国首批国家5A级旅游景区。[2]</p>
    </div>
  </div>

  <script>

    (function(){
      let aInput = document.querySelectorAll("#wrap input");
      let aP = document.querySelectorAll("#wrap .bottom p");

      // 存储一下初始的p内容
      let apTextArr = [];
      aP.forEach(node=>{
        apTextArr.push(node.innerText);
      });
      /*let apTextArr = [].slice.call(aP).map(node=>node.innerText);*/
      // let apTextArr = [...aP].map(n=>n.innerText);


      //搜索按钮的点击
      aInput[1].onclick = function(){
        //获取搜索框输入的内容
        let val = aInput[0].value;

        //没有输入内容的时候，不需要之后后面的逻辑
        if(!val)return;

        //后续的逻辑
        aP.forEach(goudan=>{
          let text = goudan.innerText;
          goudan.innerHTML = text.split(val).join("<b>"+val+"</b>");
        });


        /*let html = oBottom.innerHTML;
        oBottom.innerHTML = html.split(val).join("<b>"+val+"</b>");
*/
      };

      //替换按钮的点击
      aInput[3].onclick = function(){
        //获取搜索框的内容
        let val1 = aInput[0].value;
        //获取替换框的内容
        let val2 = aInput[2].value;

        //
        if( !val1 || !val2 )return;
        // if( !(val1&&val2) )return;
        //后续的逻辑
        aP.forEach(goudan=>{
          let text = goudan.innerText;
          goudan.innerHTML = text.split(val1).join("<b>"+val2+"</b>");
        });

      };

      //重置按钮的点击
      aInput[4].onclick = function(){

        //还原p的内容
        aP.forEach((node,index)=>{
          node.innerHTML = apTextArr[index];
        });

        //清空所有的输入框
        aInput[0].value = "";
        aInput[2].value = "";
      };

    })();

  </script>
</body>
</html>
```


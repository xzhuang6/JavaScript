## 一.认识JS

1. HTML(骨架，元素，结构)CSS(表现，效果，状态)JS(响应行为，交互，复杂操作)

2. JavaScript(JS)是什么？

   > 基于原型，动态类型，解释型，弱类型 脚本语言 
   >
   > ```
   > 传统语言： OOL 基于类/对象=>实例
   > 	 
   > Javascript： 基于原型，对象(万物皆对象)，原型可以指定，方法可灵活使用
   > 	
   > 脚本语言： 依赖环境(宿主环境)运行，浏览器可以使用DOM/BOM等，还有nodeJS(服务端)
   > 	
   > 弱类型/动态类型： 变量声明不需要规定类型，并且可以相互转换
   > 	
   > 解释型： 没有编译过程，不生成其他可执行文件，完成语法分析后逐行解析执行(暂时这么理解)
   > ```

3. JavaScript在`客户端`的三大组成： （语法，浏览器，页面元素）  

   > ECMAScript es5 6 7	语法，使用规则(等同于html里的<>和css里的{})，JS的本质
   >
   > es是js的标准 js是es的实现
   >
   > BOM	BrowserObjectModel 浏览器对象模型，浏览器提供的工具箱，我们可以直接使用
   >
   > DOM	DocumentObjectModel 文档对象模型，页面元素和方法的整合工具箱，我们可以直接使用

   <img src="https://cdn.nlark.com/yuque/0/2020/png/335089/1578574917022-76618071-003e-43b2-89c7-ea3aa39e161d.png" alt="image.png" style="zoom:80%;" />

## 二.JS 实现

JS有3种书写位置，分别为行内、内嵌和外部

**行内JS**

- 可以将单行或少量JS代码写在HTML标签的事件属性中（以on开头的属性），如：`onclick`(不常用，不推荐)

```html
<input type="button" value="点击" onclick="alert('这是写在标签属性中的JS代码!')">
```

- 单双引号的使用：在HTML中推荐使用双引号，在JS中推荐使用单引号
- 行内JS的缺点：

- - 可读性差，在HTML中编写大量JS代码时，不方便阅读
  - 引号易错，引号多层嵌套匹配时，容易混淆

**内嵌JS**

- 可以将多行JS代码写到`<script></script>`标签中
- `<script></script>`标签可以放在HTML的`<body>`和`<head>`中，一般放在`<body>`中的最后
- JS代码中不能出现`</script>`字符串，可以通过转义字符来解决：`<\/script>`

```html
<script>
    alert('这是写在script标签中的JS代码!')
</script>
```

**外部JS**

- JS代码可以放在外部的.js文件中，通过src属性引入`<script src="example.js"></script>`
- 放在外部的好处：

- - 利于HTML页面代码结构化
  - 可维护性强、可缓存、适应未来

- Script标签如果引入了外部文件，则不能再在`<script></script>`标签中编写代码

```js
//test.js
alert('这是写在外部.js文件中的JS代码！')
```

在html文件中引用：

```html
<script src="test.js"></script>
```

## 三.JS 输入

可以在JS中使用`prompt(info)`在浏览器弹出一个输入框，供用户输入

```html
<script>
    prompt('请输入您的姓名：')
</script>
```

## 四.JS 输出

`**alert()**`：弹出一个警告框

```html
<script>
        alert('密码不能为空！')
</script>
```

`**document.write()**`：向body中输出内容

```html
<script>
        document.write('你好鸭~')
</script>
```

`**console.log()**`：向控制台输出内容

```html
<script>
    console.log('hello js'')
</script>
```

## 五.JS 语句

- JS代码是从上往下执行的（而且是阻断式执行）
- 每行结尾的分号可有可无（建议写分号）
- JS对大小写敏感
- 字符串使用单引号或双引号均可
- 在文本字符串中使用反斜杠换行：`document.write("Hello\World!");`

## 六.JS 注释

- 单行注释：//（默认快捷键：Ctrl+/）
- 多行注释：/**/（默认快捷键：ALt+Shitf+A）
- 一般在行末使用注释

```html
<script>
// 单行注释 
/* 多
   行
   注
   释 */
</script>
```

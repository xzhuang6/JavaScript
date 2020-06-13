## 第二十章.DOM

## DOM

DOM（Document Object Model）文档对象模型，是W3C组织规定的用来操作页面的各种API。前面我们所学习的所有和页面相关的操作都是DOM规定好的。

### 1.节点类型

- childNodes

    获取一个元素的所有子节点……

- 节点类型

    DOM包含了多种节点，我们通常获取的标签，只是节点中的一种：

| 节点名称         | nodeType |
| ---------------- | -------- |
| *元素节点*       | *1*      |
| *属性节点*       | *2*      |
| *文本节点*       | *3*      |
| CDATA节点        | 4        |
| 实体引用名称节点 | 5        |
| 实体名称节点     | 6        |
| 处理指令节点     | 7        |
| 注释节点         | 8        |
| 文档节点         | 9        |
| 文档类型节点     | 10       |
| 文档片段节点     | 11       |
| DTD声明节点      | 12       |

重点理解前三种节点。

每个节点有`nodeName`属性，文本节点和属性节点的`nodeValue`属性。

- 常见的节点获取API

    常用：children  parentNode  offsetParent

    不常用：firstElementChild / firstChild     lastElementChild / lastChild   nextElementSibling / nextSibling    previousElementSibling / previouSibling

### 2.创建、添加、删除节点

- 创建节点

    **createElement**   创建一个元素节点；

    **createTextNode**   创建一个文本节点；

    **createDocumentFragment**  创建一个文档碎片，先将多个节点整合到这里面再统一添加。

- 添加节点

    **appendChild**   元素最后添加一个子节点；

    **insertBefore**   在元素某个子节点之前添加新子节点，第一个参数为新节点，第二个参数为已存在的子节点。

- 替换节点

    **replaceChild**  用新节点替换某个子节点，第一个参数为新节点，第二个参数为已存在的某个子节点。

- 删除节点

    **removeChild**  删除元素的某个子节点。

    

- DOM

```html
<!DOCTYPE html>
<html lang="zh-cn">
<head>
  <meta charset="UTF-8">
  <title>Title</title>
</head>
<body>
  <div id="wrap">
    <!--注释-->
    <p class="a">p1</p><!--balabalabl-->
    <p>p2</p>
    <a href="">a</a>
    哈哈哈哈
    <b>b</b>
  </div>
  <script>

    /*
    * DOM  Document Object Model
    *   文档对象模型
    *
    * ECMAScript  DOM   BOM
    *
    * 所有和HTML页面相关的操作都是DOM提供给我们的
    *   document
    *
    *
    * */
    /*
    * 节点类型  12种
    *
    * 元素节点
    * 文本节点
    * 注释节点
    *
    * */

    /*
    * 子节点
    * */

    let oWrap = document.getElementById("wrap");

    console.log( oWrap.childNodes );

    oWrap.childNodes[7].innerText = "balabalabl";

    //oWrap.childNodes[1].nodeValue = "修改注释";

    console.log(
      document.querySelector("#wrap a") === oWrap.childNodes[7]
    );

    oWrap.childNodes[0].nodeValue = "mint";
      //nodeValue修改文本的内若或者注释节点的内容
      //nodeValue针对元素节点是没有意义的，null，元素节点用innerHTML和innerText来操作
      
    /*
    * nodeName
    * nodeValue
    * nodeType
    * */

  </script>
</body>
</html>
```

![1590918784794](C:/Users/%E7%AB%B9%E9%9D%92%E6%9A%AE%E9%9B%A8/AppData/Roaming/Typora/typora-user-images/1590918784794.png)

![1590918806199](C:/Users/%E7%AB%B9%E9%9D%92%E6%9A%AE%E9%9B%A8/AppData/Roaming/Typora/typora-user-images/1590918806199.png)

```html
<div id="wrap"><!--注释--><p>p1</p><p>p2</p><a href="">a</a><b>b</b></div>

<script>
    let oWrap = document.getElementById("wrap");
    console.log( oWrap.childNodes );//
</script>   
```

- 元素节点

```html
   <div id="wrap">
    <!--注释-->
    <p class="a">p1</p>
    <p>p2</p>
    <a href="">a</a>
    哈哈哈哈
    <b>b</b>
  </div>
  
   <script>
   /*
    * 平常操作最多的就是元素节点
    *
    * children
    *   只获取元素子节点
    * */

    let oWrap = document.getElementById("wrap");

    console.log( oWrap.children );

    console.log( document.querySelector("#wrap .a") === oWrap.children[0] );


    [...oWrap.children].forEach((node,index)=>{
      console.log(node, index);
    });
   </script>
```

- 父节点

```html
<div id="nav">
    <div id="wrap">
      <p>pppp</p>
      <a href="">aaaa</a>
    </div>
  </div>
  <script>

    /*
    * parentNode
    *   html结构上的父级
    *
    * offsetParent
    *   定位父级
    *   （元素自身没有加定位属性的话，也是有定位父级的）
    *
    * */

    let oP = document.querySelector("#wrap p");

    console.dir(oP);//直接console.log打印浏览器做过预处理，用dir看更加明了一些
    console.dir(oP.parentNode);
    console.dir(oP.parentNode === document.getElementById("wrap"));

    console.dir(oP.offsetParent);

    console.log(oP.parentNode.parentNode);
      
  </script>
```

![1590936087958](C:/Users/%E7%AB%B9%E9%9D%92%E6%9A%AE%E9%9B%A8/AppData/Roaming/Typora/typora-user-images/1590936087958.png)

- 所有子节点

```html
<div id="wrap">
    <div id="nav">
      <p></p>
    </div>
    <div>
      <a href=""></a>
    </div>
  </div>

<script>
    let oWrap = document.getElementById("wrap");
    
    console.log( oWrap.getElementsByTagName("*") );
</script>
```

![1590936220746](C:/Users/%E7%AB%B9%E9%9D%92%E6%9A%AE%E9%9B%A8/AppData/Roaming/Typora/typora-user-images/1590936220746.png)

- 其他元素节点的获取

```html
 <div id="wrap">
    <p>p1</p>
    <p>p2</p>
  </div>
  <script>

    /*
    * firstChild
    * firstElementChild
    *
    * lastChild
    * lastElementChild
    *
    * nextSibling
    *
    * */
    var oWrap = document.getElementById("wrap");

    console.log(oWrap.firstChild);
    console.log(oWrap.firstElementChild);
    
    console.log( getFirstElementChild(oWrap) );

    function getFirstElementChild( node ){
      if (node.firstElementChild === undefined){
        return node.firstChild;
      }else{
        return node.firstElementChild;
      }
    }
    console.log( oWrap.children[0] );
    console.log( oWrap.children[oWrap.children.length-1] );
```

- 其他节点的获取

```html
<div id="wrap">
    <p>p1</p>
    <p>p2</p>
  </div>
  <script>
    /*
    * firstChild
    * firstElementChild
    *
    * lastChild
    * lastElementChild
    *
    * nextSibling
    *
    * */
    var oWrap = document.getElementById("wrap");

    console.log(oWrap.firstChild);
    console.log(oWrap.firstElementChild);

    console.log( getFirstElementChild(oWrap) );

    function getFirstElementChild( node ){
      if (node.firstElementChild === undefined){
        return node.firstChild;
      }else{
        return node.firstElementChild;
      }
    }
    console.log( oWrap.children[0] );
    console.log( oWrap.children[oWrap.children.length-1] );
  </script>
```

![1591083971638](C:/Users/%E7%AB%B9%E9%9D%92%E6%9A%AE%E9%9B%A8/AppData/Roaming/Typora/typora-user-images/1591083971638.png)

- 例子

```html
<style>
	 #wrap p{
      width: 100px;
      height: 100px;
      background-color: orange;
    }
</style>
<div id="wrap">
    <p id="ppp"></p>
  </div>
  <script>
    let oWrap = document.getElementById("wrap");
    let oP = document.getElementById("ppp");

    oP.onclick = function(){
      alert("Hello World！");
    };


    oWrap.innerHTML += `<a href="">我是一个a标签</a>`;
    console.log(oWrap.innerHTML + `<a href="">我是一个a标签</a>`)
// <p id="ppp"></p>
//  <a href="">我是一个a标签</a><a href="">我是一个a标签</a>
//此时的打印结果是以上这个字符串，oWrap里面的内容通过+=innerHTML 被覆盖点掉了，点击盒子不会弹框。
  </script>
```

<img src="C:/Users/%E7%AB%B9%E9%9D%92%E6%9A%AE%E9%9B%A8/AppData/Roaming/Typora/typora-user-images/1591084895557.png" alt="1591084895557" style="zoom:50%;" />

- 新增节点

```html
style>
    *{margin:0;padding:0;font-family:"Microsoft Yahei";}

    #wrap p{
      width: 100px;
      height: 100px;
      background-color: orange;
    }
  </style>
  
  <div id="wrap">
    <b>bbbbb</b>
    <p id="ppp"></p>
  </div>
  <script>

    /*
    * document.createElement()
    *   创建元素节点
    *
    * ele.appendChild()
    *   给ele添加一个子节点
    *
    * ele.insertBefore(newChild, refChild)
    *   在refChild子节点之前，插入新子节点newChild
    *
    * */

    let oWrap = document.getElementById("wrap");
    let oP = document.getElementById("ppp");

    oP.onclick = function(){
      alert("Hello World！");
    };

    //创建新节点
    let oA = document.createElement("a");
    oA.innerText = "我是一个a标签";
    oA.href = "https://www.baidu.com/";

    //放入owrap
    // oWrap.appendChild( oA );

    // oWrap.insertBefore(oA, oWrap.children[0]);
    oWrap.insertBefore(oA, oP);
  </script>
```

- 删除节点

```html
<div id="wrap">
    <p class="p1">p1</p>
    <p class="p2">p2</p>
  </div>
  <script>

    /*
    * removeChild
    *   删除
    *   （节点是不能自杀的，必须通过父级移除）
    * */

    /*document.onclick = function(){
      let p2 = document.querySelector("#wrap .p2");
      let oWrap = document.getElementById("wrap");

      oWrap.removeChild( p2 );
    };*/

    document.onclick = function(){
      let p2 = document.querySelector("#wrap .p2");
      p2.parentNode.removeChild(p2);

    };//点击页面删除了p1，再次点击页面报错 Uncaught TypeError: Cannot read property 'parentNode' of null
      //说明：节点是不能自杀的，必须通过父级移除
  </script>
```

- 关于节点的储存

```html
 <div id="wrap">
    <p class="p1">p1</p>
    <p class="p2">p2</p>
    <button id="btn">删除p2</button>
    <button id="btn2">把p2加回来</button>
  </div>
  <script>

    let oWrap = document.getElementById("wrap"),
      p1 = document.querySelector("#wrap .p1"),
      p2 = document.querySelector("#wrap .p2"),
      btn = document.getElementById("btn"),
      btn2 = document.getElementById("btn2")
    ;

    p1.onclick = function(){
      alert("我是P1 ！！");
    };
    p2.onclick = function(){
      alert("我是P2 ！！");
    };

    btn.onclick = function(){
      oWrap.removeChild(p2);
    };
    btn2.onclick = function(){
      oWrap.appendChild(p2);
    };
  </script>
```

- 案例

```html
<!DOCTYPE html>
<html lang="zh-cn">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            font-family: "Microsoft Yahei";
        }


        #wrap {
            background: linear-gradient(to bottom, #8cc1de, #f9a886);
            user-select: none;
        }

        #wrap .content {
            display: flex;
            width: 800px;
            height: 530px;
            margin: 0 auto;
            padding-top: 50px;
        }

        #wrap .content .left {
            flex: 1;
            box-sizing: border-box;
            padding: 60px 20px;
            background-color: #fff;
        }

        #wrap .content .right {
            flex: 1;
            box-sizing: border-box;
            padding: 60px 20px;
            background-color: rgba(0, 0, 0, .5);
        }

        #wrap .left-top {
            color: #f60;
        }

        #wrap .left-top span {
            color: #000;
            margin-left: 6px;
            cursor: pointer;
        }

        #wrap .left-top span:hover {
            color: red;
        }

        #wrap .left-bottom {
            margin-top: 15px;
        }

        #wrap .left-bottom li {
            float: left;
            list-style: none;
            padding: 5px 10px;
            margin: 5px;
            color: #aaa;
            border: 1px solid #aaa;
        }

        #wrap .left-bottom li i {
            cursor: pointer;
        }

        #wrap .left-bottom li:hover i {
            color: red;
        }

        #wrap .right ul li {
            float: left;
            margin: 10px;
            list-style: none;
            color: #fff;
            border: 1px solid #fff;
            padding: 5px 10px;
        }
    </style>
</head>
<body>
<div id="wrap">
    <div class="content">
        <div class="left">
            <p class="left-top">
                热门目的地：
                <!--<span>马来西亚</span><span>泰国</span><span>三亚</span><span>新西兰</span><span>云南</span>-->
            </p>
            <ul class="left-bottom">
                <!--<li>
                  <span>马来西亚 | </span><i>x</i>
                </li>-->
            </ul>
        </div>
        <div class="right">
            <ul>
                <!--<li>马来西亚</li>
                <li>云南</li>-->
            </ul>
        </div>
    </div>
</div>
<script>
	(function () {

		let leftTopP = document.querySelector("#wrap .left-top")
			, oLeftUl = document.querySelector("#wrap .left-bottom")
			, oRightUl = document.querySelector("#wrap .right ul")
		;


		//模拟城市数据
		let data = ["泰国", "新加坡", "印度尼西亚", "咖喱", "肉骨茶", "印尼九层塔"];
		//文档碎片
		let f = document.createDocumentFragment();
		//用于检测对应的tag有没有被点击过
		let ifClickArr = [];
		//生成目的地tag
		data.forEach((item, index) => {
			let oSpan = document.createElement("span");
			oSpan.innerText = item;
			//每个tag的点击事件
			oSpan.onclick = function () {
				//先判断对应的内容有没有生成过
				if (ifClickArr[index]) return;
				ifClickArr[index] = true;

				//创建ul的内容
				createNode(index);
			};
			f.appendChild(oSpan);
		});
		leftTopP.appendChild(f);

		//生产节点的函数
		function createNode(index) {
			//生产node
			let leftLi = document.createElement("li");
			let rightLi = document.createElement("li");

			//左边ul对应的函数
			(function () {
				let oSpan = document.createElement("span");
				let oI = document.createElement("i");
				oSpan.innerText = `${data[index]} | `;
				oI.innerText = "x";

				//每一个i是有点击事件的
				oI.onclick = function () {
					//干掉自己的爸爸
					oLeftUl.removeChild(leftLi);
					//干掉右边对应的结构
					oRightUl.removeChild(rightLi);
					//改变记录的状态
					ifClickArr[index] = false;
				};

				leftLi.appendChild(oSpan);
				leftLi.appendChild(oI);

				oLeftUl.appendChild(leftLi);
			})();

			//右边ul对应的函数
			(function () {
				rightLi.innerText = data[index];
				oRightUl.appendChild(rightLi);
			})();
		}

	})();
</script>
</body>
</html>
```


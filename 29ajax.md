## 第二十九章.ajax

- 原生ajax

```js
  //创建ajax对象
    let xhr = new XMLHttpRequest();

    //监听当前请求的进度
    /*
    * readyState 请求状态
    *   1 -- 请求建立（open执行之后）
    *   2 -- 请求发送（send执行之后）
    *   3 -- 请求已经发送，正在等在后端处理
    *   4 -- 请求完成，数据可用
    * */
    xhr.onreadystatechange = function(){
      // console.log(this.readyState);
      //一般情况下，在 4 状态下，进行后续的操作
      if (this.readyState === 4){
        //拿到后端返回的数据
        console.log(this.responseText);

        //拿到数据之后，怎么使用这个数据，用什么方法使用这个数据，这个是你前端说了算
        let oImg = new Image();
        // let oImg = document.createElement("img");
        oImg.src = this.responseText;
        document.body.appendChild(oImg);
      }
    };


    //创建请求
    /*
    * 参数一：请求方式
    *   - get
    *   - post
    *   用哪一个？ --- 实际开发中，用什么方式后端会告诉你
    *
    * 参数二：接口地址(一个完整的网络地址 或者是 服务器路径)
    *   - 字符串
    *   具体写什么？ --- 实际开发中，地址后端会告诉你
    *
    * 参数三：是否异步
    *   - true 异步
    *   - false 不异步
    *   固定为true，任何情况没有用到false的需求
    * */
    xhr.open("GET", "./test.txt", true);

    //发送请求
    xhr.send();
```

- 案例–-模拟ajax

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

    </ul>
    <ul class="btn">
      <li>从高到低</li>
      <li>从低到高</li>
      <li>随机排序</li>
    </ul>
  </div>
  <script>

    (function(){
      //发送ajax请求拿到数据
      let xhr = new XMLHttpRequest();
      xhr.onreadystatechange = function(){
        if (xhr.readyState !== 4)return;
        //把 xhr.responseText 处理成对象
        /*
        * 处理成对象的方式有很多，但是最方便的是通过JSON对象来处理
        * 通过JSON对象来处理的前提是，后端返回的是json格式的数据
        * */
        let data = JSON.parse( xhr.responseText );

        //执行后续的前端逻辑代码
        goudan(data);

      };
      xhr.open("GET","./02.txt",true);
      xhr.send();



      //前端DOM处理代码
      function goudan(data){
        /*需要从后台请求数据 */
        //先假装我们请求到了数据data

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
      }
        
    })();
      
  </script>
</body>
</html>
```

```txt
//02.txt

[
  {
    "src" : "./img/xh_img1.jpg",
    "price" : 100,
    "title" : "深红色经典玫瑰"
  },
  {
    "src" : "./img/xh_img2.jpg",
    "price" : 97,
    "title" : "甜美七分袖荷叶边条纹设"
  },
  {
    "src" : "./img/xh_img3.jpg",
    "price" : 99.5,
    "title" : "甜美七分袖荷叶边条纹设"
  },
  {
    "src" : "./img/xh_img4.jpg",
    "price" : 215,
    "title" : "甜美七分袖荷叶边条纹设"
  },
  {
    "src" : "./img/xh_img5.jpg",
    "price" : 130,
    "title" : "经典红色我的最爱"
  },
  {
    "src" : "./img/xh_img6.jpg",
    "price" : 300,
    "title" : "清淡优雅百年百合"
  },
  {
    "src" : "./img/xh_img7.jpg",
    "price" : 700,
    "title" : "紫色冷艳系列"
  },
  {
    "src" : "./img/xh_img8.jpg",
    "price" : 500,
    "title" : "粉色浪漫系列玫瑰"
  }
]

```

- 发送数据

```js
(function(){
      let xhr = new XMLHttpRequest();
      xhr.onreadystatechange = function(){
        if (xhr.readyState !== 4)return;

        console.log(JSON.parse(xhr.responseText));

      };
      xhr.open("GET","http://47.105.155.167/luyujin?name=afei&age=18",true);
      xhr.send();
    })();


    (function(){
      let xhr = new XMLHttpRequest();
      xhr.onreadystatechange = function(){
        if (xhr.readyState !== 4)return;

        console.log(JSON.parse(xhr.responseText));

      };
      xhr.open("POST","http://47.105.155.167/pika",true);
      //post传参需要设置一下请求头数据格式
      xhr.setRequestHeader("Content-type","application/x-www-form-urlencoded");
      xhr.send("name=afei&age=18");
    })();
```

- jq的ajax

```html
<!--引入jq-->
  <script src="https://cdn.jsdelivr.net/npm/jquery@3.2.1/dist/jquery.min.js"></script>
  <script>

    //假设我已经拿到了用户输入的数据 或者是 整合好了需要发送给后端的数据
    let x = {
      name : "皮卡",
      age : 20,
      sex : "男"
    };

    $.ajax({
      type : "GET"//请求方式
      ,url : "http://47.105.155.167/luyujin" //地址
      ,data : {name:"Sherry",age:16} //需要把什么数据传给后端
      ,dataType : 'json' //按照 json 格式预处理后端返回过来的数据
      ,success(msg){
        console.log(msg); //msg就是处理过后的后端数据
      } //成功之后的回调函数
      ,error(){} //失败之后的回调函数
    });

    $.ajax({
      type : "POST"//请求方式
      ,url : "http://47.105.155.167/pika" //地址
      ,data : x //需要把什么数据传给后端
      ,dataType : 'json' //按照 json 格式预处理后端返回过来的数据
      ,success(msg){
        console.log(msg); //msg就是处理过后的后端数据
      } //成功之后的回调函数
      ,error(){} //失败之后的回调函数
    });
</script>
```

- Promise

```js
/*
    * ES6 Promise
    *
    *   解决异步代码回调层数很深的问题
    *    	避免回调地狱
    *
    * */

    // new Promise().then().catch();

    new Promise((res, rej)=>{
      setTimeout(()=>{
        console.log("第一个定时器");
        res();
        // rej();
      },2000);
    }).then(()=>{
      return new Promise((res,rej)=>{
        setTimeout(()=>{
          console.log("第二个定时器");
          res();
        },2000);
      });
    }).then(()=>{
      return new Promise((res,rej)=>{
        setTimeout(()=>{
          console.log("第三个定时器");
          res();
        },2000);
      });
    }).then(()=>{
      setTimeout(()=>{
        console.log("第四个定时器");
      },2000);
    });
```

```js
function p(str){
      return new Promise((res,rej)=>{
        setTimeout(()=>{
          console.log(str);
          res();
        },2000);
      });
    }

    p("第一个定时器").then(()=>{
      return p("第二个定时器");
    }).then(()=>{
      return p("第三个定时器");
    }).then(()=>{
      return p("第四个定时器");
    });
```

- fetch

```js
/*
    * fetch
    *   ES6新增的原生js的api
    *
    * */

    /*
    * 链接里面最好不要有中文
    * */
    //console.log(encodeURI("http://47.105.155.167/luyujin?name=皮卡"));

    fetch(encodeURI("http://47.105.155.167/luyujin?name=皮卡"),{method:"GET"}) //路径，各项参数
      .then(res=>{
        return res.json(); //将返回的数据格式化
      })
      .then(data=>{
        console.log(data); //最终拿到的数据
      });
```

- axios

```html
 <!--引入axios-->
  <script src="https://cdn.bootcss.com/axios/0.19.0-beta.1/axios.min.js"></script>
  <script>
    /*
    * axios
    *   一个用来发送ajax请求的包
    * */

    // console.log(axios);
    axios.get(
      "http://47.105.155.167/luyujin", //请求地址
      {params:{x:10,y:20}} //get方式传递数据的写法
    ).then(res=>{
      // console.log(res);
      console.log(res.data);
    });


    axios.post(
      "http://47.105.155.167/pika",
      {a:30,b:40}
    ).then(res=>{
      console.log(res.data);
    });
   </script>
```

```html
  <!--引入axios-->
  <script src="https://cdn.bootcss.com/axios/0.19.0-beta.1/axios.min.js"></script>
  <script>

    axios.defaults.baseURL = "http://47.105.155.167/";

    axios.get(
      "/luyujin", //请求地址
      {params:{x:10,y:20}} //get方式传递数据的写法
    ).then(res=>{
      // console.log(res);
      console.log(res.data);
    });


    axios.post(
      "/pika",
      {a:30,b:40}
    ).then(res=>{
      console.log(res.data);
    });

  </script>
```

- 跨域

```html
 <script src="https://cdn.bootcss.com/axios/0.19.0-beta.1/axios.min.js"></script>
  <script>
    /*
    * 协议  http https
    * ip
    * 端口
    *
    * 三个一样叫 同域
    * 三个不一样叫 跨域
    * */

    axios.get(
      "https://www.baidu.com/"
    ).then(res=>{
      console.log(res);
    });
</script>  
```

- jsonp

```html
 <script src="https://cdn.jsdelivr.net/npm/jquery@3.2.1/dist/jquery.min.js"></script>
  <script>

    $.ajax({
      type : "GET",
      url : "./1.txt",
      dataType : "json",
      success(data){
        console.log(data);
      },
      error(...rest){
        console.log(rest);
      }
    });


  </script>
```

```txt
//1.txt

pika([
{
  "name":"皮卡"
  ,"age" : 18
  ,"sex" : "男"
},
{
  "name":"薄荷er"
  ,"age" : 16
  ,"sex" : "女"
}
])

```

- jsonp案例--模拟百度联想关键词

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

    #wrap{
      width: 300px;
      margin: 50px auto;
    }
    #search{
      width: 296px;
      height: 40px;
      font-family: "Microsoft Yahei";
      text-indent: 1em;
    }
    #list{
      width: 100%;
      list-style: none;
    }
    #list li{
      width: 100%;
      height: 25px;
      line-height: 25px;
    }
    #list li a{
      display: block;
      width: 100%;
      height: 100%;
      text-indent: 1em;
      font-size: 12px;
      color: #999;
      background-color: #f6f6f6;
      text-decoration: none;
    }
    #list li a:hover{
      background-color: #eee;
    }

  </style>
</head>
<body>
  <div id="wrap">
    <input type="text" id="search">
    <ul id="list">
      <!--<li><a href="">内容</a></li>
      <li><a href="">内容</a></li>
      <li><a href="">内容</a></li>-->
    </ul>
  </div>

  <script>

    /*function fly( data ){
      //得到联想关键词的内容
      let g = data.g || [];
    }*/


    //https://www.baidu.com/sugrec?prod=pc&wd=bbbb&cb=fly

    let oList = document.getElementById("list");
    let oSearch = document.getElementById("search");
    oSearch.oninput = function(){
      let val = this.value;

      //每一个src就对应一个js文件，我们要引入这个文件
      let oScript = document.createElement("script");
      //拼接对应的url
      oScript.src = `https://www.baidu.com/sugrec?prod=pc&wd=${encodeURI(val)}&cb=fly`;
      //添加到页面之后，script标签才会执行
      document.body.appendChild(oScript);
    }


    function fly( {g=[]} ){
      //得到联想关键词的内容
      // console.log(g);

      //根据g的内容来生成对应的li，添加给ul
      let html = "";
      g.forEach(item=>{
        html += `<li><a href="https://www.baidu.com/s?wd=${item.q}" target="_blank">${item.q}</a></li>`
      });
      oList.innerHTML = html;
    }

  </script>


</body>
</html>
```


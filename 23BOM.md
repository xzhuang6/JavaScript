## 第二三章.BOM

## BOM

BOM（Browser Object Model）浏览器对象模型，提供了一些和浏览或窗口相关的操作。学过的*弹窗*、*日志*、*定时器*就属于BOM的一部分。

### 1.重要事件

- onresize

    宽口大小发生改变的时候触发。

- onscroll

    页面滚动的时候触发，也可以用于某个元素节点上。

- onfocus onblur

    进入页面和离开页面时触发，也可以用于其他能获得焦点的元素节点上。



open()   close()

### 2.重要对象

- location

    获取/设置 URL相关的属性。

- history

    操作当前标签页的历史，类似于点击浏览器地址栏左侧的前进和后退按钮。

    `history.go(number)` -- 前进或后退指定的页面数。

    `history.back()` -- 后退一页。

    `history.forward()` -- 前进一页。

- navigator

    获取浏览器相关的信息。

- Screen

    获取用户显示屏幕的各种信息。

    `.width   .height`  获取显示器分辨率。

    `.availWidth   .availHeight` 获取除去任务栏的大小。

```js
  /*
    * BOM
    *  Browser Object Model
    * 浏览器对象模型
    *
    * */

    // window.open("http://www.baidu.com","_blank");
    // window.close();

    window.onresize = function(){
      console.log("浏览器的宽高在变动");
      console.log(window.innerWidth, window.innerHeight);
    };

    window.onscroll = function(){
      console.log("滚动条滚动的时候触发");
    };

    window.onfocus = function(){
      console.log("切换到了当前标签页");

      document.title = "mint的个人博客";
    };
    window.onblur = function(){
      console.log("离开了当前标签页");

      document.title = "快回来！出bug了！！";
    };
```


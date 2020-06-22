# WebAPI 第三天

> 目标：

- [ ] 能使用节点关系获取元素

- [ ] 能使用innerHTML创建元素

- [ ] 能使用document.createElement创建元素

- [ ] 能使用appendChild和insertBefore插入元素

- [ ] 能使用removeChild删除元素

- [ ] 能理解window顶级对象

- [ ] 能使用定时器实现倒计时

  

## 1.操作节点

> 目标：能使用节点关系获取元素、能创建元素、能将元素插入到网页中、能将网页中的某个元素删除

### 1.1 节点概述

- **定义**：网页中的所有内容都是节点（**标签**、**属性**、**文本**、注释等），在DOM 中，节点使用 node 来表示。
- **特点**：因为DOM 树中的所有节点均可通过 JavaScript 进行访问，所有 HTML 元素（节点）均可被修改，也可以创 建或删除。

<img src="image/2.png"/>

- **节点基本属性**

  - **nodeType** :  节点类型    （**在实际开发中，常用的是元素节点**）

    - 元素节点：element.nodeType == 1
    - 属性节点：element.nodeType == 2
    - 文本节点：element.nodeType == 3 

  - **nodeName**:  节点名称   element.nodeName

    ```js
    1. 创建一个div元素，内容是'我是div'
    2. 查看节点类型，和节点name
    var div = document.querySelector('div');
    console.log(div.nodeType);
    console.log(div.nodeName);
    ```

### 1.2 利用节点层级获取元素

- 利用 DOM 树可以把节点划分为不同的层级关系，常见的是**父子兄层级关系**。
- **获取套路**：1. 先要获取到某个具体元素  2. 通过具体元素获取它的父子兄弟   

<img src="image/2.png"/>

#### 1.2.1  获取父节点

- **语法**：`element.parentNode`
- **返回**：元素对象

```js
1. 创建一个含有4个li的ul
2. 通过li元素获取ul元素
var li1 = document.querySelector('li');
console.log(li1.parentNode);
```

#### 1.2.2  获取子节点

- **获取所有子节点 **    不常使用
  - 语法：`element.childNodes`  
  - 返回：**伪数组**  元素的所有子节点 ，包含（元素节点、文本节点（换行算在内）等）
- **获取所有子元素节点**    经常使用
  - 语法：`element.children`
  - 返回:   **伪数组**   元素的子元素节点

```js
1. 创建一个含有4个li的ul
2. 通过ul，获取ul的所有子节点,获取所有li元素 ，获取第二个li元素
var ul = document.querySelector('ul');
console.log(ul.children);
console.log(ul.children[1]);
```

- **获取第一个子节点**    不常使用
  - 语法：`element.firstChild`
  - 返回：返回第一个子节点，可能是（元素节点、文本节点（换行算在内）等），找不到则返回null
- **获取第一个子元素节点**    经常使用
  - 语法：`element.firstElementChild`
  - 返回：返回第一个子元素节点，找不到则返回null 

```js
1. 创建一个含有4个li的ul
2. 通过ul，获取第一个子节点，获取第一个li元素
var ul = document.querySelector('ul');
console.log(ul.firstChild)
console.log(ul.firstElementChild);
```

- **获取最后一个子节点**   不常使用
  - 语法：`element.lastChild`
  - 返回:  最后一个子节点，可能是（元素节点、文本节点（换行算在内）等），找不到则返回null
- **获取最后个子元素节点**   经常使用
  - 语法：`element.lastElementChild`
  - 返回：返回第一个子元素节点，找不到则返回null 

```js
1. 创建一个含有4个li的ul
2. 通过ul，获取最后一个子节点，获取最后一个li元素
var ul = document.querySelector('ul');
console.log(ul.lastChild)
console.log(ul.lastElementChild);
```

#### 1.2.3 获取兄弟节点

- **获取前一个元素兄弟节点**
  - 语法：`element.previousElementSibling`
  - 返回:  返回前一个兄弟元素节点，找不到则返回null 
- **获取后一个元素兄弟节点**
  - 语法：`element.nextElementSibling`
  - 返回:  返回后一个兄弟元素节点，找不到则返回null 

```js
1. 创建一个含有4个li的ul
2. 获取第二个li元素的前一个兄弟元素和后一个兄弟元素
var li2= document.querySelectorAll('li')[1];
console.log(ul.previousElementSibling)
console.log(ul.previousElementSibling);
```

### 1.3  创建元素节点

- **语法**：document. createElement('标签名')
- **返回**：一个元素对象，标签名是传入的标签名
- **注意**：不是创建了就渲染到页面上了，还需要插入到页面上

```js
1. 创建一个按钮，内容为发布
2. 点击按钮时，创建一个p元素
btn.onclick = function(){
	document. createElemnet('p');
}
```

### 1.4 添加节点

#### 1.4.1  追加到某个元素内部

- **语法**：`element.appendChild(child)`
- **描述**：将child插入到element的子节点列表的末尾

```js
1. 创建一个空ul和button
2. 点击button，给ul内部动态添加一个li元素
btn.onclick = function(){
	var li = document. createElemnet('li');
	ul.appendChild(li);
}
```

#### 1.4.2  将一个元素插入到某个元素的内部的指定元素的前面

- **语法**：element.insertBefore(child,指定元素)
- **描述**：将child插入到element的内部的'指定元素'的前面

```js
1. 创建一个button和一个ul内部有4个li元素
2. 点击button，创建一个li，内容为‘我是新增li元素’，将该li元素添加到第一个li元素的前面
btn.onclick = function(){
	var li = document. createElemnet('li');
	ul.insertBefore(li,ul.children[0]);
}
```

- **案例**   简单版发布留言

```js
      var btn = document.querySelector('input');
      btn.addEventListener('click',function(){
        var textarea = document.querySelector('textarea');
        if(textarea.value == ''){
          return;
        }
        var liNew = document.createElement('li');
        liNew.innerHTML =   textarea.value;
        var ul = btn.nextElementSibling;
        var li0 = ul.firstElementChild;
        ul.insertBefore(liNew,li0);
        textarea.value = '';
      })
```



#### 1.4.3  通过innerHTML给一个元素内部添加元素

- **语法**： `element.innerHTML = '标签'`
- **案例**  发布留言板，给li元素中添加删除按钮

```js
  liNew.innerHTML = '<p>'+textarea.value+'</p><span>删除</span>';
```



### 1.5 删除节点

- **语法**：`element.removeChild(child)`
- **描述**：从element中删除child元素
- **案例**   优化发布留言板，点击删除按钮，能够删除评论

```js
      var ul = document.querySelector('ul');
      ul.addEventListener('click',function(){
        if(event.target.nodeName == 'SPAN'){
          ul.removeChild(event.target.parentNode);
        }
      })
```



## 2. BOM

> 目标：知道什么是BOM、了解window对象、掌握window对象常用事件、会使用定时器、

### 2.1  什么是BOM

#### 2.2.1 BOM的概念

- **定义**：BOM（Browser Object Model）即浏览器对象模型，它提供了独立于内容而与浏览器窗口进行交互的对象，其核心对象是 window。

![1551319264407](D:/%E4%BC%A0%E6%99%BA%E6%92%AD%E5%AE%A2%E5%8F%8C%E5%85%83/04-Web%20APIs/Web%20APIs-day04/4-%E7%AC%94%E8%AE%B0/images/1551319264407.png)

#### 2.2.2  BOM的构成

- BOM 由一系列相关的对象构成，并且每个对象都提供了很多方法与属性
- BOM 比 DOM 更大，它包含 DOM。

<img src='image/1551319344183.png'>

### 2.3. 顶级对象window

- 特点：

  - window对象在浏览器中被称为**顶级对象**；
  - **顶级对象**：页面中所有的东西都是依赖于这个对象存在的；

  - 所有window对象的属性和方法，**都可以直接省略  `window.`，而直接使用**
    - 例如：alert()、 prompt()等
  - 变量与函数：
    - **所有的全局变量和全局函数都是window对象的属性和方法**；
    - 在js代码里面，不使用var声明的变量，都是隐式全局变量，这个方式是不推荐的，因为如果不使用var声明，是不会变量提升的；

### 2.4. window对象的常见事件

#### 2.4.1  页面加载事件  （也称入口函数）

- **描述**：当**页面所需的静态资源**（html文件、css文件、js文件、图片...）全部加载完毕，就会立刻执行该事件的事件处理程序

- **作用**：将所有js代码全部放到该事件的执行程序中，就可以把**js代码写在html文档页面元素的上方**

  ​           （浏览器在解析html文档时，都是从上到下一行一行读取的，如果直接把js写在页面元素的上方

  ​           先读取js，但是这时候在浏览器内部还没有加载页面元素，进而没有将页面转换成DOM树，因此
  ​			js就获取不到页面元素，但是js又用到了某个元素，就会报错 ）          

- **事件类型**：`load` 

- **语法**：

  - `window.onload = function(){}`
  - `window.addEventListener('load',function(){})`   

```
1. 创建一个button元素，内容为点击
2. 将js代码放在button元素上方，获取该元素，并给该元素添加点击事件，事件处理程序，打印‘事件生效’查看控制台
3. 将所有js代码放在页面加载事件中，查看控制台，测试点击事件
```

#### 2.4.2  调整窗口大小事件

- **描述**：当窗口大小发生改变时，就触发该事件，并执行事件处理程序
- **作用**：经常利用这个事件完成响应式布局。         
- **事件类型**：`resize` 
- **语法**：
  - `window.onresize = function(){}`
  - `window.addEventListener('resize',function(){})`   

```js
1. 创建一个div元素，宽高分别400px
2. 在入口函数中，监听窗口大小事件，如果窗口宽度小于800px,则修改div的宽度为200px;
  window.onload = function(){
      window.onresize = function(){
        if(window.innerWidth < 800){
          var div = document.querySelector('div');
          div.style.width = '200px';
            
        }
      }
    }
```

> 案例涉及知识点：window.innerWidth 当前屏幕的宽度  

### 2.5 定时器（两种）

#### 2.5.1 延迟定时器（炸弹定时器） 

##### 1. 创建延迟定时器  setTimeout

- **描述**：经过多少毫秒之后执行某个函数 （一次性）
- **语法**：
  - `window.setTimeout(函数名/匿名函数,[延迟毫秒数]) ` (window可以省略)
  - `setTimeout(函数名/匿名函数,[延迟毫秒数]) `
  - 通常我们在使用定时器时，都会给定时器赋值一个标识符(名字)，用以区别多个定时器
- **参数**：
  - 第一个参数：要做的事情，也称回调函数
    - 回调函数：回头调用的函数（普通函数是一行一行从上往下读取执行的，但是回调函数是在满足某个条件之后执行的）比如：我们之前学过的事件中的事件处理程序就是回调函数（在事件触发之后执行）element.onclick=function(){}
  - 第二个参数：延迟的时间（毫秒数），该参数不写默认为0
- **案例**：打开页面5秒后关闭广告

```js
     var timer1 = setTimeout(function(){
        var img = document.querySelector('.ad');
        img.style.display = 'none';
      },5000)
```



##### 2. 停止延迟定时器 clearTimeout

- **描述**：清除延迟定时器，让延迟定时器的函数不再执行
- **语法**：
  - `window.clearTimeout(延迟定时器名称)`   (window可以省略)
  - `clearTimeout(延迟定时器名称)`
- **参数**：延迟定时器名称

```js
1. 创建一个按钮
2. 创建一个延迟定时器，在3s后打印'爆炸了'
3. 给按钮添加点击事件，在事件处理程序中，清除定时器
    var timer = setTimeout(function(){
      console.log('爆炸了');
    },3000)
    var btn = document.querySelector('button');
    btn.onclick = function(){
      clearTimeout(timer);
    }
```

#### 2.5.2  周期定时器（闹钟定时器） setInterval

##### 1. 创建周期定时器

- **描述**：**每**隔多少毫秒之后就执行一次某个函数（**多次性**）

- **语法**：

  - `window.setInterVal(函数名/匿名函数,[间隔毫秒数]) ` (window可以省略)
  - `setInterVal(函数名/匿名函数,[间隔毫秒数]) `
  - 通常我们在使用定时器时，都会给定时器赋值一个标识符(名字)，用以区别多个定时器

- **参数**：

  - 第一个参数：要做的事情，也称回调函数
    - 回调函数：回头调用的函数（普通函数是一行一行从上往下读取执行的，但是回调函数是在满足某个条件之后执行的）比如：我们之前学过的事件中的事件处理程序就是回调函数（在事件触发之后执行）element.onclick=function(){}
  - 第二个参数：间隔的时间（毫秒数），该参数不写默认为0

  ```js
  1. 创建一个div元素，内容为10
  2. 创建一个全局变量var num = 10
  3. 每隔一秒让num-1,并将div的内容设置为num
      var num = 10;
      var timer = setInterval(function(){
        num--;
        if(num == 0){
          clearInterval(timer)
        }
        var div = document.querySelector('div');
        div.innerHTML = num;
      },1000)
  ```

- **案例**：钟表

```js
function time(){
    var date = new Date();
    var year = date.getFullYear();
    var month = date.getMonth()+1;
    var day = date.getDate();
    var hour = date.getHours()< 10 ? '0'+date.getHours():date.getHours();
    var min = date.getMinutes()<10 ? '0'+ date.getMinutes(): date.getMinutes();
    var sec = date.getSeconds()<10 ? '0'+ date.getSeconds(): date.getSeconds();
    return year + '-' + month + '-' +day +'  ' +hour+':'+min+':'+sec;
  }
  var div = document.querySelector('div');
  div.innerHTML = time();
  setInterval(function(){
    div.innerHTML = time();
  },1000)
```



##### 2. 停止周期定时器

- **描述**：清除周期定时器，让周期定时器的函数不再执行
- **语法**：
  - `window.clearInterval(周期定时器名称)`   (window可以省略)
  - `clearInterval(周期定时器名称)`
- **参数**：周期定时器名称

- **案例**：验证码获取倒计时

```js
    var btn = document.querySelector('.btn');
    btn.onclick = function(){
      btn.disabled = true; 
      var num = 5;
      btn.value = '获取验证码('+num+')';
      var timer = setInterval(function(){
        num--;
        btn.value = '获取验证码('+num+')';
        if(num == 0){
           clearInterval(timer);
           btn.value = '获取验证码';
           btn.disabled = false;
        }
      },1000)

    }  
```


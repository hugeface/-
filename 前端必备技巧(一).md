# 页面布局

### 题目
假设高度已知，请写出三栏布局，其中左栏、右栏宽度各为300px，中间自适应

### 五种方法

- 浮动布局
    优势：兼容性比较好
    劣势：脱离文档流，需要清除浮动，并且注意浮动元素与其周围元素的关系

- 绝对布局
    优势：快捷
    劣势：布局脱离文档流，意味着子元素都脱离了文档流，有效性差

- flexbox布局
    优势：比较完美
    劣势：IE8不支持

- 表格布局
    优势：兼容性好
    劣势：无法灵活调整单元格高度，当某个单元格高度增高，其他元素也会随之增高

- 网格布局
    优势：代码量少
    劣势：兼容性

### 总结

- 语义化掌握到位
- 页面布局理解深刻
- CSS基础知识扎实
- 思维灵活（要掌握多种方案）且积极上进（最新的技术方案要掌握，对应该题为网格布局）
- 代码书写规范

### 作业

###### 三栏布局

- 左右宽度固定，中间自适应
- 上下高度固定，中间自适应

###### 两栏布局

- 左宽度固定，右自适应
- 右宽度固定，左自适应
- 上高度固定，下自适应
- 下高度固定，上自适应

# CSS盒模型

- 基本概念： 标准模型 + IE模型
    盒模型包括margin、padding、border、content

- 标准模型和IE模型的区别
    IE模型和标准模型的主要却别在于：IE模型的content是计算padding和border的，而标准模型并不包括两者

- CSS如何设置这两种模型
```less
box-sizing: content-box // 标准模型(浏览器默认)
box-sizing: border-box  //IE模型
```

- JS如何设置获取盒模型对应的宽和高
    1. dom.style.width/height
    2. dom.currentStyle.width/height
    3. window.getComputedStyle(dom).width/height
    4. dom.getBoundingClientRect().width/height

- 实例题（根据盒模型解释边距重叠）
    两个或多个块级盒子的垂直相邻边界会重合。结果的边界宽度是相邻边界宽度中最大的值。如果出现负边界，则在最大的正边界中减去绝对值最大的负边界。如果没有正边界，则从零中减去绝对值最大的负边界。

- BFC（块级格式化上下文-边距重叠解决方案）
    BFC就是页面上的一个隔离的独立容器，容器里面的子元素不会影响到外面的元素

# DOM事件

- 基本概念：DOM事件的级别
    1. DOM0
        element.onclick=function(){}
    2. DOM2
        element.addEventListener('click', function(){}, false)
    3. DOM3
        element.addEventListener('keyup', function(){}, false)

- DOM事件模型
    捕获和冒泡

- DOM事件流
    事件通过捕获到达目标元素，再通过冒泡上传到window对象
    捕获：window->document->html->body->target element
    冒泡：target element->body->html->document->window

- 描述DOM事件捕获的具体流程
    捕获：window->document->html(document.documentElement)->body(document.body)->target element

- Event对象的常见应用

- 自定义事件
    ```
    var eve = new Event('test');
    ev.addEventListener('test', function () {
        console.log('test dispatch');
    });
    ev.dispatchEvent(eve);
    ```

# 类型转换

最新ECMAScript标准定义了7种数据类型

原始类型：Boolean、Null、Undefined、Number、String、Symbol

对象：Object

### 显示类型转换

显示地调用Number函数、String函数、Boolean函数进行类型转换

#####  Number函数

- 原始类型转换
    数值：转换后还是原来的值
    字符串：如果可以被解析为数值，则转换为相应的数值，否则得到NaN；空字符串转为0
    布尔值：true转为1，false转为0
    undefined：转成NaN
    null：转成0

- 对象类型转换
    1. 调用对象自身的valueOf方法，如果该方法返回原始类型的值（数值、字符串和布尔值），则直接对该值使用Nember方法，不再进行后续步骤
    2. 如果valueOf方法返回复合类型的值，再调用对象自身的toString方法，如果toString方法返回原始类型的值，则对该值使用Number方法，不再进行后续步骤
    3. 如果toString方法返回的是符合类型的值，则报错

##### String函数

- 原始类型转换
    数值：转换为相应的字符串
    字符串：转换后还是原来的值
    布尔值：true转为“true”，false转为“false”
    undefined：转为“undefined”
    null：转为“null”

- 对象类型转换
    1. 调用toString方法，如果toString方法返回的是原始类型的值，则对该值使用String方法，不再进行以下步骤
    2. 如果toString方法返回的是符合类型的值，再调用valueOf方法，如果valueOf方法返回的是原始类型的值，则对该值使用String方法，不再进行以下步骤
    3. 如果valueOf方法返回的是复合类型的值，则报错

##### Boolean函数

undefined、null、-0、+0、NaN、‘’(空字符串) => false，其他都转为true

### 隐式类型转换

四则运算、判断语句、Native调用

1. -、 *、/ 和 % 等算术运算符都会把操作数转换成数字的，但是 + 不一样，有些情况下，它是算术加号，有些情况下，是字符串连接符号，具体的要看它的操作数
2. 字符串和数字相加结果是字符串
3. 一个对象同时存在valueOf方法和toString方法，那么，valueOf方法总是会被优先调用

### 常见题目

在加法运算中：{}可被不同浏览器解析成"[object Object]"字符串和代码块；[]被解析成空数组

- [] + [] = ""  
    ```
    // 转String
    [].toString() = "";    // OK，加号可以处理String
    [] + [] = "" + "" = "";
    
    // 等同于
    [] + [] = String([]) + String([]) = "" + "" = "";
    ```
- [] + {} = "[object Object]"  
    ```
    // 转String
    [].toString() = "";  // OK
    ({}).toString() = "[object Object]";    // OK
    [] + {} = "" + "[object Object]" = "[object Object]";
    
    // 等同于
    [] + {} = String([]) + String({}) = "" + "[object Object]" = "[object Object]";
    ```
- {} + [] = 0  
    ```
    // 此处在google浏览器中此处{}被解析成代码块，不执行，[]被解析成Number([])=0
    {} + [] = +[] = +Number([]) = +0 = 0;
    ```
- {} + {} = "[object Object][object Object]"  
    ```
    //google将两个{}解析成[object Object]
    {} + {} = "[object Object]"  + "[object Object]"  = "[object Object][object Object]";
    
    // fireFox将{}解析成代码块
    {} + {} = +{} = NaN;
    ```

- true + true = 2
- 1 + {a:1} = "1[object Object]"
    ```
    1 + {a:1} = 1 + String({a:1}) = 1 + "[object Object]"  = "1[object Object]"；
    ```

# HTTP协议

### HTTP协议的主要特点

简单快速、灵活、无连接、无状态

### HTTP报文的组成部分

请求报文：请求行，请求头，空行，请求体

响应报文：状态行，响应头，空行，响应体

### HTTP方法

- GET：获取资源
- POST：传输资源
- PUT：更新资源
- DELETE：删除资源
- HEAD：获得报文首部

### POST和GET的区别

- GET在浏览器回退时是无害的，而POST会再次提交请求
- GET产生的URL地址可以被收藏，而POST不可以
- GET请求会被浏览器主动缓存，而POST不会，除非手动设置
- GET请求只能进行url编码，而POST支持多种编码方式
- GET请求参数会被完整保留在浏览器历史记录里，而POST中的参数不会被保留
- GET请求在URL中传送的参数是有长度限制的，而POST没有限制
- 对参数的数据类型，GET只接受ASCII字符，而POST没有限制
- GET比POST更不安全，因为参数直接暴露在URL上，所以不能用来传递敏感信息
- GET参数通过URL传递，POST放在Request body中

### HTTP状态码

- 1xx：指示信息-表示请求已接收，继续处理
- 2xx：成功-表示请求已被成功接收
- 3xx：重定向-要完成请求必须进行更进一步的操作
- 4xx：客户端错误-请求有语法错误或请求无法实现
- 5xx：服务器错误-服务器未能实现合法的请求


- 200 OK：客户端请求成功
- 206 Partial Content：客户端发送了一个带有Range头的GET请求，服务器完成了它
- 301 Moved Permanently：所有请求的页面已经转移至新的url
- 302 Found：所请求的页面已经临时转移至新的url
- 304 Not Modified：客户端有缓冲的文档并发出了一个条件性的请求，服务器告诉客户，原来缓冲的文档还可以继续使用
- 400 Bad Request：客户端请求有语法错误，并不能被服务器所理解
- 401 Unauthorized：请求未经授权，这个状态码必须和WWW-Authenticate报头域一起使用
- 403 Forbidden：对被请求页面的访问被禁止
- 404 Not Found：请求资源部存在
- 500 Internal Server Error：服务器发生不可预期的错误原来缓冲的文档还可以继续使用
- 503 Server Unavailable：请求未完成，服务器临时过载或当机，一段时间后可能恢复正常

### 持久连接

HTTP协议采用"请求-应答"模式，当使用普通模式，即非Keep-Alive模式时，每个请求/应答客户端和服务器都要建立一个连接，完成之后立即断开连接（HTTP协议为无连接协议）

当使用Keep-Alive模式（又称持久连接、连接重用）时，Keep-Alive功能使客户端到服务器端的连接持续有效，当出现对服务器的后继请求时，Keep-Alive功能避免了建立或者重现建立连接

### 管线化

在使用持久连接的情况下，某个连接上消息的传递类似于：

> 请求1 -> 响应1 -> 请求2 -> 响应2 -> 请求3 -> 响应3

在使用管线化时，某个连接上的消息类似于：

> 请求1 -> 请求2 -> 请求3 -> 响应1 -> 响应2 -> 响应3

- 管线化机制通过持久连接完成，仅HTTP/1.1支持此技术
- 只有GET和HEAD请求可以进行管线化，而POST则有所限制
- 初次建立连接时不应启动管线机制，因为对方（服务器）不一定支持HTTP/1.1版本的协议
- 管线化不会影响响应到来的顺序，如上面的例子所示，响应返回的顺序并未改变
- HTTP/1.1要求服务器端支持管线化，但并不要求服务器端也对响应进行管线化处理，只是要求对于管线化的请求不失败即可
- 由于上面提到的服务器端问题，开启管线化很可能并不会带来大幅的性能提升，而且很多服务器端和代理程序对管线化的支持并不友好，因此现代浏览器如Chrome和Firefox默认并未开启管线化支持

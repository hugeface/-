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

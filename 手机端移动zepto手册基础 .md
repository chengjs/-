# 一、文档加载
**方法一：** 
```javascript
 Zepto(function($){ 
    //当文档内容的加载后。相当于jQuery里面的$(function ($) {})
 })
```

方法二： 

ready(function($){ 
    //添加一个事件侦听器，当页面dom加载完毕 “DOMContentLoaded” 事件触发时触发。建议使用 $()来代替这种用法。
})
方法三（推荐使用这个）： 
$(function () {
    ///当文档内容的加载后
})
注意：通过执行css选择器包装dom节点，创建元素或者从一个html片段来创建一个Zepto对象。

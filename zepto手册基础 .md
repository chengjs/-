中文官网：[http://www.wenshuai.cn/Manual/Zepto/](http://www.wenshuai.cn/Manual/Zepto/)

源码：[https://github.com/madrobby/zepto/](https://github.com/madrobby/zepto/blob/master/src/zepto.js)
**如果你会jQuery的话，那么你就会zepto.js**
# 一、文档加载
**方法一：** 
```javascript
 Zepto(function($){ 
    //当文档内容的加载后。相当于jQuery里面的$(function () {})
 })
```

方法二： 
```javascript
ready(function($){ 
    //添加一个事件侦听器，当页面dom加载完毕 “DOMContentLoaded” 事件触发时触发。建议使用 $()来代替这种用法。
})
```
方法三（推荐使用这个）： 
```javascript
$(function () {
    ///当文档内容的加载后
})
注意：通过执行css选择器包装dom节点，创建元素或者从一个html片段来创建一个Zepto对象。
```
# 二、操作的方法及属性
> ### 下面是创建节点

**方法一：**
```javascript
var a = $('<p class="box">zepto.js</p>');
$('body').append(a);
```
**方法二：**
```javascript
var a = $('<p/>',{ text:'zepoto.js', id:'box', css:{ color:'red'} })
//               对象   属性    值          属性 值   属性  值
//可以通过一个html字符串片段来创建一个dom节点。也可以通过给定一组属性映射来创建节点。最快的创建但元素，使用<div> 或 <div/>形式。
```

## 节点操作

1、append() 将某个元素插入到元素的末尾； 比如：

``` javascript
$('div').append('<span>节点插入</span>');  //解释：将后面的节点插入到div里面
```
#### 2、appendTo()  和上面的是一样的。将某个元素插入到元素的末尾，比如：
``` javascript
var pObj = $('<p/>',{ text:'zepoto.js', id:'box', css:{ color:'red'} })
pObj.appendTo($('div'));
```
#### 3、prepend() //将参数内容插入到每个匹配元素的前面（元素内部），比如：
``` javascript
$('ul').prepend('<li>first list item</li>')
```
#### 4、prependTo() //将所有元素插入到目标前面（元素内）。 
``` javascript
$('<li>first list item</li>').prependTo('ul')
```
#### 5、parent()  //获取Zepto对象集合中每个元素的直接父元素。如果css选择器参数给出。过滤出符合条件的元素。
``` javascript
$('div').parent().addClass('no1');
```
#### 6、parents()  //获取Zepto对象集合每个元素所有的祖先元素。如果css选择器参数给出，过滤出符合条件的元素。
``` javascript
$('div').parents().addClass('no1');
```
#### 7、next()    //获取Zepto对象集合中每一个元素的下一个兄弟节点(可以选择性的带上过滤选择器)。
``` javascript
$('div').next().addClass('no1');
```
####  8、prev()  //获取Zepto对象集合中每一个元素的前一个兄弟节点，通过选择器来进行过滤。
``` javascript
$('div').prev().css({'background':teal,'height':'300px'});
```
#### 9、remove()  //移出当前Zepto对象中的元素。有效的从dom中移除。
``` javascript
$('div').remove()
```
#### 10、before() //在匹配每个元素的前面（外面）插入内容。内容可以为html字符串，dom节点，或者节点组成的数组。
``` javascript
$('table').before('<p>See the following table:</p>')
```
#### 11、after() //在每个匹配的元素后插入内容。内容可以为html字符串，dom节点，或者节点组成的数组。
``` javascript
$('form label').after('<p>A note below the label</p>')
```
#### 12、children() //这个可以获取多个对象，并且以数组的方式存储，能够将对应对象的id与class类名存在数组内。官方：获得每个匹配元素集合元素的直接子元素，如果selector存在，只返回符合css选择器的元素。比如：多个li。然后给height还有宽。
``` javascript
$('ol').children('*:nth-child(2n)').css('background','red');
```
12.1、上面的第二个方法就是获取多个子元素：
``` javascript
$('ol').children().length; //也是可以获取到的。
```
12.2、可以给子元素筛选出来：
``` javascript
$('ol').children('.no1').css('background','red')
```
#### 13、prop()  //读取或设置dom元素的属性值。它在读取属性值的情况下优先于 attr，因为这些属性值会因为用户的交互发生改变，如checked and selected。下面是例子：
``` html
<input class="taiyang" id="check1" type="checkbox" checked="checked">
<input class="yaotaiyang" id="check2" type="checkbox">
```
``` javascript
<script type="text/javascript">
	$("#check1").attr("checked"); //=> "checked"
	$("#check1").prop("checked"); //=> "true"
	$("#check2").attr("checked"); //=> "false"
	$("#check2").prop("checked"); //=> "false"
	$("input[type='checkbox']").prop("type",function(index,oldvalue){
		console.log(index+"|"+oldvalue);
	});
	//=> 0|checkbox//=> 1|checkbox
	$("input[type='checkbox']").prop("className",function(index,oldvalue){
		console.log(index+"|"+oldvalue);
	});
	//=> 0|taiyang//=> 1|yaotaiyang
</script>
```
#### 14、closest()//从元素本身开始，逐级向上级元素匹配，并返回最先匹配selector的祖先元素。如果context节点参数存在。那么直考虑该节点的后代。这个方法与 parents(selector)有点相像，但他只返回最先匹配的祖先元素。如果参数是一个Zepto对象集合或者一个元素，结果必须匹配给定的元素而不是选择器。

#### 15、contents() //获得每个匹配元素集合元素的子元素，包括文字和注释节点。.contents()和.children()方法类似，只不过前者包括文本节点以及jQuery对象中产生的HTML元素。

#### 16、empty() //从Zepto对象集合中移除所有的dom子节点(**注意找回来的节点，是会把事件也会带回来的**)。比如：
```html
<button>单击找回</button>
<!-- ol下面有多个li，然后给上单击事件， -->
<ol>
    <li>1</li>
    <li>2</li>
    <li>3</li>
    <li>4</li>
</ol>
``` 
``` javascript
//单击事件
$('li').click(function () {
 alert('yyyy')
});
var li = $('ol li'); 
$('ol').empty();
//单击找回
$('button').click(function(){
    li.appendTo('ol')；
});
//注意：当节点删除找回后，事件也会有。
```
- ## 样式操作及选择器
1、css //给样式
2、removeAttr(自定义属性) //移动当前Zepto对象集合中所有元素的指定属性（可以移除多个）。比如：
```html
<div class="no1"><div>
```
```javascript
$('div').removeAtter('class');
```
3、eq() //从当前Zepto对象集合中获取给定索引号的元素（如果给负数的话，是从倒数第几个往后面数）。比如：
```html
<ol>
<li>1</li>
<li>2</li>
<li>3</li>
<li>4</li>
<ol>
```
```javascript
$('li').eq(-1).css('b ackground','teal'); //给负数的话，是给倒数第几个。
//下面是选着
$('li').eq(2).css('b ackground','teal')； //选着第一个。
```
4、filter() //过滤Zepto集合对象，返回的Zepto集合对象里面的项满足参数中的css选择器。如果参数为一个函数，函数返回有实际值得时候，元素才会被返回。在函数中， this 关键字指向当前的元素。
**例子1：**
```html
<ol>
<li class="no1">1</li>
<li>2</li>
<li class="no1">3</li>
<li>3</li>
<li>4</li>
</ol>
```
```javascript
$('li').filter('.no1').css('background','red'); 
```
**例子2：**
```javascript
$('li').filter(function (index) {
 alert(this) //alert(index);
}) 
//前面弹出this指向谁。然后弹出传参的是什么鬼。你可以试试
```
5、not() //过滤当前Zepto对象集合，获取一个新的Zepto对象集合，它里面的元素不能匹配css选择器（与上面是反过来的，选中的元素不变，其他的变化）。如果另一个参数为Zepto集合对象，那么返回的新Zepto对象中的元素都不包含在该参数对象中。如果参数是一个函数。仅仅包含函数执行为false值得时候的元素，函数的 this 关键字指向当前循环元素。
6、pluck()  //获取Zepto对象集合中每一个元素的属性值。返回值为 null或undefined值得过滤掉。
**这是一个Zepto的方法，不是jquery的api。**
===========什么意思 ===========
7、attr() //读取或设置dom的属性。如果没有给定value参数，则读取Zepto对象第集合一个元素的属性值。当给定了value参数。则设置Zepto对象集合中所有元素所有元素的属性值。当value参数为null，那么这个属性将被移除(类似removeAttr)，多个属性能以通过对象值对的方式进行设置。
要读取dom的属性如 checked和selected, 使用 prop。
**例子一：**
```javascript
$('div').attr('class','no1');
//给div来个定义属性。名字叫class，值为no1
```
**例子二：**
```html
<ol>
<li>1<li>
<li>2<li>
<li name="box">3<li>
<li>4<li>
</ol>
```
```javascript
$('li').attr('name',function (index,oldValue) {
 alert(index)
 //alert(oldValue)
 }) 
//弹出index是每个li的索引值，而弹出oldValue是自定义属性的值
```
**例子三：**
```javascript
//（可以设置多个属性和值）：多个li
$('li').attr({'class':'box','data-src':'img/1.jpg'})
```
8、first() 获取当前Zepto对象集合中的第一个元素。
```javascript
$('div').first().css('background','red');
```
9、get() 从当前Zepto对象集合中获取所有元素或单个元素。当index参数不存在的时候，以普通数组的方式返回所有的元素。当指定index时，只返回该置的元素。这点与与eq不同，该方法返回的不是Zepto集合对象。
10、has()  判断当前Zepto对象集合的子元素是否有符合选择器的元素，或者是否包含指定的dom节点，如果有，则返回新的Zepto集合对象，该对象过滤掉不含有选择器匹配元素或者不含有指定dom节点的对象。
**例子一：**
```javascript
$('ol > li').has('a[href]').css('background','red');
//选着li里面子元素，只有a是有href的
```
**例子二：**
```javascript
$('ol').has('span').css('background','red');
```

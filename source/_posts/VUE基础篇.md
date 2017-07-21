---
layout: w
title: VUE基础篇
date: 2017-07-20 16:16:57
tags: 

- javascript
- vue


categories: 

- web前端 
---


**前言**

话不多说，希望大家可以学到更多！

> ### .  [Vue.js API(英文)](https://vuejs.org/v2/api/)
> ### .  [Vue.js API(中文)](https://vuefe.cn/v2/guide/)
> ### .  [Vue.js 开源网站](https://github.com/vuejs/vue)
> ### .  [在线编辑器](https://jsfiddle.net/chrisvfritz/50wL7mdz/)



# 一、Vue基础介绍

Vue.js 是什么
Vue.js是当下很火的一个JavaScript MVVM库，它是以数据驱动和组件化的思想构建的。相比于Angular.js，Vue.js提供了更加简洁、更易于理解的API，使得我们能够快速地上手并使用Vue.js。

如果你之前已经习惯了用jQuery操作DOM，学习Vue.js时请先抛开手动操作DOM的思维，因为Vue.js是数据驱动的，你无需手动操作DOM。它通过一些特殊的HTML语法，将DOM和数据绑定起来。一旦你创建了绑定，DOM将和数据保持同步，每当变更了数据，DOM也会相应地更新。

当然了，在使用Vue.js时，你也可以结合其他库一起使用，比如jQuery




# 二、vue和其他MVVM大比拼

关于MVVM，目前市面上比较火的MVVM框架也是一抓一大把，比如常见的有Knockout.js、Vue.js、[AvalonJS](https://github.com/RubyLouvre/avalon)、[Angularjs](https://angularjs.org/)等，每一款都有它们自己的优势。

*   Knockout：微软出品，可以说是MVVM的模型领域内的先驱，使用函数偷龙转凤，最短编辑长度算法实现DOM的同步，兼容IE6，实现高超，但源码极其难读，最近几年发展缓慢。
*   Vue：是最近几年出来的一个开源Javascript框架，语法精简，实现精致，但对浏览器的支持受限，最低只能支持IE9。
*   AvalonJS：是一个简单易用迷你的MVVM框架，由大神司徒正美研发。使用简单，实现明快。
*   React：React并不属于MVVM架构，但是它带来virtual dom的革命性概念，受限于视图的规模。
*   Angularjs：Google出品，已经被用于Google的多款产品当中。AngularJS有着诸多特性，最为核心的是：MVC、模块化、自动化双向数据绑定、语义化标签、依赖注入等等。入门容易上手难，大量避不开的概念也是很头疼的。

更多MVVM框架优缺点比较，可以看下 [这里](https://vuefe.cn/guide/comparison.html) 。





# 三、Vue基础入门



## 1、MVVM图例

说到MVVM，先来看看下面下面这张图

![](http://images2015.cnblogs.com/blog/459756/201611/459756-20161113194248577-1540305634.png)

这张图足以说明MVVM的核心功能，在这三者里面，ViewModel无疑起着重要的桥梁作用。

*   **一方面，通过ViewModel将Model的数据绑定到View的Dom元素上面，当Model里面的数据发生变化的时候，通过ViewModel里面数据绑定的机制，触发View里面Dom元素的变化；**
*   **另一方面，又通过ViewModel来监听View里面的Dom元素的数据变化，当页面上面的Dom元素发生变化的时候，ViewModel通过Dom树的监听机制，触发对应的Model的数据变化。**

当然在Vue.js里面ViewModel也是核心部件，它就是一个Vue实例。这个实例作用于单个或者多个html元素，从而实现Dom树监听和数据绑定的双向更新操作。


## 2、第一个Vue实例

关于第一个实例，无疑是最简单的应用。要使用vue，不用多说，肯定是先去github上面下载源码喽，然后引入到我们的项目中来，需要引用的js就一个vue.js，版本是2.0.5。

![](http://images2015.cnblogs.com/blog/459756/201611/459756-20161113210624452-1027999713.png)

先来看一个最简单的例子：


```
<body>
    <div id="app">
        <h1>姓名：{{ Name }}</h1>
        <h1>年龄：{{ Age }}</h1>
        <h1>学校：{{ School }}</h1>
    </div>

    <script src="Content/vue/dist/vue.js"></script>
    <script type="text/javascript">
    //Model
    var data = {
        Name: '小明',
        Age: 18,
        School:'光明小学',
    }

    //ViewModel
    var vue = new Vue({
        el: '#app',
        data: data,
    });
   
    </script>
</body>
```


这段代码不难理解，我们的Model就是data变量，而ViewModel就是这里的new Vue()得到的对象。这里两个最简单的属性相信大家一看就能明白。

*   el：表示绑定的Dom元素，此例子中表示的是父级的Dom元素。
*   data：需要绑定的数据Model。

如果仅仅是展示，只需要 <span class="cnblogs_code">姓名：{{ Name }}</span> 这样写就好了。运行的效果如下：

![](http://images2015.cnblogs.com/blog/459756/201611/459756-20161113204618702-2059130554.png)

值得一提的是 <span class="cnblogs_code">{{ Name }}</span> 这种写法仅仅只能实现单向绑定，只有在Model里面数据发生变化的时候会触发界面Dom元素的变化，反之并不能触发Model数据的变化。可以通过浏览器的Console来验证这一理论。

![](http://images2015.cnblogs.com/blog/459756/201611/459756-20161114101817420-1132976771.gif)

那么，对于双向绑定的机制，Vue是如何实现的呢？



## 3、双向绑定

vue里面提供了v-model指令，为我们方便实现Model和View的双向绑定，使用也非常简单。还是上文的例子，我们加入一个文本框，里面使用v-model指令。


```
<body>
    <div id="app">
        <h1>编辑姓名：<input type="text" v-model="Name" /></h1>
        <h1>姓名：{{ Name }}</h1>
        <h1>年龄：{{ Age }}</h1>
        <h1>学校：{{ School }}</h1>
    </div>

    <script src="Content/vue/dist/vue.js"></script>
    <script type="text/javascript">
    //Model
    var data = {
        Name: '小明',
        Age: 18,
        School:'光明小学',
    }

    //ViewModel
    var vue = new Vue({
        el: '#app',
        data: data,
    });
    </script>
</body>
```

得到效果：

![](http://images2015.cnblogs.com/blog/459756/201611/459756-20161114103414545-284342155.gif)

双向绑定效果展示：

![](http://images2015.cnblogs.com/blog/459756/201611/459756-20161114103738810-574896604.gif)

通过v-model指令，很方便的实现了Model和View之间的双向绑定。单从这种绑定的方式来看，还是比Knockout要简单一点，至少不用区分什么普通属性和监控属性。

<div style="text-align: right">[回到顶部](#_labelTop)<a name="_label3"></a></div>

# 四、常用指令

本来按照Vue文档说明，常用指令应该是放在后面介绍的，但是从使用的层面考虑，先介绍常用指令还是非常必要的，因为博主觉得这些指令是我们入手使用Vue的桥梁，没有这些基石，一切的高级应用都是空话。

Vue里面为我们提供的常用指令主要有以下一些。

*   [v-text](https://vuefe.cn/api/#v-text)
*   [v-html](https://vuefe.cn/api/#v-html)
*   [v-if](https://vuefe.cn/api/#v-if)
*   [v-show](https://vuefe.cn/api/#v-show)
*   [v-else](https://vuefe.cn/api/#v-else)
*   [v-for](https://vuefe.cn/api/#v-for)
*   [v-on](https://vuefe.cn/api/#v-on)
*   [v-bind](https://vuefe.cn/api/#v-bind)
*   [v-model](https://vuefe.cn/api/#v-model)
*   [v-pre](https://vuefe.cn/api/#v-pre)
*   [v-cloak](https://vuefe.cn/api/#v-cloak)
*   [v-once](https://vuefe.cn/api/#v-once)

每一个指令都可以链接到相关文档，博主觉得文档里面每种指令的语法写得非常详细，在此就没必要重复做说明了，下面博主打算将一些常用的指令以分组的形式分别结合demo来进行解释说明。



## 1、v-text、v-html指令

v-text、v-html这两者分为一组很好理解，一个用于绑定文本，一个用于绑定html。上文使用到的 <span class="cnblogs_code">{{ Name }}</span>这种写法就是v-text的的缩写形式。这个很简单，没什么好纠结的，看一个Demo就能明白。


```
<body>
    <div id="app">
        <h1>姓名：<label v-text="Name"></label></h1>
        <h1>姓名：{{ Name }}</h1>
        <div style="font-size:30px;font-weight:bold;" v-html="Age">年龄：</div>
    </div>

    <script src="Content/vue/dist/vue.js"></script>
    <script type="text/javascript">
    //Model
    var data = {
        Name: '小明',
        Age: "<label>20</label>",
        School:'光明小学',
    }

    //ViewModel
    var vue = new Vue({
        el: '#app',
        data: data,
    });
    </script>
</body>
```


效果如下：

![](http://images2015.cnblogs.com/blog/459756/201611/459756-20161114115449654-1270095991.png)

代码说明：

1.  {{Name}}这种写法和v-text的作用是相同的，用于绑定标签的text属性。注意如果标签没有text属性，该绑定会失效，比如你在一个文本框上面使用v-text是没有效果的
2.  由得到的效果可以看出，v-html绑定后会覆盖原来标签里面的内容（比如上面的“年龄：”），记住此处是覆盖而非append。
3.  对于v-html应用的时候要慎重，在网站上动态渲染任意 HTML 有一定的危险存在，因为容易导致 [XSS 跨站脚本攻击](https://en.wikipedia.org/wiki/Cross-site_scripting)。所以最好是在信任的网址上面使用。
4.  注意v-text和v-html绑定都是单向的，只能从Model到View的绑定，不能实现View到Model的更新。


## 2、v-model指令

v-model上面有介绍它的双向绑定功能，对于v-model指令，vue限定只能对表单控件进行绑定，常见的有`<input>、``<select>、``<textarea>等。`


```
<body>
    <div id="app">
        <h2>编辑姓名：<input type="text" v-model="Name" /></h2>
        <h2>姓名：{{Name}}</h2>
        <hr />
        <h2>编辑备注：<textarea v-model="Remark"></textarea></h2>
        <h2>备注：{{Remark}}</h2>
        <hr />

        <input type="checkbox" id="basketball" value="篮球" v-model="Hobby">
        <label for="basketball">篮球</label>
        <input type="checkbox" id="football" value="足球" v-model="Hobby">
        <label for="football">足球</label>
        <input type="checkbox" id="running" value="跑步" v-model="Hobby">
        <label for="running">跑步</label>
        <br>
        <h2>学生爱好： {{ Hobby }}</h2>

        <hr />
        <h2>户籍：{{ Huji }}</h2>
        <select style="width:100px;" class="form-control" v-model="Huji">
            <option>湖南</option>
            <option>广东</option>
            <option>北京</option>
        </select>
        
</div>

    <script src="Content/vue/dist/vue.js"></script>
    <script type="text/javascript">
    //Model
    var data = {
        Name: '小明',
        Age: 18,
        School: '光明小学',
        Hobby: [],
        Remark: '三好学生',
        Huji:""
    }

    //ViewModel
    var vue = new Vue({
        el: '#app',
        data: data,
    });
    </script>
</body>
```

以上列举了v-model的一些常见用法，应该都不难，基本都是双向绑定，效果如下：

![](http://images2015.cnblogs.com/blog/459756/201611/459756-20161114151246076-1082399133.gif)

关于selece的数据源的动态绑定，我们留在v-for指令的时候介绍。



## 3、v-if、v-else指令

 v-if和v-else是一对离不开的好兄弟，使用条件运算符判断时常用。**需要说明的是，v-if可以单独使用，但是v-else的前面必须要有一个v-if的条件或者v-show指令（后面介绍）**，这个和我们编程的原理是一样一样的。

它们作为条件渲染指令，他们的基础语法如下：

```
<body>
    <div id="app">
        <h1>姓名：<label v-text="Name"></label></h1>
        <h1>是否已婚：<span v-if="IsMarry">是</span></h1>
        <h1>大人or小孩：<span v-if="Age>18">大人</span><span v-else>小屁孩</span></h1>
        <h1>学校：{{ School }}</h1>
    </div>

    <script src="Content/vue/dist/vue.js"></script>
    <script type="text/javascript">
    //Model
    var data = {
        Name: '小明',
        IsMarry: true,
        Age: 20,
        School:'光明小学',
    }

    //ViewModel
    var vue = new Vue({
        el: '#app',
        data: data,
    });
    </script>
</body>
```



得到结果：

![](http://images2015.cnblogs.com/blog/459756/201611/459756-20161114153343576-151718156.png)

只有有一点编程基础，上述应该不难看懂。

<div style="text-align: right;">[回到顶部](#_labelTop)<a name="_label3_3"></a></div>

## 4、v-show指令

v-show指令表示根据表达式之bool值，觉得是否显示该元素。需要说明的是，如果bool值false，对应的Dom标签还是会渲染到页面上面，只是将该标签的css属性display设为none而已。而如果你用v-if值，bool值为false的时候整个dom树都不被渲染到页面上面。从这点上来说看，如果你的需求是需要经常切换元素的显示和隐藏，使用v-show效率更高，而如果你只做一次条件判断，使用v-if更加合适。

v-show还常和v-else一起使用，表示如果v-show条件满足，则显示当前标签，否则显示v-else标签。


```
<body>
    <div id="app">
        <h1>姓名：<label v-text="Name"></label></h1>
        <h1>是否已婚：<span v-show="IsMarry">是</span></h1>
        <h1>学校：{{ School }}</h1>
    </div>

    <script src="Content/vue/dist/vue.js"></script>
    <script type="text/javascript">
    //Model
    var data = {
        Name: '小明',
        IsMarry: false,
        Age: 16,
        School:'光明小学',
    }

    //ViewModel
    var vue = new Vue({
        el: '#app',
        data: data,
    });
    </script>
</body>
```


得到效果：

![](http://images2015.cnblogs.com/blog/459756/201611/459756-20161114155134888-858138586.png)

<div style="text-align: right;">[回到顶部](#_labelTop)<a name="_label3_4"></a></div>

## 5、v-for指令

 `v-for` 指令需要以 `item in items` 形式的特殊语法。常用来绑定数据对象。

最简单的例子：


```
<body>
    <div id="app">
        <ul>
            <li v-for="value in nums">{{value}}</li>
        </ul>
    </div>

    <script src="Content/vue/dist/vue.js"></script>
    <script type="text/javascript">
    //ViewModel
    var vue = new Vue({
        el: '#app',
        data: {
            nums: [1, 2, 3, 4, 5, 6, 7, 8, 9]
        }
    });
    </script>
</body>
```




效果：

![](http://images2015.cnblogs.com/blog/459756/201611/459756-20161114165537029-868472103.png)

除了基础数据之外，还支持Json数组的绑定。比如：

```
<div id="app">
        <ul>
            <li v-for="value in values">姓名：{{value.Name}}，年龄：{{value.Age}}</li>
        </ul>
    </div>

    <script src="Content/vue/dist/vue.js"></script>
    <script type="text/javascript">
    //ViewModel
    var vue = new Vue({
        el: '#app',
        data: {
            values: [{ Name: "小明", Age: 20 }, { Name: "小刚", Age: 18 }, { Name: "小红", Age: 16 }]
        }
    });
    </script>
```



效果：

![](http://images2015.cnblogs.com/blog/459756/201611/459756-20161114165930795-783712142.png)

在v-for里面，可以使用`<template>` 标签来渲染多个元素块，下面就基于bootstrap样式使用v-for、v-if、v-else等实现一个简单的demo。

```
<div id="app">
        <nav>
            <ul class="pagination pagination-lg">
                <template v-for="page in pages ">
                    <li v-if="page==1" class="disabled"><a href="#">上一页</a></li>
                    <li v-if="page==1" class="active"><a href="#">{{page}}</a></li>
                    <li v-else><a href="#">{{page}}</a></li>
                    <li v-if="page==pages"><a href="#">下一页</a></li>
                </template>
            </ul>
        </nav>
    </div>

    <script src="Content/vue/dist/vue.js"></script>
    <script type="text/javascript">
    //ViewModel
    var vue = new Vue({
        el: '#app',
        data: {
            pages: 10
        }
    });
    </script>
```



得到效果

![](http://images2015.cnblogs.com/blog/459756/201611/459756-20161115093728076-324094916.png)

是不是很easy！需要说明一点的是，pages是10，然后遍历它的时候，page的值会从1依次到10。

v-for指令除了支持数据对象的迭代以外，还支持普通Json对象的迭代，比如：

```
<div id="app">
        <ul>
            <li v-for="(value, key)  in values">
                {{ key }} : {{ value }}
            </li>
            <li v-for="(value, key, index) in values">
                {{ index }}. {{ key }} : {{ value }}
            </li>
        </ul>
    </div>

    <script src="Content/vue/dist/vue.js"></script>
    <script type="text/javascript">
    //ViewModel
    var vue = new Vue({
        el: '#app',
        data: {
            values: { Name: "小明", Age: 20, School: "**高中" }
        }
    });
    </script>
```



得到效果：

![](http://images2015.cnblogs.com/blog/459756/201611/459756-20161114170903545-1554785575.png)

<div style="text-align: right;">[回到顶部](#_labelTop)<a name="_label3_5"></a></div>

## 6、v-once指令

v-once表示只渲染元素和组件一次。随后的重新渲染,元素/组件及其所有的子节点将被视为静态内容并跳过。什么意思呢？还是来看demo说话：

```
<div id="app">
        <h1>姓名：<label v-once v-text="Name"></label></h1>
        <h1 v-once>年龄：{{ Age }}</h1>
        <h1>学校：{{ School }}</h1>
    </div>

    <script src="Content/vue/dist/vue.js"></script>
    <script type="text/javascript">
    //Model
    var data = {
        Name: '小明',
        Age: 18,
        School:'光明小学',
    }

    //ViewModel
    var vue = new Vue({
        el: '#app',
        data: data,
    });
    </script>
```



效果动态图：

![](http://images2015.cnblogs.com/blog/459756/201611/459756-20161114172241076-46897422.gif)

可以看出，只要使用v-once指令的，View和Model之间除了初次渲染同步，之后便不再同步，而同一次绑定里面没使用v-once指令的还是会继续同步。

<div style="text-align: right;">[回到顶部](#_labelTop)<a name="_label3_6"></a></div>

## 7、v-bind指令

 对于html标签的text、value等属性，Vue里面提供了v-text、v-model去绑定。但是对于除此之外的其他属性呢，这就要用到接下来要讲的v-bind指令了。博主的理解是v-bind的作用是绑定除了text、value之外的其他html标签属性，常见的比如class、style、自定义标签的自定义属性等。它的语法如下：

```
<head>
    <meta http-equiv="Content-Type" content="text/html; charset=utf-8" />
    <title></title>
    <link href="Content/bootstrap/css/bootstrap.css" rel="stylesheet" />
    <style type="text/css">
        class1 {
            padding:20px;
        }
        .backred {
            background-color:red;
        }
    </style>
</head>
<body>
    <div id="app">
        <h1>姓名：<label v-text="Name"></label></h1>
        <h1>是否红领巾：<span class="class1" v-bind:class="{backred:IsBack}"><label v-if="IsBack">是</label></span></h1>
        <h1>学校星级：<span v-bind:style="{color:SchoolLevel}">aa</span></h1>
    </div>

    <script src="Content/vue/dist/vue.js"></script>
    <script type="text/javascript">
    //Model
    var data = {
        Name: '小明',
        Age: 18,
        School: '光明小学',
        SchoolLevel: 'red',
        IsBack:true
    }

    //ViewModel
    var vue = new Vue({
        el: '#app',
        data: data,
    });
    </script>
</body>
```



**需要说明的是同一个标签里面的同一个属性，可以既有绑定的写法，也有静态的写法，组件会自动帮你合并，比如上文中的class属性**。

得到效果如下：

![](http://images2015.cnblogs.com/blog/459756/201611/459756-20161115101646279-153825235.png)

关于自定义属性的绑定，打算在综合应用里面来说。



## 8、v-on指令

属性jquery的朋友应该很熟悉这个“on”，对于时间的监听和绑定，jquery里面最常用的就是on了。同样，在Vue里面，v-on指令用来绑定标签的事件，其语法和v-bind基本类似。

```
<div id="app">
        <h1>姓名：<label v-text="Name"></label></h1>
        <h1>年龄：{{ Age }}</h1>

        <button class="btn btn-primary" v-on:click="Age++;if(Name=='小明')Name='吉姆格林';else Name='小明';">年龄递增</button>
    </div>

    <script src="Content/vue/dist/vue.js"></script>
    <script type="text/javascript">
    //Model
    var data = {
        Name: '小明',
        Age: 18,
    }

    //ViewModel
    var vue = new Vue({
        el: '#app',
        data: data,
    });
    </script>
```


这段代码是一个最简单的应用，直接在click事件里面执行逻辑，改变变量的值。效果如下：

![](http://images2015.cnblogs.com/blog/459756/201611/459756-20161115103457842-1914428688.gif)

除了直接在标签内写处理逻辑，还可以定义方法事件处理器。

```
<div id="app">
        <h1>姓名：<label v-text="Name"></label></h1>
        <h1>年龄：{{ Age }}</h1>

        <button class="btn btn-primary" v-on:click="Hello">Hello</button>
    </div>

    <script src="Content/vue/dist/vue.js"></script>
    <script type="text/javascript">
    //Model
    var data = {
        Name: '小明',
        Age: 18,
    }

    //ViewModel
    var vue = new Vue({
        el: '#app',
        data: data,
        methods: {
            Hello: function (event) {
                // `this` 在方法里指当前 Vue 实例
                alert('Hello ' + this.Name + '!');
                this.Age++;
            }
        }
    });
    </script>
```



结果应该不难猜。

![](http://images2015.cnblogs.com/blog/459756/201611/459756-20161115104059513-533400322.gif)

<div style="text-align: right;">[回到顶部](#_labelTop)<a name="_label3_8"></a></div>

## 9、实例一：30分钟搞定增删改查

有了我们的Vue框架，关于行内编辑的增删改查，我们很简单即可实现，如果你熟的话应该还不用30分钟吧。代码如下：

```
<html xmlns="http://www.w3.org/1999/xhtml">
<head>
    <meta http-equiv="Content-Type" content="text/html; charset=utf-8" />
    <title></title>
    <link href="Content/bootstrap/css/bootstrap.css" rel="stylesheet" />
    <style type="text/css">
        table thead tr th {
            text-align:center;
        }
    </style>
</head>
<body>
    <div style="padding:20px;" id="app">
        <div class="panel panel-primary">
            <div class="panel-heading">用户管理</div>
            <table class="table table-bordered table-striped text-center">
                <thead>
                    <tr>
                        <th>用户名</th>
                        <th>年龄</th>
                        <th>毕业学校</th>
                        <th>备注</th>
                        <th>操作</th>
                    </tr>
                </thead>
                <tbody>
                    <template v-for="row in rows ">
                        <tr><td>{{row.Name}}</td><td>{{row.Age}}</td><td>{{row.School}}</td><td>{{row.Remark}}</td>
                        <td><a href="#" @click="Edit(row)">编辑</a>&nbsp;&nbsp;<a href="#" @click="Delete(row.Id)">删除</a></td>
                        </tr>
                    </template>
                    <tr>
                        <td><input type="text" class="form-control" v-model="rowtemplate.Name" /></td>
                        <td><input type="text" class="form-control" v-model="rowtemplate.Age" /></td>
                        <td><select class="form-control" v-model="rowtemplate.School">
   　　　　　　　　　　　　　　　　 <option>中山小学</option>
    　　　　　　　　　　　　　　　　<option>复兴中学</option>
    　　　　　　　　　　　　　　　　<option>光明小学</option>
　　　　　　　　　　　　　　　　</select></td>
                        <td><input type="text" class="form-control" v-model="rowtemplate.Remark" /></td>
                        <td><button type="button" class="btn btn-primary" v-on:click="Save">保存</button></td>
                    </tr>
                </tbody>
            </table>
        </div>
    </div>
    <script src="Content/jquery-1.9.1.min.js"></script>
    <script src="Content/vue/dist/vue.js"></script>
    <script type="text/javascript">
        //Model
        var data = {
            rows: [
            { Id: 1, Name: '小明', Age: 18, School: '光明小学', Remark: '三好学生' },
            { Id: 2, Name: '小刚', Age: 20, School: '复兴中学', Remark: '优秀班干部' },
            { Id: 3, Name: '吉姆格林', Age: 19, School: '光明小学', Remark: '吉姆做了汽车公司经理' },
            { Id: 4, Name: '李雷', Age: 25, School: '复兴中学', Remark: '不老实的家伙' },
            { Id: 5, Name: '韩梅梅', Age: 22, School: '光明小学', Remark: '在一起' },
            ],
            rowtemplate: { Id: 0, Name: '', Age: '', School: '', Remark: '' }
        };
    //ViewModel
    var vue = new Vue({
        el: '#app',
        data: data,
        methods: {
            Save: function (event) {
                if (this.rowtemplate.Id == 0) {
                    //设置当前新增行的Id
                    this.rowtemplate.Id = this.rows.length + 1;
                    this.rows.push(this.rowtemplate);
                }
                
                //还原模板
                this.rowtemplate = { Id: 0, Name: '', Age: '', School: '', Remark: '' }
            },
            Delete: function (id) {
                //实际项目中参数操作肯定会涉及到id去后台删除，这里只是展示，先这么处理。
                for (var i=0;i<this.rows.length;i++){
                    if (this.rows[i].Id == id) {
                        this.rows.splice(i, 1);
                        break;
                    }
                }
            },
            Edit: function (row) {
                this.rowtemplate = row;
            }
        }
    });
    </script>
</body>
</html>
```



行内编辑效果如下：

![](http://images2015.cnblogs.com/blog/459756/201611/459756-20161115134220795-584069517.gif)





## 10、实例二：带分页的表格

上面的例子用最简单的方式实现了一个增删改查，为了进一步体验我们Vue的神奇，博主更进了一步，用Vue去做了一个客户端分页的表格功能。其实代码量并不大。

```
<html xmlns="http://www.w3.org/1999/xhtml">
<head>
    <meta http-equiv="Content-Type" content="text/html; charset=utf-8" />
    <title></title>
    <link href="Content/bootstrap/css/bootstrap.css" rel="stylesheet" />
    <style type="text/css">
        table thead tr th {
            text-align: center;
        }
    </style>
</head>
<body>
    <div style="padding:20px;" id="app">
        <div class="panel panel-primary">
            <div class="panel-heading">用户管理</div>
            <table class="table table-bordered table-striped text-center">
                <thead>
                    <tr>
                        <th>用户名</th>
                        <th>年龄</th>
                        <th>毕业学校</th>
                        <th>备注</th>
                    </tr>
                </thead>
                <tbody>
                    <template v-for="(row, index) in rows ">
                        <tr v-if="index>=(curpage-1)*pagesize&&index<curpage*pagesize">
                            <td>{{row.Name}}</td>
                            <td>{{row.Age}}</td>
                            <td>{{row.School}}</td>
                            <td>{{row.Remark}}</td>
                        </tr>
                    </template>
                </tbody>
            </table>
        </div>
        <nav style="float:right;">
            <ul class="pagination pagination-lg">
                <template v-for="page in Math.ceil(rows.length/pagesize)">
                    <li v-on:click="PrePage()" id="prepage" v-if="page==1" class="disabled"><a href="#">上一页</a></li>
                    <li v-if="page==1" class="active" v-on:click="NumPage(page, $event)"><a href="#">{{page}}</a></li>
                    <li v-else v-on:click="NumPage(page, $event)"><a href="#">{{page}}</a></li>
                    <li id="nextpage" v-on:click="NextPage()" v-if="page==Math.ceil(rows.length/pagesize)"><a href="#">下一页</a></li>
                </template>
            </ul>
        </nav>
    </div>
    <script src="Content/jquery-1.9.1.min.js"></script>
    <script src="Content/vue/dist/vue.js"></script>
    <script type="text/javascript">
        //Model
        var data = {
            rows: [
            { Id: 1, Name: '小明', Age: 18, School: '光明小学', Remark: '三好学生' },
            { Id: 2, Name: '小刚', Age: 20, School: '复兴中学', Remark: '优秀班干部' },
            { Id: 3, Name: '吉姆格林', Age: 19, School: '光明小学', Remark: '吉姆做了汽车公司经理' },
            { Id: 4, Name: '李雷', Age: 25, School: '复兴中学', Remark: '不老实的家伙' },
            { Id: 5, Name: '韩梅梅', Age: 22, School: '光明小学', Remark: '在一起' },
            ],
            pagesize: 2,
            curpage:1,//当前页的页码
        };
    //ViewModel
    var vue = new Vue({
        el: '#app',
        data: data,
        methods: {
            //上一页方法
            PrePage: function (event) {
                $(".pagination .active").prev().trigger("click");
            },
            //下一页方法
            NextPage: function (event) {
                $(".pagination .active").next().trigger("click");
            },
            //点击页码的方法
            NumPage: function (num, event) {
                if (this.curpage == num) {
                    return;
                }
                this.curpage = num;
                $(".pagination li").removeClass("active");
                if (event.target.tagName.toUpperCase() == "LI") {
                    $(event.target).addClass("active");
                }
                else {
                    $(event.target).parent().addClass("active");
                }
                if (this.curpage == 1) {
                    $("#prepage").addClass("disabled");
                }
                else {
                    $("#prepage").removeClass("disabled");
                }
                if (this.curpage == Math.ceil(this.rows.length / this.pagesize)) {
                    $("#nextpage").addClass("disabled");
                }
                else {
                    $("#nextpage").removeClass("disabled");
                }
            }
        }
    });
    </script>
</body>
</html>
```


来看看效果吧：

![](http://images2015.cnblogs.com/blog/459756/201611/459756-20161115144239982-426306474.gif)

什么，数据少了不过瘾？那我们加一点数据试试呗。调整一下data变量，其他不用做任何变化。


```
var data = {
            rows: [
            { Id: 1, Name: '小明', Age: 18, School: '光明小学', Remark: '三好学生' },
            { Id: 2, Name: '小刚', Age: 20, School: '复兴中学', Remark: '优秀班干部' },
            { Id: 3, Name: '吉姆格林', Age: 19, School: '光明小学', Remark: '吉姆做了汽车公司经理' },
            { Id: 4, Name: '李雷', Age: 25, School: '复兴中学', Remark: '不老实的家伙' },
            { Id: 5, Name: '韩梅梅', Age: 22, School: '光明小学', Remark: '在一起' },
            { Id: 1, Name: '小明', Age: 18, School: '光明小学', Remark: '三好学生' },
            { Id: 2, Name: '小刚', Age: 20, School: '复兴中学', Remark: '优秀班干部' },
            { Id: 3, Name: '吉姆格林', Age: 19, School: '光明小学', Remark: '吉姆做了汽车公司经理' },
            { Id: 4, Name: '李雷', Age: 25, School: '复兴中学', Remark: '不老实的家伙' },
            { Id: 5, Name: '韩梅梅', Age: 22, School: '光明小学', Remark: '在一起' },
            { Id: 1, Name: '小明', Age: 18, School: '光明小学', Remark: '三好学生' },
            { Id: 2, Name: '小刚', Age: 20, School: '复兴中学', Remark: '优秀班干部' },
            { Id: 3, Name: '吉姆格林', Age: 19, School: '光明小学', Remark: '吉姆做了汽车公司经理' },
            { Id: 4, Name: '李雷', Age: 25, School: '复兴中学', Remark: '不老实的家伙' },
            { Id: 5, Name: '韩梅梅', Age: 22, School: '光明小学', Remark: '在一起' },
            { Id: 1, Name: '小明', Age: 18, School: '光明小学', Remark: '三好学生' },
            { Id: 2, Name: '小刚', Age: 20, School: '复兴中学', Remark: '优秀班干部' },
            { Id: 3, Name: '吉姆格林', Age: 19, School: '光明小学', Remark: '吉姆做了汽车公司经理' },
            { Id: 4, Name: '李雷', Age: 25, School: '复兴中学', Remark: '不老实的家伙' },
            { Id: 5, Name: '韩梅梅', Age: 22, School: '光明小学', Remark: '在一起' },
            ],
            pagesize: 6,
            curpage:1,//当前页的页码
        };
```

测试效果：

![](http://images2015.cnblogs.com/blog/459756/201611/459756-20161115144638373-2064246540.gif)

如果再进一步封装，是不是有点分页组件的概念了。简单吧！当然，这只是为了体现常用指令而提供的一个实现思路，可能很多地方都有待优化，待深入研究组件之后再进一步封装。



# 五、总结

以上学习了下Vue的一些常用指令，基本都是些比较常用的，等下篇有时间再来研究下它的一些高级功能。如果你也对它有兴趣，用起来试试吧！博主觉得它的文档还是挺全的。

如果你觉得本文能够帮助你，可以在下边随意 **打赏 **博主。你的支持是博主继续坚持的不懈动力。

内容参考：[原创](http://www.cnblogs.com/landeanfen/)


 

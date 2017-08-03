---
layout: w
title: Vue-7种定义组件模板的方法
date: 2017-07-15 11:16:57
tags: 

- javascript
- vue


categories: 

- web前端 
---

# Vue-7种定义组件模板的方法

vue中定义模板组7种不同的方法：

1.   字符串（String）

2.   模板字符串（Template literal）

3.   X-Templates

4.   内联（Inline）

5.  Render函数（Render functions）

6.  JSX

7.  单文件组件（Single page components）


在这篇文章里，我们将会展示每一个方法的示例，分析其优缺点，以便你能明白在特定的情形下，哪种方式是合适的。



## [](#1-strings) 1\. 字符串

默认情况下，<span style="font-size: 1rem;">在JS文件里</span>模板会被定义为一个字符串。但是我觉得大家都会同意这种写法很难看懂，它除了有广泛的浏览器支持之外，并没有什么优势。

```
Vue.component('my-checkbox', {
  template: '<div class="checkbox-wrapper" @click="check"><div :class="{ checkbox: true, checked: checked }"></div><div class="title">{{ title }}</div></div>',
  data() {
    return { checked: false, title: 'Check me' }
  },
  methods: {
    check() { this.checked = !this.checked; }
  }
});

```

## [](#2-template-literals) 2\. 模板字符串（Template literals）

通过ES6的模板字符串（反引号）语法，你在定义模板时可以直接换行，这是通过常规的JavaScript字符串没法做到的。
这种写法更容易阅读，并且这种模板字符串语法得到了许多新版本浏览器的支持。当然，为了安全起见，你仍然应该把它转译为ES5的语法形式。

然而，这种方式并不完美，我发现大多数的IDE在语法高亮上做的差强人意，并且在缩进和换行等的格式方面，仍然很痛苦。

```
Vue.component('my-checkbox', {
  template: `<div class="checkbox-wrapper" @click="check">
              <div :class="{ checkbox: true, checked: checked }"></div>
              <div class="title">{{ title }}</div>
            </div>`,
  data() {
    return { checked: false, title: 'Check me' }
  },
  methods: {
    check() { this.checked = !this.checked; }
  }
});

```

## [](#3-x-templates) 3\. X-Templates

使用这种方法，你需要在_index.html_文件里的script标签中定义你的模板。script标签需要添加`text/x-template`类型作为标记，并且在定义组件时，通过id来引用。

我喜欢这种方式，它允许你使用真正的HTML标记来书写你的HTML文件，但是不足之处在于，这种方式会把模板和组件其它部分的定义分开。

```
Vue.component('my-checkbox', {
  template: '#checkbox-template',
  data() {
    return { checked: false, title: 'Check me' }
  },
  methods: {
    check() { this.checked = !this.checked; }
  }
});

```

```
<script type="text/x-template" id="checkbox-template">
  <div class="checkbox-wrapper" @click="check">
    <div :class="{ checkbox: true, checked: checked }"></div>
    <div class="title">{{ title }}</div>
  </div>
</script>

```

## [](#4-inline-templates) 4\. 内联模板（Inline Templates）

通过给组件添加`inline-template`属性来告诉Vue，里面的内容就是模板，而不是把它当作是分发内容(见 [slots](https://vuejs.org/v2/guide/components.html#Content-Distribution-with-Slots))。

它的缺点和x-templates一样，但是有一个优点就是，它的内容就在HTML模板对应的位置，所以页面一加载就会渲染，而不用等到JavaScript执行。

```
Vue.component('my-checkbox', {
  data() {
    return { checked: false, title: 'Check me' }
  },
  methods: {
    check() { this.checked = !this.checked; }
  }
});

```

```
<my-checkbox inline-template>
  <div class="checkbox-wrapper" @click="check">
    <div :class="{ checkbox: true, checked: checked }"></div>
    <div class="title">{{ title }}</div>
  </div>
</my-checkbox>

```

## [](#5-render-functions) 5\. Render functions（渲染函数）

渲染函数需要你把模板当作一个JavaScript对象来进行定义，它们是一些复杂并且抽象的模板选项。

然而，它的优点是你定义的模板更接近编译器，你可以使用所有JavaScript方法，而不仅是指令提供的那些功能。

```
Vue.component('my-checkbox', {
  data() {
    return { checked: false, title: 'Check me' }
  },
  methods: {
    check() { this.checked = !this.checked; }
  },
  render(createElement) {
    return createElement(
      'div',
        {
          attrs: {
            'class': 'checkbox-wrapper'
          },
          on: {
            click: this.check
          }
        },
        [
          createElement(
            'div',
            {
              'class': {
                checkbox: true,
                checked: this.checked
              }
            }
          ),
          createElement(
            'div',
            {
              attrs: {
                'class': 'title'
              }
            },
            [ this.title ]
          )
        ]
    );
  }
});

```

## [](#6-jsx) 6\. JSX

Vue中最有争议性的模板选项就是JSX，一些开发者认为JSX语法太丑，不直观，而且和Vue的简洁特性背道而驰。

JSX需要事先编译，因为浏览器并不支持JSX。但是如果你需要使用渲染函数，那么JSX语法绝对是一种更简洁的定义模板的方法。

```
Vue.component('my-checkbox', {
  data() {
    return { checked: false, title: 'Check me' }
  },
  methods: {
    check() { this.checked = !this.checked; }
  },
  render() {
    return <div class="checkbox-wrapper" onClick={ this.check }>
             <div class={{ checkbox: true, checked: this.checked }}></div>
             <div class="title">{ this.title }</div>
           </div>
  }
});

```

## [](#7-single-file-components) 7\. 单文件组件（Single File Components）

只要你愿意在项目中使用构建工具，那么单文件组件绝对是这些方法中的首选。它们有两个最好的优点：允许你使用标记，同时把所有组件定义都写在一个文件中。

尽管单文件组件需要编译，并且一些IDE不支持这种类型文件的语法高亮，但它仍然很难被其它方法战胜。

```
<template>
  <div class="checkbox-wrapper" @click="check">
    <div :class="{ checkbox: true, checked: checked }"></div>
    <div class="title">{{ title }}</div>
  </div>
</template>
<script>
  export default {
    data() {
      return { checked: false, title: 'Check me' }
    },
    methods: {
      check() { this.checked = !this.checked; }
    }
  }
</script>

```



本文转载自：[众成翻译](http://www.zcfy.cc)



                
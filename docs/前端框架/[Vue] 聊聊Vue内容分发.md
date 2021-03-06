# 聊聊Vue内容分发.md

## 什么是内容分发？

简单来说，假如父组件需要在子组件内放一些DOM，那么这些`DOM`哪些显示、不显示，在何处显示、如何显示，就是通过`slot`分发实现。

## 起步

默认情况下，父组件在子组件内套的内容，是不显示的。[jsbin在线](http://jsbin.com/xacarey/edit?html,js,output)

```html
<div id="app">  
    <children>
        <!--然而你想要显示得子组件允许你显示才行，所以在子组件无任何设置前提下，这里不会显示-->
        <span>我想要在子组件中显示</span>  
    </children>  
</div> 
```

```js
 var vm = new Vue({  
        el: '#app',
        components: {  
            children: {  
                template: "<div>Children Template</div>"  
            }  
        }  
    });  
```

那么如何才能够显示呢？修改一下`children`的`template`如下：
```html
template: '<div><slot></slot>Children Template</div>'
```

最终渲染出来的结果将会是这样：

```html
<div><span>我想要在子组件中显示</span>Children Template</div>
```

## 具名slot

上述的例子中，我们在子组件中注入`<slot></slot>`非常轻松地实现了内容分发，但是，当我们需要指定分发内容的位置的时候，这种方式就显得无能为力了。此时，我们需要——`具名slot`。

来一个很直观例子：

```html
<div id="app">  
    <children>  
        <li slot="header">I am header</span>  
        <li slot="footer">I am footer</span>  
    </children>  
</div>  
```

```js
var vm = new Vue({  
        el: '#app',  
        components: {  
            children: {    
                template: 
                   "<ul>" +
                       "<slot name='header'></slot>" +
                       "<li>I am contet</li>" +
                       "<slot name='footer'></slot>" +
                    "</ul>"
            }  
        }  
    });  
```

最终，生成的html如下；

```html
<ul>
    <li>I am header</li>
    <li>I am contet</li>
    <li>I am footer</li>
</ul>
```

实际上，开源UI库`iview`在其`modal`中就用到了这种思路，可以设置默认的`header`和`footer`,但是用户又可以自定义。这样的功能，对于组件化编程来说，是不是如虎添翼？

## 对比AngularJS和React

- `ng1`的自定义指令中有一个`transclude`参数，可以实现类似的功能（但是本人亲测有作用域的坑）。
- React就更直观了，在子组件中可以通过`this.props.children`来访问父组件分发的内容。


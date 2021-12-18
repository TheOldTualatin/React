# React

React起源于Facebook内部项目，一开始用于假设instageam,在2012年5月开源，它是一个用于构建用户界面的JavaScript库,React拥有较高的性能，代码逻辑简单，所以越来越多的人开始关注和使用它。

## React特点:

1. 声明式设计：采用声明式设计，可以轻松描述应用。
2. 高效：React通过对DOM的模拟，最大限度的减少了与真实DOM的交互。
3. 灵活：React可以与已知的库或框架很好的配合。
4. JSX：JSX是一种JavaScript扩展语法。
5. 组件：通过React构建组件，使得代码容易得到复用，能够更好的应用在大型项目中。

# 虚拟DOM

浏览器在初始化时会载入一个HTML文档，当页面内容需要改变时，JavaScript会根据用户操作来创建或者删除节点或者是插入新元素，这让JavaScrpit管理DOM变得非常复杂而效率又低，这意味着开发人员要认真的了解如何修改UI的细节来优化程序。从编码角度来看，先将特定的元素清空然后重新构建他们，比保留原有的元素然后研究怎么跟新他们更容易一些。<font color = orange>React提出了虚拟DOM的概念，采用虚拟DOM之后，我们将不需要直接与DOM API直接交互，而是使用一组指令，让React和浏览器交互。虚拟DOM实际是javaScript对象，直接访问javaScript对象比直接与DOM交互效率高的多。</font>

# Hello React

使用React很简单，只需要在页面中引入React的依赖：

```javascript
//ReactUI库，用来创建视图
<script src="https://unpkg.com/react@17/umd/react.production.min.js" crossorigin></script>
//ReactDOM库，用于在浏览其中渲染UI
<script src="https://unpkg.com/react-dom@17/umd/react-dom.production.min.js" crossorigin></script>
//支持JSX语法
<script src="https://unpkg.com/babel-standalone@6/babel.min.js"></script>
```

现在然我们来创建第一个React页面：

1. 在页面中加入依赖
2. 在`<script>`中添加`Type=text/babel`使其支持JSX语法
3. 在HTML中准备一个容器，用于将我们用React创建的虚拟DOM添加进去
4. 创建一个虚拟DOM，将虚拟DOM放入容器中

在HTML中创建一个容器:这个稍后我们将会将虚拟DOM装入div中

```html
<div id="text"></div>
```

在JavaScript中添加以下代码：

```javascript
<script type="text/babel">
    //JSX
    const element = <h1>Hello,world!</h1>
    ReactDOM.render(
        element,
        document.querySelector("#text")
    );
</script>
```

于是我们便可以在网页中看到效果：

![image-20211212213433037](C:\Users\VanNess\AppData\Roaming\Typora\typora-user-images\image-20211212213433037.png)

`<h1>Hello,world!</h1>`就是JSX语法，JSX具有JavaScript的全部功能，它用于创建一个虚拟的DOM元素，然后使用`ReactDOM.render()`将这些元素渲染为DOM。

# JSX

Jsx是一种快速创建React虚拟节点的语法，我们先来看看不是用JSX创建React虚拟节点：

```react
//创建虚拟节点
const element1 = React.createElement("h1",null,"Baked Salmon");
//将节点渲染到DOM中
ReactDOM.render(
        element1,
        document.querySelector("#text")
    );
```

其中`React.createElement("h1",null,"Baked Salmon")`渲染到DOM后会变成`<h1>Baked Salmon<h1>`,如果要再标签中添加属性的话，只需要将`React.createElement()`的第二个参数传递一个对象即可：

```react
const element2 = React.createElement("h1",{className:"title",id:"recipe0"},"Baked Salmon");
```

class因为与JavaScript关键字重合故React中class使用className代替

很明显，以这种方式创建虚拟节点并不高效，如果需要多个节点嵌套将会非常麻烦，JSX语法将会高效得多，我们再来看看JSX定义同样一个虚拟节点：

```react
<script type="text/babel">
    const element1 = <h1>Baked Salmon</h1>;
    ReactDOM.render(
        element1,
        document.querySelector("#text")
    );
</script>
```

JSX语法与HTML语法非常类似，但是有几个需要注意的地方1.不需要使用引号，2.必须要有babel的支持。

## JSX小技巧

### 1.在JSX中嵌入JS表达式:

 我们是可以在JSX语法中嵌入JS变量的，只需要用`{}`包裹起来，支持运算、名称、对象。

```react
const name = "React";
const peple = {name:"zhangsan",age:"12"};
const element1 =
    <div>{name}
        <p>{2+2}</p>+
        <p>{peple.name},{peple.age}</p>
    </div>;
ReactDOM.render(
    element1,
    document.querySelector("#text")
);
```

在JSX中还支持函数表达式,下面例子中我们定义一个求和函数，接收两个参数，然后返回他们的和：

```react
 const sum = (a,b)=>a+b;
 const element1 =
     <div>{
         <p>{sum(1,2)}</p>
     </div>;
 ReactDOM.render(
     element1,
     document.querySelector("#text")
 );
```

### 2.用 JSX 指定属性值

你可以使用双引号来指定字符串字面量作为属性值：

```react
const element = <div tabIndex="0"></div>;
```

您也可以用花括号嵌入一个 JavaScript 表达式作为属性值:

```react
const element = <img src={user.avatarUrl}></img>;
```

## 渲染元素到DOM

我们知道，将React虚拟元素添加到DOM中需要一个容器，这个容器我们称这个是一个 “root” DOM 节点，因为该节点内的所有内容都由 React DOM 管理。

要渲染一个React元素到rootDome节点，把他们传递给ReactDOM.render()方法：

```react
const element = <h1>Hello, world</h1>;
ReactDOM.render(element, document.getElementById('root'));
```

React元素是不可变的，一旦你创建了一个元素，这个元素就不可更改了，一个元素就像是一个动画里的每一帧，它只表示再某一时间的特定状态。

现在我们所知的更新元素的唯一办法就是创建一个新元素，并将它传入`ReactDOM.render()`方法，他会将容器里的元素覆盖。

我们来写一个程序体验一下：

```react
const name = "React";
//时钟函数
const tick = ()=>{
    const element = (
        <div>
            It is {new Date().toString()} o‘clock.
        </div>
    )
    ReactDOM.render(element,document.querySelector("#text"))
};
//每隔一秒调用一次
setInterval(tick, 1000);
```

以上代码每隔1秒就会重新渲染一次元素。实际上大部分React应用只会调用一次`ReactDOM.render()`，这将会涉及到有状态和无状态组件，我们将在后面学习。
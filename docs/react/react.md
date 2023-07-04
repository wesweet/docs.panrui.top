<!--
 * @Description:
 * @Author: panrui
 * @Date: 2023-03-29 20:23:30
 * @LastEditTime: 2023-06-05 15:15:00
 * @LastEditors: panrui
 * 不忘初心,不负梦想
-->

## 文档 最后更新时间：2023-03-30 22-34-01

## 函数组件与 class 组件的区别

> 1.  语法：函数组件是一个函数，而 class 组件是一个 ES6 类。
> 2.  内部状态：函数组件没有内部状态，而 class 组件可以使用 state 来维护内部状态。
> 3.  this 关键字：在函数组件中，没有 this 关键字，而在 class 组件中，需要使用 this 关键字来访问组件的属性和方法。

## 跨组件通信

## react 的 hook

> 1.  [hook](https://react.docschina.org/reference/react/useCallback)

## react.memo()

React.memo()只会对 props 进行浅比较。如果 props 中包含了复杂的数据结构，比如对象或数组，那么 React.memo()可能会出现误判，导致组件不必要地重新渲染。如果你需要对复杂的数据结构进行比较，可以考虑使用自定义的 shouldComponentUpdate 函数或者使用 Immutable.js 等库来进行比较。

<!-- > 1. JSX 可以生成 React “元素”，react 将元素渲染为 DOM，jsx 中使用变量，用{}包裹起来，{}包裹任何 js 表达式。Babel 会把 JSX 转译成一个名为 React.createElement() 函数调用，实际上创建了一个对象，这个对象称为 react 元素

> 2. ReactDOM.render() 将一个 react 元素渲染进去 dom 节点，React 元素是不可变对象。

> 3. 接收唯一带有数据的 “props”（代表属性）对象与并返回一个 React 元素。这类组件被称为“函数组件”，因为它本质上就是 JavaScript 函数。

> 4. class 组件中，每次组件更新时 render 方法都会被调用，相同的 DOM 节点中渲染 <Clock /> ，就仅有一个 Clock 组件的 class 实例被创建使用

> 5. class 组件都包含构造函数 constructor，为数据初始化赋值，继承 super(props);

> 6.  使用 this.setState()来更新 state，this.setState()更新是异步的，不要依赖他们的值来更新下一个状态。最好的使用方式是让 setState() 接收一个函数而不是一个对象。这个函数用上一个 state 作为第一个参数，将此次更新被应用时的 props 做为第二个参数

> 7. React 事件的命名采用小驼峰式（camelCase），而不是纯小写，使用 JSX 语法时你需要传入一个函数作为事件处理函数，而不是一个字符串

> 8. class 中的方法不会默认绑定 this，事件传递参数。

> 9. props.children 就是插槽

> 10. 也具有命名插槽，一个组件原则上只能负责一个功能

> 11. useState 给组件内部添加 state。useState 会返回一对值：当前状态和一个让你更新它的函数，唯一的参数就是初始的 state

> 12. hook 不能在 class 组件中使用，useEffect(副作用函数)，React 会在每次渲染后调用副作用函数 —— 包括第一次渲染的时候

> 13. 只能在函数最外层调用 Hook。不要在循环、条件判断或者子函数中调用，只能在 React 的函数组件中调用 Hook。不要在其他 JavaScript 函数中调用。（还有一个地方可以调用 Hook —— 就是自定义的 Hook 中

> 14. 如果函数的名字以 “use” 开头并调用其他 Hook，我们就说这是一个自定义 Hook

> 15. useContext 让你不使用组件嵌套就可以订阅 React 的 Context，另外 useReducer 可以让你通过 reducer 来管理组件本地的复杂 state -->

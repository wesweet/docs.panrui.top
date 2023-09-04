<!--
 * @Description: react hook
 * @Author: panrui
 * @Date: 2023-06-05 09:05:09
 * @LastEditTime: 2023-09-04 13:05:32
 * @LastEditors: panrui
 * 不忘初心,不负梦想
-->

## 最后更新时间：2023-06-14 16-24-28

## React.FC

> 1.  FC 是一个泛型类型，代表 FunctionComponent 的缩写。FunctionComponent 是一个 React 函数组件的类型定义，它接收一个泛型类型参数，用于指定组件的 props 类型，返回一个 React 元素或者 null。

```js
import React from "react";
type Props = {
  name: string,
};
const Greeting: React.FC<Props> = ({ name }) => {
  return <h1>Hello, {name}!</h1>;
};
```

> 2. 添加 FC 与不添加 FC 的区别

```
在于函数组件的返回值类型,React.FC 表示函数组件的返回值是一个 React 元素，即一个 React 组件或 HTML 标签。如果不添加 React.FC，则函数组件的返回值类型为 any，即可以返回任意类型的值，包括字符串、数字、布尔值等，也包括 React 元素。
```

## useState

useState 是 React Hooks 中的一个基础 Hook, 用于在函数组件中添加状态,useState Hook 接收一个初始状态的参数，返回一个数组，该数组包含了当前状态的值和一个更新状态的函数。唯一的参数就是初始的 state

```js
import React, { useState } from "react";
function Counter() {
  const [count, setCount] = useState(0);
  return (
    <div>
      <p>You clicked {count} times</p>
      <button onClick={() => setCount(count + 1)}>Click me</button>
    </div>
  );
}
```

## useEffect

useEffect 是 React 中的一个 Hook，用于在函数组件中添加类似于生命周期函数的行为。

> 1.  它可以在组件渲染后执行副作用操作（effect），如订阅数据、更新 DOM 等。通常情况下，我们可能会在类组件的 componentDidMount，componentDidUpdate 和 componentWillUnmount 等生命周期方法中添加这些副作用。而 useEffect 可以让我们在函数组件中完成这些操作。
> 2.  useEffect Hook 接收两个参数：第一个参数是一个函数，用于执行副作用操作；第二个参数是一个数组，它用于控制副作用代码的执行时间

执行时间：

> 1.  如果第二个参数为空数组 []，则表示只在组件挂载时执行一次。这是我们通常使用的效果，类似于类组件中的 componentDidMount
> 2.  如果第二个参数中指定了依赖，例如[count]，则表示只在依赖项 count 发生变化时才执行副作用代码。
> 3.  如果第二个参数省略不传，则会在每次组件渲染时执行副作用代码，类似于没有指定 componentDidUpdate 依赖的类组件中的 componentDidUpdate 方法

清理副作用：

> 1.  在进行某些副作用操作时，可能需要清除定时器、解除事件绑定或取消订阅等。在这种情况下，需要在返回的函数中清理资源。如果没有需要清理的资源，则可以返回一个空函数

```js
import React, { useState, useEffect } from "react";
function Example() {
  const [count, setCount] = useState(0);
  useEffect(() => {
    console.log("Component mounted");
  }, []);
  function handleClick() {
    setCount(count + 1);
  }
  return (
    <div>
      <h1>Count: {count}</h1>
      <button onClick={handleClick}>Increment</button>
    </div>
  );
}
```

## useContext

useContext 是 React 中的一个 Hook，Context API 是 React 提供的一种跨组件传递数据的方式

> 1.  使用 useContext 函数，你可以在函数组件中访问 Context 中的数据，而不需要使用类组件中的 this.context 或者 Consumer 组件。useContext 接收一个 <span class="red-text"> Context 对象</span>作为参数，并返回该 Context 的当前值。如果没有对应的 Provider，useContext 的返回值等同于 Context 对象的 defaultValue 参数

需要注意的是，如果你想在函数组件中使用多个 Context 对象，你需要多次调用 useContext 函数。每次调用 useContext 函数时，你需要传递一个不同的 Context 对象作为参数。

```js
import React, { useContext } from "react";
import { ThemeContext } from "./theme-context";
function ThemeTogglerButton() {
  const { theme, toggleTheme } = useContext(ThemeContext);
  return (
    <button
      onClick={toggleTheme}
      style={{ backgroundColor: theme.background, color: theme.foreground }}
    >
      Toggle Theme
    </button>
  );
}
```

## useRef

useRef 是 React 中的一个 Hook，它可以用于获取 DOM 节点或者 <span class="red-text">保存任何可变值</span> 的“盒子”。useRef 的返回值是一个包含 .current 属性的对象(ref)，该属性指向被保存的值。返回的 ref 对象在组件的整个生命周期内保持不变，它类似于在 class 组件中使用实例属性的方式

> 1.  我们可以使用 useRef 来保存组件或者 DOM 元素的引用，通过它我们可以实现与 DOM 元素进行交互。

```js
import React, { useRef } from "react";
function TextInputWithFocusButton() {
  const inputEl = useRef(null);
  const onButtonClick = () => {
    // `current` 指向已挂载到 DOM 上的文本输入元素
    inputEl.current.focus();
  };
  return (
    <>
      <input ref={inputEl} type="text" />
      <button onClick={onButtonClick}>Focus the input</button>
    </>
  );
}
```

> 2.  保存上一次的值

```js
import React, { useState, useEffect, useRef } from "react";
function Counter() {
  const [count, setCount] = useState(0);
  const prevCountRef = useRef();
  useEffect(() => {
    prevCountRef.current = count;
  });
  const prevCount = prevCountRef.current;
  return (
    <div>
      <h1>Previous count: {prevCount}</h1>
      <h1>Current count: {count}</h1>
      <button onClick={() => setCount(count + 1)}>+</button>
    </div>
  );
}
```

## useCallback

useCallback 是 React 中的一个 Hook，优化函数组件的性能

> 1. 在函数组件中，每次重新渲染都会导致函数的重新定义和创建，尤其是如果这个函数是作为 prop 传递到子组件中的话，这就会导致触发子组件的不必要的重新渲染。如果这种情况发生在性能敏感的组件上，可能会导致应用的性能下降。
> 2. 为了解决这个问题，React 提供了 useCallback Hook，它可以用于缓存函数，避免函数的重新定义和创建。useCallback 接收两个参数：第一个参数是一个函数，第二个参数是一个数组，用于指定依赖项。useCallback 会返回一个 <span class="red-text">缓存的函数</span> ，该函数会在依赖项发生变化时才会更新
> 3. 如果传递空数组，或者不传，这意味着方法没有依赖项，将不会被更新

```js
import React, { useState, useCallback } from "react";

function Button({ onClickButton, children }) {
  return (
    <>
      <button onClick={onClickButton}>{children}</button>
      <span>{Math.random()}</span>
    </>
  );
}

function App() {
  const [count1, setCount1] = useState(0);
  const [count2, setCount2] = useState(0);
  const [count3, setCount3] = useState(0);

  const handleClickButton1 = () => {
    setCount1(count1 + 1);
  };

  const handleClickButton2 = useCallback(() => {
    setCount2(count2 + 1);
  }, [count2]);

  return (
    <div>
      <div>
        <Button onClickButton={handleClickButton1}>Button1</Button>
      </div>
      <div>
        <Button onClickButton={handleClickButton2}>Button2</Button>
      </div>
      <div>
        <Button
          onClickButton={() => {
            setCount3(count3 + 1);
          }}
        >
          Button3
        </Button>
      </div>
    </div>
  );
}
```

- 点击 Button1 的时候只会更新 Button1 和 Button3 后面的内容;
- 点击 Button2 会将三个按钮后的内容都更新;
- 点击 Button3 的也是只更新 Button1 和 Button3 后面的内容。

> 4.  使用场景

以下是 useCallback 的常见使用场景：

- 在 props 中传递回调函数时，尤其是当回调函数是复杂的计算函数时，可以使用 useCallback 仅仅包装一次回调函数，避免它被重复地创建，从而提高性能。

- 在使用 useMemo 缓存一个值的同时，如果这个值依赖于一个函数，可以使用 useCallback 来缓存这个函数，并将其作为 useMemo 的依赖项，这样可以避免不必要的函数重定义和浪费。

- 在使用 useEffect 时，如果需要传递一个回调函数给 useEffect，可以使用 useCallback 缓存这个函数以确保它不会在组件重新渲染时被重复创建。

- 在使用 Redux 或其他状态管理库时，若需要将一个回调函数作为 action creator 进行传递，可以使用 useCallback 缓存这个函数，避免在每次组件重新渲染时都被重新创建。

总而言之，如果在函数组件中有任何回调函数需要传递或缓存，考虑使用 useCallback 来提高应用的性能。

## useMemo

useMemo 是 React 中的一个 Hook，它用于缓存计算结果，避免浪费不必要的计算资源。

> 1.  在函数组件中，每次重新渲染都会重新计算变量的值，如果这个变量的计算需要耗费很多资源，会导致应用的性能下降。在这种情况下，可以使用 useMemo Hook 来缓存计算结果，避免不必要的计算过程。
> 2.  useMemo 接收一个计算函数和依赖项数组作为参数。当依赖项数组中的任何一个元素改变了，useMemo 会重新计算一个新的值；否则，它会返回之前缓存的值。这样，React 就能够避免在重新渲染时不必要地重复计算。

```js
import React, { useState, useMemo } from "react";

function fibonacci(n) {
  if (n === 1 || n === 2) {
    return 1;
  }

  return fibonacci(n - 1) + fibonacci(n - 2);
}

function App() {
  const [count, setCount] = useState(1);

  const fib = useMemo(() => fibonacci(count), [count]);

  return (
    <div>
      <h1>Count: {count}</h1>
      <h2>Fibonacci: {fib}</h2>
      <button onClick={() => setCount(count + 1)}>+1</button>
    </div>
  );
}
```

> 3.  使用场景

- 如果你有一个复杂的计算函数，而且这个计算函数在每次组件重新渲染时都需要被执行，你可以使用 useMemo 来缓存计算函数的结果，以避免在每次重新渲染时重复计算。这样可以提高应用的性能。

- 如果你有一个需要从服务器获取数据的组件，并且这个请求可能需要一段时间才能完成，你可以使用 useMemo 来缓存请求结果，以避免在每次重新渲染时重新发起 API 请求或者重新处理数据。这样可以减少网络流量并提高应用的响应速度。

## useReducer

useReducer 是一个 React 中的 Hook，它用于管理复杂的组件状态，其功能类似于 Redux 中的 reducer 功能。

> 1.  使用 useReducer，你可以将组件的状态和它的更新函数封装在一起，这样可以更好地组织和管理复杂的组件状态，避免出现“状态分散”的问题。
> 2.  useReducer 接收一个 reducer 函数和初始状态作为参数，它会返回一个当前状态和一个 dispatch 函数。当 dispatch 函数被调用时，它会将一个操作（也被称作 action）作为参数传入 reducer 函数，并更新当前组件状态。

```js
import React, { useReducer } from "react";

const initialState = { count: 0 };

function reducer(state, action) {
  switch (action.type) {
    case "increment":
      return { count: state.count + 1 };
    case "decrement":
      return { count: state.count - 1 };
    default:
      throw new Error();
  }
}

function Counter() {
  const [state, dispatch] = useReducer(reducer, initialState);

  return (
    <>
      Count: {state.count}
      <br />
      <button onClick={() => dispatch({ type: "increment" })}>+</button>
      <button onClick={() => dispatch({ type: "decrement" })}>-</button>
    </>
  );
}
```

在上面的例子中，我们定义了一个 Counter 组件，它使用 useReducer 来管理计数器的状态。我们定义了一个 reducer 函数来更新状态，并使用 useReducer 来初始化当前状态和 dispatch 函数。

在组件中，我们使用 state.count 来渲染当前计数器的值，并使用 dispatch 函数来更新计数器的值。当 dispatch 函数被调用时，它会将一个操作作为参数传入 reducer 函数，并更新组件状态。

总而言之，如果你的组件需要管理复杂的状态，并且需要更好地组织和管理组件状态逻辑，你可以使用 useReducer Hook。

> 3.  使用场景

以下是使用 useReducer 的常见场景：

1. 管理组件中的复杂状态

如果你的组件需要管理复杂的状态，例如包含多个属性和子属性的状态，你可以使用 useReducer 来管理这些状态的操作。通过将所有的状态操作都封装在一个 reducer 函数中，可以更好地组织和管理组件状态操作的逻辑。

2. 管理组件状态的多种操作

如果你的组件需要支持多种状态操作，例如增加、减少、修改等，你可以使用 useReducer 来管理这些状态的操作。通过将所有的状态操作都封装在一个 reducer 函数中，可以更好地组织和管理组件状态操作的逻辑。

3. 处理组件状态的异步操作

如果你的组件需要处理异步操作，例如通过 API 获取数据或发送请求等，你可以使用 useReducer 来管理这些状态的操作。通过将异步操作的状态封装在 reducer 函数中，并使用 useEffect 处理异步逻辑，可以更好地组织和管理复杂的异步操作逻辑。

总而言之，如果你的组件需要管理或处理复杂的状态或操作，推荐使用 useReducer 来更好地组织和管理组件状态操作的逻辑，并提高应用的可维护性和可扩展性。

> 4.  useReducer、useState、reducer 的区别

useState 是 React Hooks 中的一个 Hook，它可以用于管理单个状态变量（state）。可以使用多个 useState 来管理多个状态变量。每次状态变量更新时，组件都会重新渲染。

useReducer 也是 React Hooks 中的一个 Hook，它可以用于管理复杂的组件状态。它适用于管理需要多种状态操作的组件状态。useReducer 接收一个 reducer 函数和初始状态作为参数，它会返回当前状态和一个 dispatch 函数。当 dispatch 函数被调用时，它会将一个操作作为参数传入 reducer 函数，并更新当前组件状态。

reducer 是一个概念，它用于管理状态对象的所有可用操作。在使用 useReducer 时，需要传入一个 reducer 函数，用于管理状态操作的逻辑。reducer 接收当前状态和一个操作作为输入，并返回一个新的状态。

可以使用 useState 来管理简单的单个状态变量，而对于复杂的状态，可以使用 useReducer 来更好地组织和管理组件状态操作的逻辑。使用 reducer 来统一管理所有状态操作，能够提高代码的可维护性和可扩展性。

## useLayoutEffect

useLayoutEffect 是 React Hook 中的一个钩子函数，其输出结果与 useEffect 一致。useLayoutEffect 在浏览器绘制之前同步执行所有 DOM 变更，这可能会导致阻塞。

使用场景：

useLayoutEffect 应该仅在必要时使用，因为它的阻塞特性可能会降低性能。以下是一些建议的使用场景：

1. 计算 DOM 元素的尺寸或位置

由于 useLayoutEffect 在 DOM 更新后立即运行，因此在此钩子函数内进行 DOM 元素的尺寸或位置计算将非常准确，因为页面尚未进行下一轮渲染。这使得您可以避免影响其他 DOM 元素的排列和渲染。

2. 执行重要的 DOM 操作

如果您具有需要确保在页面渲染之前执行的重要 DOM 操作，例如向页面添加新的 DOM 元素，则可以使用 useLayoutEffect。这可以确保您的 DOM 操作不会在用户看到之前被中断。

3. 处理样式

由于浏览器渲染引擎可能适用于不同的 CSS 样式，因此在计算元素样式时，也可以使用 useLayoutEffect。

注意事项：

1. 避免使用过多的 useLayoutEffect 钩子函数。

每个 useLayoutEffect 钩子函数都会在 DOM 更新后同步运行，如果使用过多，可能会影响性能。

2. 避免副作用

由于 useLayoutEffect 钩子函数是同步运行的，因此它们可能会有副作用，例如阻塞渲染或阻止用户交互。使用时需要小心。

3. 与 useEffect 的区别

useEffect 只有在 DOM 渲染完成后异步执行，而 useLayoutEffect 会在 DOM 更新后同步执行。如果您只需要在渲染完成后运行函数，那么请使用 useEffect。如果必须在 DOM 更新后运行函数，则可以使用 useLayoutEffect。

## useImperativeHandle

## useDebugValue

## useErrorBoundary

## useTransition

## useDeferredValue

## useOpaqueIdentifier

## useMutableSource

## useCache

## useSyncExternalStore

## useNavigate

> 1.  用于在函数组件中进行页面导航。它可以替代原来的 useHistory 和 useLocation Hooks

```js
import { useNavigate } from "react-router-dom";
function MyComponent() {
  const navigate = useNavigate();
  function handleClick() {
    navigate("/my-path");
  }
  return <button onClick={handleClick}>Go to my path</button>;
}
```

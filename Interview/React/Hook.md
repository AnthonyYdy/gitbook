#Hook

## Hook简介

* 可以在不编写class的情况下使用state以及其他React特征。
* Hook是一个特殊的函数，可以i“钩入”React特性

### 动机
* 在组件之间复用状态逻辑很难。：**Hook使你在无需修改组件结构的情况下复用状态逻辑**
* 复杂组件变得难以理解：**Hook将组件中相互关联的部分拆成更小的函数（比如设置订阅或请求数据）**
* 难以理解的class：**Hook使你在非class情况下可以使用更多React特征**

## Hook概览

### Stack Hook
```javascript
import React,{useState} from "react";
function Example(){
    const [count,setCount] = useState(0)
    //相当于 componentDidMount 和 componentDidUpdate:
    useEffect(
        ()=>{
            //使用浏览器的Api更新页面标题
            document.title = `You clicked ${count} times`
        }
    )
    return(
        <div>
        <p>You clicked {count} times</p>
        <button onClick = {()=>setCount(count+1)}>Click me</button>
        </div>
    )
}
```
* useState就是一个Hook 
1. useState返回一对值：当前state和一个让你更新它的函数，可以在任何地方调用这个函数
2. 唯一参数就是一个初始值，state不一定要是一个对象，这个初始state的参数，只会在第一次渲染的时候被用到
3. 不能在class组件中使用

### Effect Hook
```javascript
import React,{useState,useEffect} from "react";

```

* useEffect就是一个Effect Hook，给函数组件增加了操作副作用的能力。它跟 class 组件中的 componentDidMount、componentDidUpdate 和 componentWillUnmount 具有相同的用途，只不过被合并成了一个 API。

* 调用useEffect，就是在告诉react，在完成对dom的更改后，运行Effect Hook

```javascript
useEffect(() => {
    ChatAPI.subscribeToFriendStatus(props.friend.id, handleStatusChange);
    return () => {
        //组件销毁时执行，类似于willUnmount
      ChatAPI.unsubscribeFromFriendStatus(props.friend.id, handleStatusChange);
    };
  });
  //使用副作用函数来订阅好友的在线状态，并通过取消订阅来进行清除操作
```
* Effect Hook可以返回一个函数，如何“清除”副作用
* 可以在组件中多次使用useEffect

### Hook使用规则
* Hook就是js函数，但是有两个额外的规则
1. 只能在函数最外层调用。不要在循环、条件判断、或者子函数中调用
2. 只能在React 的函数组件中调用 Hook（或者自定义的 Hook）

### 自定义Hook

* 可以在不增加组件的情况下，**在组件之间重用一些状态逻辑**
```js
import React, { useState, useEffect } from 'react';
//将friendID作为参数，返回好友是否在线的状态
function useFriendStatus(friendID) {
  const [isOnline, setIsOnline] = useState(null);

  function handleStatusChange(status) {
    setIsOnline(status.isOnline);
  }

  useEffect(() => {
    ChatAPI.subscribeToFriendStatus(friendID, handleStatusChange);
    return () => {
      ChatAPI.unsubscribeFromFriendStatus(friendID, handleStatusChange);
    };
  });

  return isOnline;
}

//以下两个组件state完全独立，但是复用状态逻辑
function FriendStatus(props) {
  const isOnline = useFriendStatus(props.friend.id);

  if (isOnline === null) {
    return 'Loading...';
  }
  return isOnline ? 'Online' : 'Offline';
}

function FriendListItem(props) {
  const isOnline = useFriendStatus(props.friend.id);

  return (
    <li style={{ color: isOnline ? 'green' : 'black' }}>
      {props.friend.name}
    </li>
  );
}
```
### 其他Hook
* useContext
```js
function Example() {
  const locale = useContext(LocaleContext);
  const theme = useContext(ThemeContext);
}
```

* useReducer 可以让你通过reducer来管理本地复杂的state。
```js
function Todos() {
  const [todos, dispatch] = useReducer(todosReducer);
}
```

## Hook使用规则

* React是靠Hook的调用顺序知道哪个state对应哪个useSate，所以要不能在条件语句之类的调用（要保证每次渲染后，Hook 的调用顺序相同）
```javascript
  //错！
 if (name !== '') {
    useEffect(function persistForm() {
      localStorage.setItem('formData', name);
    });
  }
// 👍 将条件判断放置在 effect 中
useEffect(function persistForm() {
    if (name !== '') {
      localStorage.setItem('formData', name);
    }
  });
```
## 使用自定义Hook

* 自定义Hook必须以use开头，因为自定义Hook也要遵义Hook规则，如果不以use开头，React就无法检查是否违反了Hook规则
* 两个组件使用相同的Hook不会共享state

## Hook API

### useState
* 函数式更新
```js
const [count,setCount] = useState(0)
<button onClick = {setCount(prevCount=>prevCount + 1)}></button>
```

* 惰性初始state
```js
const [count,setCount] = useState(()=>{
    let initialState = getinitialState()
    return initialState
})
//只在初始渲染时被调用
```
* 跳过state更新
1. 调用State Hook 的更新函数并传入当前的state时，React将跳过子组件的渲染及effect的执行

### useEffect

* effect调用时机

1. unlike componentDidMount and componentDidUpdate,the function passed to useEffect  fires after  layout and paint， during a deferred event.（异步）This makes it suitable for the many common side effects(副作用)，because most type of work should't block the browser from updating the creen;
2. 有的effects需要同步执行，比如在下一次更新钱，修改dom，可以用useLayoutEffect，和useEffects有相同的特征，只是调用时机不同。

* effect条件执行，
```js
useEffect(()=>{},[props.source])
```
1. 确保数组中包含了所有外部作用域中会发生切在effect中使用的变量，否则代码会引用先前渲染的旧变量。
2. 传第二个参数，只有在source改变的时候才会执行。
3. 若第二个参数为[]，则仅在组件挂载和卸载时执行。

### useContext
```js
const value = useContext(myContext)
```

1. 接收一个context对象（React.createContext返回值）。当前的context值由上层组件中距离当前组件最近的<MyContext.Provider>的value props决定
2. useContext的参数必须是context对象本身。

### useReducer
```js
const initialState = {count: 0};

function reducer(state, action) {
  switch (action.type) {
    case 'increment':
      return {count: state.count + 1};
    case 'decrement':
      return {count: state.count - 1};
    default:
      throw new Error();
  }
}

function Counter() {
  const [state, dispatch] = useReducer(reducer, initialState,init);
  return (
    <>
     <button
        onClick={() => dispatch({type: 'reset', payload: initialCount})}>
        Reset
      </button>
      Count: {state.count}
      <button onClick={() => dispatch({type: 'decrement'})}>-</button>
      <button onClick={() => dispatch({type: 'increment'})}>+</button>
    </>
  );
}

function init(initialCount) {
  return {count: initialCount};
}
```





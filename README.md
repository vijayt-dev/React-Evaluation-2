# React Evaluation 2

## 1. What are React Hooks?

- Hooks are the functions which "hook into" React state and lifecycle features from function components.
- It allows you to use state and other React features without writing a class.
- It does not work inside classes.

## 2. What are the rules that must be followed while using React Hooks?

- Hooks can only be called inside React function components.
- Hooks can only be called at the top level of a component. It cannot be used within loops, conditions, or functions.

## 3. Explain the difference between useState and useRef hooks?

| useState  | useRef  |
| ------------ | ------------ |
| useState returns the current state and has an updater function that updates the state. | useRef returns an object. |
| When the value changes, the component must render again to update the state or its value.  | In useRef, it is updated without the need to refresh or re-render.

useState
**Example**

```javascript
import { useState } from "react";

function Counter(){
    const [count,setCount] = useState(0)
    return (
        <div>
            <h1>{count}</h1>
			 <button onClick={() => setCount(count + 1)}>
            Count
        </button>
        </div>
    )
}
export default Counter;
```
useRef
**Example**

```javascript
import React, { useEffect, useRef, useState } from "react";

function RefH() {
  const [name, setName] = useState("");
  const inputRef = useRef(0);
  console.log(inputRef)
  useEffect(() => {
    inputRef.current = inputRef.current + 1
  })
  return (
    <div>
      <input
        type="text"
        onChange={(e) => setName(e.target.value)}
      />
      <h1>{name}</h1>
      <h2>{inputRef.current}</h2>
    </div>
  );
}

export default RefH;
```

## 4. What are the differences between React.memo() and useMemo()?

| React.memo()   |  useMemo()  |
| ------------ | ------------ |
| React. memo to memoize an entire component.   | Use useMemo to memoize a value within a functional component.  |

## 5. What's the difference between useCallback and useMemo in practice?

| useCallback   | useMemo  |
| ------------ | ------------ |
| useCallback returns memoised function.  | useMemo returns memoized value.   |
| useCallback is called by the user	| A useMemo is called using React	|
| useCallback accept arguments	 | useMemo didn't accept arguments	|
| **Syntax:** useCallback(fn, deps);		| 	**Syntax:** useMemo(fn, deps);	|

UseCallback 
**Example**
```javascript

import React, {useState,useCallback, useEffect } from 'react'

function Callback() {
const [number,setNumber] = useState(1)
const [dark,setDark] = useState(false)

const getItems = useCallback(() => {
    return [number, number + 1, number + 2]
},[number])
const theme = {
    backgroundColor: dark ? "#333" : "#fff",
    color: dark ? "#fff" : "#333"
}
useEffect(() => {
    console.log("Update")
},[getItems])
  return (
    <div style={theme}>
        <input type="number" value={number} onChange={e => setNumber(e.target.value)} />
        <button onClick={() => setDark(prevDark => ! prevDark)}>
            Toggle Theme
        </button>

        <div>
            {
                getItems().map(item => <div key={item}>{item}</div>)
            }
        </div>
    </div>
  )
}

export default Callback
```
useMemo.js

```javascript
import React, { useCallback, useMemo, useState } from 'react'
function CounterMemo() {
    const [countOne,setCountOne] = useState(0)
    const [countTwo,setCountTwo] = useState(0)
    const [toggle,setToggle] = useState(false)
    const incrementOne = () => {
        setCountOne(countOne+ 1)
    }
    const incrementTwo = () => {
        setCountTwo(countTwo + 1)
    }
     const isEven = useMemo( () => {
         while(i < 9000000000) i++
        console.log("Render")
         return countOne % 2 === 0
     },[countOne])

  return (
    <div>
        <h1>Count1 {countOne}</h1>
        <button onClick={incrementOne}>Increment</button>
        {isEven()}
        <h1>Count2 {countTwo}</h1>
        <button onClick={incrementTwo}>Increment</button>
        <button onClick={() => setToggle(!toggle)}>Toggle</button>
        {toggle && <p>Toggle</p>}
    </div>
  )
}

export default CounterMemo
```

## 6. What is the useEffect hook used for?

The useEffect Hook allows you to perform side effects in your components. Ex: fetching data and timers.

## 8.  Name the different lifecycle methods.

There are three categories of lifecycle methods:
1. mounting
2. updating
3. unmounting.

## 9. What is React Router?

React Router is a standard library for routing in React. It enables the navigation among  various components in a React Application.

## 10. What is activeClassName and what is its usage in React Router?

It is used in NavLink component to determine the current active link of sub links. The default given class is active.

**Example**

```javascript

import React from 'react'
import { NavLink } from 'react-router-dom'

function NavBar() {
    const navLinkStyle = ({isActive}) => {
        return {
            fontWeight: isActive ? "bold" : "normal",
            color: isActive ? "#eee" : "#123"
        }
    }
  return (
    <div>
        <nav>
            <NavLink style={navLinkStyle} to="/">Home </NavLink>
            <NavLink style={navLinkStyle} to="/about">About </NavLink>
            <NavLink style={navLinkStyle} to="/product">Product</NavLink>

        </nav>
    </div>
  )
}

export default NavBar

```

## 11. How to get query parameters in React Router?

Using useSearchParams hook have a get function to get query params.

**Example**
```javascript
   const [urlparams,setUrlparams] = useSearchParams();
    const isActive = urlparams.get("filter")
    console.log(isActive)
```

## 12. Differences Between NavLink, Link, and a?

- The NavLink is used when you want to highlight a link as active.  
 **Example**  
 ```javascript
import React from 'react'
import { NavLink } from 'react-router-dom'

function NavBar() {
    const navLinkStyle = ({isActive}) => {
        return {
            fontWeight: isActive ? "bold" : "normal",
            color: isActive ? "#eee" : "#123"
        }
    }
  return (
    <div>
        <nav>
            <NavLink style={navLinkStyle} to="/">Home </NavLink>
            <NavLink style={navLinkStyle} to="/about">About </NavLink>
            <NavLink style={navLinkStyle} to="/product">Product</NavLink>
        </nav>
    </div>
  )
}
```

- Link is for links that need no highlighting.  

**Example**
```javascript
import React from 'react'
import { Link } from 'react-router-dom'

function NavBar() {
  return (
    <div>
        <nav>
            <Link style={navLinkStyle} to="/">Home </Link>
            <Link style={navLinkStyle} to="/about">About </Link>
            <NavLink style={navLinkStyle} to="/product">Product</Link>
        </nav>
    </div>
  )
}
```
- A is for external links.  
```javascript
import React from 'react'

function NavBar() {
  return (
    <div>
        <nav>
            <a href="https://www.google.com" > Google </Link>
        </nav>
    </div>
  )
}
```

## 13. How do I redirect a route in react?

using useNavigate hook to programmatically route.

App.js

```javascript

import { Routes,Route } from "react-router-dom";
import Home from "./components/Home";
import Login from "./components/Login";
import Dashboard from "./components/Dashboard";

function App() {
  return (
    <div className="App">
     <Routes>
      <Route path="/" element={<Home />} />
      <Route path="login" element={<Login />} />
	   <Route path="dashboard" element={<Dashboard />} />
     </Routes>
    </div>
  );
}

export default App;
```
Login.js

```javascript

import Dashboard from "./components/Dashboard";

function Login() {
const navigate = useNavigate()
  return (
    <div className="Login">
 	{isLoginSucess && navigate("/dashboard")}
    </div>
  );
}

export default Login;
```

## 14. What is the use of useLocation in react JS?

The useLocation hook returns the location object that represents the current URL and also get data.

**Example**

```javascript
import React from 'react'
import { useLocation } from 'react-router-dom'

function NavBar() {
    const location = useLocation()
	console.log(location) /* {
    "pathname": "/product",
    "search": "",
    "hash": "",
    "state": null,
    "key": "50pv7p0n"
} */
  return (
    <div>
		useLocation
    </div>
  )
}

export default NavBar
```

## 15. What is an outlet in react router?

An Outlet component should be used in parent route elements to render their child route elements.

**Example**

App.js

```javascript

import {Routes,Route} from "react-router-dom"
import Admin from "./Admin";
import Featured from "./Component/Featured";
import Home from "./Component/Home";
import NavBar from "./Component/NavBar";
import New from "./Component/New";
import NoMatch from "./Component/NoMatch";
import Order from "./Component/Order";
import OrderSummary from "./Component/OrderSummary";
import Product from "./Component/Product";
import UserDetails from "./UserDetails";
import Users from "./Users";
import React from 'react'
function App() {

  return (
    <div className="App">
      <NavBar />
      <Order />
      <Routes>
        <Route path="/" element={<Home />} />
        <Route path="product" element={<Product />}>
          <Route index element={<Featured />} />
          <Route path="featured" element={<Featured />} />
          <Route path="new" element={<New />} />
        </Route>
        <Route path="user" element={<Users />}>
        <Route path=":userID" element={<UserDetails />} />
        <Route path="admin" element={<Admin />} />
        </Route>

        <Route path="order-summary" element={<OrderSummary />} />
        <Route path="*" element={<NoMatch />} />
      </Routes>
    </div>
  );
}

export default App;
```

Product.js

```javascript
import React from 'react'
import { NavLink, Outlet } from 'react-router-dom'

function Product() {
  return (
    <div>
        <input type="search" placeholder="Search products" />
        <nav>
            <NavLink to="featured">Featured</NavLink>
            <NavLink to="new">New</NavLink>
        </nav>
        <Outlet />
    </div>
  )
}

export default Product
```

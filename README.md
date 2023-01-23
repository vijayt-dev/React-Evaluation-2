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

## 4. What are the differences between React.memo() and useMemo()?

| React.memo()   |  useMemo()  |
| ------------ | ------------ |
| React. memo to memoize an entire component.   | Use useMemo to memoize a value within a functional component.  |

## 5. What's the difference between useCallback and useMemo in practice?

| useCallback   | useMemo  |
| ------------ | ------------ |
| useCallback returns memoised function.  | useMemo returns memoized value.   |

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

## 11. How to get query parameters in React Router?

Using useSearchParams hook have a get function to get query params.

**Example**
```javascript
   const [urlparams,setUrlparams] = useSearchParams();
    const isActive = urlparams.get("filter")
    console.log(isActive)
```

## 12. Differences Between NavLink, Link, and a?

| NavLink  | Link  | a  |
| ------------ | ------------ | ------------ |
| The NavLink is used when you want to highlight a link as active.  | Link is for links that need no highlighting.   | A is for external links.   |


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

The useLocation hook returns the location object that represents the current URL.

## 15. What is an outlet in react router?

An Outlet component should be used in parent route elements to render their child route elements.

# React Hooks Overview

## Introduction

React Hooks were introduced in version 16.8, providing powerful features that allow function components to manage state and utilize other React functionalities without needing to convert to class components.

## What is a Hook?

Hooks are functions that let you "hook" into React features like state and lifecycle methods directly from function components.

## Hook Rules

There are three fundamental rules for using Hooks in React:

1. **Only Call Hooks Inside React Functions**: Hooks should be called only within React function components or other custom Hooks.
2. **Call Hooks at the Top Level**: Always use Hooks at the top level of your function component. They should not be called inside loops, conditions, or nested functions.
3. **Do Not Call Hooks Conditionally**: Hooks should be used unconditionally to ensure that the state and side effects are applied consistently across renders.

# useState Hook

The `useState` Hook is a built-in React Hook that allows you to manage state in function components.

### What is State?

State generally refers to data or properties that need to be tracked in an application. It can change over time, and React will re-render the component whenever the state is updated.

### How to Use useState

To use `useState`, first import it from React:

```javascript
import { useState } from "react";
```

### Initialize useState

You initialize state by calling `useState` within your function component. `useState` accepts an initial state and returns two values:

1. The current state.
2. A function that allows you to update the state.

### Example

Here's an example of how to use `useState`:

```javascript
import { useState } from "react";

function FavoriteColor() {
  const [color, setColor] = useState("");
}
```

In this example, `color` is the current state, and `setColor` is the function used to update the state. The initial state is set to an empty string.

# `useEffect` Hook 

## Introduction

The `useEffect` Hook is a powerful feature in React that allows you to perform side effects in your function components. Side effects can include tasks such as fetching data, directly manipulating the DOM, or setting up timers.

## What is a Side Effect?

Side effects are operations that affect something outside the scope of the function being executed. In the context of React, common side effects include:

- **Fetching data** from an API
- **Updating the DOM** directly (e.g., manipulating an element's style or attributes)
- **Setting up timers** or intervals

## How to Use `useEffect`

The `useEffect` Hook takes two arguments:

```javascript
useEffect(<function>, <dependency>)
```

- **First Argument**: A function that contains the side effect logic.
- **Second Argument (Optional)**: An array of dependencies that determines when the effect should run.

### Basic Example

Here’s an example of using `useEffect` to update a counter every second:

```javascript
useEffect(() => {
  setTimeout(() => {
    setCount((count) => count + 1);
  }, 1000);
}, []);
```

In this example, the effect runs once after the initial render because the dependency array is empty (`[]`).

## Effect Cleanup

Some effects require cleanup to avoid issues such as memory leaks. Common examples include:

- **Timeouts**
- **Subscriptions**
- **Event listeners**

To perform cleanup, return a function from within the `useEffect` Hook. This function will be executed when the component unmounts or before the effect runs again.

### Cleanup Example

Here’s an example of using `useEffect` with cleanup:

```javascript
useEffect(() => {
  let timer = setTimeout(() => {
    setCount((count) => count + 1);
  }, 1000);

  return () => clearTimeout(timer);
}, []);
```

In this example, the cleanup function clears the timeout to ensure that it doesn’t continue running unnecessarily.

# useContext` Hook

## Introduction

The `useContext` Hook is a powerful feature in React that allows components to access and share state more efficiently across deeply nested component trees without the need for prop drilling. It works in conjunction with React Context, which provides a way to manage state globally across your application.

## React Context

React Context is a mechanism for managing state at a global level. It enables you to share state between components without having to pass props manually through each level of the component hierarchy.

### The Problem with Prop Drilling

When multiple nested components need access to the same state, you might traditionally pass the state as "props" through each component in the hierarchy. This technique, known as "prop drilling," can become cumbersome and difficult to maintain, especially in large applications with deep component trees.

### Solution: React Context

React Context solves the problem of prop drilling by allowing you to create a context and provide it to any component in the tree, regardless of how deeply nested it is.

## How to Use React Context

### 1. Create Context

To create a context, you use the `createContext` function provided by React:

```javascript
import { useState, createContext } from "react";
import ReactDOM from "react-dom/client";

const UserContext = createContext();
```

### 2. Context Provider

Wrap the components that need access to the state with a Context Provider. The Provider component accepts a `value` prop that contains the state you want to share.

```javascript
function Component1() {
  const [user, setUser] = useState("Jesse Hall");

  return (
    <UserContext.Provider value={user}>
      <h1>{`Hello ${user}!`}</h1>
      <Component2 user={user} />
    </UserContext.Provider>
  );
}
```

In this example, `Component1` provides the `user` state to all of its child components, making the state available without needing to pass it explicitly as props.

### 3. Use the `useContext` Hook

To access the context in a child component, use the `useContext` Hook. This allows you to consume the context value directly.

```javascript
import { useState, createContext, useContext } from "react";

function Component5() {
  const user = useContext(UserContext);

  return (
    <>
      <h1>Component 5</h1>
      <h2>{`Hello ${user} again!`}</h2>
    </>
  );
}
```

In this example, `Component5` accesses the `user` state provided by `Component1` using the `useContext` Hook, allowing it to use the state without needing to receive it as a prop.




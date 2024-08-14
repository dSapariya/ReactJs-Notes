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

## useState Hook

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

---

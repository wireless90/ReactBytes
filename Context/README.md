# React Context

The UI elements that most of us work on are complex. The root of the tree is often very far from the leaves. This puts data the application depends on many layers away from the components that use the data. Every component must receive props that they only pass to their
children. This will bloat our code and make our UI harder to scale. 

Passing state data through every component as props until it reaches the component that needs to use it becomes very complex.

In React, context is like jet-setting for your data. You can place data in React context by creating a context provider. A context provider is a React component you can wrap around your entire component tree or
specific sections of your component tree. The context consumer is the React component that retrieves the data from context.

# Placing Data into a Context Provider

```jsx

import React, {createContext} from "react";
import colors from "./color-data";
import {render} from "react-dom";
import App from "./App";

export const ColorContext = createContext()

render (
  <ColorContext.Provider values={{colors}}>
    <App />
  </ColorContext.Provider>,
  
  document.getElementById("root")
);

```

Now that we’re providing the colors value in context, the App component no longer needs to hold state and pass it down to its children as props.


# Refactoring

## Render Props


```jsx
import React from 'react'

const groceries = [
    {name: 'Potatoes', price: 1.5},
    {name: 'Tomatoes', price: 0.5},
    {name: 'Onions4', price: 0.3},
];

export default function RenderProps()
{
    return (
        <ul>
            {
                groceries.map((grocery, index) =>{
                    return <li key={index}>Name: {grocery.name}, Price: {grocery.price}</li>      
                })
            }
        </ul>
    );
}


```

![image](https://user-images.githubusercontent.com/12537739/147867426-64d9c5ef-11cc-4c6c-924c-c5e346f3a194.png)

This code above makes sense, but mapping over an array to
render each item individually does introduce some code complexity.
Mapping over an array of items is also a pretty common task. We may
find ourselves frequently repeating this pattern. We could create a `List
component` that we can reuse as a solution whenever we need to render
an unordered list.

Let's refactor it by making an `unorder list component`. This list will allow other devs to specift how to render the item. That is render props!

```jsx
import React from 'react'

export default function GenericUnorderedList(
    { 
        data=[], 
        renderItemFunc= f => f, 
        renderIfEmpty
    }
)
{
    if(dataNullOrEmpty(data))
        return renderIfEmpty;

    return (
        <ul>
            {
                data.map((item, index) =>
                {
                    return <li key={index}>{renderItemFunc(item)}</li>;
                })
            }
        </ul>
    );
}

function dataNullOrEmpty(data) {
    return !data || data.length === 0;
}


```

```jsx
const groceries = [
  {name: 'Potatoes', price: 1.5},
  {name: 'Tomatoes', price: 0.5},
  {name: 'Onions4', price: 0.3},
];

ReactDOM.render(
    <GenericUnorderedList 
      data= {groceries}
      renderIfEmpty="List is empty"
      renderItemFunc= {item => <>Name: {item.name}, Price: {item.price}</>}
    />,
  document.getElementById('root')
);

```

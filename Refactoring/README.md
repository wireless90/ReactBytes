# Refactoring

## Render Props

The term “render prop” refers to a technique for sharing code between React components using a prop whose value is a function.

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

Now if there are any items in the list, the item will be rendered as specified in the render prop, `renderItemFunc`.

![image](https://user-images.githubusercontent.com/12537739/147867623-bf3b1287-bd42-499d-bd39-ec497a4c08d1.png)


If there are no items, the `renderIfEmpty` will be specified.

![image](https://user-images.githubusercontent.com/12537739/147867632-30866dbe-533d-48cd-aa59-4a35e4794923.png)


But what if the list is huge? Our list component will take a long time to render everything.

```jsx
import faker from 'faker';

const biglist = [...Array(5000)].map(() =>({
  name: faker.name.findName(),
  email: faker.internet.email(),
  avatar: faker.internet.avatar()
}));

ReactDOM.render(
  <>
    <GenericUnorderedList 
      data= {biglist}
      renderIfEmpty="List is empty"
      renderItemFunc= {item => 
      <>
        <span>Name: {item.name}, Price: {item.price}</span>
        <div>
          <img src={item.avatar}  />
        </div>
      </>
      }
    />
    </>,
  document.getElementById('root')
);

```

We can make use of libraries like `react-window`.

```jsx
import React from 'react';
import ReactDOM from 'react-dom';
import faker from 'faker';
import { FixedSizeList } from 'react-window';

const biglist = [...Array(2000)].map(() =>({
  name: faker.name.findName(),
  email: faker.internet.email(),
  avatar: faker.internet.avatar()
}));

//react-window examples here> https://react-window.vercel.app/#/examples/list/fixed-size
const rowFunc = ({index, style}) =>
(
  <div>
    {biglist[index].name} - {biglist[index].email}
  </div>
);

ReactDOM.render(
    <FixedSizeList
      height={200}
      itemCount={biglist.length}
      itemSize={35}
    >
      {rowFunc}
    </FixedSizeList>,
  document.getElementById('root')
);

```

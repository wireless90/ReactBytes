# Destructuring Objects

## Scoping out members of an object

If we have an object like

```js
const menu = {
  main: "biryani",
  dessert: "ice cream",
  drinks: "lime juice"
};
```

We can scope of `main` and `drinks` using implicit object destructuring.

```js
const {main, drinks} = menu;
console.log(main); //biryani
console.log(drinks); //lime juice
```


## Scoping out members of an object into function arguments

If we have a function that takes in the `menu` object and prints out the `main` dish as such below,
```js
const announceMenu = (menu) => console.log(menu.main);
```
We can instead simply destructure the `main` member of the `menu` object as below.

```js
const announceMenu = ({main}) => console.log(main);
```

## Scoping out nested members

Take a look at the following nested object.

```js
const menu = {
  main: "biryani",
  dessert: "ice cream",
  drinks: "lime juice",
  prepared: {
    chef: "tom riddle",
    assistant: "malfoy"
  }
};
```
If we wanted to print the `chef` member, we would do so normally like,

```js
const announceChef = (menu) => console.log(menu.prepared.chef);
```

Instead with object destructuring, we can do it in a more readable way as such.

```js
const announceChef = ({prepared: {chef}}) => console.lof(chef);
```

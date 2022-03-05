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

We can scope out `main` and `drinks` using implicit object destructuring.

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
const announceChef = ({prepared: {chef}}) => console.log(chef);
```
# Object literal Enhancement

## Implicit Object literal Enhancement

This is the opposite of `Object Destructuring`. We want to put back an object together.

```js
const name="Razali";
const age = 3;
const person = {name, age}; //Object Literal Enhancement
```

## Implicit Object literal Enhancement with function as a key

```js
const speak = () => console.log(`Hello i am ${this.name} and i ame ${this.age} years old!`); //name and age need not exist at this point

const name="Razali";
const age = 3;


const person = {name, age, speak}; //Object Literal Enhancement
```


# Restructuring Objects

## Restructuring Objects with the Spread operator

```js
const morning = {
  breakfast:"oatmeal",
  lunch:"pizza"
};
const dinner="noodles";
```
We can restructure the above into a single object.

```js
const meals = {
  ...morning, 
  dinner
};
```

# Destructuring Arrays

## Implicit Array Destructuring

Let's say we have a list of strings as an array.

```js
const languages = ["js", "c++", "python", "c#"];
```

We can destructure the first variable simply by

```js
const [favLanguage] = ["js", "c++", "python", "c#"];
```

Now `favLanguage` contains `"js"`.

## Implicit Array Destructuring using Discards

If we want `python` to be our favourite language, we can use the discard operator by simply

```js
const [, , , favLanguage] = ["js", "c++", "python", "c#"]; //skips the first 3 elements and stores the next element into favLanguage
```

# Restructuring Arrays

## Restructuring Arrays with the Spread operator
Given 2 arrays,
```js
const boys = ["Tom", "Malfoy", "Harry"];
const girls = ["Jinny", "Hermoine"];
```
We can combine them using the spread operator~
```js
const students = [...boys, ...girls];
```

## Reversing without mutation

The following code below is bad as it mutates the array which might not be what we intended.
```js
const [lastStudent] = students.reverse();
```

Instead, we can use the spread operator which creates a new array for us.

```js
const [lastStudent] = [...students].reverse();
```

## Get the rest of the elements
Let's say we do not want the first 2 students, we can do so easily as such.

```js
const [first, second ...others] = students; 
```


# Rest parameters
Multiple arguments in a function can be collated together into an array using the spread operator as well.

For example, if we have a function as such,

```js
const collatePeople = (firstPerson, secondPerson, thirdPerson) => [firstPerson, secondPerson, thirdPerson];
```
Instead we can use `Rest Parameters`.

```js
const collatePeople = (...persons) => persons;
```

# Functional Concepts
Introducing the core concepts of functional programming: immutability, purity, data transformation, higher-order functions, and recursion.

## Immutability

We instead of changing the original data structures, we build changed copies of those data structures and use them instead.

Let's say we have a color object.
```jsx
let color_lawn = {
  title: "lawn",
  color: "#00FF00", 
  rating: 0
};
```
And we want to write a function that takes in this object and changes its rating.

```jsx
function rateColor(color_obj, rating) {
  color.rating = rating;
  return color
}

console.log(rateColor(color_lawn, 5).rating); //5
console.log(color_lawn.rating); //5
```

As we can see, the object is mutated which is not a core principle of functional programming. In order to make it immutable, we could

```jsx
function rateColor(color_obj, rating) {
  return {
    ...color_obj,
    rating
  };
}

console.log(rateColor(color_lawn, 5).rating); //5
console.log(color_lawn.rating); //0
```

## Purity / Pure Functions

### Pure functions
- Take in atleast one argument
- Returns a value or another function
- Does not cause side effects (A side effect is when a function relies on, or modifies, something outside its parameters to do something)
- Does not set global variables
- Treat arguments as immutable data

### Whats the use of having these conditions?

Pure functions, with the above criteria, are naturally testable. They do not change what was given to them. Everything it needs to operates is passed to it as arguments.
They are another core concept of functional programming. They will make your life much easier because they will not affect your application’s state. When writing functions, try to follow these three
rules:

1. The function should take in at least one argument.
2. The function should return a value or another function.
3. The function should not change or mutate any of its
arguments

## Data Transformation
How does anything change in an application if the data is immutable? Functional programming is all about transforming data from one form to another. We’ll produce transformed copies using functions. These functions make our code less imperative and thus reduce complexity.

There are two core functions that you must master in order to be proficient with functional Javascript:
- Array.map
- Array.reduce
- Array.join
- Array.filter
- Array.reduce
- Array.reduceRight

Consider this array of strings.

```jsx
const colors = ['black', 'red', 'green', 'blue'];
```

### Array.join

How do we get a comma-delimted string out of it?

```jsx
const concatenatedColors = colors.join(', ');
```

### Array.filter
How do we filter colors that start with the letter 'r'?

```jsx
const filteredColors = colors.filter(color => color.startsWith('r'));
```

DO NOT USE `Array.pop` or `Array.splice` AS THEY ARE NOT IMMUTABLE FUNCTIONS.


### Array.map

How do we edit the list to add a label called 'Color: '?

```jsx
const labeledColors = colors.map(color => `Color: ${color}`);
```

### Array.reduce

The `reduce` and `reduceRight` functions can be used to transform an array into any value, including a number, string, boolean, object, or even a function.

Let’s say we need to find the maximum number in an array of numbers. We need to transform an array into a number; therefore, we can use reduce:



```jsx
const ages = [21, 18, 42, 40, 64, 63, 34];
const maxAge = ages.reduce((max, age) => 
{
  if (age > max) 
  {
    return age;
  } 
  else 
  {
    return max;
  }
}, 0);
```

`Array.reduceRight` works the same way as Array.reduce; the difference is that it starts reducing from the end of the array rather than the beginning.

## Higher-Order Functions

## Recursion

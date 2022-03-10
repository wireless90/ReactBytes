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

## Higher-Order Functions

## Recursion

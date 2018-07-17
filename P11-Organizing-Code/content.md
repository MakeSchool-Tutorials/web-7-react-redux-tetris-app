---
title: "React Redux Tetris - Organizing Code"
slug: react-redux-tetris-organizing-code
---

Keeping files organized is important. Rather than 
clutter components with more code its a good idea
to move code to other modules and import it where 
needed. 

# Introduction 

The game will manage the game board as an array. 
Each of the blocks will also be defined as an 
array and each shape will be defined as one or 
more arrays representing the rotation of a block. 
This is a lot of arrays that need to be defined. 

Rather than clutter a component or reducer with 
all of these the goal will be to make another
file that contains functions and variables that 
are used by components. 

## Challenges

Make a new folder 'src/utils'. Add a new file 
to this folder 'src/utils/index.js'. 

The game needs to generate random numbers. 
The `Math.random()` works but we will need to 
get integers in a range. It will be good define 
a function that is easier to work with.

Add the function below to 'src/utils/index.js'.

```JavaScript
export const random = (min, max) => {
  return Math.floor(Math.random() * (max - min + 1)) + min
}
```

As the project progresses any time we need more 
general purpose code we can add it to this file, 
export, and import as needed. 

## Conclusion


## Resources

 

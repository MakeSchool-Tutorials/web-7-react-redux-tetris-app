---
title: "Organizing Code"
slug: organizing-code
---

Keeping files organized is important. Rather than
clutter components with more code, it's a good idea
to move code to other modules and import it where
needed.

# Overview of the code

Let's get a sense of the structure of our game:

- The game will manage the game board as an array.
- Each of the blocks will also be defined as an array
- Each shape will be defined as one or more arrays representing the rotation of a block.

This is a lot of arrays that need to be defined.

Rather than clutter a component or reducer with all of these the goal will be to make _another file_ that contains functions and variables that are used by components.

# Utils

The game needs to generate random numbers. The `Math.random()` works but we will need to get integers in a range. It will be good to define a function that is easier to work with.

> [action]
>
> Add a new file `/src/utils/index.js` with the following function in it:
>
```JavaScript
export const random = (min, max) => {
  return Math.floor(Math.random() * (max - min + 1)) + min
}
```

As the project progresses any time we need more
general purpose code we can add it to this file,
export, and import as needed.

# Now Commit

>[action]
>
```bash
$ git add .
$ git commit -m 'Added utils'
$ git push
```

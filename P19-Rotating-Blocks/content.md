---
title: "React Redux Tetris - Rotating Blocks"
slug: react-redux-tetris-rotating-blocks
---

Rotating blocks is a key part of game play. 

# Introduction 

Rotating blocks is an important part of game 
play. Rotation is handled by setting the 
rotation property on state. This integer
represents the index in the shapes array of 
the shape at a rotation. 

Quick review of the Array that holds the 
shapes and their rotations. Remember the 
the shapes array at the top level holds 
arrays of rotations. 

![Shapes-Array](assets/Shapes-Array.png)

At the top level the array holds the shapes. 

`[I,O,Z,T,S,J,L]`

Each of the letters above represents an Array 
of shapes. Each of these shapes is a rotation 
of the same shape. For example, in abstract. 

`[ [I, –], [O], T, Z, S, J, L]`

The first array is bar in it's two rotations, 
vertical and horizontal. 

Some shapes have a single rotation the O shape
is a square. Others have four for example J, 
and L. 

From the shapes array the actual shape is 
accessed from the shape and rotation index. 
For example: 

`shapes[shape][rotation]`

This can be observed in `GameBoard` component
in the `makeGrid()` method. 

Rotation is a property on game state in Redux. 
It's time to start working with the game reducer. 

## Challenges

**Handle 'ROTATE'**

In '.src/reducers/game-reducer.js' create a copy
of state and increment the rotation property. 

Hint, rotation can't exceed the last index of the
the rotations for that shape.

Hint: You can move the block into view by setting 
the default value for y, then clicking the rotate
button will show the rotation. 

## Conclusion


## Resources

 

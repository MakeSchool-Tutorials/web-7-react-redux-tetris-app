---
title: "Rotating Blocks"
slug: rotating-blocks
---

1. ~~Implement the overall grid square~~
1. ~~Implement the game board~~
1. ~~Implement the "next block" area~~
1. ~~Implement the score board~~
1. ~~Arrange the layout of the game~~
1. ~~Implement the controls~~
1. ~~Implement the message popup~~
1. ~~Implement the actions and reducers~~
1. ~~Do some code organizing and cleanup~~
1. ~~Implement state and shapes~~
1. ~~Connect each component up to state and reducers~~
1. **Implement block rotation**
    1. **Implement a util function to provide the next rotation of a shape**
    1. **Implement a util function that tells the game if a shape can move to a certain location**
    1. **Build out the ROTATION case in the `game-reducer`**
1. Implement moving blocks
1. Building a timer system
1. Implementing Game Over and Restart

Rotation is handled by setting the `rotation` property on `state`. This integer represents the _index in the shapes array of the shape at a rotation._

Let's do a quick review of the Array that holds the shapes and their rotations. Remember the the shapes array at the top level holds arrays of rotations.

![Shapes-Array](assets/Shapes-Array.png)

At the top level the array holds the shapes.

`[x, I, T, L, J, Z, S, O]`

(Remember `x` is the empty shape)

Each of the letters above represents an Array
of shapes. Each of these shapes is a rotation
of the same shape. For example, in abstract.

`[ [x], [I, –], [T, ...], ... ]`

We see that after the empty shape `x`, the bar array (`I`) is in it's two rotations, vertical and horizontal.

Some shapes have a single rotation, such as the `O` shape, which is a square. Others have four for example `J`, and `L`.

From the shapes array, the actual shape is accessed from the shape and rotation index. As we've seen previously:

`shapes[shape][rotation]`

# Make Some New Utils

First off, we're going to be dealing with a lot of moving blocks here. Whether we're rotating, going left, right, or down, we need to know if we can move somewhere. The game needs a function to determine if the current block can move to a new x, y, and rotation. This function will take in the shape, the grid, the x, y, and rotation, and determine if drawing the block with these options would make the block overlap the edges of the board or some placed  blocks. This function will return true if the move is possible, false if not.

Secondly, more specific to the rotation action, we need to be able to easily find the next rotation of a shape, if given the shape and its current rotation.

Both of these functions can be accomplished by making new utilities!

> [action]
>
> In `/src/utils/index.js`, add the following functions to handle the above scenarios:
>
```js
// Returns the next rotation for a shape
// rotation can't exceed the last index of the the rotations for the given shape.
export const nextRotation = (shape, rotation) => {
    return (rotation + 1) % shapes[shape].length
}
>
export const canMoveTo = (shape, grid, x, y, rotation) => {
    const currentShape = shapes[shape][rotation]
    // Loop through all rows and cols of the **shape**
    for (let row = 0; row < currentShape.length; row++) {
        for (let col = 0; col < currentShape[row].length; col++) {
            // Look for a 1 here
            if (currentShape[row][col] !== 0) {
                // x offset on grid
                const proposedX = col + x
                // y offset on grid
                const proposedY = row + y
                if (proposedY < 0) {
                    continue
                }
                // Get the row on the grid
                const possibleRow = grid[proposedY]
                // Check row exists
                if (possibleRow) {
                    // Check if this column in the row is undefined, if it's off the edges, 0, and empty
                    if (possibleRow[proposedX] === undefined || possibleRow[proposedX] !== 0) {
                        // undefined or not 0 and it's occupied we can't move here.
                        return false
                    }
                } else {
                    return false
                }
            }
        }
    }
    return true
}
```

# Handle 'ROTATE'

Let's get our rotation going:

> [action]
>
> In `/src/reducers/game-reducer.js`, include the new imports, set the props, and update the ROTATE switch case to the following:
>
```js
import {
  defaultState,
  nextRotation,
  canMoveTo } from '../utils'
>
const gameReducer = (state = defaultState(), action) => {
  const { shape, grid, x, y, rotation, nextShape, score, isRunning } = state
>
  switch(action.type) {
    case ROTATE:
      const newRotation = nextRotation(shape, rotation)
      if (canMoveTo(shape, grid, x, y, newRotation)) {
          return { ...state, rotation: newRotation }
      }
      return state
>
    ...
  }
}
```

Since no blocks are falling on the screen yet, we can't test this out quite yet, but we will soon!

# Now Commit

>[action]
>
```bash
$ git add .
$ git commit -m 'rotate reducer'
$ git push
```

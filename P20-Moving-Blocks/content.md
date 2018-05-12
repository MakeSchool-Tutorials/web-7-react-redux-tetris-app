---
title: "React Redux Tetris - Moving Block"
slug: react-redux-tetris-moving-block
---

Moving the blocks left 

# Introduction 

Moving the blocks is handled by the `x` and `y` 
properties on game state. Imagine these determine 
where the upper left corner of the next block 
box will positioned when drawing the current 
block onto  the game board grid. 

A big problem to solve with moving (and rotating
for that matter) is determining if a proposed move
is allowed. By this I mean if a block moves to
far to the left or right it should stop at the 
edge of the game board. If there are blocks 
that have been previously dropped, and the 
current block would run into them we can't allow 
this move. 

The game needs a function to determine if the 
current block can move to a new x, y, and rotation. 
This function will take in the shape, the grid, 
the x, y, and rotation, and determine if drawing 
the block with these options would make the block
overlap the edges of the board or some placed 
blocks. This function will true if the move is 
possible, false if not. 

The signature of this function might look like 
this: 

`canMoveTo(shape, grid, x, y, rotation)`

## Challenges

**Add the canMoveTo function to utils**

Add this function to './src/utils'. 

```JavaScript
// Check if a proposed move is possible.
export const canMoveTo = (shape, grid, x, y, rotation) => {
  const currentShape = shapes[shape][rotation]
  // Loop through all rows and cols of the **shape**
  for (let row = 0; row < currentShape.length; row++) {         // Loop through rows
    for (let col = 0; col < currentShape[row].length; col++) {  // Loop through cols
      if (currentShape[row][col] !== 0) {                       // Look for a 1 here
        const proposedX = col + x                               // x offset on grid
        const proposedY = row + y                               // y offset on grid
        if (proposedY < 0) {
          continue
        }
        const possibleRow = grid[proposedY]                     // Get the row on the grid 
        if (possibleRow) {                                      // Check row exists
          // Check this column in the row undefined and it's off the edges, 0 and it's empty
          if (possibleRow[proposedX] === undefined || possibleRow[proposedX] !== 0) {                         // check the contents
            return false // undefined or not 0 and it's occupied we can't move here. 
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

**Fix rotate**

It's possible for a new rotation to cause a shape to 
hit another shape or end up off the screen. The game 
should check if the new rotation is possible before 
allowing it by calling `canMoveTo()`. 

The case for 'ROTATE' in game reducer might look 
like this: 

```JavaScript
case ROTATE:
  const newRotation = nextRotation(shape, rotation)
  if (canMoveTo(shape, grid, x, y, newRotation)) {
      return { ...state, rotation: newRotation }
  }
  return state
```

**Left button**

In the game reducer the move left action should 
subtract 1 from the x and check if this new position
is possible by calling `canMoveTo()`. 

**Right button**

Adding 1 to `x` should move the block to the right. 
Do this and check if the move is possible. 

Test your work. 

Does the block staop at the edges of the grid? 
Does the rotation respect the edge of the grid? 

## Conclusion



## Resources

 

---
title: "React Redux Tetris - Moving Block"
slug: react-redux-tetris-moving-block
---

Moving the blocks left, right, and down.

# Introduction 

Moving the blocks is handled by the `x` and `y` 
properties on game state. These properties determine 
where the upper left corner of the block box will 
positioned when drawing the current block onto  the 
game board grid.

![map-shape-to-grid.png](assets/map-shape-to-grid.png)

Here `shapes[2][0]` is being mapped at x = 7 and y = 3. 

The block is defined in a 4 by 4 array. Some of these
squares are empty and some are filled. 

A big problem to solve with moving (and rotating
for that matter) is determining if a proposed move
is allowed. By this I mean if a block moves to
far to the left or right it should stop at the 
edge of the game board. If a move on the x would 
move the block past an edge this move should not be 
allowed. 

If a move would cause the block to overlap squares 
that have been placed then that move should not be 
allowed. 

In the case of a move down. If the block would hit 
the bottom of the grid or squares that have been 
placed then the block should be added to the squares
that have been placed. 

The game needs a function to determine if the 
current block can move to a new x, y, and rotation. 
This function will take in the shape, the grid, 
the x, y, and rotation, and determine if drawing 
the block with these options would make the block
overlap the edges of the board or some placed 
blocks. This function will return true if the move is 
possible, false if not.

The signature of this function might look like 
this: 

`canMoveTo(shape, grid, x, y, rotation)`

Since it returns true or false we can use it like
this: 

```
if (canMoveTo(shape, grid, x, y, rotation)) {
  // Allow the move since it is possible
} else {
  // The move is not possible 
} 
```

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
      // The shape array contains 0 and 1.
      if (currentShape[row][col] !== 0) {                       // Look for a 1 here
        // Need to offset the block to it's x and y on the grid
        const proposedX = col + x                               // x offset on grid
        const proposedY = row + y                               // y offset on grid
        // If less than 0 this off the top edge of the grid
        if (proposedY < 0) {
          // Continue skips to the next step in the loop
          continue
        }
        // Get the row array at the proposed y in the grid
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

Now you can start making use of the new `canMoveTo()` 
helper function. 

You need to use this for moving and rotating. 

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
      return { ...state, rotation: newRotation };
  }
  return state;
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

 

---
title: "React Redux Tetris - Move down and placing blocks"
slug: react-redux-tetris-moving-down-and-placing-blocks
---

Moving blocks down not only moves them down it 
is also the point where blocks are placed on
to the grid and a new block is added. 

# Introduction 

Moving down is more complex than moving left
right or rotating. When a block moves down if 
it would hit the bottom of the grid it should 
become part of the grid and be fixed in place
and the next block added to the grid at the top. 

This is also the point where the game will 
end if a new block would hit placed blocks 
when it is added. 

If a block can't move down it should be added
to the grid board array. This will happen by 
writing the shape number into grid array at 
position of the block. If a grid square is 
empty the value is 0. 

## Challenges

**Implement an Add block to grid function**

This function takes in the shape (index), grid
(array), rotation, x, and, y. The values in the 
new shape should be written into the grid. 

```JavaScript
// Adds current shape to grid
export const addBlockToGrid = (shape, grid, x, y, rotation) => {
  const block = shapes[shape][rotation]
  const newGrid = [ ...grid ]
  for (let row = 0; row < block.length; row++) {
    for (let col = 0; col < block[row].length; col++) {
      if (block[row][col]) {
        newGrid[row + y][col + x] = shape
      }
    }
  }
  return newGrid
}
```

It's important that this method create a copy of 
grid, before making any changes! 

**Scoring points**

Teris awards points when a row is completely filled
with squares. The number is greater if multiple
rows are filled. 

When the game moves a block down and it can't that 
block is placed. At this momentthe game should 
check if a row or rows have been filled. If so 
we score points. 

Implement a method that looks at the grid and 
determines of any rows are filled. 

```JavaScript
// Checks for completed rows and scores points
export const checkRows = (grid) => {
  const points = [0, 40, 100, 300, 1200]
  let completedRows = 0
  for (let row = 0; row < grid.length; row++) {
    if (grid[row].indexOf(0) === -1) {
      completedRows += 1
      grid.splice(row, 1)
      grid.unshift(Array(10).fill(0))
    }
  }
  return points[completedRows]
}
```

**Implement MOVE_DOWN in game reducer**

The 'MOVE_DOWN' action is likely the most complicated 
block of code in the game. Alot happens here. 

- Check if we can move the block down
  - if so we're done
- If block can't move down we need to place it
by doing the following. 
  - make a new copy of grid
  - add the block to the grid (`addBlockToGrid`)
  - Properties to start a new block
    - set shape to next shape
    - set nextShape to a new random shape
  - Check if the next shape can be displayed
    - If not game is over
  - Call `checkRows` to score some points
  and remove completed rows

```JavaScript
case MOVE_DOWN:
  // Get the next potential Y position
  const maybeY = y + 1
  // Check if the current block can move here
  if (canMoveTo(shape, grid, x, maybeY, rotation)) {
      // If so move the block 
      return { ...state, y: maybeY }
  }
  // If not place the block
  const newGrid = addBlockToGrid(shape, grid, x, y, rotation)
  // reset some things to start a new shape/block
  const newState = defaultState()
  newState.grid = newGrid
  newState.shape = nextShape
  newState.nextShape = randomShape()
  newState.score = score
  newState.isRunning = isRunning

  if (!canMoveTo(nextShape, newGrid, 0, 4, 0)) {
    // Game Over
    console.log("Game Should be over...")
    newState.shape = 0
    return { ...state, gameOver: true }
  }
  // Score increases decrease interval
  newState.score = score + checkRows(newGrid)

  return newState
```

## Conclusion

This should get a good portion of the game working. 
The core mechanic is now in place. The next step is 
get the blocks to move down on their own. 

## Resources

 

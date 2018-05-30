---
title: "React Redux Tetris - Game Over"
slug: react-redux-tetris-game-over
---

In Tetris you lose of the blocks stack to the top of 
the screen. 

# Introduction 

The last step is to handle Game Over. This will occur 
when the blocks reach the top of the game board. 

Let's take a closer look at game state. This describes 
how the game looks and what is happening at the moment
in the game. Game state is stored in redux as an object 
with several properties. Take a look at those properties. 

- `grid` : An array describing the game board.
This contains all of the squares that have been placed.
It does not contain the current block that you are 
controlling. 
- `shape` : The index of the current shap that you are 
controlling. The idex identifies the array of shapes 
for each rotation in the shape array. 
- `rotation` : The index of the rotation for the 
current block. 
- `x` : horizontal position of the shape you are controlling. 
- `y` : vertical position of the shape you are controlling.
nextShape : index of the next shape that will appear after 
the current shape is placed. 
- **`isRunning`** : when tru the game is running, false when the 
game is paused. 
- **`gameOver`** : true when the game is over. 
- speed : the number of milliseconds before a block is 
moved down. 
- `score` : your score

`isRunning` and `gameOver` are the two important propties for 
this discussion. 

`isRunning` is is set by the Play/Resume button. When 
`isRunning` is false the game is paused but not over. 

On the other hand when `gameOver` is true the game is over. 

The controls should not issue actions when `isRunning` is
false or `gameOver` is true. 

The move down action that forces tha game along should also 
not happen when `isRunning` is false or `gameOver` is true.

`gameOver` is set to false by default. Its gets set to true 
when the game is over. A game is over when a block is 
added to the grid and part of that block ends up off the
top edge of the grid. 

## Challenges

**Handle gameOver in the controls component**

Here you need to disable the controls when the gameOver 
property on state is false. 

Map `gameOver` to props in `mapStateToProps`. 

When the component renders get the `gameOver` property
from props. You can deconstruct props at the top of the 
function like this: 

`const { isRunning, gameOver } = this.props`

The `onClick` handler for each function should check 
`isRunning` and `gameOver`. If `isRunning` is `false`
or `gameOver` is `true` the buttons should not send actions. 

Here is an example: 

```JavaScript
<button className="control-button" onClick={(e) => {
  if (!isRunning || gameOver) { return }
  this.props.moveRight()
}}>Right</button>
```

Notice the function returns if `isRunning` is `false` 
(`!isRunning`) or (`||`) `gameOver` is `true`.

**Detecting a game over**

We can detect or game over in the `addBlockToGrid` 
function. This is in the 'utils/index'. 

The fix here is a little awkward. As it is this function 
takes the following parameters: shape, grid, x, y, rotation. 
It uses these to map the current block you controlling  
onto the grid array. The function returns a new grid array. 

This function know when the game is over when you map a
block to the grid and part of the block is off the top 
edge of the grid. 

The goal is to have the function return the new grid and 
a bool that says the game is over true or the game is not 
over false. Since we can only return one value from a 
function the return type will have to change to an object 
with two properties: `grid` and `gameOver`. 

```JavaScript
// Adds current shape to grid
export const addBlockToGrid = (shape, grid, x, y, rotation) => {
  let blockOffGrid = false
  const block = shapes[shape][rotation]
  const newGrid = [ ...grid ]
  for (let row = 0; row < block.length; row++) {
    for (let col = 0; col < block[row].length; col++) {
      if (block[row][col]) {
        const yIndex = row + y
        // If the yIndex is less than 0 part of the block
        // is off the top of the screen and the game is over
        if (yIndex < 0) {
          blockOffGrid = true
        } else {
          newGrid[row + y][col + x] = shape
        }
      }
    }
  }
  // Return both the newGrid and the gameOver bool                                                
  return { grid: newGrid, gameOver: blockOffGrid }
}
```

Changing this will mean changes to the reducer and the 
MOVE_DOWN case where this method is called. 

**Modify the game-reducer**

Here you'll want to modify the MOVE_DOWN case. 

```JavaScript
case MOVE_DOWN:
  // Get the next potential Y position
  const maybeY = y + 1

  // Check if the current block can move here
  if (canMoveTo(shape, grid, x, maybeY, rotation)) {
      // If so move down don't place the block
      return { ...state, y: maybeY }
  }

  // If not place the block
  // (this returns an object with a grid and gameover bool)
  const obj = addBlockToGrid(shape, grid, x, y, rotation)
  const newGrid = obj.grid
  const gameOver = obj.gameOver

  if (gameOver) {
    // Game Over
    const newState = { ...state }
    newState.shape = 0
    newState.grid = newGrid
    return { ...state, gameOver: true }
  }

  // reset somethings to start a new shape/block
  const newState = defaultState()
  newState.grid = newGrid
  newState.shape = nextShape
  newState.nextShape = randomShape()
  newState.score = score
  newState.isRunning = isRunning
  console.log(state)
  console.log(newState)


  // TODO: Check and Set level
  // Score increases decrease interval
  newState.score = score + checkRows(newGrid)

  return newState
```

Here there are three exit points. 

The first if statement exits by **returning** new state 

## Conclusion


## Resources

 

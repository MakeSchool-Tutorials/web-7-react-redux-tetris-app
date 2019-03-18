---
title: "Game Over and Restart"
slug: game-over-and-restart
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
1. ~~Implement block rotation~~
1. ~~Implement moving blocks~~
1. ~~Building a timer system~~
1. **Implementing Game Over and Restart**
    1. **Handle the behavior of Controls in relation to the game over state**
    1. **Handle the game over state in the `addBlockToGrid` function to know if the blocks are off the screen**
    1. **Modify `game-reducer` to handle the game over state**
    1. **Modify `game-reducer` to handle the restart state**

If the blocks stack to the top of the screen, it's game over. We need to make sure we can handle this state.

Let's take a closer look at `state`:

- `grid` : An array describing the game board. This contains all of the squares that have been placed. It does not contain the current block that you are controlling.
- `shape` : The index of the current shape that you are controlling. The index identifies the array of shapes for each rotation in the shape array.
- `rotation` : The index of the rotation for the current block.
- `x` : horizontal position of the shape you are controlling.
- `y` : vertical position of the shape you are controlling.
- `nextShape` : index of the next shape that will appear after
the current shape is placed.
- **`isRunning`** : when true, the game is running, false when the
game is paused.
- **`gameOver`** : true when the game is over.
- `speed` : the number of milliseconds before a block is moved down.
- `score` : your score

`isRunning` and `gameOver` are the two important properties for
this discussion, let's go over the basic rules of these properties:

- `isRunning` is is set by the Play/Resume button. When `isRunning` is false, the game is paused but not over.
- On the other hand when `gameOver` is true the game is over.
- The controls should not issue actions when `isRunning` is
false or `gameOver` is true.
- The move down action that forces the game along should also
not happen when `isRunning` is false or `gameOver` is true.
- `gameOver` is set to false by default. It gets set to true
when the game is over.
- A game is over when a block is added to the grid and part if that block ends up off the top edge of the grid.

# Handle gameOver in the controls component

Here you need to disable the controls when the `gameOver`
property on `state` is false.

> [action]
>
> Map `gameOver` to props in `mapStateToProps` in `/src/components/controls.js`:
>
```js
const mapStateToProps = (state) => {
  return {
    isRunning: state.game.isRunning,
    gameOver: state.game.gameOver
  }
}
```

The `onClick` handler for each function should check
`isRunning` and `gameOver`. If `isRunning` is `false`
or `gameOver` is `true` the buttons should not send actions.

> [action]
>
> Update all of the `button` elements in the `render` method of `/src/components/controls.js` to check `isRunning` and `gameOver`. Also make sure to extract the `gameOver` property from `props`:
>
```js
render() {
    const { isRunning, gameOver } = this.props
>
...
>
    // for all the below, Notice the function returns if `isRunning` is `false` (`!isRunning`), or (`||`) `gameOver` is `true`.
    <div className="controls">
        {/* left */}
        <button className="control-button" onClick={(e) => {
            console.log(isRunning, gameOver)
            if (!isRunning || gameOver) { return }
            this.props.moveLeft()
        }}>Left</button>
>
        {/* right */}
        <button className="control-button" onClick={(e) => {
            if (!isRunning || gameOver) { return }
            this.props.moveRight()
        }}>Right</button>
>
        {/* rotate */}
        <button className="control-button" onClick={(e) => {
            if (!isRunning || gameOver) { return }
            this.props.rotate()
        }}>Rotate</button>
>
        {/* down */}
        <button className="control-button" onClick={(e) => {
            if (!isRunning || gameOver) { return }
            this.props.moveDown()
        }}>Down</button>
    </div>
>
...
>
}
```

# Detecting a game over

We can detect a game over in the `addBlockToGrid`
function `utils/index.js`

The `addBlockToGrid()` function adds a block to the grid. If part of the block ends up off the top the grid the game is over.

The goal is to have the function return the new grid and a bool that says the game is over (true) or the game is not over (false). Since we can only return one value from a function, the return type will have to change to an object with two properties: `grid` and `gameOver`.

> [action]
>
> In `/src/utils/index.js`, update `addBlockToGrid` to the following:
>
```JavaScript
// Adds current shape to grid
export const addBlockToGrid = (shape, grid, x, y, rotation) => {
  // At this point the game is not over
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

# Modify the game-reducer

> [action]
>
> Modify the MOVE_DOWN case for `/src/reducers/game-reducer.js`:
>
```JavaScript
case MOVE_DOWN:
  // Get the next potential Y position
  const maybeY = y + 1
>
  // Check if the current block can move here
  if (canMoveTo(shape, grid, x, maybeY, rotation)) {
      // If so move down don't place the block
      return { ...state, y: maybeY }
  }
>
  // If not place the block
  // (this returns an object with a grid and gameover bool)
  const obj = addBlockToGrid(shape, grid, x, y, rotation)
  const newGrid = obj.grid
  const gameOver = obj.gameOver
>
  if (gameOver) {
    // Game Over
    const newState = { ...state }
    newState.shape = 0
    newState.grid = newGrid
    return { ...state, gameOver: true }
  }
>
  // reset somethings to start a new shape/block
  const newState = defaultState()
  newState.grid = newGrid
  newState.shape = nextShape
  newState.score = score
  newState.isRunning = isRunning
>
  // TODO: Check and Set level
  // Score increases decrease interval
  newState.score = score + checkRows(newGrid)
>
  return newState
```

Try to force a game over and make sure you see the popup:

![gameover](assets/gameover.png)

Almost done! One more feature and we've got a full Tetris game!

# Now Commit

>[action]
>
```bash
$ git add .
$ git commit -m 'game over implemented'
$ git push
```

# Restart Game-Reducer

Now that the game knows when it's ended, we need a way to restart it!

Restarting the game will only require setting the game `state` in redux back to default, and there already is a function for this!

> [action]
>
> Return default state with a call to `defaultState()` in the `RESTART` case in `/src/reducers/game-reducer.js`:
>
```js
case RESTART:
    return defaultState()
```

Try pressing the restart button and make sure it starts the game from a clean slate.

# Now Commit

>[action]
>
```bash
$ git add .
$ git commit -m 'restart implemented'
$ git push
```

You now have a fully functioning Tetris game! Congrats!

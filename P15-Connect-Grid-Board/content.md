---
title: "React Redux Tetris - Connect Grid Board"
slug: react-redux-tetris-connect-grid-board
---

Display the grid board from state. This is the core rendering
feature of the game. 

# Introduction 

The `GridBoard` component displays an array of `GridSquare`s. 
It will also map the current shape block at it's rotation into 
this grid at the x, and y. 

Tapping the left, right, rotate, down buttons update game state 
which in turn triggers this component to update. Updates are 
also generated as the timer triggers move down actions. 

## Challenges

**Import connect**

You need to connect the component to Redux to do this you 
need `connect` from 'react-redux'.

Import `connect` from 'react-redux' at the top of the `GridBoard`
component. 

**Map state to props**

Define a `mapStateToProps` method. This method takes in state 
as a parameter. 

Return an object that maps the following properties from state 
to these props: 

```JavaScript
grid: state.game.grid,
shape: state.game.shape,
rotation: state.game.rotation,
x: state.game.x,
y: state.game.y,
speed: state.game.speed,
isRunning: state.game.isRunning
```

This component will issue `MOVE_DOWN` actions. It needs to call 
on the `moveDown` action. 

**Map dispatch to props**

Import the `moveDown` action and map it to props. 

Add a `mapDispatchToProps` method that returns an Object 
containing the actions issued by this component. 

**Connect the component**

Use the connect method to connect `mapStateToProps`, 
`mapDispatchToProps` and the `GridBoard` component. 

**Mapping the Grid to GridSquares**

Previously the grid was mocked up. Now it's time to 
get the grid data from props and map to the grid. You need to 
replace the current that generates the mocked up grid in this 
step.

The `makeGrid()` method is responsible for this. 
`Array.map` is a good tool here since we want to 
transform the integer values into Grid Squares of a 
color. 

The source Grid is two dimensional the ouput Grid will 
just be one dimensional. Use `Array.map()` to map 
across all rows, inside use `Array.map()` again to map
across each column. Inside this second map function
generate Grid Squares. 

Let's go over that again. You need to map the row arrays
then map each row to get the value at each column. 

The value is an integer representing the color of each 
square.

Next you'll need to map the shape on to the grid. The 
shape is represented by an integer value. 

When Grid Squares are created find the color for the 
square by looking at the shape array. If there is a 1
in the shape array use the shape index as the color. 

```JavaScript
makeGrid() {
  const { grid, shape, rotation, x, y } = this.props
  const block = shapes[shape][rotation]
  const blockColor = shape
  // map rows
  return grid.map((rowArray, row) => {
    // map columns
    return rowArray.map((square, col) => {
      // Find the block x and y on the shape grid
      const blockX = col - x
      const blockY = row - y
      let color = square
      // Map current falling block to grid. 
      if (blockX >= 0 && blockX < block.length && blockY >= 0 && blockY < block.length) {
        color = block[blockY][blockX] === 0 ? color : blockColor
      }
      // Generate a unique key for every block
      const k = row * grid[0].length + col;
      // Generate a grid square
      return <GridSquare
              key={k}
              square={square}
              color={color}>{square}
            </GridSquare>
    })
  })
}
```

This should generate the main grid for the game and 
map a random shape to it. The default x and y position 
of this shape is 5, -4 so the shape by default is above
the top of the screen! 

You can make the shape visible by setting the default 
value for y to a positive number like 4. 

## Conclusion


## Resources

 

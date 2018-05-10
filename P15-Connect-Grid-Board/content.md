---
title: "React Redux Tetris - Connect Grid Board"
slug: react-redux-tetris-connect-grid-board
---

Display the grid board from state

# Introduction 

The grid board component display the array of grid. 
It will also map the current shape block into this 
grid at the x, y, and rotation. 

This component will also be responsible for updating 
the game over time. It will have a timer that moves 
the current block down at regular intervals. 

## Challenges

**Import connect**

**Map state to props**

Map the following properties from state to props: 

```JavaScript
grid: state.game.grid,
shape: state.game.shape,
rotation: state.game.rotation,
x: state.game.x,
y: state.game.y,
speed: state.game.speed,
isRunning: state.game.isRunning
```

**Map dispatch to props**

Import the `moveDown` action and map it to dispatch. 

**Connect the component**

Use the connect method to connect `mapStateToProps`, 
`mapDispatchToProps` and the `GridBoard` component. 

**Mapping the Grid to GridSquares**

Previously the grid was mocked up. Now it's time to 
get the grid data from props and map to the grid. 

The `makeGrid()` method is responsible for this. 
`Array.map` is a good tool here since we want to 
transform the integer values into Grid Squares of a 
color. 

The source Grid is two dimensional the ouput Grid will 
just be one dimensional. Use `Array.map()` to map 
across all rows, inside use `Array.map()` again to map
across each column. Inside this second map function
generate Grid Squares. 

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

 

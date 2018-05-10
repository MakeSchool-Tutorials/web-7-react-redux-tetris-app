---
title: "React Redux Tetris - Displaying Game State"
slug: react-redux-tetris-displaying-game-state
---

Connecting game state to components. 

# Introduction 

With default game state defined it's time to connect 
game state to components. 

The goal here is to get the index of the next block, 
this is `game.nextShape` on state. Use this to find 
the array that represents this shape, at the first 
rotation, and map it to the grid. 

The color will be set by the same index value.

To get state from Redux into this Component you'll
need to connect the component with React-Redux. 

## Challenges

**Import connect**

`import { connect } from 'react-redux'`

**Map State to Props**

```JavaScript
// Map State to props
const mapStateToProps = (state) => {
  return {
    // Return nextShape as shape
    shape: state.game.nextShape
  }
}
```

**Connect component**

`export default connect(mapStateToProps)(NextBlock)`

**Mape the block shape into the grid**

```JavaScript
makeGrid() {
  const { shape } = this.props    // deconstruct shape
  const block = shapes[shape][0]  // get the array for this shape first rotation
  const box = shapes[0][0]        // get the empty shape

  // Map the block to the grid
  return box.map((rowArray, row) => {
    return rowArray.map((square, col) => {
      const color = block[row][col] === 0 ? 0 : shape // If there is a 1 use the shape index
      return <GridSquare key={`${row}${col}`} color={color} />
    })
  })
}
```

A block should draw itself into the next block grid. 
Since the next block is chosen randomly refreshing the 
page should redraw a random block. 

## Conclusion


## Resources

 

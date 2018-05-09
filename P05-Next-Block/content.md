---
title: "React Redux Tetris - Next Block"
slug: react-redux-tetris-next-block
---

Tetris shows you the next block that will appear to 
the side of the game grid. This section makes a component 
for this purpose. 

# Introduction 

The next block will be displayed in a component that will 
draw itself as a 4 by 4 grid of grid squares. 

## Challenges

Make a new component: './src/components/next-block.js'.

Define the component like this: 

```jsx
import React, { Component } from 'react'
import GridSquare from './grid-square'

// Draws the "next" block view showing the next block to drop

class NextBlock extends Component {

  makeGrid() {
    const box = [[0,0,0,0], [0,0,0,0], [0,0,0,0], [0,0,0,0]]
    // Map the block to the grid
    return box.map((rowArray, row) => {
      return rowArray.map((square, col) => {
        return <GridSquare key={`${row}${col}`} color={0} />
      })})
    }

  render () {

    return (
      <div className="next-block">
        {this.makeGrid()}
      </div>
    )
  }
}
```

Add some styles to arrange these into a grid. 

```css
/* Next Block */
.next-block {
  display: grid;
  grid-template-columns: repeat(4, var(--tile-size));
  align-self: flex-start;
}
```

At this point the page is lacking arranement but the tiles 
in each component are arranged in a grid. 

You will CSS grid to arrange the page after we add a couple
more elements. 

## Conclusion 



## Resources

- 

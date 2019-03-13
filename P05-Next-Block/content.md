---
title: "Next Block"
slug: next-block
---

Tetris shows you the next block that will appear to
the side of the game grid. This section makes a component
for this purpose.

The **next block** will be displayed in a component that will
draw itself as a 4 by 4 grid of grid squares. We will reuse the
grid square component here.

You might visualize the array that describes the next block
like this:

![Next-Block-Array](assets/Next-Block-Array.png)

It's just like the Grid Board array only smaller with
4 rows and 4 columns!

# Make the Next Block Component

> [action]
>
> Make a new component `/src/components/next-block.js` and add the following code to it:
>
```js
import React, { Component } from 'react'
import GridSquare from './grid-square'
>
// Draws the "next" block view showing the next block to drop
class NextBlock extends Component {
>
  makeGrid() {
    const box = [[0,0,0,0], [0,0,0,0], [0,0,0,0], [0,0,0,0]]
    // Map the block to the grid
    return box.map((rowArray, row) => {
      return rowArray.map((square, col) => {
        return <GridSquare key={`${row}${col}`} color={0} />
      })})
    }
>
  render () {
    return (
      <div className="next-block">
        {this.makeGrid()}
      </div>
    )
  }
}
```

# Add styles for the Next Block

Add some styles to arrange these into a grid.

> [action]
>
> Add the following to `/src/index.css`:
```css
/* Next Block */
.next-block {
  display: grid;
  grid-template-columns: repeat(4, var(--tile-size));
  align-self: flex-start;
}
```

At this point the page is lacking arrangement but the tiles
themselves in each component are arranged in a grid.

Also notice the GridSquares are using the default color 0 in the `Next Block` component. We will get the block shape as an array later and use this to set the color of the blocks.

We won't export and display this for now, as there's still some work to be done on this component before we can view it in the browser.

# Now Commit

>[action]
>
```bash
$ git add .
$ git commit -m 'Added initial next block'
$ git push
```

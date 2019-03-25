---
title: "Next Block"
slug: next-block
---

1. ~~Implement the overall grid square~~
1. ~~Implement the game board~~
1. **Implement the "next block" area**
    1. **Build the next block component**
    1. **Add style to the component**
    1. **Add the component to `App.js`**
1. Implement the score board
1. Arrange the layout of the game
1. Implement the controls
1. Implement the message popup
1. Implement the actions and reducers
1. Do some code organizing and cleanup
1. Implement state and shapes
1. Connect each component up to state and reducers
1. Implement block rotation
1. Implement moving blocks
1. Building a timer system
1. Implementing Game Over and Restart

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
>
export default NextBlock
```

# Add styles for the Next Block

Add some styles to arrange these into a grid.

> [action]
>
> Add the following to `/src/index.css`:
>
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

# Add to App.js

Let's see what we have so far:

> [action]
>
> Add the following to `/src/App.js`:
>
```js
import React, { Component } from 'react';
>
import GridBoard from './components/grid-board'
[bold]import NextBlock from './components/next-block'[/bold]
>
import './App.css';
>
class App extends Component {
  render() {
    return (
      <div className="App">
        <header className="App-header">
          <h1 className="App-title">Tetris Redux</h1>
        </header>
        <GridBoard />
[bold]        <NextBlock />[/bold]
      </div>
    );
  }
}
>
export default App;
```

# Product So Far

You should see the following in your browser:

![initial-next-block](assets/initial-next-block.png)

Doesn't look amazing right now, but we'll spruce it up in future chapters. For now, we've gotten some practice with **using functional programming methods like `map`!**

# Now Commit

>[action]
>
```bash
$ git add .
$ git commit -m 'Added initial next block'
$ git push
```

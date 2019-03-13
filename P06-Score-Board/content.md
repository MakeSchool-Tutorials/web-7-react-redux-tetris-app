---
title: "Tetris Score Board"
slug: tetris-score-board
---

We need a score board to show the game score and
provide a place for the play and pause buttons
to live.

The scoreboard when completed will display on the
right side of the game board.

![score-board](assets/score-board.png)

Some requirements for the score board:

- The score board component will display the game score.
- As blocks are placed when a row is filled with colored squares, the game scores points.
- The game also needs a button to pause game play and restart the game.
- As the game progresses you can speed up game play or make it
more difficult in other ways for the current level.
- The component added in this chapter will give these previously described elements a place to live.



# Create the ScoreBoard Component

> [action]
>
> Make a new file: `/src/components/score-board.js` with the following code:
>
```js
import React, { Component } from 'react'
>
class ScoreBoard extends Component {
>
  render() {
    return (
      <div className="score-board">
        <div>Score:{ this.props.score }</div>
        <div>Level: 1</div>
>
        <button className="score-board-button" onClick={(e) => {
>
        }}>Play</button>
>
        <button className="score-board-button" onClick={(e) => {
>
        }}>Restart</button>
>
      </div>
    )
  }
}
>
export default ScoreBoard
```

Now we can define some styles for these elements. No need to worry about
the text, we'll just focus on the buttons for now.

> [action]
>
> Add the following to `/src/index.css`
>
```css
/* Score Board */
.score-board-button {
  padding: 0;
  display: block;
  padding: 1em;
  border-width: 5px;
  border-top-color: var(--button-color-t);
  border-left-color: var(--button-color-l);
  border-right-color: var(--button-color-r);
  border-bottom-color: var(--button-color-b);
}
```

Notice we used the CSS variables again!

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
import NextBlock from './components/next-block'
[bold]import ScoreBoard from './components/score-board'[/bold]
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
        <NextBlock />
[bold]        <ScoreBoard />[/bold]
      </div>
    );
  }
}
>
export default App;
```

You should see the following in your browser:

![initial-scoreboard](assets/initial-scoreboard.png)

This needs work, but we will take care the details later. For now this is a solid start.

# Now Commit

>[action]
>
```bash
$ git add .
$ git commit -m 'Added initial score board'
$ git push
```

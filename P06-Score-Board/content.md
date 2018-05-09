---
title: "React Redux Tetris - Score Board"
slug: react-redux-tetris-score-board
---

We need a score board to show the game score and 
provide a place for the play and pause buttons 
to live. 

# Introduction 

The score board component will display the game 
score. This will also give us a place to place 
the play pause buttons. 

## Challenges

Make a new file: './src/components/score-board.js'.

Setup the component: 

```jsx
import React, { Component } from 'react'

class ScoreBoard extends Component {

  render() {
    return (
      <div className="score-board">
        <div>Score:{ this.props.score }</div>
        <div>Level: 000</div>

        <button className="score-board-button" onClick={(e) => {

        }}>Play</button>


        <button className="score-board-button" onClick={(e) => {

        }}>Restart</button>

      </div>
    )
  }
}

export default ScoreBoard
```

Might as well style some of this. No need to worry about the 
text now focus on the buttons. 

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

This needs work but we can take care the details later. 
For now this is good. 

## Conclusion 



## Resources

 
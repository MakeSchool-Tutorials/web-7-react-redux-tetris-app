---
title: "React Redux Tetris - Connect Score Board"
slug: react-redux-tetris-connect-score-board
---

Connect the score board component. 

# Introduction 

The score board component shows the current score. 
It also has a play and restart button. 

The play button should toggle it's text from 'Play'
to 'Pause' as the game changes state. 

## Challenges

**Import Connect**

Import `connect` from 'react-redux'.

**Import Actions**

Import the `pause`, `resume`, `restart` actions. 

**Map State to Props**

Map the `score`, `isRunning`, `gameOver` from state 
to props. 

**Map Dispatch to Props**

Map the `pause`, `resume`, and `restart` actions to 
the dispatcher.

**Pause/Play button**

Use the following logic to handle the text of the 
Play/Pause button. 

- If `isRunning` is `true` the button text should show
'Pause'.
- If `isRunning` is `false` the button text should show
'Play'. 

Use the following logic to handle clicks on the button. 

- If `gameOver` is `false` exit without any action, 
otherwise if `isRunning` is `true` call `this.props.pause()`
otherwise call `this.props.resume()`. 

**Restart Button**

Clicking this button should call `this.props.restart()`.

## Conclusion


## Resources

 

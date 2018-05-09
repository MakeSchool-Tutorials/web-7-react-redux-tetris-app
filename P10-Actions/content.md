---
title: "React Redux Tetris - Actions"
slug: react-redux-tetris-actions
---

The game will use Redux to store the state of the application. 
The game board, the next block, whether the game is playing or 
paused, and the game score are all application state. 

# Introduction 

The game will respond to a range of actions. You need to 
define each action. Actions will be handled by various 
different components but this won't effect how we define 
actions since React-Redux will connect actions to any 
component. 

**Game Meta**
These actions handle running the game. 

- Pause : Paues the game 
- Resume : Resumes the game 
- Restart : Restarts the game

**Game Play**
These actions work with the player controls to move the block.

- Move Left : Moves the current block left
- Move Right : Moves the current block right 
- Move Down : Moves the current block down
- Rotate : Rotates the current block

**Game Automation**
These actions are issued by the game periodically as play 
progreses. Note: Move Down can be issued by the player or
the game. 

- Move Down
- Set Next
- Game Over 

## Challenges

Make a new file: './actions/index.js'. 

Define some actions: 

```JavaScript
export const PAUSE      = "PAUSE"       // Pause the game
export const RESUME     = "RESUME"      // Resume a paused game
export const MOVE_LEFT  = "MOVE_LEFT"   // Move piece left
export const MOVE_RIGHT = "MOVE_RIGHT"  // Move piece right
export const ROTATE     = "ROTATE"      // Rotate piece
export const MOVE_DOWN  = "MOVE_DOWN"   // Move piece down
export const SET_NEXT   = "SET_NEXT"    // ???
export const GAME_OVER  = "GAME_OVER"   // The game is over
export const RESTART    = "RESTART"     // Restart Game
```

Then define an action creator for each action.

```JavaScript
export const setNext = () => {
  return { type: SET_NEXT }
}

export const moveRight = () => {
  return { type: MOVE_RIGHT }
}

export const moveLeft = () => {
  return { type: MOVE_LEFT }
}

export const rotate = () => {
  return { type: ROTATE }
}

export const moveDown = () => {
  return { type: MOVE_DOWN }
}

export const pause = () => {
  return { type: PAUSE }
}

export const resume = () => {
  return { type: RESUME }
}

export const restart = () => {
  return { type: RESTART }
}
```

In many applications you'll need to pass parameters to 
action creators and action objects will need to 
incorporate data in a payload. The game is simple in it's
use of data. All of the data is handled and stored in the 
Redux store, all the actions need only pass the type. 

Define a reducer to handle actions. 

Make a new file '.src/reducers/game-reducer.js'. 

```JavaScript
import {
  SET_NEXT,
  MOVE_RIGHT, MOVE_LEFT, MOVE_DOWN, ROTATE,
  PAUSE, RESUME, RESTART, GAME_OVER
} from '../actions'

const gameReducer = (state = {}, action) => {

  switch(action.type) {
    case ROTATE:

      return state

    case MOVE_RIGHT:

      return state

    case MOVE_LEFT:

      return state

    case MOVE_DOWN:

      return state

    case RESUME:

      return state

    case PAUSE:

      return state

    case GAME_OVER:

      return state

    case RESTART:
    
      return state

    default:
      return state
  }
}

export default gameReducer
```

This is a stub for the final implementation. So far it 
imports the actions and defines and exports the 
`gameReducer` method. 

There is a lot of work to do here. Currently all cases 
return state unchanged. The entire game state will be 
handled by a single Object which will pass through 
this reducer and each case will be responsible for making 
changes to state and returing a copy of state. 

Reducers are responsible for defining the initial value 
for state. Currently the stub method sets the default 
value of state to an empty object `{}`. 

## Conclusion



## Resources

 

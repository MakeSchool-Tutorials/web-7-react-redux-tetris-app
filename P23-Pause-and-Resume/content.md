---
title: "React Redux Tetris - Pause and Resume"
slug: react-redux-tetris-pause-and-resume
---

We might need to pause the game and resume it later. 

# Introduction 

The game already implements a Pause and Resume buttons. 
At this point they don't do anything. The game state 
has an `isRunning` property for this purpose. 
 
## Challenges

**Implement the Play Resume  button**

The button already calls the action. The reducer needs
to handle the action. 

The RESUME action in game-reducer needs to set 
isRunning to true. 

The PAUSE action in the game-reducer needs to set 
isRunning to false. 

## Conclusion


## Resources

 

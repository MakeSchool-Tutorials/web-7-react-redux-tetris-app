---
title: "React Redux Tetris - Connect Controls"
slug: react-redux-tetris-connect-controls
---

Connect the controls to actions. The controls allow 
the game to be played. Tapping the leftm, right, and
down buttons move the block. Tapping the rotate button
changes the rotation of the block. 

# Introduction 

Controls need to issue actions to control the game. 
You'll need to connect this component to state so it 
can issue actions that move the block. 

This works by sending actions that change state updating
the x, y, and rotation values. Changing these updates 
components that use these values as props. 

We can also use the `isRunning` to control the display 
of the buttons. Imagine the case where the came is paused. 
In this case we might want the buttons to display as 
disabled. It might be a good idea to map `isRunning` to 
props on this component. 

## Challenges

**Import Actions**

Import the `moveDown, moveLeft, moveRight, rotate` actions.

**Map state to props**

Map the `isRunning` property from state to props. This can be 
used to enable and disable the buttons as the game runs. 

**Map Dispatch to Props**

Define the `mapDispatchToProps` with the actions you imported. 

**Connect this component**

Connect this component with the `mapStateToProps` and 
`mapDispatchToProps`. 

**Call Actions**

The buttons in this component just call actions from 
props with no params. Set that up now. 

Actions should only be sent if the `isRunning` is true. 

```JSX
<button className="button"
  onMouseDown={(e) => {
    if (!isRunning) { return }
    this.props.moveDown()
  }}>Down</button>
```

Make the Left, Right, and Rotate buttons work the same. 

## Conclusion


## Resources

 

---
title: "React Redux Tetris - Connect Controls"
slug: react-redux-tetris-connect-controls
---

Connect the controls to actions.

# Introduction 

Controls need to issue actions to control the game. 

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

 

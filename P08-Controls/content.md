---
title: "React Redux Tetris - Controls"
slug: react-redux-tetris-controls
---

Tetris has a couple controls. Blocks can be moved left right 
and down, blocks can also be rotated. 

The original game used a joystick and button. This game will use 
four buttons.

# Introduction 

The next step is to create a component with four buttons. These 
buttons will all issue actions. 

Notice that using Redux/React-Redux we can easily connect a 
component make changes to application state. Without Redux 
It would be important to understand this components relationship 
to other components. In this case it is unimportant since we 
need only send an action to the dispatcher. 

## Challenges

Make a new component to hold the buttons. Make a new file
'./src/components/controls.js'. The following stubs in the 
the controls component class. 

```JSX
import React, { Component } from 'react'

class Controls extends Component {

  render() {
    return (
      <div className="controls">
        {/* left */}
        <button className="control-button" onClick={(e) => {

        }}>Left</button>

        {/* right */}
        <button className="control-button" onClick={(e) => {

        }}>Right</button>

        {/* rotate */}
        <button className="control-button" onClick={(e) => {

        }}>Rotate</button>

        {/* down */}
        <button className="control-button" onClick={(e) => {

        }}>Down</button>

      </div>
    )
  }
}

export default Controls
```

Add some new styles for the controls in './src/index.css'.

Add some styles for the controls. These will style the controls
container. 

```CSS
/* controls */
.controls {
  grid-area: b;
  display: flex;
  flex-direction: row;
}
```

The controls container will use Flex Box for layout. Flex Box is 
a one dimensional layout. All of the buttons in the controls 
container are arranged in a horizontal row along a single axis. 

Notice the `grid-area` is set to `b`. This was a grid are we had 
defined in the previous section. 

Now define some styles for the control buttons. 

```CSS
control-button {
  --size: calc(var(--tile-size) * 2.5);
  width: var(--size);
  height: var(--size);
  text-align: center;
  display: block;
  border-width: 5px;
  border-top-color: var(--button-color-t);
  border-left-color: var(--button-color-l);
  border-right-color: var(--button-color-r);
  border-bottom-color: var(--button-color-b);
}
```

These buttons are styled very similarly to play and reset buttons. 
Since they use the same CSS custom properties we can set the styles 
on all buttons on the page. 

I wanted the buttons to be square with a width of 25% of grid board. 
The grid is 10 tiles wide, so the size of the buttons is 2.5 * tile
size. 

Add the controls to the App component. 

Import the new component at the top of `.src/App.js`. 

`import Controls from './components/controls'`

Then add the new component in the render method. 

`<Controls />`

## Conclusion 



## Resources

 

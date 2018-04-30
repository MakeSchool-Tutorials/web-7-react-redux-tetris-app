---
title: "React Redux Tetris - "
slug: react-redux-tetris-
---

The game board is played on a grid. In this section you will 
make component that represents a grid square. 

# Introduction 

React uses a component based architecture. Everything is a 
component. 

Breaking components down into smaller and more granular 
components is usually the best strategy with React. 

In Tetris the game is played on a grid. We will make a grid 
square component, when we make the game grid it will be made
of many grid squares. 

## Challenges

Make a new component: 'src/components/grid-square.js'

```jsx
import React, { Component } from 'react'

// Represents a grid square with a color

class GridSquare extends Component {

  render () {
    const classes = `grid-square color-${this.props.color}`
    return <div className={classes} />
  }
}

export default GridSquare
```

The GridSquare is just a div with some class names. In this 
case: 

- `grid-square` : This will define default grid square properties
- `color-${this.props.color}` : The color of the square will be 
passed as props.

## Resources

- 

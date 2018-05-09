---
title: "React Redux Tetris - "
slug: react-redux-tetris-
---

The game board is played on a grid. In this section you will 
make a component that represents a single grid square. 

# Introduction 

React uses a component based architecture. Everything you see 
in the browser is a component. 

Breaking components down into smaller and more granular 
components is usually the best strategy with React. 

In Tetris the game is played on a grid. We will make a grid 
square component, when we make the game grid it will be made
of many grid squares. 

Each component for game will require CSS styles. The 
components used in this project will not have much use 
outside which makes keeping all of the styles in a single 
stylesheet more convenient. 

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

## Define some CSS

Thsi project will store all of it's styles in 'index.css'. The 
components in the project are not portable, they would find 
little use outside of this project. 

By keeping all of the styles in one place it will make for a 
large body of CSS code. To keep this as DRY as possible we can 
use CSS custom properties. 

Define some properties for the colors and sizes used. 

```css
:root {
  --bg-color: rgba(150, 150, 150, 1);
  
  /* Border Colors */
  --border-left-color: rgba(255, 255, 255, 0.20);
  --border-top-color: rgba(255, 255, 255, 0.33);
  --border-right-color: rgba(0, 0, 0, 0.15);
  --border-bottom-color: rgba(0, 0, 0, 0.5);

  /* Square Colors */
  --color-0: #eaeaea;
  --color-1: #ff6600;
  --color-2: #eec900;
  --color-3: #0000ff;
  --color-4: #cc00ff;
  --color-5: #00ff00;
  --color-6: #66ccff;
  --color-7: #ff0000;

  /* Button Colors */
  --button-color-t: rgba(200, 200, 200, 1);
  --button-color-r: rgba(150, 150, 150, 1);
  --button-color-b: rgba(120, 120, 120, 1);
  --button-color-l: rgba(222, 222, 222, 1);

  /* Numbers */
  --cols: 10;
  --rows: 18;
  --tile-size: 20px;
  --border-width: 5px;
}
```

The **Border Colors** are all transparent colors. These will 
tint or shade the background color of the square. 

The **Square Colors** are the background colors for the 
squares. 

The **Numbers** define values that will be used throughout 
the CSS, `--tile-size: 20px` for example will set size of 
the grid squares.

**Color Classes**

The colors will applied to grid squares as classes. 
Define some color classes. CSS variables set above are 
used here. 

```css
/* Colors */
.color-0 {
  background-color: var(--color-0);
}

.color-1 {
  background-color: var(--color-1);
}

.color-2 {
  background-color: var(--color-2);
}

.color-3 {
  background-color: var(--color-3);
}

.color-4 {
  background-color: var(--color-4);
}

.color-5 {
  background-color: var(--color-5);
}

.color-6 {
  background-color: var(--color-6);
}

.color-7 {
  background-color: var(--color-7);
}
```

Define the appearance of a grid square. 

```css
/* Grid Square */
.grid-square {
  border-style: solid;
  width: var(--tile-size);
  height: var(--tile-size);
  border-width: var(--border-width);
  border-left-color: var(--border-left-color);
  border-top-color: var(--border-top-color);
  border-right-color: var(--border-right-color);
  border-bottom-color: var(--border-bottom-color);
}
```

That might seem like a lot of styles but much of what is 
there will be reused in future styles. Allow us to easily 
change sizes and colors in a single place at the top of
the style sheet. 

## Test a Grid Sqaure

Import './components/grid-square' at the top of 'App.js'
and add the component within render. 

`<GridSquare color="1" />`

Setting the color to 1 should display an orange square. 

Try some other values. 

## conclusion



## Resources

- 

---
title: "React Redux Tetris - Grid"
slug: react-redux-tetris-grid
---

In this section you will make a component that represents a single 
grid square. The game board is played on a grid made up of grid 
squares. 

# Introduction 

React uses a component based architecture. Everything you see 
rendered in the browser is a component. 

Breaking components down into smaller and more granular 
components is usually the best strategy with React. While you 
could make the game from a single Game Component. A better 
strategy would be to make Game Component from Grid Component 
that is made of GridSquare Components. 
 
Each component will require CSS styles. The components used in 
this project will not have much use in other projects. They are 
too specialized. This makes keeping all of the styles in a single 
stylesheet more convenient. 

## Challenges

**Make the GridSquare Component**

This component will render as a single square of color. 

Make a new file: 'src/components/grid-square.js'

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

- `grid-square` : Define default grid square properties shared by all grid squares.
- `color-${this.props.color}` : The color of the square will be 
passed as props. The value of `props.color` will be a number e.g. 1, 2, 3. 
The class name for any grid square will be: `color-0`, `color-1`, 
`color-2`, `color-3` etc. 

## Define some CSS

This project will store all of it's styles in 'index.css'. The 
components in the project are not portable, they would find 
little use outside of this project. 

By keeping all of the styles in one place it will make for a 
large body of CSS code. To keep this as [DRY](https://en.wikipedia.org/wiki/Don%27t_repeat_yourself) 
as possible you can use CSS custom properties.

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

The **Square Colors** are the background colors for the 
squares. 

The **Border Colors** are all transparent colors. These will 
tint or shade the background color of the square. 

The **Numbers** define values that will be used throughout 
the CSS, `--tile-size: 20px` for example will set size of 
the grid squares.

**Color Classes**

The colors will be assigned to grid squares as classes. 
With class names: `color-0`, `color-1`, `color-2` etc. 
Define these classes using the color variables. CSS 
variables set above are used here. 

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

With this arrangement you can use the colors anywhere your 
stylesheet. You can also make global changes to colors in 
one location. 

**Grid Square Appearance**

Define the appearance of a grid square. The grid squares 
all have a border style, and a width and a height. By defining 
these as variables it will be easier to make changes to the 
appearance of the grid squares through the variables at the 
top of the stylehseet. 

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
there will be reused in future styles. With this arrangement 
you can easily make changes to the size and border in a 
single place, at the top of the style sheet. 

## Test a Grid Sqaure

Import './components/grid-square' at the top of 'App.js'
and add the component within render. 

`<GridSquare color="1" />`

Setting the color to 1 should display an orange square. 

Try some other values by changing the value of `color`. 

## conclusion

CSS Variables, also known as CSS Custom Properties are an 
amazing feature, that can go a long way to making your code
easier to manage, and more DRY. 

Colors will be managed by a classes named `color-#` where # will 
be a number 0-7. 0 is an empty square and the numbers 1-7 are 
the colors for each of the different block shapes. 

## Resources

- https://developer.mozilla.org/en-US/docs/Web/CSS/--*
- https://www.quackit.com/css/css_color_codes.cfm

---
title: "React Redux Tetris - making things move"
slug: react-redux-tetris-making-things-move
---

Blocks fall constantly. This is what gives Tetris
it's challenge. Every so often a blokc needs to 
move down this is what gives the game it's 
challenge. 

# Introduction 

With everything so far in place all of the game 
is almost finished. One important step is needed
to make turn this into a playable game  
the blocks need to move down on their own. 

To make this work the game needs to issue 
'MOVE_DOWN' actions on it's own. The time between
each of these messages will determine the 
diffculty. 

There are acouple approaches that can be used. 
The obvious choice is `setInterval`. This is 
an easy solution. I'm going to outline a
different solution using `requestAnimationFrame`.

This solution might seem a little strange. But,
it has a couple advantages and will (hopefully)
introduce you to new ideas. 

**Dispatching a periodic MOVE_DOWN action**

The goal here is issue a MOVE_DOWN action 
every time period. Where the time period might 
start at once per second and decrease over time
as the game is played to increase diffculty. 

Where we place the code for this is a design 
decision. Since we are using Redux we can 
call the `moveDown` action from just about 
anywhere. 

The real question is where does it make sense to
place the code, or where would we expect to find
it when we look for it. The real goal is to place 
it in a place we would expect to find it. This 
will make our job easier. 

**Keep track of time**

Delta time represents the difference between 
now and the last time the browser redrew the 
window. 

**Where to handle timer events**

The game needs to handle time and issue MOVE_DOWN
actions at intervals. The interval will be the 
speed set on state. 

With those ideas in consideration where you 
store the code that handles these update is a
matter where you can access speed from the 
Redux store and where you would logically look 
for this code. 

I made the decision to handle timing in the 
GameBoard component. You could place this 
code in the App or Controls or other 
Component also. 

**Request Animation Frame**

The browser draws the contents of the window at 
regular intervals, about every 16.7 milliseconds. 
It's advantageous to our application to update
our views on the same clock. 

JavaScript provides a method to notify our 
applications when the browser is about to redraw 
the screen. 

`requestAnimationFrame()` this method takes a 
callback that is executed just before the 
browser redraws the window. 

## Challenges

**Keeping track of Delta Time**

To keep track of delta time the game needs two 
variables: `lastUpdateTime` to hold the time of 
the last update, and `progressTime` to hold the 
amount of time since the last update. 

These don't need to be part of state. I made them 
class properties of the GameBoard. 

```JavaScript
constructor(props) {
  super(props)

  this.lastUpdateTime = 0
  this.progressTime = 0
}
```

**Request Animation Frame**

The goal is to calculate the number of 
milliseconds that have elapsed since the last 
frame by subtracting the current time from 
the last update time. 

The game will keep a running total of the 
milliseconds that have elapsed since the last 
update. When the total is greater than the 
speed issue a MOVE_DOWN. 

In other words we will add up milliseconds with 
each frame that is rendered and when the total 
is greater than the speed we move a the block down. 

`requestAnimationFrame()` takes a callback and 
only calls it once. So you will need to make 
the first call to `requestAnimationFrame()` in 
`componentDidMount()`.

Issue the first call to `requestAnimationFrame`.

```JavaScript
componentDidMount() {
  window.requestAnimationFrame(this.update.bind(this))
}
```

When the browser calls `requestAnimationFrame()` it's 
going to call `update()`, we will define that next, 
notice we're 'binding _this_' on the callback to 
guarantee that `this` in `update()` references the 
component. 

Define the callback for `requestAnimationFrame()`.

```JavaScript
// Handle game updates
update(time) {
  // If the game is is running we want to make reques a callback at the next animation frame. 
  window.requestAnimationFrame(this.update.bind(this))
  if (!this.props.isRunning) {
    return
  }
              
  // If lastUpdateTime not been set set it to the current time. 
  if (!this.lastUpdateTime) {
    this.lastUpdateTime = time
  }

  // Cacluate delta time and progress time
  const deltaTime = time - this.lastUpdateTime
  this.progressTime += deltaTime
  
  // If the progress time is greater than speed move the block down
  if (this.progressTime > this.props.speed) {
    this.props.moveDown()
    this.progressTime = 0
  }

  // set the last update time. 
  this.lastUpdateTime = time
}
```

Try testing the timing. Change the default 
value for speed on game state. The blocks should fall 
faster. You can use thise during game play to increase
the difficulty of the game. 

## Conclusion



## Resources

 

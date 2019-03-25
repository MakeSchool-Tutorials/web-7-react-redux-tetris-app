---
title: "Creating a Timer"
slug: creating-a-timer
---

1. ~~Implement the overall grid square~~
1. ~~Implement the game board~~
1. ~~Implement the "next block" area~~
1. ~~Implement the score board~~
1. ~~Arrange the layout of the game~~
1. ~~Implement the controls~~
1. ~~Implement the message popup~~
1. ~~Implement the actions and reducers~~
1. ~~Do some code organizing and cleanup~~
1. ~~Implement state and shapes~~
1. ~~Connect each component up to state and reducers~~
1. ~~Implement block rotation~~
1. ~~Implement moving blocks~~
1. **Building a timer system**
    1. **Overview of timing and how to use `requestAnimationFrame`**
    1. **Track delta time in the GridBoard**
    1. **Build out an `update` function to update the GridBoard as blocks fall down**
    1. **Implement the logic in the Pause/Resume button**
1. Implementing Game Over and Restart

With what we have so far, the game is almost finished. One important step is needed to make turn this into a playable game: the blocks need to move down on their own!

To make this work the game needs to issue
`MOVE_DOWN` actions on it's own. The time between each of these actions will determine the difficulty.

We're going to use `requestAnimationFrame` to implement this feature. It may seem a little strange, but it has a couple advantages over using something like `setInterval`, and is a great way to practice some new ideas.

# Dispatching a periodic MOVE_DOWN action

The goal here is issue a MOVE_DOWN action every time period, where the time period might start at once per second and decrease over time as the game is played to increase difficulty.

> [info]
>
> We're going to be referring to **Delta time** a lot in this chapter. Delta time represents the difference between now and the last time the browser redrew the window.

As usual, let's go over some basic requirements:

- The game needs to handle time and issue MOVE_DOWN
actions at intervals.
- The interval will be the speed set on state.
- Timing should be handled in the GameBoard component

> [info]
>
> You could place the timing code in the App or Controls or other Component as well

# Request Animation Frame Overview

The browser draws the contents of the window at regular intervals, about every 16.7 milliseconds. It's advantageous to our application to update our views on the same clock.

JavaScript provides a method to notify our applications when the browser is about to redraw the screen.

[requestAnimationFrame()](https://developer.mozilla.org/en-US/docs/Web/API/window/requestAnimationFrame) is a method that takes a callback that is executed just before the browser redraws the window.

# Keeping track of Delta Time

To keep track of delta time the game needs two
variables:

- `lastUpdateTime` to hold the time of the last update
- `progressTime` to hold the amount of time since the last update.

These don't need to be part of `state`. We will make them class properties of the GameBoard.

> [action]
>
> Add the following within the `GridBoard` class in `/src/components/grid-board.js`:
>
```JavaScript
class GridBoard extends Component {
    constructor(props) {
      super(props)
>
      this.lastUpdateTime = 0
      this.progressTime = 0
    }
>
...
>
}
```

# Implementing Request Animation Frame

The goal is to calculate the number of
milliseconds that have elapsed since the last
frame by subtracting the current time from
the last update time.

The game will keep a running total of the
milliseconds that have elapsed since the last
update. When the total is greater than the
speed, we will issue a MOVE_DOWN.

In other words, we will add up milliseconds with
each frame that is rendered and when the total
is greater than the speed, we move a the block down.

`requestAnimationFrame()` takes a callback and
only calls it once. So you will need to make
the first call to `requestAnimationFrame()` in
[componentDidMount()](https://reactjs.org/docs/react-component.html#componentdidmount).

> [action]
>
> Add the `componentDidMount` to `/src/components/grid-board.js`, which will issue the first call to `requestAnimationFrame`.
>
```JavaScript
componentDidMount() {
  window.requestAnimationFrame(this.update.bind(this))
}
```

Now you may have noticed that this will break your app in its current state. When the browser calls `requestAnimationFrame()`, it's
going to call a function `update()`, which we will define next.

Notice we're binding `this` on the callback to guarantee that `this` in `update()` references the component.

> [action]
>
> Define the callback `update` for `requestAnimationFrame()` in `/src/components/grid-board.js`:
>
```JavaScript
// Handle game updates
update(time) {
  // If the game is is running we want to request a callback at the next animation frame.
  window.requestAnimationFrame(this.update.bind(this))
  if (!this.props.isRunning) {
    return
  }
>
  // If lastUpdateTime not been set, set it to the current time.
  if (!this.lastUpdateTime) {
    this.lastUpdateTime = time
  }
>
  // Calculate delta time and progress time
  const deltaTime = time - this.lastUpdateTime
  this.progressTime += deltaTime
>
  // If the progress time is greater than speed move the block down
  if (this.progressTime > this.props.speed) {
    this.props.moveDown()
    this.progressTime = 0
  }
>
  // set the last update time.
  this.lastUpdateTime = time
}
```

Try testing the timing. Decrease the default value for speed in `defaultState()` and the blocks should fall faster!

# Now Commit

>[action]
>
```bash
$ git add .
$ git commit -m 'timer created'
$ git push
```

# Implement the Pause Resume button

What if we need to use the bathroom, or get a snack, or both? With the timer now running, we might need to pause the game and resume it later.

We've already built the Pause and Resume buttons, but at this point they don't do anything. Luckily the game state has an `isRunning` property for this purpose!

The button already calls the action, we just need the reducer needs to handle the action.

> [action]
>
> Implement the `RESUME` and `PAUSE` cases in `/src/reducers/game-reducer.js`:
>
```js
case RESUME:
>
      return { ...state, isRunning: true }
>
case PAUSE:
>
      return { ...state, isRunning: false }
```

# Product So Far

You should now be able to pause/resume the game!

![paused](assets/paused.png)

# Now Commit

>[action]
>
```bash
$ git add .
$ git commit -m 'Resume and pause implemented'
$ git push
```

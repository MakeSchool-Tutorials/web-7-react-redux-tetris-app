---
title: "Connect Controls"
slug: connect-controls
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
1. **Connect each component up to state and reducers**
    1. ~~NextBlock~~
    1. ~~GridBoard~~
    1. **Controls**
        1. **Add the actions needed for the controls**
        1. **Implement the `mapStateToProps` function**
        1. **Implement the `mapDispatchToProps` function**
        1. **Connect the `controls` component**
        1. **Call the actions in their appropriate buttons**
1. Implement block rotation
1. Implement moving blocks
1. Building a timer system
1. Implementing Game Over and Restart

Now we'll connect the controls to actions so that we can play the game! Tapping the left, right, and down buttons move the block. Tapping the rotate button changes the rotation of the block.

Controls need to issue actions to control the game.
We'll need to connect this component to `state` so it
can issue actions that move the block.

This works by sending actions that change `state`, updating
the `x`, `y`, and `rotation` values. _Changing these updates
the components that use these values as props!_

We can also use `isRunning` to control the display of the buttons. Imagine the case where the game is paused.In this case we might want the buttons to display as disabled. It might be a good idea to map `isRunning` to props on this component.

# Import Actions

Let's get those actions in there

> [action]
>
> Import the `moveDown, moveLeft, moveRight, rotate` actions (as well as `connect`) into `/src/components/controls.js`
>
```js
import { connect } from 'react-redux'
import { moveDown, moveLeft, moveRight, rotate } from '../actions'
```

# Map state to props

> [action]
>
> Build out the `mapStateToProps` method in `/src/components/controls.js` to map the `isRunning` property from state to props. This can be used to enable and disable the buttons as the game runs.
>
```js
const mapStateToProps = (state) => {
    return {
        isRunning: state.game.isRunning
    }
}
```

# Map Dispatch to Props

> [action]
>
> Define the `mapDispatchToProps` method in `/src/components/controls.js` with the actions you imported.
>
```js
const mapDispatchToProps = () => {
    return {
        moveRight,
        moveLeft,
        moveDown,
        rotate
    }
}
```

# Connect this component

> [action]
>
> Edit the `export` in `/src/components/controls.js` so that we can connect this component with `mapStateToProps` and `mapDispatchToProps`:
>
```js
export default connect(mapStateToProps, mapDispatchToProps())(Controls)
```

# Call Actions

Currently the buttons in this component just call actions from props with no params. Let's set that up properly now:

> [action]
>
> Edit the `render` method in `/src/components/controls.js` to actually call actions. Remember that actions should only be sent if the `isRunning` is true:
>
```JS
render() {
    const { isRunning } = this.props
>
    return (
      <div className="controls">
        {/* left */}
        <button className="control-button" onClick={(e) => {
          if (!isRunning) { return }
          this.props.moveLeft()
        }}>Left</button>
>
        {/* right */}
        <button className="control-button" onClick={(e) => {
          if (!isRunning) { return }
          this.props.moveRight()
        }}>Right</button>
>
        {/* rotate */}
        <button className="control-button" onClick={(e) => {
          if (!isRunning) { return }
          this.props.rotate()
        }}>Rotate</button>
>
        {/* down */}
        <button className="control-button" onClick={(e) => {
          if (!isRunning) { return }
          this.props.moveDown()
        }}>Down</button>
>
      </div>
    )
  }
```

Still no visual changes yet, we still have a couple more components to connect up. Make sure everything still loads correctly in the browser!

# Now Commit

>[action]
>
```bash
$ git add .
$ git commit -m 'Added connection for controls'
$ git push
```

---
title: "Moving Blocks"
slug: moving-blocks
---

Let's make sure we can move the blocks left and right. Down is going to involve a bit more complexity, so we'll do that in the next chapter. Now that we have our `canMoveTo` function, this will be a _lot_ easier!

# Left button

In the `game-reducer`, the move left action should _subtract 1 from the x and check if this new position is possible by calling `canMoveTo()`_

> [action]
>
> Edit the MOVE_LEFT case in `/src/reducers/game-reducer.js` to be the following:
>
```js
case MOVE_LEFT:
    // subtract 1 from the x and check if this new position is possible by calling `canMoveTo()
    if (canMoveTo(shape, grid, x - 1, y, rotation)) {
        return { ...state, x: x - 1 }
    }
    return state
```

# Right button

_Adding 1 to `x` should move the block to the right._

> [action]
>
> Edit the MOVE_RIGHT case in `/src/reducers/game-reducer.js` to be the following:
>
```js
case MOVE_RIGHT:
    if (canMoveTo(shape, grid, x + 1, y, rotation)) {
      return { ...state, x: x + 1 }
    }
    return state
```

# Now Commit

>[action]
>
```bash
$ git add .
$ git commit -m 'move left and right'
$ git push
```

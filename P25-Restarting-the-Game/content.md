---
title: "Restarting the Game"
slug: restarting-the-game
---

Now that the game knows when it's ended, we need a way to restart it!

Restarting the game will only require setting the game `state` in redux back to default, and there already is a function for this!

# Restart Game-Reducer

> [action]
>
> Return default state with a call to `defaultState()` in the `RESTART` case in `/src/reducers/game-reducer.js`:
>
```js
case RESTART:
    return defaultState()
```

Try pressing the restart button and make sure it starts the game from a clean slate.

# Now Commit

# Now Commit

>[action]
>
```bash
$ git add .
$ git commit -m 'restart implemented'
$ git push
```

You now have a fully functioning Tetris game! Congrats!

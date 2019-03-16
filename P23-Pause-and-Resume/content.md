---
title: "Pause and Resume"
slug: pause-and-resume
---

What if we need to use the bathroom, or get a snack, or both? We might need to pause the game and resume it later.

We've already built the Pause and Resume buttons, but at this point they don't do anything. Luckily the game state has an `isRunning` property for this purpose!

# Implement the Play Resume  button

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

You should now be able to pause/resume the game!

![paused](assets/paused.png)

# Now Commit

>[action]
>
```bash
$ git add .
$ git commit -m 'play and pause implemented'
$ git push
```

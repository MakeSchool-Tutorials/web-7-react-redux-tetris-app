---
title: "React Redux Tetris - "
slug: react-redux-tetris-
---

Blocks fall constantly. This is what gives Tetris
it's challenge. 

# Introduction 

With everything so far in place all of the game 
is almost finished. One important step needed
to make turn this into a playable game is to 
make the blocks move down on their own. 

To make this work the game needs to issue 
'MOVE_DOWN' actions on it's own. The time between
each of these messages will determine the 
diffculty. 

There are acouple approaches that can be used. 
The obvious choice is `setInterval`. This is 
an easy solution. I'm going to outline a
different solution using `requestAnimationFrame`.
This solution might seem a little strange. 

It has a couple advantages and will (hopefully)
introduce you to new ideas. 

## Challenges

**Dispatching a periodic MOVE_DOWN action**

The goal here is issue a MOVE_DOWN action 
every time period. Where the time period might 
start at once per second, and decrease over time
as the game is played to increase diffculty. 

Where we place the code for this is a design 
decision. Since we are using Redux we can 
call the `moveDown` action from just about 
anywhere. 

The real question is where does it make sense to
place the code, or where would be expect to find
it when we look for it. The real goal is to place 
it in a place we would expect to find it. This 
will make our job easier. 

I'll leave it up to you to choose where to place 
the code.

## Conclusion



## Resources

 

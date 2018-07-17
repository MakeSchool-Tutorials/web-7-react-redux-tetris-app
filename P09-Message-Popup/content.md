---
title: "React Redux Tetris - Message Popup"
slug: react-redux-tetris-message-popup
---

The game will need to display messages about the game 
state. Messages will be 'Game Over' and 'Paused' for 
now but can be expanded to showing score, advancing 
to a new level, and more. 

# Introduction 

The Message Popup will be a component connected to 
application state. 

This component will appear above the game board in the 
center of the screen. The HTML element that holds this 
component needs to display over the rest of the 
component elements. 

It won't be arranged with Grid and instead will use CSS 
absolute position. Position allows us to place this 
anywhere on the screen regardless of the other elements. 

## Challenges

Add a new file: './src/components/message-popup.js'. 

```JSX
import React, { Component } from 'react'

// Displays a message

class MessagePopup extends Component {

  render() {
    return (
      <div className='message-popup'>
        <h1>Message Title</h1>
        <p>Message info...</p>
      </div>
    )
  }
}

export default MessagePopup
```

Import and add the message Popup to the _bottom_ of App. 
_It should be the last compnent in App._ 

Use styles to position and display the Message Popup. 

```CSS
/* Message Popup */
.message-popup {
  position: absolute;
  left: 50%;
  top: 50%;
  transform: translate(-50%, -50%);
  
  width: calc(var(--tile-size) * 10);
  height: calc(var(--tile-size) * 10);
  background-color: rgba(255, 255, 255, 0.5);
  text-align: center;
}

.message-popup.hidden {
  display: none;
}

```

The styles under `.message-popup` apply to the `MessagePopup`
container. With `position:absolute` this element can be placed 
anywhere on the screen, `left, top, transform:translate` 
perform this function. 

The style is applied only when the message popup container
has both `message-popup` class and the `hidden` class. In this 
case the Message Popup is not displayed. 

## Conclusion


## Resources

 

---
title: "Create Store and Provider"
slug: create-store-and-provider
---

We need to define the Redux store and wrap child components in a provider component to share the store.

# Add Store and Provider

Define the store in App and Create a Provider
component that wraps the components rendered by
App.

> [action]
>
> Update `/src/App.js` to include the following:
>
```js
import React, { Component } from 'react';
[bold]import { createStore } from 'redux'[/bold]
[bold]import { Provider } from 'react-redux'[/bold]
>
import GridBoard from './components/grid-board'
import NextBlock from './components/next-block'
import ScoreBoard from './components/score-board'
import Controls from './components/controls'
import MessagePopup from './components/message-popup'
>
import './App.css';
>
[bold]const store = createStore(reducers)[/bold]
>
class App extends Component {
  render() {
    return (
[bold]      <Provider store={store}>[/bold]
        <div className="App">
          <header className="App-header">
            <h1 className="App-title">Tetris Redux</h1>
          </header>
          <GridBoard />
          <NextBlock />
          <ScoreBoard />
          <Controls />
          <MessagePopup />
        </div>
[bold]      </Provider>[/bold]
    );
  }
}
>
export default App;
```

# Now Commit

>[action]
>
```bash
$ git add .
$ git commit -m 'Added store and provider'
$ git push
```

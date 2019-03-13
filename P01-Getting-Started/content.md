---
title: "Getting Started"
slug: getting-started
---

This section sets up the default project using [Create React
App](https://github.com/facebook/create-react-app).

The Create React App starter project is a great place to start
for any React project.

React projects require a build process and must be run from a
server when testing locally. Create React App creates a complete
project with all of these things in place.

# Create a default app

Firs thing we need to do is get our default React app set up

> [action]
>
> Create a default app using Create React App. You can follow the instructions [here](https://github.com/facebook/create-react-app).
>
> Test your app with: `npm start` or `yarn start` to make sure everything is working.

You can visit the project in a browser at `http://localhost:3000/`. It should open at the this address automatically. If all went well, you should see the below in your browser:

![react-app](assets/react-app.png)

# Clean up the Default Project

Clean up the default project by removing the header and default
content.

> [action]
>
> In `/src/App.js` edit the `render` method to provide the following JSX:
>
```html
<div className="App">
  <header className="App-header">
    <h1 className="App-title">Tetris Redux</h1>
  </header>
</div>
```
>
> Since we removed the logo we should remove the import for it:
> remove the `import logo from './logo.svg';` line from the top of `/src/App.js`
>
> Lastly, make a folder for components: `src/components`

# Test the changes

With the server running any changes you make to the code should
trigger the server to refresh automatically. You should now see the below in the browser:

![tetris-redux](assets/tetris-redux.png)

## Resources

- https://github.com/facebook/create-react-app

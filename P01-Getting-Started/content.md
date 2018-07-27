---
title: "React Redux Tetris - Getting Started"
slug: react-redux-tetris-getting-started
---

This project will be built with Node.js, React.js, 
and Redux.js. 

![node-icon](assets/node-icon.png)
![react-icon](assets/react-icon.png)
![redux-icon](assets/redux-icon.png)

# Introduction 

This section sets up the default project using [Create React
App](https://github.com/facebook/create-react-app). 

The Create React App starter project is a great place to start 
for any React project. 

React projects require a build process and must be run from a 
server when testing locally. Create React App creates a complete 
project with all of these things in place. 

## Challenges

**Create a default app**

Create a default app using Create React App. You can follow 
the instructions [here](https://github.com/facebook/create-react-app).

Test your app with: 

`npm start` 

or 

`yarn start` 

to make sure everything is working. 

You can visit the project in a browser at `http://localhost:3000/`. 
It should open at the this address automatically. 

**Clean up the Default Project**

Clean up the default project by removing the header and default
content. 

In 'App.js' edit the render method to render the following: 

```jsx
<div className="App">
  <header className="App-header">
    <h1 className="App-title">Tetris Redux</h1>
  </header>
</div>
```

Since we removed the logo we should remove the import for it: 

`import logo from './logo.svg';`

Make a folder for components: 'src/components'.

**Test the changes**

With the server running any changes you make to the code should 
trigger the server to refresh automatically. 

## conclusion

In this step you created a default project with Create React App, 
started the dtest server, and then modified default project. 

## Resources

- https://github.com/facebook/create-react-app

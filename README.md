# Step by step React App.

*The step by step to creating a React App.*

The intention of this project, is to guide you through the process of creating a React App step by step.

## Table of Contents

  1. [Folder Structure](#folder-structure)
  1. [Webpack](#webpack)
  1. [Babel](#babel)
  1. [React](#react)

## Folder Structure
  * ##### Create your App's directory and step into it.
    `mkdir [appName] && cd [appName]`

  * ##### Create Source directory and `index.js` file.
    > This *index.js* file will be the entry point to your app.  
    
    `mkdir [sourceDirectoryName] && touch [sourceDirectoryName]/index.js`

  * ##### Create distribution/bundle directory and `index.html` file.
    > This HTML file will have the container div where your
    > React App will live. Also, will be referencing the bundled js
    > file created by webpack.

    `mkdir [distDirectoryName] && touch [distDirectoryName]/index.html`
  
  * ##### Create webpack's configuration file.
    `touch webpack.config.js`

  * ##### Create babel's configuration file.
    `touch .babelrc`

  * ##### Create package.json 
    > **-y**: Will initialize your package.json file with default values.
  
    `npm init -y`

  > To this point, you have all the directories and files that your app wil 
  > need. Lets take a look at your folder structure:
    
  *To make things a bit easier we will be using the following files' and directories' names. Change as necessary.*

  ```
  app
  |- dist
  |   |- index.html
  |- src 
  |   |-index.js
  |- .babelrc
  |- .package.json
  |- webpack.config.js
  ```
  
  > Now it is time to start adding some content to those files and installing some packages.

## Webpack
  * ##### Install webpack
    
    > ...*(And two other important packages).*  
    > **webpack**: The actual package bundler.  
    > **webpack-cli**: webpack's toolbelt. Configurations will be handled in webpack.config.js file.  
    > **webpack-dev-server**: Your localhost Node.js server.  
    > **--save-dev**: Will add those dependencies to your package.json as `devDependencies`  

    `npm install --save-dev webpack webpack-cli webpack-dev-server`


  * ##### Add configurations to `webpack.config.js` file.
    ```javascript
    module.exports = {
      entry: ['./src/index.js'],
      output: {
        path: __dirname + '/dist',
        publicPath: '/',
        filename: 'bundle.js',
      },
      devServer: {
        contentBase: './dist',
      },
    }

  * ##### Add a *start* script to your [package.json](https://github.com/mauriciolealmx/react-step-by-step/blob/master/package.json) file.
    > **webpack-dev-server** Running the Node server.  
    > **--config**: Utilizing our `webpack.config.js` file  
    > **--mode**: Development mode.  

    ```json
    "start": "webpack-dev-server --config webpack.config.js --mode development",
    ```

  * ##### Add your basic HTML structure to `dist/index.html` file.
    > The `output.filename` that you specify in `webpack.config.js`
    > has to be the same as the one specified as src in
    > the script tag. (e.g. `<script src="bundle.js"></script>`)  
    > If in doubt, please see this project's [index.html](https://github.com/mauriciolealmx/react-step-by-step/blob/master/dist/index.html) file.  
    
    ```html
    <!DOCTYPE html>
    <html>
    <head>
      <title>Page Title</title>
    </head>
    <body>
      <div id="container"></div>
      <script src="bundle.js"></script>
    </body>
    </html>
    ````

## Babel
  * ##### Install Babel.
    > **babel-core**: Babel's source code.  
    > **babel-loader**: webpack's plugin for babel.  
    > **babel-preset-env**: Compiles ES2015+ down to ES6.  

    `npm install --save-dev babel-core babel-loader babel-preset-env`

  * ##### Install Babel presets for React and [*stage-2*](https://babeljs.io/docs/plugins/preset-stage-2) js features.
    > **babel-preset-react**: Transpiles *jsx* into *js*  
    > **babel-preset-stage-2**: Gives you the ability to use js features currently in Stage 2 (Draft).  

    `npm install --save-dev babel-preset-react babel-preset-stage-2`
        
  * ##### Add `module.rules` and `resolve.extensions` to `webpack.config.js`
    > Confused about what this file should end up with? [webpack.config.js](https://github.com/mauriciolealmx/react-step-by-step/blob/master/webpack.config.js).
    ```javascript
    ...
    },
    module: {
      rules: [
        {
          test: /\.(js|jsx)$/,
          exclude: /node_modules/,
          use: ['babel-loader'],
        },
      ],
    },
    resolve: {
      extensions: ['*', '.js', '.jsx'],
    },
    ```

  * ##### Add presets to [.babelrc](https://github.com/mauriciolealmx/react-step-by-step/blob/master/.babelrc).
    > We are just specifying the use of the three presets we
    > previously installed.  

    ```json
    {
      "presets": [
        "env",
        "react",
        "stage-2"
      ]
    }
    ```
  * ##### Let's add some *js* to your app's `src/index.js` file.
    `echo "console.log('Hello World')" >> src/index.js`

  * ##### Run your App to verify webpack is working.
    > Once your app is running, you can visit you app at [localhost:8081](http://localhost:8081/)  
    > Open the console and you will see your "Hello World"  
    > Stop your app in console with `Ctrl + c`

    `npm start`

## React
  * ##### Install React.
    > ...*(And react-dom).*  
    > **react-dom**: We will be needing react-dom to render our app.  
    
    `npm install react react-dom`

  * ##### Add a bit of `js` and `React` code to `src/index.js`.
    ```jsx
    import React from 'react'
    import ReactDOM from 'react-dom'

    function App() {
      return <h1>Hello From App</h1>
    }

    ReactDOM.render(<App />, document.getElementById('container'))
    ```

## Run your app.
  > Now you can finally run your app and see a `"Hello From App"`
  > message in your browser. This means that `React` is working and `Babel` is
  > correctly transpiling `React Elements`.  
  > Remember, your app will be running at [localhost:8081](http://localhost:8081/)  
    
  `npm start`

If you have any questions or suggestions please feel free to shoot me an email.

Best Regards,

[Mauricio Leal](https://github.com/mauriciolealmx)
[LinkedIn](https://www.linkedin.com/in/mauriciolealmx/?locale=en_US)

***

**[⬆ back to top](#table-of-contents)**

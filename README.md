### Static Website Setup Checklist


- In the terminal, make a new directory for your project files.

``mkdir project-name``

- From that new directory, create some starter files

``cd project-name``

``touch index.html``

``touch webpack.config.js``

``touch entry.js``

``touch root.jsx``

- Initialize project with git

``git init``

- Add .gitignore file and include node_modules

``touch .gitignore``

Add /node_modules

- Now, install necessary packages using npm

``npm install react react-dom react-router-dom webpack babel-core babel-loader babel-preset-react babel-preset-es2015``

- You should have a package.json file. Ensure the ``script`` object contains ``"webpack": "webpack"``

- Add and commit changes locally, and push them to a new repository on GitHub
- Ensure node_modules were ignored

- Configure webpack (this is a bare bones configuration file that I use as a starting point for most projects):

```javascript
const path = require("path");
const webpack = require("webpack");

module.exports = {
  context: __dirname,
  entry: "./entry.js",
  output: {
    path: path.resolve(__dirname),
    filename: "./bundle.js"
  },
  module: {
    loaders: [
      {
        test: [/\.jsx?$/, /\.js?$/],
        exclude: /node_modules/,
        loader: 'babel-loader',
        query: {
          presets: ['es2015', 'react']
        }
      }
    ]
  },
  devtool: 'source-map',
  resolve: {
    extensions: [".js", ".jsx", "*"]
  }
};
```

- Add a div with id="root" to html body
- Add a DOMContentLoaded callback to your entry file:

```javascript
import React from 'react';
import ReactDOM from 'react-dom';
import Root from './root';

document.addEventListener('DOMContentLoaded', () => {
  const root = document.getElementById('root');
  ReactDOM.render(<Root />, root);
});
```

- Write a functional component in your root file and have it render some test content (don't forget to export)

- run ``npm run webpack`` to create a bundle.js file

- Add the relative route to your bundle in index.html

```html
<script type="text/javascript" src="./bundle.js"></script>
```

- Add, commit and push changes

- From terminal: ``open index.html`` to view your test content in Chrome

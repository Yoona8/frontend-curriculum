# Webpack
<details>
<summary>Basic config</summary>

- install npm first
- for working with styles import css file into js file, where we use the styles, by default webpack's css loader adds `<link rel="stylesheet">`

```bash
# for webpack usage
$ npm i -DE webpack
$ npm i -DE webpack-cli

# optional, if dev server needed
$ npm i -DE webpack-dev-server
```

```JavaScript
// webpack.config.js
// for the proper path configs for different OS
const path = require('path');

module.exports = {
  // build mode
  mode: 'development',
  // application entry point
  entry: './src/main.js',
  // settings for the output file
  output: {
    filename: 'bundle.js',
    // __dirname is a root directory of our app
    path: path.join(__dirname, 'public')
  },
  devtool: 'source-maps',
  devServer: {
    // where to look for a build
    contentBase: path.join(__dirname, 'public'),
    // detects changes in js files and reloads a page
    watchContentBase: true
  },
  module: {
    rules: [{
      // what files to look for (.scss, .css here)
      test: /\.s?css/,
      // style-loader handles the importing of the files (injects css into DOM as link tag by default)
      // css-loader handles the css code (resolves the css file)
      // order matters (which loader to use)
      use: ['style-loader', 'css-loader']
    }]
  }
};
```

```JavaScript
// component.js
import "./src/style.css";
```

</details>

<details>
<summary>Learn more</summary>

- [Webpack official](https://webpack.js.org/)

</details>

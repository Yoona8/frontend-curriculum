# Webpack
<details>
<summary>Basic config</summary>

- install npm first
```bash
# for webpack usage
$ npm i -DE webpack
$ npm i -DE webpack-cli

# optional, if dev server needed
$ npm i -DE webpack-dev-server
```
- by default works in a production mode
- if you need different configs, add more config files (ex `webpack.config.js` and `webpack.config.prod.js`) and use the script
```JavaScript
"scripts": {
  "build:prod": "webpack --config webpack.config.prod.js"
}
```
- if there are dynamic imports `import('file-name');` webpack generates a separate file
```JavaScript
// webpack.config.js
// for the proper path configs for different OS
const path = require('path');
// to clean the unused files
const CleanPlugin = require('clean-webpack-plugin');

module.exports = {
  // build mode
  mode: 'development',
  // application entry point
  entry: './src/main.js',
  // for multiple entries (creates 1 bundle per entry)
  entry: {
    main: './src/main-page/main.js',
    contacts: './src/contacts-page/main.js'
  }
  // settings for the output file
  output: {
    filename: 'bundle.js',
    // for prod mode good to change the filename
    filename: '[contenthash].js',
    // __dirname is a root directory of our app
    path: path.join(__dirname, 'public'),
    // if public/scripts
    path: path.join(__dirname, 'public', 'scripts'),
    // to fix the paths inside files upon bundling
    publicPath: 'public/scripts/'
  },
  devtool: 'source-maps',
  devServer: {
    // where to look for a build
    contentBase: path.join(__dirname, 'public'),
    // detects changes in js files and reloads a page
    watchContentBase: true
  },
  plugins: [
    new CleanPlugin.CleanWebpackPlugin()
  ],
  module: {
    rules: [{
      // what files to look for (.scss, .css here)
      test: /\.s?css/,
      // style-loader handles the importing of the files (injects css into DOM as link tag by default)
      // css-loader handles the css code (resolves the css file)
      // order matters (from right to left css, style)
      use: ['style-loader', 'css-loader']
    }]
  }
};
```
- for working with styles import css file into js file, where we use the styles, by default webpack's css loader adds `<link rel="stylesheet">`
```JavaScript
// component.js
import "./src/style.css";
```

</details>

<details>
<summary>Learn more</summary>

- [Webpack official](https://webpack.js.org/)
- [Code Splitting](https://webpack.js.org/guides/code-splitting/)
- [Entry](https://webpack.js.org/concepts/#entry)
- [Guides](https://webpack.js.org/guides/)

</details>

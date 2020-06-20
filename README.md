# Webpack Installs 🚀

## Step 1
**Make sure you are in the correct directory and run:** `npm init -y`
## Step 2
In `package.json` add/replace:
```json
"main": "src/javascripts/main.js",
```
```json
"scripts": {
  "start": "webpack-dev-server --mode development --open",
  "build": "webpack --mode production --module-bind js=babel-loader",
  "deploy": "npm run build && firebase deploy"
},
```
```json
"author": "Ryan Beiden <rdbeiden@gmail.com>",
```
## Step 3
To install Dev Dependencies, run:
```
npm install @babel/core @babel/preset-env babel-loader css-loader eslint eslint-config-airbnb-base eslint-loader eslint-plugin-import file-loader html-loader html-webpack-plugin mini-css-extract-plugin node-sass sass-loader webpack webpack-cli webpack-dev-server --save-dev
```
## Step 4
`.gitignore` file may already have been made, but if not, create the file in root and add:
```
.vscode/
.DS_Store
package-lock.json
node_modules/
dist/
build/
.firebase/
```
## Step 5
In root, create a file named `.babelrc` and add:
```json
{
  "presets": [
      "@babel/preset-env"
  ]
}
```
## Step 6
In root, create a file named `.eslintignore` and add:
```
webpack.config.js
node_modules
build
```
## Step 7
In root, create a file named `.eslintrc` and add:
```json
{
  "parserOptions": {
    "ecmaVersion": 9,
    "sourceType": "module"
  },
  "extends": "airbnb-base",
  "globals": {
    "document": true,
    "window": true,
    "$": true,
    "XMLHttpRequest": true,
    "allowTemplateLiterals": true
  },
  "rules": {
    "no-console": [1, { "allow": ["warn", "error"] }],
    "no-debugger": 1,
    "class-methods-use-this": 0,
    "linebreak-style": 0,
    "max-len": [1,200,2]
  }
}
```
## Step 8
To install Regular Dependencies, run:
```
npm install axios firebase jquery popper.js --save
```
>I've gotten errors here before, and it seemed to be because node was not up to date so run `brew upgrade node` and try again.
## Step 11
In root, create a file `webpack.config.js` and add:
```js
const webpack = require('webpack');
const HtmlWebPackPlugin = require("html-webpack-plugin");
const MiniCssExtractPlugin = require("mini-css-extract-plugin");
module.exports = {
  entry: './src/javascripts/main.js',
  devtool: "eval-source-map",
  module: {
    rules: [
      {
        enforce: "pre",
        test: /\.js$/,
        exclude: /node_modules/,
        loader: "eslint-loader",
	options: {
          formatter: require('eslint/lib/cli-engine/formatters/stylish')
        }
      },
      {
        test: /\.js$/,
        exclude: /node_modules/,
        use: {
          loader: "babel-loader"
        }
      },
      {
        test: /\.html$/,
        use: [
          {
            loader: "html-loader",
            options: { minimize: true }
          }
        ]
      },
      {
        test: /\.scss$/,
        use: [
          MiniCssExtractPlugin.loader,
            { loader: 'css-loader', options: { sourceMap: true, importLoaders: 1 } },
            { loader: 'sass-loader', options: { sourceMap: true } },
        ],
      },
      {
        test: /\.(png|svg|jpg|gif)$/,
        use: ['file-loader']
      },
      {
        test: /\.(woff|woff2|eot|ttf|otf)$/,
        use: ['file-loader']
      }
    ]
  },
  plugins: [
    new HtmlWebPackPlugin({
      template: "./src/index.html",
      filename: "./index.html"
    }),
    new MiniCssExtractPlugin({
      filename: "[name].css",
      chunkFilename: "[id].css"
    }),
    new webpack.ProvidePlugin({
      $: "jquery",
      jQuery: "jquery"
    })
  ],
  output: {
		path: __dirname + "/build",
		filename: "bundle.js"
	}
};
```
## Step 12
Add some test code to your `index.html`, `main.js`, & `main.scss` files and finally run:
```
npm start
```
# Frontend Dependencies

## Bootstrap
Run `npm install bootstrap --save` and add this to your `main.scss` file:
```css
@import "~bootstrap/scss/bootstrap";
```
For Bootstrap JS, add this to your `main.js` file:
```js
import 'bootstrap';
```
## Fontawesome
Run `npm install @fortawesome/fontawesome-free --save` and add this to your `main.scss` file:
```css
@import "~@fortawesome/fontawesome-free/css/all.min.css";
```
## Images
Add something like this to the file you are adding an image too:
```js
import cat from './assets/cat.jpg';

let domString = `<img src=${cat} alt="picture of a cat"/>`;

document.getElementById('cat').innerHTMl = domString;
```
## Axios
Run `npm install axios --save`
> For every file you will need to make an XHR request in, you will need to require Axios
```js
import axios from 'axios';

const examplePromise = () => new Promise((resolve, reject) => {
  axios.get('http://localhost:3001/example')
    .then((data) => {
      resolve(data);
    })
    .catch((error) => {
      reject(error);
    });
});
```

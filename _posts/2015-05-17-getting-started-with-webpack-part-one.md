---
layout: post
title: "Getting Started With Webpack: Part One"
---

[Webpack](http://webpack.github.io/) is a module bundler that allows us to write modular client-side JavaScript code without having to manage the order in which the modules are loaded in the browser. With support for CommonJS, AMD, and ES6 module systems, integrating 3rd party libraries with your application code has never been simpler. Wepback is an extremely powerful tool that is much more than a module bundler. This series will take you from the basics of installing and configuring Webpack to exploring some of it's more advanced features. 

## Setup

To get started, install Webpack globally:

```bash
$ npm install webpack -g
```

Next, create a directory for the project with this structure:

```
.
├── public
│   └── index.html
├── src
│   └── index.js
└── webpack.config.js
```

Configuring Webpack is very straight foward. For the simplest of setups it only needs the location of the entry JavaScript file and where to output the bundled file.

**webpack.config.js** 

```js
module.exports = {
    entry: './src/index.js',
    output: {
        path: __dirname + '/public',
        filename: 'bundle.js'
    }
}
```

The entry file is where all of the modules needed for a page will be included. You can have multiple entry and output files, a pair for each page of your application, ensuring that you're users aren't being served unused code. 

Let's test that we've set everything up properly:

**src/index.js**  

```js
console.log('Hello Webpack!');
```

**public/index.html**  

```html
<!doctype html>
<html lang="en">
    <head>
        <meta charset="utf-8">
    </head>
    <body>
        <script src="bundle.js"></script>
    </body>
</html>
```

Next, from the root of the project directory run:

```bash
$ webpack
```

Not too exciting yet, but Webpack should have created a file at `public/bundle.js`, and if you load `public/index.html` in the browser you should see "Hello Webpack!" in your console.

## CommonJS Module Loading

Now we'll look at Webpack's ability to load CommonJS style modules in the browser. First, install the popular JavaScript utility library [lodash](https://lodash.com/) in your project directory:

```bash
$ npm install lodash --save-dev
```

Require the lodash library in the entry file, and use it to sort a list of users by name and age:

**src/index.js**  

```js
var _ = require('lodash');

var users = [
    {name: 'Zack', age: 45},
    {name: 'Robby', age: 19},
    {name: 'Alice', age: 67}
];

var byAge = _.sortBy(users, 'age');

console.log(byAge);
```

Run **webpack** from the root of the project and load the page in a browswer. You should see the list of users sorted by age in your console. Very cool. Integrating 3rd party npm packages in your client-side application code with one line.

This can be taken a step further by only requiring the **sortBy** function. This is possible because the lodash npm package breaks each function into it's own module.

**src/index.js**  

```js
var sortBy = require('lodash/collection/sortBy');

var users = [
    {name: 'Zack', age: 45},
    {name: 'Robby', age: 19},
    {name: 'Alice', age: 67}
];

var byAge = sortBy(users, 'age');

console.log(byAge);
```

Run **webpack** again and you should see the same results in your console, but now **bundle.js** only includes the code needed for the **sortBy** function and not the entire lodash library.

We've only scratched the surface of features and power that Webpack can bring to your workflow in this first part of the series. In Part Two we'll look at installing and working with **webpack-dev-server**, a tool that provides file watching, a live reload server, and completely automates the bundling process so you can focus on writing code.


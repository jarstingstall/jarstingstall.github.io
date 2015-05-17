---
layout: post
title: "Getting Started With Webpack: Part One"
---

This is the first installment in a series of posts on [Webpack](http://webpack.github.io/docs/), a module bundler with a great set of features that distinguish it from similar tools. In this post we'll cover setting up Webpack on your machine and loading CommonJS modules in the browser.

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

Configuring Webpack is very straight foward. For the simplest of setups all that's needed is the location of the main entry file and where to output the bundled file. In a future post we'll look at how to set up multiple entry and output files.

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

Nothing too exciting yet, but you should have a bundled file at **public/bundle.js**. If you load **public/index.html** in a browser you should see "Hello Webpack!" in the console.

## CommonJS Module Loading

Now we'll look at Webpack's ability to load CommonJS style modules in the browser. We'll use [lodash](https://lodash.com/) for this example:

```bash
$ npm install lodash --save-dev
```

Require the lodash library and use it to sort a list of users by age:

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

Run **webpack** from the root of the project and load the page in a browser. You should see the list of users sorted by age in the console. Very cool. Integrating 3rd party npm packages in your client-side application code with one line.

This can be taken a step further by only requiring the **sortBy** function. This is possible because the lodash npm package breaks each function into it's own module that can be required individually.

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

Run **webpack** again and you should see the same results in the console, but now **public/bundle.js** only includes the code needed for the **sortBy** function and not the entire lodash library. Modularization for the win!

We've only scratched the surface of Webpack's features and the benefits it can bring to your workflow. In Part Two we'll look at installing and working with **webpack-dev-server**, a tool that provides a file watcher, a live reload server, and completely automates the bundling process so you can focus on writing code.


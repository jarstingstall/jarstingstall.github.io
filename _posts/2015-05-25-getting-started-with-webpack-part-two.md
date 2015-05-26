---
layout: post
title: "Getting Started With Webpack: Part Two"
---

Part Two of this series on Webpack will introduce [webpack-dev-server](http://webpack.github.io/docs/webpack-dev-server.html), a tool that offers a local development server with file watching, automated bundling, and a live reload server.

First, install webpack-dev-server globally:

```bash
$ npm install webpack-dev-server -g
```

Then add some configuration for the server:

```js
// webpack.config.js

module.exports = {
    entry: './src/index.js',
    output: {
        path: __dirname + '/public',        
        filename: 'bundle.js'
    },
    devServer: {
    	contentBase: __dirname + '/public'
    }
}
```

The **devServer.contentBase** option specifies the directory from which content will be served.

This is all that is needed to install and configure the server. From the command line run:

```bash
$ webpack-dev-server
```

Webpack has created the bundle file and started a development server. Visit **localhost:8080** in the browser, and you should see the same results from [Part One](http://jarstingstall.github.io/getting-started-with-webpack-part-one/) of this series in the console. A cool feature of **webpack-dev-server** is that it does not write the bundle files to disc, but instead stores them in memory. To test this out, delete the bundle file at **public/bundle.js** and refresh the page. Look in the console and you should still see the same results.

While **webpack-dev-server** is running, you no longer need to run **webpack** when you make changes to your files. It watches your files and recompile the bundle file when anything changes. To test this out, sort the users by name instead of age:

```js
// src/index.js

var sortBy = require('lodash/collection/sortBy');

var users = [
    {name: 'Zack', age: 45},
    {name: 'Robby', age: 19},
    {name: 'Alice', age: 67}
];

var byName = sortBy(users, 'name');

console.log(byName);
```

Refresh the page in your browser, and you should see the users sorted by name in the console. 

Reloading the page everytime you make a change is tedious, so **webpack-dev-server** comes with a live reload server out of the box. Visiting **localhost:8080/webpack-dev-server/** is all that it takes to initiate it. Now any time you change a file, Webpack will detect the changes, recompile the bundle file, and reload the page in your browser.

Add another user to the array, save the file, and check the console for the additional user:

```js
// src/index.js

var sortBy = require('lodash/collection/sortBy');

var users = [
    {name: 'Zack', age: 45},
    {name: 'Robby', age: 19},
    {name: 'Alice', age: 67},
    {name: 'Carl', age: 32}
];

var byName = sortBy(users, 'name');

console.log(byName);
```

With very little setup and configuration we have a local development server that will watch files for changes, recompile the bundle file, and reload the page in the browser. In Part Three we'll look at Webpack's loaders, a killer feature that allows you to preprocess files as you "require" them and also load in any file (css, html, images, fonts, etc...) as a module. We'll see how Webpack's loaders can eliminate the need for a task based build tool like Grunt or Gulp.

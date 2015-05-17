---
layout: post
title: Getting Started With Webpack: Part One
---

[Webpack](http://webpack.github.io/) is a module bundler that allows us to write modular JavaScript code and not 
have to worry about managing a list of `<script>` tags and the order in which they're loaded in the browser. It supports CommonJS, AMD, and ES6 module systems, providing the ability to easily integrate 3rd party libraries with your application code. It has some killer features, a few of which we'll see soon that, in my opinion, make it more powerful than similar tools.

To get started, install the following npm packages globally:

```bash
$ npm install webpack -g
```

Next, create a fresh directory for the project with this simple structure:

```
.
├── public
│   └── index.html
├── src
│   └── index.js
└── webpack.config.js
```

Configuring Webpack is very straight foward. For the simplest of setups it only needs the location of the entry JavaScript file and where to output the bundled file:

```js
module.exports = {
    entry: './src/index.js',
    output: {
        filename: './public/bundle.js'
    }
}
```

The entry file is where all of the modules needed for a page will be included. You can have multiple entry and output files, a pair for each page of your application, ensuring that you're users aren't being served unused code. 

To test that we have set everything up properly, add the following to `src/index.js`:

```js
console.log('Hello Webpack!');
```

and in `public/index.html`:

```xhtml
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

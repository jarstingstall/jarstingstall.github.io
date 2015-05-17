---
layout: post
title: Building Reusable Components with Angular and Webpack
---

With **Angular 2** in Developer Preview, the API is changing nearly every day, but there is one thing that
we know we can count on: *Components Are King*. Other frontend libraries and tools like **React** and **Webpack** have fully embraced the component approach, and the Angular team is now on board as well. The sooner 
you embrace this approach in your Angular 1.x applications, the easier it will be to upgrade when the time comes. 

In this post, we'll go through the process of creating a reusable component using Angular's current stable version 
(1.3.15). We'll also use Webpack which will allow us to use ES6 features, CommonJS modules in the browser, and structure our code as a stand-alone, reusable component to be dropped into any Angular app.

## Webpack Setup

[Webpack](http://webpack.github.io/) is a module bundler that allows us to write modular JavaScript code and not 
have to worry about managing a list of `<script>` tags and the order in which they're loaded in the browser. It supports CommonJS, AMD, and ES6 module systems, providing the ability to easily integrate 3rd party libraries with your application code. It has some killer features, a few of which we'll see soon that, in my opinion, make it more powerful than similar tools.

To get started, install the following npm packages globally:

```bash
$ npm install webpack webpack-dev-server -g
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

Configuring Webpack is very straight foward. For the most simple setup it only needs the location of the entry javascript file and where to put the bundled file:

```js
module.exports = {
    entry: ['./src/index.js'],
    output: {
        path: './public',
        filename: 'bundle.js'
    }
}
```

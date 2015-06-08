---
layout: post
title: "Getting Started With Webpack - Part Three: Transpiling ES6"
---

Webpack loaders perform the work of "tasks" in Gulp and Grunt and are very similar to "transforms" in Browserify. Building on our work from the previous two posts, let's convert our application code to ES6 and use a loader to transpile it to ES5.  

Loaders can be installed with npm:

```bash
$ npm install babel-loader --save-dev
``` 

The [babel-loader](https://github.com/babel/babel-loader) will allow us to take advantage of ES6 features by transpiling the code to ES5 before being bundled. Setting up loaders is very simple:

```js
// webpack.config.js

module.exports = {
    entry: './src/index.js',
    output: {
        path: './public/',        
        filename: 'bundle.js'
    },
    devServer: {
        contentBase: './public/'
    },
    module: {
        loaders: [
            {test: /\.js$/, exclude: /node_modules/, loader: 'babel'}
        ]
    }
}
```

This configuration tells Webpack to preprocess every module loaded that ends in ".js" with the babel-loader. We also tell it to exclude modules from the node_modules directory. That is all we need to begin utilizing ES6 features in our code!

To test this out let's add a User class to the mix and move the users collection to a separate module.

```js
// src/User.js

export class User {
    constructor(name, age) {
        this.name = name;
        this.age = age;
    }

    get display() {
        return `${this.name} is ${this.age} years old.`;
    }
}
```

```js
// src/users.js

export var users = [
    {name: 'Zack', age: 45},
    {name: 'Robby', age: 19},
    {name: 'Alice', age: 67},
    {name: 'Carl', age: 32}
];
```

Now let's adjust our entry file to use these new modules:

```js
// src/index.js

import sortBy from 'lodash/collection/sortBy';
import {users} from './users';
import {User} from './User';

sortBy(users, 'name')
    .map(user => {
        return new User(user.name, user.age);
    })
    .forEach(user => {
        console.log(user.display);
    });
```

Notice that now we can use the ES6 module system instead of CommonJS which will help with future-proofing our client-side JavaScript code. We import three modules we'll need, sort the users collection by name, create new User objects for each of them, and then log out the display message for each of them.

In the next post we'll look at using Webpack loaders to transpile SASS into CSS and also introduce a modular CSS workflow.


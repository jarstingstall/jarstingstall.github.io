---
layout: post
title: Building Reusable Components with Angular and Webpack
---

While **Angular 2** is only in Developer Preview and the API is changing nearly everyday, there is one point that 
has been made very clear: **Components Are King**. Libraries like **React** and tooling like **Webpack** have fully 
embraced the component approach to frontend developement and the Angular team is now on board as well. The more 
you embrace this approach in your Angular 1.x applications, the easier it will be to upgrade when the time comes. 

In this post, we'll go through the process of creating a reusable component using Angular's current stable version 
(1.3.15). We'll also use Webpack which will allow us to use ES6 features, CommonJS modules in the browser, and structure our code as a stand-alone, reusable component to be dropped into any Angular app.

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



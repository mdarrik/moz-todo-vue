# Vue Basics

## Introduction
Vue is a uniquely progressive JavaScript framework. You can use it as a drop-in replacement for JQuery or to build full Single Page Applications. Vue also takes a progressive approach to writing components. Most components are written using templates, with the option of JSX and render functions when you need a more power to create a component.

The Vue docs are found here: https://vuejs.org

For a good (but biased) comparison between Vue and many of the other frameworks, see [Vue Docs: Comparison with Other Frameworks](https://vuejs.org/v2/guide/comparison.html). 

## Installation and Getting Started
To use Vue in an existing web page, you can simply drop one of the following `<script>` tags into your web page. This is a great way to test out Vue without needing to use a CLI or worry about build tools or bundling. This is also a great option when migrating an existing project from something like JQuery to Vue. However, this isn't great for large or complex projects, especially full-featured SPA's. 

- Development Script (Unoptimized, but includes console warnings)
    ```html
    <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
    ```
- Production Script (Optimized version, minimal console warnings. Recommend that you pin to a version)
    ```html
    <script src="https://cdn.jsdelivr.net/npm/vue@version"></script>
    ```
For more complex apps, you will probably want to use the npm package to create your application. There's also a CLI which has features to help manage and scaffold out your project. To use the NPM package & the CLI you will need 
1. NodeJS 8.11+ installed. 
2. npm or yarn (This guide uses yarn, but everything is similar for npm.)

If you want to use vue without the CLI, make sure that you have a `package.json` created in your project and then run `yarn add vue`. 


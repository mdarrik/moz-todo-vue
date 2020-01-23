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
- Production Script (Optimized version, minimal console warnings. Recommended that you pin to a version)
    ```html
    <script src="https://cdn.jsdelivr.net/npm/vue@version"></script>
    ```
For more complex apps, you will probably want to use the npm package to create your application. There's also a CLI which has features to help manage and scaffold out your project. To use the NPM package & the CLI you will need 
1. NodeJS 8.11+ installed. 
2. npm or yarn (This guide uses yarn, but everything is similar for npm.)


To install the CLI, run the following command in your terminal of choice: `yarn global add @vue/cli`

To initialize the project, open a terminal in the folder you want to create the project in and run `vue create mdn-reading-list`.

The CLI will give you a list of project configurations you can use. There are a few preset ones, and you can make your own. These options let you configure things like Typescript, linting, vue-router, testing, and more.

Use the arrow keys to select the `manually select features` option. When you do, you'll see a list of options. Make sure that `Babel` and `Linter / Formatter` are selected. Once they are, press <kbd>enter</kbd>. 

Next, it will ask you to select a config for the linter / formatter. We'll keep it at `Eslint with error prevention only`, so just click <kbd>enter</kbd> again. This will help us catch common errors, but not be overly opinionated. 

Next, it will ask you about whether it should do any automated linting. `Lint on save` will check for errors when we save, so select that. If you want it to fix issues when you commit code, navigate to `Lint and fix on commit`, and use the <kbd>space</kbd> key to select that option. 

Then, it will ask you about where you want your config files. I find having dedicated config files easier to manage, so I'd recommend selecting `In dedicated config files`. This will separate out configuration settings into their own files. The other option will put all of your config settings inside your `package.json`, which can make it hard to reason about your settings since the `package.json` is full of other information already.

Lastly, it will ask you if you want to save this as a preset. This will put it in that first menu so you don't have to always manually select your preferred options. If you like these options, feel free to type <kbd>y</kbd>. Otherwise, type <kbd>N</kbd> and hit <kbd>enter</kbd>. The CLI will begin scaffolding out your project, and installing all of your dependencies. 



# Vue Basics

## Introduction

Vue is a uniquely progressive JavaScript framework. You can use it as a drop-in replacement for JQuery or to build full Single Page Applications. Vue also takes a progressive approach to writing components. Most components are written using templates, with the option of JSX and render functions when you need more control in creating components.

The Vue docs are found here: https://vuejs.org

For a good (but potentially biased) comparison between Vue and many of the other frameworks, see [Vue Docs: Comparison with Other Frameworks](https://vuejs.org/v2/guide/comparison.html).

## Prerequisites

To get started with Vue, you'll need to have a working knowledge of HTML and JavaScript. This is Vue components are written as a combination of JavaScript objects and an HTML-based template syntax. The JS objects manage your data, while the template syntax maps to the underlying DOM structure. To use some of the more advanced features of Vue, like Single File Components or render functions, you'll need a terminal with node + npm installed.

## Installation and Getting Started

To use Vue in an existing site, you can drop one of the following `<script>` tags onto a page. This allows you to start using Vue on existing sites, and why Vue prides itself on being a progressive framework. This is a great option when migrating an existing project using something like JQuery to Vue. With this method, you can use a lot of the core features of Vue, such as the attributes, custom components, and data-management.

- Development Script (Unoptimized, but includes console warnings. Great for development.)
  ```html
  <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
  ```
- Production Script (Optimized version, minimal console warnings. Recommended that you pin to a version to prevent potentially breaking changes.)
  `html <script src="https://cdn.jsdelivr.net/npm/vue@version"></script>`
  However, this approach has some limitations. To build more complex apps, you'll want to use the NPM package. This will let you use advanced features of Vue and take advantage of bundlers like WebPack. To make building apps with Vue easier, there is a CLI to streamline the development process. To use the NPM package & the CLI you will need

1. NodeJS 8.11+ installed.
2. npm or yarn.

To install the CLI, run the following command in your terminal:

npm: `npm install --global @vue/cli`.
yarn: `yarn global add @vue/cli`
Note: This will install the CLI globally, so you'll need to have the appropriate permissions.

To initialize the project, open a terminal in the folder you want to create the project in and run `vue create {project-name}`.

The CLI will then give you a list of project configurations you can use. There are a few preset ones, and you can make your own. These options let you configure things like Typescript, linting, vue-router, testing, and more.

Use the arrow keys to navigate to the configuration you want to use and select it with <kbd>enter</kbd>. To customize the configuration for your project, you can select the `manually select features` option. We won't go over all of the options here, but you can find more information on the CLI at https://cli.vuejs.org

### Initialize A New Project

To make it easier to explore various features in Vue, we will be building parts of an app to manage your reading list of MDN articles. To practice using the CLI, you can follow along with the setup options below.

1. Run `vue create mdn-reading-list`
2. Use the arrow keys to select the `manually select features` option.
3. Make sure that `Babel` and `Linter / Formatter` are selected. Once they are, press <kbd>enter</kbd>.
4. Select a config for the linter / formatter. Navigate to `Eslint with error prevention only`, and just hit <kbd>enter</kbd> again. This will help us catch common errors, but not be overly opinionated.
5. Configure automated linting. Select `Lint on save`. This will check for errors when we save. If you want it to fix issues when you commit code, navigate to `Lint and fix on commit`, and use the <kbd>space</kbd> key to select that option. Either way, hit <kbd>enter</kbd> to continue.
6. Select how you want your config files to be managed. `In dedicated config files` will put your config settings for things like ESLint into their own, dedicated file. The other option will put all of your config settings into your `package.json`. Select `In dedicated config files` and push <kbd>enter</kbd>.
7. Decide if you want to save this as a preset for future options. This is entirely up to you. If you like these settings over the existing presets and want to use them again, type <kbd>y</kbd>, otherwise type <kbd>N</kbd>.
   After this, the CLI will begin scaffolding out your project, and installing all of your dependencies.

### Project Structure

If everything went successfully, the CLI should have created a series of files and directories for your project.

- .eslintrc.js: this is a config file for eslint. You can use this to manage your linting rules.
- babel.config.js: this is the config file for babel. You can register additional babel plugins here.
- .browserslistrc: this is a config for [Browserslist](https://github.com/browserslist/browserslist). You can use this to control which browsers your tooling optimizes for.
- public: this folder contains static assets that are published, but not processed by webpack during build (with one exception, index.html gets some processing).
  - favicon.ico: this is the favicon for your app. Currently, it's the Vue logo.
  - index.html: this is the template for your app. Your Vue app is mounted into this template, and you can use lodash template syntax to interpolate values into it. Note: this is not the template for managing the layout of your application, this template is for managing static html that is outside of your Vue app.
- src: this folder contains the core of your Vue app.
  - main.js: this is the entry point to your application. Currently, this file mounts your Vue application.
  - App.vue: this is the top-level component in your Vue app.
  - components: this folder is where you keep your components. Currently it just has one example component.
  - assets: This folder is for keeping static assets like CSS and images. Because these files are in the source directory, they can be processed by Webpack. This means you can use pre-processors like SCSS or Stylus.

## .Vue files (Single File Components)

Like in many front-end frameworks, components are a central part of building apps in Vue. These components let you break a large application into discrete building blocks. These small blocks can help you reason about and test your code.

While some frameworks encourage you to separate your template, logic, and CSS into separate files, Vue takes the opposite approach. Using [Single File Components](https://vuejs.org/v2/guide/single-file-components.html), Vue lets you group your templates, corresponding code, and CSS altogether in a single file ending in .Vue. These files are processed by a JS build tool (like Webpack), which means you can take advantage of build-time tooling in your project. This allows you to use tools like Babel, TypeScript, SCSS and more to create more sophisticated components.

As a bonus, projects created with the CLI are configured to use .Vue files with Webpack out of the gate. In fact, if you look inside the `src` folder in the project we created with the CLI, you'll see your first `.vue` file: `App.vue`.

If you open your `App.vue` file, you'll see that Single File Components have three parts: `<template>`, `<script>`, and `<style>`. These three parts correspond to to their corresponding tags in a standard HTML file.

`<template>` is the markup of your component. All of the HTML for your component goes here. Your template can contain any valid HTML, as well as some Vue-specific syntax which we'll cover later. By setting the lang attribute on the template tag, you can use Pug template syntax instead. e.g. `<template lang="pug">`

`<script>` contains all of the non-display logic of your component. This is where you locally register components, define component inputs (props), handle local state, define methods, and more. In the case of `App.Vue`, the script tag is currently setting it's name to "app" and registering the "HelloWorld" Component by adding it to the `Components` object. When you register a component in this way, you're registering it locally. Locally registered components can only be used inside the components that register them. This can be useful for bundle splitting/tree shaking. When using Typescript, you can set the "lang" on the script tag to signify to your compiler that you're using TypeScript, e.g. `<script lang="ts">`

<figure>

```js
import HelloWorld from './components/HelloWorld.vue';

export default {
  name: 'app',
  components: {
    //You can register components locally here.
    HelloWorld
  }
};
```

<figcaption>The contents of the script tag within `App.Vue` generated by the Vue CLI. </figcaption>
</figure>

`<style>` is where you can write CSS. If you add a `scoped` attribute (`<style scoped>`), Vue will scope the styles to the contents of your SFC. This works similar to CSS-in-JS solutions, but allows you to just write plain CSS. If you selected a CSS pre-processor via the CLI, you can add a lang attribute to the style tag so that the contents can be processed by webpack (e.g. `<style lang="scss">` will allow you to write scss instead).

## Running our app locally

The Vue CLI comes built in with a development server. This allows you to run your app locally so you can test it without needing to configure a server yourself. The CLI even added the command to your package.json as a script. So in your terminal, you can run `npm run serve` or `yarn serve`.
Your terminal should output something like the following:

```bash
$ vue-cli-service serve
 INFO  Starting development server...
98% after emitting CopyPlugin

 DONE  Compiled successfully in 18121ms

  App running at:
  - Local:   http://localhost:8080/
  - Network: http://192.168.1.9:8080/

  Note that the development build is not optimized.
  To create a production build, run npm run build.
```

If you navigate to the "local" address (this should be something like http://localhost:8080 but may vary based on setup) output by the CLI, you should see your app. Right now, it should have a welcome message, a link to the documentation, links to the plugins you added when you initialized the app with your CLI, and then some more links to the Vue community and ecosystem.
![The initial Vue app created by the CLI](article-images/initial-app-screenshot.png).

<aside>If you want to keep track of this in git, now is a good time to check everything in.</aside>

Let's make our first change to the app; let's delete the Vue logo from our app. Open the `App.vue` file. In the template section, you'll see an `img` tag with the alt text "vue logo". Delete that. If your app is still running, you should see the logo removed from the site almost instantly. Let's also remove the HelloWorld component from our template. We can also remove it from the "components" object in the script tag.

With the HelloWorld component removed, we'll need a new h1 for our page. Let's add a new h1 inside the `<div id="app">`. Since we're going to be making a todo app, let's set our text to "My Todo List".

## Creating Our First Component

Let's create our first component. We'll make a component to display a single todo item. We'll use this to build our list of todos. In `src/components` folder, create a new file named "ToDoItem.vue". In your new file, create the template section by adding `<template></template>`. Also create a `<script>` section. Inside the script tags, add a default exported object `export default {}`. This exported object is your component object. Your file should now look like this:

```html
<template> </template>
<script>
  export default {};
</script>
```

We can no begin to add actual content to our ToDoItem. Vue templates are only allowed a single root element. This means that one element needs to wrap everything inside the template section. In this instance, we can use a `div` for that root element. Add a `div` to your component now. Inside that `div`, let's add a checkbox and a corresponding label. Don't forget to add an id to the checkbox, and a "for" attribute mapping the checkbox to the label.

```html
<template>
  <div>
    <input type="checkbox" id="todo-item" checked="false" />
    <label for="todo-item">My Todo Item</label>
  </div>
</template>
```

This is great, but we haven't added the component to our app yet, so there's no way to test and see if everything is working. Navigate back to App.Vue. At the top of your script tag, import your ToDoItem component: `import ToDoItem from './components/ToDoItem.vue`. Then, inside your component object, add ToDoItem to the components option. This is the same way that the HelloWorld component was registered by the Vue CLI earlier. Then, up in your template tag, we can add our ToDoItem. Underneath the h1, create an unordered list `<ul>`, and inside a `<li>` add `<to-do-item  />`. Your App.vue should now look something like this:

```html
<template>
  <div id="app">
    <h1>My Todo List</h1>
    <ul>
      <li>
        <to-do-item />
      </li>
    </ul>
  </div>
</template>

<script>
  import ToDoItem from './components/ToDoItem.vue';

  export default {
    name: 'app',
    components: {
      ToDoItem
    }
  };
</script>

<style>
  #app {
    font-family: 'Avenir', Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    margin-top: 60px;
  }
</style>
```

If you check your app, you should see your ToDo Item! You can see that we have a component with a checkbox and a label. However, it's still not very useful because we can only really include this once on a page (id's need to be unique). We also have no way to set the label text. Nothing about this is dynamic. What we need is some component state. Specifically, we'll need to add props to our component. You can think of props similar to inputs in a function. The value of a prop gives components an initial state that affects their display. In Vue, there are 2 ways to register props. The first way is to just list props out as an array of strings. Each entry in the array corresponds to the name of a prop. The second way is to define props as an object, with each key corresponding to the prop name. Listing props as an object allows you to specify default values, mark props as required, perform basic object typing (specifically around JS primitive types), and you can perform some simple prop validation. It's worth noting that prop validation only happens in development mode, so you can't strictly rely on it in production. Additionally, prop validation functions occur before the component instance is created, so they **do not** have access to the component state (or other props).

For this component, we'll use the object registration. Add a props object, with a "label" key. For the label key, create an object with 2 properties. The first, is a "required" property, which will have a value of true. This will tell Vue that we expect every instance of this component to have a "label" field. Vue will warn us if a ToDoItem component does not have a label field. The second property we'll add is a "type" property. Set the value for this property as the JavaScript "String" type (note the capital "S"). This tells Vue that we expect the value of this property to be a string. Next, we'll add a second prop, "checked". On this prop, add a "default" field, with a value of `false`. This means that when no "checked" prop is passed to a ToDoItem component, the "checked" prop will will have a value of false. Next add a "type" field with a value of "Boolean". This tells Vue we expect the value prop to be a JavaScript boolean type. Your component object should now look like this:

```html
<script>
  export default {
    props: {
      label: { required: true, type: String },
      checked: { default: false, type: Boolean }
    }
  };
</script>
```

We can now add the "label" prop to the component template. In your template, replace the contents of the `<label>` with `{{label}}`. `{{}}` is a special template syntax in Vue. This let's us print the result of JavaScript expressions inside our template. It's important to know that content inside `{{}}` is displayed as text and not HTML. We are also able to access values and methods defined on our component object. In this case, we're printing the value of the label prop.

Your component's template section should now look like this:

```html
<template>
  <div>
    <input type="checkbox" id="todo-item" checked="false" />
    <label for="todo-item">{{label}}</label>
  </div>
</template>
```

If you check the app in your browser, you'll see a checkbox without a label (oh no!). If you open the console in the browser, you'll see an error.

```js
[Vue warn]: Missing required prop: "label"

found in

---> <ToDoItem> at src/components/ToDoItem.vue
       <App> at src/App.vue
         <Root>
```

We marked the `label` as a required prop, but we never gave the component that prop. Let's fix that.
In your `App.vue` file, just add a "label" to the to-do-item component like it's an html attribute.

```html
<li>
  <to-do-item label="My ToDo Item" />
</li>
```

As soon as you save those changes, you should see your label appear next to your lone checkbox. If you change the text, you should see it update. This is great. We have a checkbox, with an updatable label. However, we're currently not doing anything with the "checked" prop. We want to match the component's "checked" prop to the "checked" attribute on the input element. However, it's important that props serve as one-way data binding. This means that a component should never alter the value of its own props. There are a lot of reasons for this. In part, components editing props can make debugging a challenge. If a value is passed to multiple children, it could be hard to track where the changes to that value were coming from. As well, changing props can cause components to re-render. So mutating props in a component would trigger the component to rerender, which may in-turn trigger the mutation again. To work around this, we can manage the "checked" state using Vue's `data` property. The `data` property is where you can manage local state in a component. The data property has the following structure: 

```js
data() { 
  return {
    key: value 
  }
}
```
You'll note that the data attribute is a function. This is to keep the data values unique for each instance of a component. If data is just an object, all instances of component will share the same values. This is a side-effect of the way Vue registers components and something you do not want. You also should not use an arrow function for the data property. You use `this` to access a component's props and other properties from inside data. Because of the way that `this` works in arrow functions (binding to the parent's context), you won't be able to access any of the necessary attributes from inside data if you used an arrow function. 

So let's add a data attribute to our ToDoItem component. We can call the data value isChecked. Our component script should now look like this: 

```js
export default {
    props: {
        label: {required: true, type: String},
        checked: {default: false, type: Boolean}
    },
    data() {
        return {
           isChecked : this.checked
        }
    },
}
```

You can see that Vue does a little magic here. Vue will bind all of your props directly to the component instance, so we don't have to call `this.props.checked`. Vue will also bind your `data`, `methods`, `computed`, and similar attributes directly to the instance. This is, in part, to make them available to your template. The down-side to this is that you need to keep the keys unique across these attributes. It's why we called our `data` attribute "isChecked" instead of just "checked". 

So now we need to attach the isChecked property to our component. Similar to how Vue uses `{{}}` expressions to display JavaScript expressions inside templates, Vue has a special syntax to bind JS expressions to html elements and components: `v-bind`. The v-bind expression looks like this: `v-bind:attribute="expression"`. In other words, you prefix whatever attribute/prop you want to bind to with v-bind. In most cases, you can also use a shorthand for the v-bind property, which is to just prefix the attribute/prop with a colon. So `:attribute="expression"` is the same thing as `v-bind:attribute="expression"`. So in the case of the checkbox in our todo item component, we can use v-bind to map the `isChecked` property to the `checked` property on the input element. Both of the following are equivalent: 

```html
<input type="checkbox" id="todo-item" v-bind:checked="isChecked" />
```

```html
<input type="checkbox" id="todo-item" :checked="false" />
```
You're free to use whichever pattern you would like. It's best to keep it consistent though. Because the shorthand syntax is more commonly used, this tutorial will stick to that pattern.

Test out your component by passing `:checked="true"` to the ToDoItem from `App.vue`. Note that you need to use the v-bind syntax, because otherwise true is passed as a string. The displayed checkbox should be checked. 

```html
<template>
  <div id="app">
    <h1>My Todo List</h1>
    <ul>
      <li>
        <to-do-item label="My ToDo Item" checked="true" />
      </li>
    </ul>
  </div>
</template>
```

Here's a screenshot showing what your site should look like: 
![A screenshot of the Vue app with a single to do item on the screen, marked as done.](article-images/single-checked-checkbox-screenshot.png)

Great! We now have a working checkbox where we can set the state programmatically. However, we still can only keep one item on the page because the id is static. This would result in errors with assistive technology since the id is needed to correctly map labels to their checkbox. To fix this, we can programmatically set the id in the component data. To help keep the id unique, we can use `lodash.uniqueid` to help keep the index unique. This package exports a function that takes in a string and appends a unique integer to the end of the prefix. This will be sufficient for keeping component ids unique. Let's add the package to our project with npm. 

npm: `npm install --save lodash.uniqueid`

yarn: `yarn add lodash.uniqueid`

We can now import this package into our ToDoItem component. We can then add an id field to our data property. 

```js
import uniqueId from 'lodash.uniqueid'
export default {
    props: {
        label: {required: true, type: String},
        checked: {default: false, type: Boolean}
    },
    data() {
        return {
           isChecked : this.checked,
           id: uniqueId('todo-')
        }
    },
}
```

Next, we should bind the id to both our checkbox's `id` attribute and the label's `for` attribute. 

```html
<template>
    <div><input type="checkbox" :id="id" :checked="isChecked" /><label :for="id">{{label}}</label></div>
</template>
```


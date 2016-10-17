#VueJS
Vue (pronounced /vjuː/, like view) is a progressive framework for building user interfaces. Unlike other monolithic frameworks, Vue is designed from the ground up to be incrementally adoptable. The core library is focused on the view layer only, and is very easy to pick up and integrate with other libraries or existing projects. On the other hand, Vue is also perfectly capable of powering sophisticated Single-Page Applications when used in combination with [modern tooling](http://vuejs.org/guide/single-file-components.html) and [supporting libraries](https://github.com/vuejs/awesome-vue#libraries--plugins).

###Installation

> * **NPM**

> ```
# latest stable
$ npm install vue
> ```

> ```
# dev build
git clone https://github.com/vuejs/vue.git node_modules/vue
cd node_modules/vue
npm install
npm run build
> ```

> * **Bower**

> ```
# latest stable
$ bower install vue
> ```

###Introduction

At the core of Vue.js is a system that enables us to declaratively render data to the DOM using straightforward template syntax:

######HTML
```
<div id="app">
  {{ message }}
</div>
```

######JS
```
var app = new Vue({
  el: '#app',
  data: {
    message: 'Hello Vue!'
  }
})
```

* **[Instance](instance.md)**

* **[Template Syntax](template-syntax.md)**

* **[Computed Properties and Watchers](computed-properties-and-watchers.md)**

* **[Class and Style Bindings](class-and-style-bindings.md)**

* **[Conditional Rendering](conditional-rendering.md)**

* **[List Rendering](list-rendering.md)**

* **[Event Handling](event-handling.md)**

* **[Form Input Bindings](form-input-binding.md)**

* **[Component](component.md)**


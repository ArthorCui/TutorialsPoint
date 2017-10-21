### Template Syntax

##### Interpolations

* **Text**

The mustache tag will be replaced with the value of the `msg` property on the corresponding data object. It will also be updated whenever the data object’s `msg` property changes.
```
<span>Message: {{ msg }}</span>
<span v-once>This will never change: {{ msg }}</span>
```

* **Raw HTML**

The contents are inserted as plain HTML - data bindings are ignored. Note that you cannot use `v-html` to compose template partials, because Vue is not a string-based templating engine. Instead, components are preferred as the fundamental unit for UI reuse and composition.

```
<div v-html="rawHtml"></div>

```

* **Attributes**

Mustaches cannot be used inside HTML attributes, instead use a v-bind directive:
It also works for boolean attributes - the attribute will be removed if the condition evaluates to a falsy value:

```
<div v-bind:id="dynamicId"></div>
<button v-bind:disabled="someDynamicCondition">Button</button>
```

* **Expression**

So far we’ve only been binding to simple property keys in our templates. But Vue.js actually supports the full power of JavaScript expressions inside all data bindings:

```
{{ number + 1 }}
{{ ok ? 'YES' : 'NO' }}
{{ message.split('').reverse().join('') }}
<div v-bind:id="'list-' + id"></div>
```

* **Filters**

Vue.js allows you to define filters that can be used to apply common text formatting. Filters should be appended to the end of a mustache interpolation, denoted by the “pipe” symbol: `{{ message | capitalize }}`

The filter function always receives the expression’s value as the first argument.

```
new Vue({
  // ...
  filters: {
    capitalize: function (value) {
      if (!value) return ''
      value = value.toString()
      return value.charAt(0).toUpperCase() + value.slice(1)
    }
  }
})
```

##### Directives

Directives are special attributes with the `v-` prefix. Directive attribute values are expected to be a single JavaScript expression (with the exception for `v-for`, which will be discussed later). A directive’s job is to reactively apply side effects to the DOM when the value of its expression changes. Let’s review the example we saw in the introduction:

```
<p v-if="seen">Now you see me</p>
```

* **Arguments**

Some directives can take an “argument”, denoted by a colon after the directive name. For example, the v-bind directive is used to reactively update an HTML attribute:

```
<a v-bind:href="url"></a>
<a v-on:click="doSomething">
```

* **Modifiers**

Modifiers are special postfixes denoted by a dot, which indicate that a directive should be bound in some special way. For example, the `.prevent` modifier tells the `v-on` directive to call `event.preventDefault()` on the triggered event:

```
<form v-on:submit.prevent="onSubmit"></form>
```

##### Shorthands

* **`v-bind` Shorthand**

```
<!-- full syntax -->
<a v-bind:href="url"></a>
<!-- shorthand -->
<a :href="url"></a>
```

* **`v-on` Shorthand**

```
<!-- full syntax -->
<a v-on:click="doSomething"></a>
<!-- shorthand -->
<a @click="doSomething"></a>
```
They may look a bit different from normal HTML, but `:` and `@` are valid chars for attribute names and all Vue.js supported browsers can parse it correctly. In addition, they do not appear in the final rendered markup. The shorthand syntax is totally optional, but you will likely appreciate it when you learn more about its usage later.

# Vue
- Questions left: 3 - 17, 19 - 230

## Core features
<details>
<summary>Why should you choose Vue?</summary>

- if you want to learn faster (choose React or Vue instead of Angular)
- if your project is going to develop gradually in many steps, extending the functionality (choose React or Vue due to the best compatibility)
- when state becomes difficult to handle with vanilla JavaScript
- focus on logic and not on preventing your application from exploding
- huge ecosystem, community, high performance, development
- easy to use with multi page applications for widgets
- easy to rewrite legacy into vue
- works with a copy of DOM (compares to the actual DOM, renders only the changed parts, less traffic used, good for mobile device)

</details>

<details>
<summary>What are the key concepts of Vue?</summary>

- declarative approach
- Virtual DOM: It uses virtual DOM similar to other existing frameworks such as ReactJS, Ember etc. Virtual DOM is a light-weight in-memory tree representation of the original HTML DOM and updated without affecting the original DOM
- Components: Used to create reusable custom elements in VueJS applications
- Templates: VueJS provides HTML based templates that bind the DOM with the Vue instance data
- Routing: Navigation between pages is achieved through vue-router
- Light weight: VueJS is light weight library compared to other frameworks

</details>

## Setup
## Vue CLI
## Templates
## Directives
## Data
## Methods
## Events
<details>
<summary>How to listen to the events?</summary>

- with `v-on` directive or shortcut `@`
```HTML
<div id="event">
  <button v-on:click="console.log(message)">Click!</button>
  <!-- or -->
  <button @click="console.log(message)">Click!</button>
</div>
```
```JavaScript
Vue.createApp({
  data() {
    return {
      message: 'Hello!'
    }
  }
}).mount('#event');
```

</details>

<details>
<summary>How to handle the events with using methods?</summary>

```HTML
<div id="event">
  <button @click="printMessage">Click!</button>
</div>
```
```JavaScript
Vue.createApp({
  data() {
    return {
      message: 'Hello!'
    }
  },
  methods: {
    printMessage(evt) {
      console.log(evt.target, this.message);
    }
  }
}).mount('#event');
```

</details>

<details>
<summary>How to access the browser event using methods with arguments?</summary>

```HTML
<div id="event">
  <button @click="printMessage('Harry', $event)">Click!</button>
</div>
```
```JavaScript
Vue.createApp({
  data() {
    return {
      message: 'Hello!'
    }
  },
  methods: {
    printMessage(name, evt) {
      console.log(evt.target, name + ' ' + this.message);
    }
  }
}).mount('#event');
```

</details>

<details>
<summary>Learn more</summary>

- [Event Handling](https://v3.vuejs.org/guide/events.html)

</details>

## Computed Properties
## Watchers
## Conditional Rendering
## Lists Rendering
## Components
## Component Communication
## Forms
<details>
<summary>What is and how to implement the two-way binding?</summary>

- combination of event and data binding
- instead of `v-bind:value v-on:input` there is a shortcut directive `v-model`
```HTML
<input v-model="name" type="text">
<p>Name is: {{ name }}</p>
```

</details>

## HTTP Requests
## Routing
## Behind the scenes
## Animations
## Vuex
## Authentication
## Deployment
## Optimizations
## Composition API

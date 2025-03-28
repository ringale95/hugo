+++
date = '2025-03-08T15:53:47-05:00'
draft = true
title = 'Vue'
+++

## Vue

Vue is a JavaScript framework for building user interfaces. It builds on top of standard HTML, CSS, and JavaScript and provides a declarative, component-based programming model that helps you efficiently develop user interfaces of any complexity.

- We use `<template>` to describe what UI should look like on JS state. Vue takes care of rendering correct HTML without manipulating DOM.
- Vue tracks JS changes and updates DOM

```
<template>
  <h1>Hello, {{ name }}!</h1>
</template>

<script setup>
import { ref } from 'vue';

const name = ref('John');
</script>
```

API styles:
 - Options API
 - Composition API

Options API: We define component's logic using object of options like `data`, `methods`, `mounted`.

`data()`: 
- Properties returned from data() become `reactive()` meaning Vue will track changes and update UI.
- This helps in initialization of app so if you perform any computation here it will not work. use 'computed()' for that

```
<template>
<h1>Count: {{ count }} </h1>
<button @click="increment">Increase</button>
</template>

<script>
    export default{
        data(){
            return{
                count:0; // Vue will track this. Here count is reactive
            };
        },
        methods:{
            increment(){
                this.count++;   //Vue will track this change and update UI
            }
        }
    }
</script>
```
`data()`:
- Function that returns initial reactive state of the component. Returns plain Javascript object which contain properties which will be made reactive by Vue. Data object can be accessed by `this.$data`.

We can directly access via `this` which is equivalent to `this.$data`   
- Cannot add new properties.
- Do not Use '_' or '$' prefixes. Use normal names like "mydata"
- Do not return browser API objects like 'localStorage'

## Navbar:
We create Navbar using Bootstrap: Set its data inside data() and bind it to html attribute:
```
<template>
<nav>
    <div v-for="link in links">
        <a :href="link.url">{{link.text}}</a>
    </div>
</nav>
</template>

(data(){
    links:{
        [ 
            {text:'Home', url:'/'},
            {text:'About', url:'/about'},
          {text:'Contact', url:'/contact'}]
    }
}).mount('nav');
```

## JS code in Vue:
 - Uses keywords like if, return, function, const, let, import;
 - Has (), {}, ';'
 - Inside `<script>` tag in html and vue script block
 - Calculation, logic, events, interactivity
 - `@click` is vue binding syntax.

## Data binding:
- Connects data in javascript code to DOM element(HTML elements). When data changes vue upates DOM making UI reactive.
- Types of Data Binding:
  - One Way (v:bind or :). Updates DOM when data changes
  - Two Way (v-model) Syncs data both ways: from JavaScript to DOM and from user input back to JavaScript

One way binding means changes in Vue instance update the DOM but changes to DOM do not update DOM instance by {{ }} and 'v-bind or :', class or css binding ':class="isActive? 'active': 'inactive'""
```
<template>
    <img :src="imageUrl" />
</template>

<script setup>
    import { ref } from "vue";
    const imageURL = ref('https://vuejs.org/images/logo.png');
</script>
```

### Binding HTML content:
`v-html` leads to rendering raw HTML which can lead to XSS.
```
<template>
    <div v-html="htmlContent"></div>
</template>

<script>
import { ref } from 'vue';
const htmlContent = ref("this is bold");
</script>
```

### Binding data to list items

For css class binding. 
- If there is more than one or space in between classes like 'navbar-light bg-light' use it as a string.
  
```
Example:
 <nav 
 class="navbar navbar-expand-light"
 :class='navbar-light navbar-bg-light': !useDarkNavbar, 'navbar-dark bg-dark': useDarkNavBar
 >
 </nav>

 <ul>
    <li>
        <a class ="nav-link"
        :class="{active: activePage == index}">Home </a>    //for single word do not use ''
    </li>
 </ul>
```
```
<template>
<ul>
    <li v-for="(item, index)" in items" :key="index">{{ item }} </li>
</ul>
</template>

<script>
import { ref } from 'vue';

const items = ref(['Apple', 'Banana', 'Cherry']);
</script>
```

## Pass data from a parent component to child using v-bind
```
<template>
    <ChildComponent :message="parentMessage" />
</template>

<script>
const parentMessage = ref("Hello from Parent!");
</script>
```
## Two way data binding

When user enters the data in input field vue updates automatically.

```
<template>
  <input v-model="name" placeholder="Enter your name" />
  <p>Hello, {{ name }}!</p>
</template>

<script setup>
import { ref } from 'vue';

const name = ref('');
</script>

```

### Binding to computed property
Computed properties are useful for dynamically calculating values based on reactive data. Instead of writing complex logic inside template  you can bind an entire object to element. Use computed if we want to just return the result. As it does not change the value. Use method when we want to perform action that changes state

```
const classObj = computed(()=>({
    active: isActive.value && !error.value;
    'text-danger': error.value && error.value.type === 'fatal'
}))

<template>
    <div :class="classObject">Data </div>
</template>
```

### Event handling
- We use vue directive `v-on:eventName` liek `v-on:click` or we use `@click=""`.
- On click we need to track which page is clicked so we store that in activepage variable which is the index of pages.
- We show title and content for that page
- @click.prevent -> prevents default behavior of  an element when clicked. Like the submit button on form will refresh the page. So we dont want that we do @submit.prevent. Similarly, clicking the link will navigate away from the page. If we want to stop that behavior we do "@click.prevent" which will not let the link navigation.


### computed() property:
Putting too much logic in template will make it bloated. So compute some logic in this property are functions that will execute. So here it will execute to generate the value.


Computed properties are cached based on reactive dependencies whereas methods are not cached. It will only re-evaluate if some of its reactive dependencies have changed. But then this also means that Date.now() will never update because it is not a reactive dependency. Mostly computed property are getter. If we need two way data binding use getter and setter.

Do not modify reactive state inside computed property like:
count.value++;

Avoid async await in computed();

Method invocation will always run if method is invoked whenever re-render happens

Vue 3.4+ has a new feature wherein computed property can access its previous value too

### CSS binding:

Object Syntax (v-bind:class="{ className: condition })
Array Syntax (v-bind:class="[class1, class2])

To bind using arrays for classes:
```
:class="[useDarkNavbar ? 'bg-dark' : 'bg-light', 'navbar', 'navbar-expand-lg']"

//Here  'navbar', 'navbar-expand-lg' will always be applied but other based on conditions
```

Object binding for classes:
```
<template>
  <p :class="{ active: isActive, 'text-danger': hasError }">Hello Vue!</p>
</template>
```

```
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <link
      href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/css/bootstrap.min.css"
      rel="stylesheet"
      integrity="sha384-QWTKZyjpPEjISv5WaRU9OFeRpok6YctnYmDr5pNlyT2bRjXh0JMhjY6hW+ALEwIH"
      crossorigin="anonymous"
    />
    <script src="https://unpkg.com/vue@3/dist/vue.global.js"></script>
    <title>Document</title>
  </head>
  <body>
    <nav 
    :class="[`navbar-${theme}`,`bg-${theme}`,'navbar','navbar-expand-lg']">
      <a class="navbar-brand" href="#">Navbar</a>
      <button
        class="navbar-toggler"
        type="button"
        data-toggle="collapse"
        data-target="#navbarNavAltMarkup"
        aria-controls="navbarNavAltMarkup"
        aria-expanded="false"
        aria-label="Toggle navigation"
      >
        <span class="navbar-toggler-icon"></span>
      </button>
      <div class="collapse navbar-collapse" id="navbarNavAltMarkup">
        <div v-for="(page,index) in pages" class="navbar-nav" :key="index">
          <a
            class="nav-item nav-link"
            :class="{'active':activePage === index}"
            :href="page.link.url"
            
            @click.prevent="activePage = index"
            >{{ page.link.text }}
          </a>
        </div>
      </div>
        <form>
            <button class="btn btn-primary" @click.prevent="changeTheme()">
              Toggle
            </button>
          </form>
    </nav>
    <div id="content" class="container">
      <h1>{{ pages[activePage].pageTitle }}</h1>
      <p>{{ pages[activePage].content }}</p>
    </div>

    <script>
      Vue.createApp({
        methods:{
            changeTheme(){
                let theme = 'light';
                if(this.theme == 'light')
                 theme = 'dark';
                
               this.theme = theme;
            }
        },
        data() {
          return {
            useDarkNavbar: false,
            activePage: 0,
            theme: "dark",
            pages: [
              {
                link: { text: "Home", url: "index.html" },
                pageTitle: "Home page",
                content: "This is homepage",
              },
              {
                link: { text: "About", url: "about.html" },
                pageTitle: "About page",
                content: "This is about page",
              },
              {
                link: { text: "Contact", url: "contact.html" },
                pageTitle: "Contact page",
                content: "This is contact page",
              },
            ],
          };
        },
      })
      app.mount("body");
    </script>
  </body>
</html>
```

## Component creation:

Props are read only we can't change them inside of component. Data flows from parent to child. If we change the value of props inside child parent will not know that the value is changed. 

How can child notify the parent that data changed?
- We use event like click

## Vue cli

Install vue globally: 
```
 npm install @vue/cli -g
 vue create vue-start-spa
```
Select Babel: a compiler which allows us to use new javascript functions that browser do understand.

### Understanding babel.config.js and tsconfig.js or jsconfig.js and module?

The "module" option in JavaScript or TypeScript determines how code is loaded and used in an application. Different module systems exist, including:
    - Commonjs: use (require)
    - ES Modules: use (import)
```
module.exports = {
  presets: ['@vue/cli-plugin-babel/preset']
};
```
module.exports = {} → This exports the configuration so Babel can use it.
presets: [...] → Defines presets (rules for transpiling code).
@vue/cli-plugin-babel/preset → A Vue CLI Babel preset that:
Supports modern JavaScript (ES6+).
Automatically handles Vue's Single File Components (.vue).
Ensures compatibility with older browsers.


`vue.config.js` -> Configures Vue CLI and Webpack settings.
`babel.config.js` -> configure babel

 `public` folder:
- favicon
- index.html (which has 'app'). It is where our application will be mounted. And built files inside this div will be auto injected.

`src` folder:
 - Entry point is 'main.js'. Here application is created and  mounted on '#app'


### Install external dependency: Bootstrap:
```
npm install bootstrap --save
```
Go to main.js:
```
import '../node_modules/bootstrap/dist/css/bootstrap.min.css'
```

### Async await:
Javascript was designed to run code line by line with each line waiting for previous line to complete.

But if few operations like fetching data, reading files, db operations, user interaction takes time
so main thread is blocked and app would freeze.

- Used callbacks: (Function passed as an argument to be used later) - Produced callback hell
- Promises -> Object representing eventual completion or failure of an async operation. But still can be complex
- Async/await - making async code look synchronous
  - async function always return a promise
  - await is used inside async functions
  - await pause execution until promise resolves.

Asyc await example:
```
function fetchData(){
    return new Promise((resolve)=>{
        setTimeout(() => resolve("Data loaded"), 2000);
    })
}

async function getData(){
    console.log("Start inside functions");
    const data = await fetchData(); // pause here until fetchdata resolves
    console.log(data);
    return data;
}
```

- When JS executes `await` it pauses execution of current function only. 
- It returns control to JS event loop.
- Rest of function becomes a continuation that runs later
- Other code can run in meantime
```
async function fetchUserData() {
  console.log("1. Starting to fetch user");
  const user = await fetch('/api/user');  // This pauses the function, not the main thread
  console.log("3. User data received");
  return user;
}

console.log("Before calling function");
fetchUserData(); // We don't await this, so execution continues immediately
console.log("2. After calling function");

// Output:
// Before calling function
// 1. Starting to fetch user
// 2. After calling function
// (later, when API responds) 3. User data received
```

### Lifecycle Hooks:

Server app: Responsible for processing data and identity stuff
Client app: Loaded in browser

How to load data? As soon as page loads the data is there on app.

`LifeCycle diagram`:


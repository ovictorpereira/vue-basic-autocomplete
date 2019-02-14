# vue-basic-autocomplete
A Vue.js autocomplete component. Compatible with Vue 2.x.

![Alt Text](https://media.giphy.com/media/cmzpTVS8rLWsxOX90l/giphy.gif)

## Installation
NPM
```bash
$ npm install vue-basic-autocomplete --save
``` 
Register the component
```js
import Vue from 'vue'
import VueBasicAutocomplete from 'vue-basic-autocomplete'

Vue.component('vue-basic-autocomplete', VueBasicAutocomplete)
``` 

## Usage
```html
<vue-basic-autocomplete v-model="selected" :options="myArray" trackby="name" classes="form-control />
```
```js
new Vue({
    data: {
        myArray: [
            {name: 'Lion', id: 1},
            {name: 'Lion Twon', id: 2}
        ],
         selected: ''
    }
})
```

## Available props

| Prop        | Type             | Default                | Description                                      |
|-------------|------------------|------------------------|--------------------------------------------------|
| options     | Array (required) |                        | Array of options to autocomplete                 |
| minlength   | Number           | 1                      | Min. length to start listing                     |
| noneFind    | String           | No matching results     | Default label when there are no matching results |
| trackby     | String           |                        | Required when you are using an array of objects    |
| placeholder | String           |                        | Placeholder                                          |
| classes     | String           |                        | Custom CSS class. Since I am using Bootstrap, I set it as 'form-control' |
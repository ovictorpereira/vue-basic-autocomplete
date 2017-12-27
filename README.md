# vue-basic-autocomplete
A Vue.js autocomplete component. Compatible with Vue 2.x.

![Alt Text](https://media.giphy.com/media/l0HU22ARPhxTXL4Zi/giphy.gif)

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
<vue-basic-autocomplete :data="myOptions" v-model="selected"></vue-basic-autocomplete>
```
```js
new Vue({
  data: {
   myOptions: ['Item One', 'Item Two'],
      selected: ''
  }
})
```

## Available props

| Prop        | Type             | Default                | Description                                      |
|-------------|------------------|------------------------|--------------------------------------------------|
| data        | Array (required) |                        | Array of ptions to autocomplete                  |
| minlength   | Number           | 3                      | Min. length to start listing                     |
| noresults   | String           | No matching result     | Default label when there are no matching results |
| placeholder | String           |                        | Placeholder                                      |

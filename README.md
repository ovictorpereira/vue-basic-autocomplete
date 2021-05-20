# vue-basic-autocomplete
A Vue.js autocomplete component. Compatible with Vue 2.x.

#### [Sandbox](https://jsfiddle.net/ovictorpereira/tk65ecL8/15/ "Sandbox")

## Installation
NPM
```bash
$ npm install vue-basic-autocomplete --save
``` 
Register the component
```js
import Vue from 'vue'
import VueBasicAutocomplete from 'vue-basic-autocomplete'

Vue.use(VueBasicAutocomplete)
``` 

## Usage
```html
<vue-basic-autocomplete v-model="result" :options="myArray" trackby="name" input-class="form-control" />
```
```js
new Vue({
    data: {
        myArray: [
            {name: 'Mariah', id: 1},
            {name: 'Josh Daves', id: 2},
            {name: 'John Sec', id: 3},
            {name: 'Robertson Daves', id: 4},
        ],
        result: ''
    }
})
```

## Available props

| Prop        | Type             | Default                | Description                                      |
|-------------|------------------|------------------------|--------------------------------------------------|
| options     | Array (required) |                        | Array of items to autocomplete                 |
| minlength   | Number           | 1                      | Min. length to start listing. If set to 0, all options will be listed on focus   |
| none-find    | String           | No matching results    | Default label when there are no matching results |
| trackby     | String           |                        | Required when you are using an array of objects  |
| placeholder | String           |                        | Placeholder                                      |
| disabled    | Boolean           |    false                    |                                       |
| list-max-height | String       |       300              | Max-heigth in px                                      |
| input-class     | String           |                  | Custom CSS class for the input. Since I am using Bootstrap, I set it as 'form-control' |
| clean-marker     | Boolean           |         false         | Shows a clean button appended to the input |


## Events
| Event    |  Description |
|----------|--------------|
| selected     |  Triggers when you select any item       |
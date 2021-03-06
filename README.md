v-autocomplete
==============

---

> Autocomplete component for Vue.js
>
> This component is css-free. The idea is to be used with any framework.

Installation
------------

### Using yarn

`yarn add v-autocomplete`

### Using npm

`npm i --save v-autocomplete`

Demo
----

[DEMO](http://paliari.github.io/v-autocomplete)

Usage
-----

### Bundler (Webpack, Rollup)

```js
import Vue from 'vue'

import Autocomplete from 'v-autocomplete'

// You need a specific loader for CSS files like https://github.com/webpack/css-loader
import 'v-autocomplete/dist/v-autocomplete.css'

Vue.use(Autocomplete)
```

### Browser

```html
<!-- Include after Vue -->
<link rel="stylesheet" href="v-autocomplete/dist/v-autocomplete.css"></link>
<script src="v-autocomplete/dist/v-autocomplete.js"></script>
<script>
  Vue.use(Autocomplete)
</script>
```

### Example

```html
<template>
  <v-autocomplete :items="items" v-model="item" :get-label="getLabel" :component-item='template' @update-items="updateItems">
  </v-autocomplete>
</template>

<script>
import ItemTemplate from './ItemTemplate.vue'
export default {
  data () {
    return {
      item: {id: 9, name: 'Lion', description: 'Lorem ipsum dolor sit amet, consectetur adipisicing elit.'},
      items: [],
      template: ItemTemplate
    }
  },
  methods: {
    getLabel (item) {
      return item.name
    },
    updateItems (text) {
      yourGetItemsMethod(text).then( (response) => {
        this.items = response
      })
    }
  }
}
</script>
```

**ItemTemplate example:**

```html
<template>
  <div>
    <b>#{{item.id}}</b>
    <span>{{ item.name }}</span>
    <abbr>{{item.description}}</abbr>
  </div>
</template>

<script>
export default {
  props: { item: { required: true } }
}
</script>
```

Properties
----------

| Name                     | Type                                | Required | Default value                  | Info                                                |
|--------------------------|-------------------------------------|----------|--------------------------------|-----------------------------------------------------|
| **items**                | Array                               | Yes      |                                | List items                                          |
| **component-item**       | Vue Component or Function or String | No       | Item                           | Item list template                                  |
| **placeholder**          | String                              | No       |                                |                                                     |
| **min-len**              | Number                              | No       | 3                              | Min length to trigger the *updateItems* event       |
| **wait**                 | String                              | No       | 500                            | Miliseconds dela to trigger the *updateItems* event |
| **get-label**            | Function                            | No       | function(item) { return item } | Anonymous function to extract label of the item     |
| **value**                | Mixed                               | No       |                                | Initial value (use v-model)                         |
| **auto-select-one-item** | Boolean                             | No       | true                           | Auto select item if result one item in items        |
| **input-class**          | String                              | No       |                                | Custom class of input search                        |

Events
------

| Name             | Params                       | Info                                                  |
|------------------|------------------------------|-------------------------------------------------------|
| **change**       | *text*: Text of search input | Triggered after every change in the search input      |
| **update-items** | *text*: Text of search input | Same as *change*, but respecting *min-len* and *wait* |
| **itemSelected** | *item*: Item selected | Triggered after a click on a suggestion |

What about appearence?
----------------------

Just overwrite their css classes. See the structure in *stylus* lang:

```stylus
.v-autocomplete
  .v-autocomplete-input-group
    .v-autocomplete-input
  .v-autocomplete-list
    .v-autocomplete-list-item
```

Follows the css used in the [DEMO](http://paliari.github.io/v-autocomplete):

```stylus
.v-autocomplete
  .v-autocomplete-input-group
    .v-autocomplete-input
      font-size 1.5em
      padding 10px 15px
      box-shadow none
      border 1px solid #157977
      width calc(100% - 32px)
      outline none
      background-color #eee
    &.v-autocomplete-selected
      .v-autocomplete-input
        color green
        background-color #f2fff2
  .v-autocomplete-list
    width 100%
    text-align left
    border none
    border-top none
    max-height 400px
    overflow-y auto
    border-bottom 1px solid #157977
    .v-autocomplete-list-item
      cursor pointer
      background-color #fff
      padding 10px
      border-bottom 1px solid #157977
      border-left 1px solid #157977
      border-right 1px solid #157977
      &:last-child
        border-bottom none
      &:hover
        background-color #eee
      abbr
        opacity 0.8
        font-size 0.8em
        display block
        font-family sans-serif
```

Authors
-------

-	[Marcos Paliari](http://paliari.com)
-	[Daniel Fernando Lourusso](http://dflourusso.com.br)

License
-------

This project is licensed under [MIT License](http://en.wikipedia.org/wiki/MIT_License)

# Pagination in Vue.js and bootstrap 4.0
A Vue.js(v2.x+) component to make pagination
![alt text](https://raw.githubusercontent.com/joserafalb/paginationVueComponent/master/gif.gif)

[Live demo](https://jsfiddle.net/joserafalb/py03hu9m/5/) on JSFiddle
# Usage
I use this on laravel but you should be good to use it anywhere. Take a look to the live demo if you are not using Laravel.
1. Add to **resources/js/app.js**
```
window.Vue = require('vue');
Vue.component('pagination', require('./components/PaginationComponent.vue'));
```
2. Run **npm run --dev**
3. Make sure you add the generated js file to your html file
4. Add component tag with properties
```
<pagination v-model="current_page"
              :button_group="4"
              :total_pages="30"
              :total_buttons="9">                
  </pagination>
```
5, Initialize Vue
```
var list_table = new Vue({
    el: '#app',
    data: {
        current_page: 1
    },
    watch: {
        current_page: function () {
            // Event to do when the page changes
        }
    }
});
```            
# Props
|Property name| Description|
|-|-|
|button_group | Number of buttons to group at the begining and the end of the nav bar |
|total_pages  | Total number of pages |
|total_buttons| Total number of buttons that you want in the bar|

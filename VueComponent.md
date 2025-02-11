# Vue Component

Simply example of **Non-Single File Components**

Include define components, data in component, rules of component-name, nesting of components, using of component

```html
<body>
    <div id="root">
        <name></name>
        <my-address/>
    </div>
    <script>
        const address = {
        template: `
                    <div>
                        <p>Address: {{address}}</p>
                        <input type="text" v-model="address">
                    </div>
                `,
        data() {
            return {
                address: 'China'
            };
        }
    }

        const name = {
                template: `
                    <div>
                      <h1>hello,{{name}}</h1>
                      <input type="text" v-model="name" autofocus>
                      <my-address/>
                    </div>
                `,
                data(){
                    return {
                        name: 'younni'
                    }
                },
                components: {
                    'my-address': address
                }
            };
            new Vue({
                el: '#root',
                components: {
                    name,

                }
            });
    </script>
</body>
```

About **nesting of components**, there is usually a set of norms

```
vm
|
app
|________________________
|           |           |
component   ...     component
```

```html
<body>
    <div id="root">
    </div>
    <script>
        const address = {
        template: `
                    <div>
                        <p>Address: {{address}}</p>
                        <input type="text" v-model="address">
                    </div>
                `,
        data() {
            return {
                address: 'China'
            };
        }
    }

        const name = {
                template: `
                    <div>
                      <h1>hello,{{name}}</h1>
                      <input type="text" v-model="name" autofocus>
                      <my-address/>
                    </div>
                `,
                data(){
                    return {
                        name: 'younni'
                    }
                },
                components: {
                    'my-address': address
                }
            };
        const welcome = Vue.extend({
            template: `<div><h1>Welcome</h1></div>`,
        });

        const app = Vue.extend({
                name: 'app',
                template: `
                  <div>
                    <welcome></welcome>
                    <name></name>
                  </div>
                `,
                components: {
                    name,
                    welcome
                }
            });
            new Vue({
                template:`<app/>`,
                el: '#root',
                components: {app}
            });
    </script>
</body>
```

In Vue DevTools

```html
v <Root>
  v <App>
      <Welcome>
    v <Name>
       <MyAddress>
```

 ###### Non-Single File Components

The style of Younnishing 

```html
v Application
   App.vue
   index.html
   main.js
  v Components
      Component1.vue
      Component2.vue
			...
```

In Vue CLI, there are 5 files you shouldn't rename.

public/

public/favicon.ico

public/index.html

src/

src/main.js

If you wanna rename them, you need to change Vue CLI config.

You need to new a file, name: `vue.config.js`

```javascript
module.exports = {
  pages: {
    index: {
      // entry for the page
      entry: 'src/index/main.js',
      // the source template
      template: 'public/index.html',
      // output as dist/index.html
      filename: 'index.html',
      // when using title option,
      // template title tag needs to be <title><%= htmlWebpackPlugin.options.title %></title>
      title: 'Index Page',
      // chunks to include on this page, by default includes
      // extracted common chunks and vendor chunks.
      chunks: ['chunk-vendors', 'chunk-common', 'index']
    },
    // when using the entry-only string format,
    // template is inferred to be `public/subpage.html`
    // and falls back to `public/index.html` if not found.
    // Output filename is inferred to be `subpage.html`.
    subpage: 'src/subpage/main.js'
  }
}
```

You can find detailed configuration in https://cli.vuejs.org/config/#vue-config-js

## $ref

You can use `ref` to get info of element or sub-component.(Used instead of  `id`)

If you use `document.getElementById` to select elements, you manipulated the `DOM`  directly.

So, Vue provides `$ref` to instead of it.

```html
...
<h1 ref='hello'>Hello</h1>
<MyComponent ref='mycomponent'/>
...
<script>
  ...
  console.log(this.$ref.hello);
	console.log(this.$ref.mycomponent)
</script>

```

> [!NOTE]
>
> If you use  `document.getElementById` to select Vue Components, it will return the DOM of it.

## 3 Methods to Recive Data

1.Simple declaration

```javascript
props: ['name', 'age', 'sex']
```

2.Declare type of data 

```javascript
props: {
	name: String,
	age: Number,
	sex: String
}
```

3.Declare all attribute of data

```javascript
props: {
  name: {
    type: String,
    required: true
  },
  age: {
    type: Number,
    default: 18
  }
  sex: {
    type: String,
    required: true
  }
}
```

## mixin

If you have some **same** code snippet, use mixin will make your code reduced code reuse.

First, create a file store your mixing code. You can name it whatever.

We named it `mixin.js`.

```javascript
export const mixin1 = {
  methods: {
    firstMethod(){
      ...
    }
  },
  mount(){
    ...
  }
};
export const mixin2 = {
    data(){
  		return {
  			x: 100,
  			y: 200
			}
		}
};
```

###### 1.Import in local

Import in your files you need.

```html
<script>
	import {mixin1, mixin2} from '../mixin.js';
  
  export default {
    name: 'YourComponent',
    data(){
      return {
        x: 0
      }
    },
    mixins: [mixin1, mixin2]
  }
</script>
```

If your components have a same content, then the mixin will not work if you are the main one.

> [!IMPORTANT]
>
> With a exception, the `Lifecycle Hooks` will be work whether you have the same content in your component or not. 
>
> If your components also have the `Lifecycle Hooks` , they will be **work together.**
>
> The `Lifecycle Hooks` of your components will be work last, the  `Lifecycle Hooks`  in `mixin` will be work first.

###### 2. Import in global

Import in your main.js, then all your components can use the contents in mixin.

```javascript
import {mixin1, mixin2} from './mixin.js';
Vue.mixin(mixin1);
Vue.mixin(mixin2);
```

> [!TIP]
>
> Because VueorHTML have a lot of Keywords, your components/methods/variable names should be written in large hump form.

## `$bus`

First, open Global Event Bus in `main.js`

```javascript
new Vue({
  render: h => h(App),
  beforeCreate() {
    Vue.prototype.$bus = this;
  }
}).$mount('#app')
```

Use `this.$bus.$emit()` to send data

```javascript
this.$bus.$emit(eventName, data);
```

Use `this.$bus.$on()` to receive data

```javascript
this.$bus.$on(eventName, () => {
  ...
});
```

## Router

router

  └──`index.js`

```javascript
export default new VueRouter({
    routes: [
        {
            path: '/',
            redirect: '/about'
        },
        {
            path: '/about',
            component: RouterAbout
        },
        {
            path: '/home',
            component: RouterHome
        },
        {
            path: '/nest',
            component: RouterNest,
            children: [
                {
                    path: '',
                    redirect: 'news'
                },
                {
                    path: 'message',
                    component: NestMessage,
                    children: [
                        {
                            name: 'detail',
                            path: 'detail',
                            component: MessageDetail
                        }
                    ]
                },
                {
                    path: 'news',
                    component: NestNews
                }
            ]
        }
    ]
});
```

`path`: The path of the component.

`name`: Name of this route.

`chileren`: All Child-Route of this route. [Array]

The path of Father-Route need a '/', its Child-Route don't add '/'.

Replace `<a></a>` with `<router-link></router-link>`, `href=""` with `to=""`.

Otherwise, `to=""` can use Object.

```javascript
:to="{
  name: 'detail',
  query: { id: m.id, title: m.title }
}">
```

This form is recommended when parameters need to be passed.

Use `<router-view></router-view>` to display component.

You can use `replace` to overwrite history.

When you switch components by router, previous component will be destroyed.

If you have a real DOM need reserve or not be destroyed, you can use `<keep-alive></keep-alive>`. And you can appoint the component needs reserve.

```html
<keep-alive include="ComponentName">
  <router-view></router-view>
</keep-alive>
```

> [!CAUTION]
>
> `include="ComponentName"` It uses the component name.

If you have more than one components need to reserve, you can use `Array` to define `include`.

```html
<keep-alive 
      :include="['Component1', 'Component2', ...]">
  <router-view></router-view>
</keep-alive>
```


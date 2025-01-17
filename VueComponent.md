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
> <Root>
  v <App>
      <Welcome>
    v <Name>
       <MyAddress>
```


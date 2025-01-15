# Vue 

## 1.Vue 实例

```javascript
new Vue({
    el: '#root',
    data: {
        name: 'younni',
        url: 'http://develop.younnishing.cn'
    },
  	methods: {
      	firstMethod() {...}
    }
});
//或者使用$mount的方法挂载
const vm = new Vue({
  data: {
        name: 'younni',
        url: 'http://develop.younnishing.cn'
    }
});
vm.$mount('#root');
//有此类需求可以使用
setTimeout(()=>{vm.$mount('#root')}, 1000);
```

#### 函数式data

> [!IMPORTANT]
>
> 使用组件时必须使用此方法

```javascript
data: function () {
            return{
                name: 'younni',
            }
        }
//简化为：data(){...}
```

> [!WARNING]
>
> ***<u>由Vue所管理的函数，不要使用箭头函数() => {}, this就不是Vue实例了</u>***

## 2.插值&指令语法

```javascript
 <h1>Hello, {{name}}</h1>
 <a :href="url">click</a>
```

> [!IMPORTANT]
>
> 指令
> ```javascript
> v-bind:  //单向数据绑定,数据仅从data流向页面,v-bind:value=""简化为:value=""
> v-model: //双向数据绑定,只能应用在表单元素value值中,简化为v-model=""
> v-on:    //事件绑定，v-on:click=""简化为@click=""
> ```

## 3.MVVM模型:前端主流框架模型

M：Model ,data 中的数据

V： View ,模板

VM：ViewModel ,Vue实例

![image-20250113上午100152875](/Users/younnishing/Library/Application Support/typora-user-images/image-20250113上午100152875.png)

## 4.数据代理

```javascript
Object.defineProperty(obj, prop, descriptor)
```

descriptor:

```javascript
{
	value: "",
	enumerable: true&false, //Default false，是否可以被枚举（遍历）
	writable: true&false, //Default false，是否可以被修改
	configurable: true&false, //Default false，是否可以被删除
}
```

> [!NOTE]
>
> 数据代理：通过一个对象代理对另一个对象属性的操作

#### 在Vue中的数据代理

通过vm对象代理data中属性（getter/setter）

开发者直接操作vm，vm自动操作data中的属性

通过Object.defineProperty()来吧data的内容添加到vm上

能够更加方便的操作data的数据，如果没有数据代理，

```javascript
{{_data.name}}
{{_data.url}}
```

所有的值都改加上`_data`才能操作

## 5.事件处理

```html
<button @click="Event1">Click1</button>    //不传参
<button @click="Event2(2)">Click2</button> //传参

  ...
        methods:{
            Event1(){
                alert('ClickEvent1');
            },
            Event2(number){
                alert('ClickEvent' + number);
            }
        }
```

#### 事件修饰符

```javascript
@click.prevent="" //阻止默认事件
@click.stop="" //阻止事件冒泡
@click.once="" //事件只触发一次
```

## 6.键盘事件

以keyup事件为例,实现通过键盘控制div移动

```javascript
<div id="item">
      <input  @keyup="move">
      1
</div>
...
methods{
		 move(e){
                const item = document.getElementById("item");
                const currentRight = parseInt(item.style.marginLeft) || 0;
                const currentTop = parseInt(item.style.marginTop) || 0;
                switch (e.keyCode){
                    case 39:item.style.marginLeft = `${currentRight + 50}px`;break;
                    case 37:item.style.marginLeft = `${currentRight - 50}px`;break;
                    case 38:item.style.marginTop = `${currentTop - 50}px`;break;
                    case 40:item.style.marginTop = `${currentTop + 50}px`;break;
                }

                console.log(e.keyCode,e.key);
            },
}
```

同时，Vue提供了9个常用的按键别名

分别为`enter` `delete` `esc` `space` `tab` `up` `down` `left` `right` 

> [!TIP]
>
> 1. `delete` 同时适用于backspace与delete
> 2. 由于Tab键的特殊性，建议与keydown事件配合使用
系统修饰键 `ctrl` `alt` `shift` `meta` 

> [!TIP]
>
> 可以搭配其他按键使用 `@keyup.ctrl.up="up"` 
>
> 搭配keyup事件使用时必须搭配其他按键，当其他按键抬起时，才能触发事件

## 7.计算属性

> [!TIP]
>
> Vue建议不要使用过于复杂的插值语法，比如
>
> ```javascript
> {{
>   fullName.split(' ').map(function (word) {
>     return word[0].toUpperCase() + word.slice(1)
>   }).join(' ')
> }}
> ```
> 而是使用计算属性或者方法

为方便使用，计算属性拥有缓存，其get()方法只会被请求一次

当所依赖的数据发生变化时会重新调用get()


同时，计算属性也有set()方法，由于计算属性的性质，此方法并不常用

那么推荐简写形式：

```javascript
data: {
  firstName: "Younni",
  lastName: "Baak"
},
computed:{
  fullName(){
    return this.firstName + '-' + this.lastName;
  }
}
```



## 8.监视属性(侦听属性)

在 Vue 中，watch 是一个用于监听和响应数据变化的选项。它允许你对数据的变化进行处理。

```javascript
watch: {
  propertyName: {
    handler(newValue, oldValue) {
      // 数据变化时的回调
    },
    immediate: true, // 是否在初始加载时立即执行
    deep: true       // 是否深度监听对象内部值的变化
  }
}
```

如果监听中不需要配置项 `immediate` `deep` 那么可以简写为：

```javascript
watch:{
	propertyName(newValue, oldValue){
		// 数据变化时的回调
	}
}
```

也可以调用`vm.$watch()` 来实现监听属性

```javascript
vm.$watch('propertyName', {
  handler(newValue, oldValue) {
      // 数据变化时的回调
    },
    immediate: true, // 是否在初始加载时立即执行
    deep: true       // 是否深度监听对象内部值的变化
});
//同样，在不需要配置项的时候可以简写为：
vm.$watch('property', function(newValue, oldValue) {
      // 数据变化时的回调
    });
```

> [!WARNING]
>
> 再次强调，由Vue管理的函数不要写成箭头函数！`this` 会指向window而不是Vue
>
> 同时，不被Vue所管理的对象最好写成箭头函数，这样`this` 才能指向Vue，
>
> 比如setTimeout()、ajax的回调函数



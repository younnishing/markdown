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

###### 常见指令
 ```html
 v-bind:  <!-- 单向数据绑定,数据仅从data流向页面,v-bind:value=""简化为:value="" -->
 ```
```html
v-model: <!-- 双向数据绑定,只能应用在表单元素value值中,简化为v-model="" -->
```
```html
v-on:    <!-- 事件绑定，v-on:click=""简化为@click="" -->
```

`v-model:`在表单提交中的小技巧

1.在绑定`radio` `checkbox`等无法输入的input时，注意要给定对应value值

2.`checkbox`默认返回boolen值，注意其`v-model='property'`中property应为一个**数组**

3.需要收集的数据为`number`时可以使用`v-model.number`修饰符

4.`.lazy`修饰符可以在**失去焦点**时再提交

5.`.trim`可以忽略字符串**前后**的空格

###### 其他内置指令

```html
v-text:/v-html: <!-- 相当于innerText/innerHTML -->
```
```html
v-cloak   <!-- 此指令没有值，该指令会在Vue接管容器时立刻被移除,搭配css使用，可以防止在Vue未接管容器时，Vue模板内容显示在页面上 -->
style{
	[v-cloak]{
		display: none;
	}
}
```

```html
v-once   <!-- 此指令没有值,仅在页面初次动态渲染时加载一次，后被视为静态内容 -->
```
```html
v-pre    <!-- 此指令没有值,Vue会跳过有该指令的节点不去编译，用于提升效率 -->
```

###### 自定义指令

Vue也允许自定义指令，并且有两种方式

1. 以函数式定义

```html
<span v-directiveName='value'></span>
<script>
  const vm = new Vue({
    data: {
      value: ''
    },
    directives{
    	directiveName(element, binding){
    		element.innerText = binding.value;
    		//自定义操作
  		}
    }
  });
</script>
```

2.以对象式来定义

```html
<span v-directiveName='value'></span>
<script>
  const vm = new Vue({
    data: {
      value: ''
    },
    directives{
    	directiveName:{
    		bind(element, binding){
    			element.innerText = binding.value;
  			},//当指令与元素绑定时调用
    		inserted(element, binding){
          //如果有需求，比如
          element.focus();
          element.parentElement;
        },//当元素被插入到页面时调用
        update(element, binding){
          element.innerText = binding.value;
        }//当所在模版被重新解析时调用
  		}
    }
  });
</script>
```

如果在对象式写法中，没有对应的`inserted()`需求，那么建议写成函数式

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

## 9.条件渲染

```html
<h1 v-show='false'>Hello</h1>
<h1 v-if='false'>Hello</h1>
```

两种控制显示隐藏的区别在于`v-show` 是通过控制元素的`style.display` 来实现的；

而`v-if` 是通过操作元素的DOM，将元元素直接删除

如果变化的频率很高建议使用`v-show` 

同理，为了提高效率，在使用`v-if` 时建议搭配`v-else-if`、`v-else`使用

> [!WARNING]
>
> `v-if` 搭配`v-else-if`、`v-else`使用时，请勿打断！

## 10.列表渲染

###### 数组遍历

```html
<ul>
    <li v-for="p in persons" :key="p.id">
        {{p.id}} - {{p.name}} - {{p.age}}
    </li>
</ul>
...
persons: [
	{id: '001', name: 'Jack', age: 18},
	{id: '002', name: 'Tom', age: 16},
	{id: '003', name: 'Younni', age: 20}
]
```

`v-for`还支持第二个参数

```html
<li v-for="(p,index) in persons" :key="p.id">
    {{index}} - {{p.name}} - {{p.age}}
</li>
```

同样地，你也可以使用`index`作为`key`值，但不建议这样做，`p.id`对于每一个p是其**唯一标识**

> [!TIP]
>
> 在虚拟DOM的**diff算法**中，虚拟DOM一致，真实DOM复用，以`p.id`为`key`值无论什么时候都可以保证其虚拟DOM一致，**保证效率**；以`index`作为`key`值，在某些特殊情况下(如逆序添加等破坏顺序的操作)，会造成没有必要的真实DOM更新
>
> 在不指定`key`的情况下，Vue会添加一个默认的 `:key = index`

###### 对象遍历

```html
<ul>
    <li v-for="(value, key) in personObj" :key="key">
        {{key}} - {{value}}
    </li>
</ul>
...
 personObj: {
	name: 'younni',
	age: 20,
}
```

###### 字符串遍历

```html
<ul>
    <li v-for="(char, index) in str" :key="index">
        {{index}} - {{char}}
    </li>
</ul>

str: 'younnishing'
```

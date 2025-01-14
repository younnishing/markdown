# Vue 笔记

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

```javascript
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


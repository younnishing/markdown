# Vue 笔记

## 1.Vue 模板

```javascript
new Vue({
    el: '#root',
    data: {
        name: 'younni',
        url: 'http://www.younnishing.cn'
    }
});
//或者使用$mount的方法挂载
const vm = new Vue({
  data: {
        name: 'younni',
        url: 'http://www.younnishing.cn'
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
> v-bind:  //单向数据绑定,数据仅从data流向页面,简化为:value=""
> v-model: //双向数据绑定,只能应用在表单元素value值中,简化为v-model=""
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

```
{
	value: "",
	enumerable: true&false, //Default false，是否可以被枚举（遍历）
	writable: true&false, //Default false，是否可以被修改
	configurable: true&false, //Default false，是否可以被删除
}
```
test 10.46


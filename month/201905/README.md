<!--
 * @Desc: 
 * @FilePath: /firewood/month/201905/README.md
 * @Author: liujianwei1
 * @Date: 2021-03-16 17:07:37
 * @LastEditors: liujianwei1
 * @Reference Desc: 
-->

### 2019年5月30日 14:44:09
[指令](./docs/directive.md)

### 2019年5月23日 17:24:58

[js装饰器模式](http://www.cnblogs.com/coolslider/p/8459729.html)

### 2019年5月22日 15:02:50

[7个有用的Vue开发技巧](https://juejin.im/post/5ce3b519f265da1bb31c0d5f?utm_source=gold_browser_extension#heading-6)

####  Get 的内容

- 状态共享  利用Object.observable实现状态共享。 Element-ui 里面table-store.js可以借鉴一下

>  

- 长列表性能优化=>

> Vue通过Object.defineProperty对数据进行劫持， 来实现视图相应数据的变化. 可以通过Object.freeze(users)数据冻结。 这样改变user里面的值， 不会响应视图更新， 如果想解冻。 可以通过给this.data.user重新赋值的方式

```javascript
export default {
    data: () => ({
        users: {}
    }),
    async created() {
        const users = await axios.get("/api/users");
        this.users = Object.freeze(users);
    },
    methods: {
        // 改变值不会触发视图响应
        this.data.users[0] = newValue
        // 改变引用依然会触发视图响应
        this.data.users = newArray
    }
};
```

- 具名插槽和作用插槽的区别
- 属性事件传递的方式
- 函数式编程的应用场景

```html
<template functional>
  <div>
    <p v-for="item in props.items" @click="props.itemClick(item);">
      {{ item }}
    </p>
  </div>
</template>
```

- 父组件监听子组件的生命周期

```html
< Child @hook: mounted = "doSomething" / >
```

### 2019年5月17日 11:01:49

[vscode插件](https://zhuanlan.zhihu.com/p/65880876?utm_source=qq&utm_medium=social&utm_oi=706045932076040192)
[VSCode插件开发全攻略（一）概览](https://www.cnblogs.com/liuxianan/p/vscode-plugin-overview.html)
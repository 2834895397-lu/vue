# 实例函数

1. $el: 获取vm管理的dom
2. $watch(): 监听想用是数据
3. $data: 获取data
4. $set(): 设置data
5. $nextTick(fn):  及时获取更新的数据
6. $options: 获取vm中的所有信息, Vue构造函数中的{}就是options
7. $mount(el): 使vm挂载



# npm的几种安装方式的区别

**npm install X:**

- 会把X包安装到node_modules目录中
- 不会修改package.json
- 之后运行npm install命令时，不会自动安装X

==**m install X –save:**==

- 会把X包安装到node_modules目录中
- 会在package.json的dependencies属性下添加X
- 之后运行npm install命令时，会自动安装X到node_modules目录中
- 之后运行npm install
  –production或者注明NODE_ENV变量值为production时，会自动安装msbuild到node_modules目录中

**npm install X –save-dev:**

- 会把X包安装到node_modules目录中
- 会在package.json的devDependencies属性下添加X
- 之后运行npm install命令时，会自动安装X到node_modules目录中
- 之后运行npm install
  –production或者注明NODE_ENV变量值为production时，不会自动安装X到node_modules目录中

**使用原则:**

运行时需要用到的包使用–save，否则使用–save-dev。





# 事件的触发

## 1. change事件

![image-20201022092043794](img/image-20201022092043794.png)

change事件会根据Input输入框的变化实时性来触发改事件



# 插槽

### slot的新语法和旧语法:

![image-20201022092427520](img/image-20201022092427520.png)





---

==v-slot:名字               		v-slot:名字='接收属性' 			slot-scope='接收属性'   	接收属性可以接收使用组件的时候传递过来的值==

![image-20201022093228993](img/image-20201022093228993.png)



# 双向绑定

vue是单向数据流, 不是双向绑定, vue的双向绑定只不过是语法糖而已, v-model实际上是v-bind和@input的简写形式:

下面的组件都实现了双向数据绑定, 但是底层更趋向于第二种, 即==属性传递和事件监听的组合方式==:

![image-20201022100424564](img/image-20201022100424564.png)



##### 例子:

==1. input框中的vue通过拿vue实例中的value属性的值得到==

==2. 改变vue实例中的值: 当input框发生改变的时候, 拿到input框中的值, 然后赋值给vue中的value变量==

```javascript
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>test</title>
    <script src="../js/vue.js"></script>
</head>
<body>
<div id="app">
    <input v-model="value">
        //1. input框中的vue通过拿vue实例中的value属性的值得到
        //2. 改变vue实例中的值: 当input框发生改变的时候, 拿到input框中的值, 然后赋值给vue中的value变量
    <input type="text" :value="value" @input="value=$event.target.value">
    {{value}}
</div>
<script>
    new Vue({
        el: '#app',
        data: {
            value: ''
        }
    })
</script>
</body>
</html>

```

##### model属性实现自定义组件的双向数据绑定

```javascript
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>test</title>
    <script src="../js/vue.js"></script>
</head>
<body>

<div id="input-test-demo">
    <span style="color: red">{{value}}</span>
    <input-test v-model="value"></input-test>
</div>

<script>
    Vue.component('input-test',{
        model:{
            prop:'value',
            event: 'input-event'
        },
        template:`<input type="text" v-bind:value="value" v-on:input="$emit('input-event', $event.target.value+'<<<====')"/>`
    })

    new Vue({
        el:'#input-test-demo',
        data:{
            value: '请输入'
        }
    })


</script>
</body>
</html>

```



==**v-model中默认的绑定的属性和事件:**==   **例如: 在text文本框中, v-model='xxx'   这就相当于value='xxx'    可以利用model属性来修改绑定的默认属性和事件**

![image-20201022155824108](img/image-20201022155824108.png)

###### 自定义一个组件, 并且用model指明绑定的默认属性和事件:













# data属性

==因为组件是复用的, 所以还没有实例化的组件必须使用函数的形式来返回组件中的数据, 以确保数据的独立性; 已经实例化的组件则使用属性的形式来声明data==

## 如何自定义一个组件?

使用vue指令绑定的值必须是接收属性, 也就是使用的时候接收过来的

![image-20201022114743586](img/image-20201022114743586.png)





​					==使用:==

![image-20201022115031712](img/image-20201022115031712.png)



## 引入组件使用异步加载的方式:

```javascript
component: () => import('xxxx')
```



---

###### 使用组件时传递了一个没有声明的属性:

**假如我们传递了一个我们没有声明的属性, 则默认挂载到组件的根据点:**

![image-20201022135553526](img/image-20201022135553526.png)

---

# 插槽

**插槽可以传递一个模板, 这一点是传递属性所做不到的**

2.5语法:

![image-20201022152918665](img/image-20201022152918665.png)

**2.6新语法: 需要一个template标签**

![image-20201022153158184](img/image-20201022153158184.png)

## **作用域插槽:**

定义插槽的时候可能会传递一些值, 在我们使用的使用就可以通过使用==**v-slot:slotName='{传递过来的属性}'**==获取传递过来的值, 然后就可以使用了:

![image-20201022154230414](img/image-20201022154230414.png)



==**假如定义的插槽没有被插入, 则默认里面的子组件会生效, 否则插槽里面的子组件会被覆盖掉**==

# ![image-20201022154621670](img/image-20201022154621670.png)



## 关于插槽的几点事件:

在定义插槽的时候可以使用slot或者template, 在定义的时候可以指定一个接收属性,  在我们使用的时候就可以使用slot-scop来进行传值:

![image-20201029214534580](img/image-20201029214534580.png)

执行结果:

![image-20201022215950561](img/image-20201022215950561.png)

---



## 相同的插槽是合并还是替换?

![image-20201022215451074](img/image-20201022215451074.png)





# 响应式更新

> **vue做响应式更新dom元素的条件(必须是被vue监视管理的属性)**

1. ==模板必须是要使用到这个属性或者对象==

2. ==属性必须是放在data函数中作为return 返回==

   

   ![image-20201022173108696](img/image-20201022173108696.png)

   

   ---

   # 计算属性

   #### ==**计算属性里面用到的属性必须是响应式的数据类型**==,不然依赖数据变化时, 不会重新计算该属性, 因为该数据没有被监听





# 监听器: watch

这里我们对e进行了深度监听, 所以当e或e的子元素发生改变时也能触发该函数的执行:

![image-20201022174547155](img/image-20201022174547155.png)

---





# 组件的生命周期

创建和销毁阶段只会执行一次, ==更新阶段会执行多次==

![image-20201022174858872](img/image-20201022174858872.png)

 

---



# vue的内置指令

**v-cloak在html中用到, 在.vue中很少用到, 作用就是防止元素还没挂在渲染在dom节点时**

![image-20201022194734092](img/image-20201022194734092.png)

## 自定义指令的生命周期

![image-20201022195322003](img/image-20201022195322003.png)

## 自定义指令

vue使用directive来自定义指令:  

1. 简单的定义指令:

   ![image-20201101152035450](img/image-20201101152035450.png)

   

   2. 完整的定义各个阶段:

   ==生命周期的回调函数会传入两个值, 一个是el, 表示使用这个指令的标签元素, 另一个是biding绑定规则, 是一个对象, 可以在这个对象中获取到我们所需要用到的值==

通过销毁按钮来销毁vue指令:(**当指令所在的标签被干掉之后指令自然被销毁**)

![image-20201022200116676](img/image-20201022200116676.png)



自定义指令修饰符:

![image-20201101154046654](img/image-20201101154046654.png)

 

# 组件的通信

## provide和inject

使用场景: ==**组件之间必须有层级关系**==(当这个组件引入并使用了其他组件, 这两个组件自然就有层级关系了)

![image-20201022201453287](img/image-20201022201453287.png)



一下结构跟上面的层级关系是一致的:

==A组件==: A组件的下一层级时B,C,D组件, 并且A组件提供了theme属性(为了保证数据的独立性, ==**provide使用函数的形式进行返回**==)

![image-20201022201747411](img/image-20201022201747411.png)



==E组件==: 通过inject来注入(向上寻找)属性 , 在h3标签中就可以使用这个属性了

![image-20201022202032916](img/image-20201022202032916.png)



==F组件==: 如果要接收的属性和本组件中的名字冲突的时候, 还可以使用别名的方式来进行替代, 用from指定要接收的属性

![image-20201022202301471](img/image-20201022202301471.png)



==C组件==: 加入我们在C组件同样提供了一样的属性, 则下层组件就不会找到A组件去拿到对应的属性, 而是在C组件中拿到对应的属性, 这点有点像**冒泡机制**, inject注入属性的时候从下网上找, 直到找到为止

![image-20201022203657459](img/image-20201022203657459.png)

==**注意点:**==我们要使父组件的对应属性的更新能重新传递给子组件的话, 必须提供响应式的数据, 而不能时字符串常量, 可以直接传递this过去, 不过这样做会传递了冗余的属性, 在a组件中可以这样子传递以达到父子联动的效果

![image-20201022204052765](img/image-20201022204052765.png)

**可以通过vue的api Vue.observable来优化响应式provide:**

![image-20201022232013315](img/image-20201022232013315.png)



## props接收属性时进行校验

![image-20201022225958057](img/image-20201022225958057.png)



# ref引用信息

**==如果是普通节点, 获取到的是dom元素, 如果是自定义组件, 获取到的是组件的实例==**

![image-20201022205250736](img/image-20201022205250736.png)



# template和jsx

这两个只是一个语法糖而已, 最终都会被编译成createElement('标签', '标签内的文本')

![image-20201022211853394](img/image-20201022211853394.png)





# 支持响应式更新的方法

![image-20201022230958172](img/image-20201022230958172.png)



# 获取dom上挂载之后的数据:

==**vm.$nextTick(function(){**==

......

==**})**==

#  vuex状态管理

1. 安装: cnpm install vuex --save

2. 引入和全局使用: 

   ```javascript
   import Vuex from 'vuex'
   //为vue全局注入了$store属性, 后面就可以通过this.$store来获取这个Store对象
   Vue.use(Vuex)
   
   const store = new Vuex.Store({....})
   //在main.js中注册store就可以全局使用了, vue实例就可以通过this.$store来获取store, 组件可以直接通过$store来获取store实例
   new Vue({
     store,
     el: '#app',
     components: {App},
     template: '<App/>'
   })
   
   ```

3. 具体配置:

   ```javascript
   const store = new Vuex.Store({
     state: {
       count: 0
     },
     mutations: {
       //第一个参数a为回调参数, 是vuex的状态state, 第二个参数可以是组件传递过来的参数
       increment(a) {
         a.count++
       }
     },
     //因为vuex都是响应式的数据, 所以也有getters属性, 它的回调参数是一个state对象, 旨在任何一个数据变化是, 都能在getter获取到对象的状态
     getters: {
       doubleCount(sate) {
         return sate.count * 2
       }
     },
   
   
     actions: {
       /**
        * @param object {
        commit: ƒ boundCommit(type, payload, options)
        dispatch: ƒ boundDispatch(type, payload)
        getters: {}
        rootGetters: {}
        rootState: {__ob__: Observer}
        state: {__ob__: Observer}
        __proto__: Object}
        由此可见, 回调参数为一个object对象, 所以我们只需要用解构的方式来获取我们所需要的数据而不用全部获取
        */
       increment({state}) {
         setTimeout(() => {
           state.count++
         }, 3000)
   
       }
     }
   })
   ```

4. 使用: ==**所需要的响应式数据只需要放在计算属性中返回即可**==

   ```javascript
   //所需要的响应式数据只需要放在计算属性中返回即可
   export default {
       name: 'App',
       computed:{
         count(){
           return this.$store.state.count
         }
       }
     }
   ```

5. 具体调用和更改响应式数据:

   ```javascript
   <template>
     <div id="app">
       {{count}}
       <br>
       {{$store.getters.doubleCount}}
       //我们commit到mutation时还可以传递自己的参数给mutation处理, mutation函数用第二个参数接收, 第一个参数固定为state对象回传, 本例不再演示
       <button @click="$store.commit('increment')">count++</button>
       <button @click="$store.dispatch('increment')">count++</button>
     </div>
   </template>
   ```

   

![image-20201022232600458](img/image-20201022232600458.png)

**vuex的运行机制:** action一般是用与做异步  的, 例如发ajax请求等等

![image-20201022232928622](img/image-20201022232928622.png)

## vuex的核心概念

state提供响应式数据,		getter提供获取响应式的值,		mutation触发state的改变,		action通过驱动mutation来改变state的状态:

![image-20201025121330490](img/image-20201025121330490.png)

底层原理:

![image-20201025121450273](img/image-20201025121450273.png)

# vuex的扩展





# vueRouter

**使用方式:**

![image-20201025142806876](img/image-20201025142806876.png)

###  路由的配置:

```javascript
import Router from 'vue-router'
//为vm对象注入全局的$router属性
Vue.use(Router);
var router = new Router({
  //n个路由
  routes: [
    {
      path: '/home',
      component: Home,
      children: [
        {
          path: '/home/news',//path最左边的斜杠永远代表根路径, 所以子路由建议不写斜杠了, 或者写了斜杠就写全称路径
          component: News
        },
        {
          path: 'message',//简化写法
          component: Message,
          children:[
            {
              path: 'detail/:id',
              component: MessageDetail
            }
          ]
        },
        {
          //子路由默认显示哪个组件
          path: '/',
          redirect: '/home/news'

        }
      ]
    },
    {
      path: '/about',
      component: About
    },
    {
      path: '/',
      redirect: '/about'
    }
  ]
})

//在vue中使用:
new Vue({
  el: '#app',
  //使用路由
  router,
  components: { App },
  template: '<App/>'
})

```

### 使用路由:

```javascript
     <router-link to="/about">About</router-link>
 	 <router-view></router-view>
```



### 配置路由404页面

在路由配置的最后面的path使用*通配符来配置, 当前面的路由都没有匹配上的时候就会走该页面:

**{**

**path: '*'**

**name: '404'**

**component: Not Found**

**}**

---

## 路由的动画

路由动画的效果: 当我们点击跳转路由时, 顶部导航栏会出现进度条

如何使用配置?

1. 安装nprogress插件:

   `cnpm install nprogress --save`

2. 在router中引入该插件和样式:

   ```javascript
   import NProgress from 'nprogress'
   import 'nprogress/nprogress.css'
   ```

3. **使用: 在router开始遍历(寻找目标路由组件)和结束遍历的时候使用进度条**

   ```javascript
   const router = new Router({...})
   /**
    * to 将要去的路由
    * from: 当前路由
    * next: 调用next之后才会继续往下走, 在next之前可以做自己的逻辑判断
    */
   router.beforeEach((to, from, next) => {
     //启动进度条
     NProgress.start();
     next();
   });
   router.afterEach(() => {
     //进度条结束
     NProgress.done();
   })
   ```

4. 最后把router实例暴露出去:

   `export default router;`







## 路由的传参:

### 方式一:

1. 定义路由时使用**:占位符**:  

   ```javascript
    path: 'message',//简化写法
             component: Message,
             children:[
               {
                 path: 'detail/:id',	//params.id获取值
                 component: MessageDetail
               }
             ]
   ```

2. ```javascript
    <router-link :to="'/home/message/detail/'+ message.id">{{message.title}}</router-link>
   ```

3. 路由的目标组件使用params来接收:

   ```javascript
    const id = this.$route.params.id
   ```



---



### 方式二:

1. 使用标签传值

```javascript
  <router-view msg="abc"></router-view>
```

2. 路由的目标组件接收:

   ```javascript
    export default {
       props:{
         msg: String
       },
     }
   ```

   ### 方式三
   
   **注意⚠️：params传参 ，路径不能使用path 只能使用name,不然获取不到传的数据**
   
   **1 params传参**
   
   `this.$router.push({name: 'dispatch', params: {paicheNo: obj.paicheNo}})`
   
   **取数据：this.$route.params.paicheNo**
   
   `this.$route.params.paicheNo`
   
   
   
   **2 query传参**
   
   `this.$router.push({path: '/transport/dispatch', query: {paicheNo: obj.paicheNo}})`
   
   **取数据：this.$route.query.paicheNo**
   
   **this.$route.query.paicheNo**
   
   

#### 自定义激活的路由的class属性

![image-20201025153341244](img/image-20201025153341244.png)

激活的路由会自动添加一个class属性: ==**class='router-link-active'**==, 所以我们可以根据这个class自定义激活路由的样式, 甚至可以在index.html中定义路由的全局样式

#### 路由组件的渲染(挂载):

1. 用户点击router-view的情况: 会在当前点击页的router-view标签进行挂在
2. 用户通过导航栏直接访问: 会挂在到访问的路由的组件的父路由的组件的router-view标签中
3. 这两种方式的效果都是一致的



#### 路由的缓存

**当切换到其他路由时, 默认是不会保存原来的路由状态, 可以使用<keep-alive>来包裹<router-view>以达到不销毁路由对象的效果:**

### 一 ，缓存全部路由

```javascript
在router-view外包裹keep-alive
例： 
	<keep-alive>
      <router-view></router-view>
    </keep-alive>
```

### 二 ，指定路由缓存

```javascript
使用  include
<keep-alive include="该路由的name名称">
  <router-view></router-view>
</keep-alive>
```

### 三，存在多个路由时，想缓存部分路由

```javascript
使用 meta
在路由中添加下面属性  
    meta: {keepAlive: true // 缓存}
    meta: {keepAlive:false // 不缓存 }
    例：
    	 {
	          path:'/Distribution',
	          name:'Distribution',
	          component: Distribution,
	          meta: {keepAlive: true // 缓存}
		 }
然后在页面  
	<keep-alive >
		//当前进入的路由 meta里面 keepAlive为true时走这里
      <router-view v-if="$route.meta.keepAlive"></router-view>
    </keep-alive>
    
    //当前进入的路由 meta里面 keepAlive为false时走这里 下面 if 判断进行了取反处理
    <router-view v-if="!$route.meta.keepAlive"></router-view>
```

#### 路由的常用api

![image-20201025153925467](img/image-20201025153925467.png)

5. **js方式来跳转路由: window.location = url**



#### 路由的类型

**hash模式:  超链接中带#号           history模式超链接中不到#号**              

![image-20201026085023864](img/image-20201026085023864.png)

​							==**更改路由类型: 在new路由的时候可以指定路由的模式mode:**==

![image-20201026085246659](img/image-20201026085246659.png)







# mixins混入

我们先来看看vue官方是怎么介绍的

混入 (mixin) 提供了一种非常灵活的方式，来分发 Vue 组件中的可复用功能。一个混入对象可以包含任意组件选项。当组件使用混入对象时，所有混入对象的选项将被“混合”进入该组件本身的选项。

官方文档说的很详细，通俗易懂的话来说一个.vue文件由template，script，style组成，混入的方法可以把mixin这个对象和.vue文件的script里面的内容“混入”（mixin对象的结构和.vue的script里面的结构一样），既此组件既可以调用组件内部的script，也可以调用混入对象。

## 场景运用：

有两个非常相似的组件，他们的基本功能是一样的，但他们之间又存在着足够的差异性。他们可能会公用一部分业务逻辑，但是他们的页面结构又不相同。这个时候就可以使用mixin来让代码复用。（类似于JS库，暴露出来的方法达到函数复用的效果。又区别于JS库，它继承了vue中script所有对象，包括生命周期，data，methods）

## 话不多说请看基础实例：

![img](https:////upload-images.jianshu.io/upload_images/17849217-3cd4a6a7145bcf38.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/364/format/webp)

这是demo的文件结构

**写在mixin.js**

```
const mixin= {
    data() {
        return {
            name: '初始名字：张三',
            mixinMsg: 'mixinMsg'
        };
    },
    methods: {
        // 获取mixin中的msg
        getMixinMsg() {
            alert(
                '我是mixin.js中的getmsg方法，mixinmsg的数据是' + this.mixinMsg
            );
        },
        // 获取home中的homeMsg
        getHomeMsg() {
            alert(
                '我是mixin.js中的getHomeMsg方法，HomeMsg的数据是' + this.homeMsg
            );
        }
    },
    created() {
        alert('在mixin中vue的data、生命周期、方法等都可以使用');
    }
};

export default mixin;
```

mixin中，暴露一个常数Vrbtmixin ，Vrbtmixin 是一个对象，里面的结构和.vue文件的script相同

**写在home.vue中**

```
<template>
  <transition name="fade">
    <div class="wrap">
      <h1>Home页面</h1>
      <h3 @click="goRule">跳转路由</h3>
      <!--主要内容-->
      <div class="content">
        <div @click="getMixinData">1.获取mixin中的name</div>
        <div @click="test">2.调用mixin.js中的getMixinMsg方法</div>
        <div @click="getHomeMsg">3.获取home.vue中的homeMsg</div>
        <div @click="changeMixinMsg">4.改变mixin中的name</div>
      </div>
    </div>
  </transition>
</template>
<script>
import mixin from '../js/mixin';
export default {
    mixins: [mixin],
    data() {
        return {
            homeMsg: 'homeMsg'
        };
    },
    methods: {
        getMixinData() {
            alert('mixin中的name为：' + this.name);
        },
        test() {
            this.getMixinMsg();
        },
        changeMixinMsg() {
            this.name = '李老二';
            alert('mixin中的name改变为：' + this.name);
        },
        goRule() {
            this.$router.push('/rule');
        }
    },
    created() {}
};
</script>
<style lang="less" scoped>
img {
    opacity: 0;
}
.wrap {
    // background-color: white;
    .content {
        div {
            height: 1rem;
            // width: 1rem;
            background-color: aqua;
            margin-top: 0.4rem;
            text-align: center;
            line-height: 1rem;
        }
    }
}
</style>
```

引入mixin.js，然后注册 mixins: [mixin],

**写在rule.vue中**

```
<template>
  <transition name="fade">
    <div class="wrap">
      <!--主要内容-->
      <div class="content">
        <div @click="getMixinData">获取mixin.js中的name</div>
      </div>
    </div>
  </transition>
</template>
<script>
import mixin from '../js/mixin';
export default {
    mixins: [mixin],
    name: 'zt',
    data() {
        return {
            homeMsg: 'homeMsg'
        };
    },
    methods: {
        getMixinData() {
            alert('mixin中的name为：' + this.name);
        }
    }
};
</script>
<style lang="less" scoped>
.wrap {
    // background-color: white;
    .content {
        div {
            height: 1rem;
            // width: 1rem;
            background-color: yellowgreen;
            margin-top: 0.4rem;
            text-align: center;
            line-height: 1rem;
        }
    }
}
</style>
```

我们这里让2个组件home.vue 和 rule.vue都混合了mixin.js，一会我们可以通过对比来证明2个组件混合了相同的mixin.js但是2个组件不是共用关系，他们彼此没有影响。

## 效果

我们在home页面中：



![img](https:////upload-images.jianshu.io/upload_images/17849217-2fa3b51ba4bc0d19.gif?imageMogr2/auto-orient/strip%7CimageView2/2/w/700/format/webp)

home页面生命周期，按钮1，按钮2的演示

1.我们可以看到我们写在mixin.js中的生命周期created()已经调用
 2.点击第一个按钮，我们获取到了mixin.js中data中的name
 3.点击第二个按钮，我们调用到了mixin.js中的getMixinMsg方法

![img](https:////upload-images.jianshu.io/upload_images/17849217-8db182f65dd82cc9.gif?imageMogr2/auto-orient/strip%7CimageView2/2/w/700/format/webp)

点击第三个按钮

![img](https:////upload-images.jianshu.io/upload_images/17849217-0199e50a37da6bf1.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/700/format/webp)

mixin.js中

1.这次我们第三个按钮是通过home.vue调用mixin.js的getHomeMsg方法，发现不但home.vue可以调用到mixin.js的数据和方法，mixin.js也可以调用home.vue的数据和方法。（更加理解“混入”）

![img](https:////upload-images.jianshu.io/upload_images/17849217-761e9568c39b3774.gif?imageMogr2/auto-orient/strip%7CimageView2/2/w/700/format/webp)

改变mixin.js的数据



1.点击第四个按钮，我们改变了mixin.js中的name数据，再点击第一个按钮，发现数据已经改变。



![img](https:////upload-images.jianshu.io/upload_images/17849217-4e38bfe41ed37c45.gif?imageMogr2/auto-orient/strip%7CimageView2/2/w/700/format/webp)

跳转到rule组件后，mixin的name为初始（其实本身并不共用）


 1.我们先在home中改变mixin的name，然后我们调到rule页面，在rule页面获取到的mixin的name为初始名字
**mixin混入就像共用的业务逻辑，可以混入到组件中去，但是组件之间不受影响**



**注意：当本组件与mixin有同名方法或同名数据时，有先调用本组件的方法或数据，混入的部分失效**

## 总结：

其实这个demo就是想展示mixin的用法，需要一边结合代码一边看效果。主要还是一个“混入”的思想，理解了这个“混入”的思想，其实也很简单。就是代码中的相同业务，你把它剥离出来，封装后单独写个mixin，到需要用的组件时再混入进去。代码维护方便，复用率高，书写简洁。

Mixin对于封装一小段想要复用的代码来讲是有用的。对你来说Mixin当然不是唯一可行的选择：比如说高阶组件就允许你组合相似函数，Mixin只是的一种实现方式。我喜欢Mixin，因为我不需要传递状态，但是这种模式当然也可能会被滥用，所以，仔细思考下哪种选择对你的应用最有意义吧！



# ant-design-vue专题

组件的引入:

```javascript
import Ant from 'ant-design-vue'
//使用css
import 'ant-design-vue/dist/antd.css'

Vue.use(Ant)
```




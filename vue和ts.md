# typescript

## 基本数据类型

> **==基本数据类型注意:(我们在平时使用中, 大多数应该使用基本数据类型)==**
>
> 1. number和Number: number是基本数据类型, Number是类
> 2. string和String: string是基本数据类型, String是类
> 3. object和Object: object是基本数据类型, Object是类
> 4. ....

```typescript
//基础数据类型
(() => {
    //布尔类型
    let flag: boolean = true
    console.log(flag)

    //数字类型
    let a1: number = 10 // 十进制
    let a2: number = 0b1010  // 二进制
    let a3: number = 0o12 // 八进制
    let a4: number = 0xa // 十六进制
    console.log(a1);
    console.log(a2);
    console.log(a3);
    console.log(a4);

    //字符串类型
    let str1: string = '床前明月光'
    let str2: string = '疑似地上霜'
    let str3: string = '举头望明月'
    let str4: string = '低头思故乡'
    console.log(`${str1},${str2},${str3},${str4}`);

    //undefined 和 null 都可以作为其他类型的子类型, 把undefined 和 null 赋值给其他的类型的变量是可以的,
    // 前提是把typescript的配置改为非严格模式("strict": false)
    // let num: number = 1
    // num = null
    // console.log(num);

    //数组的定义, 数组里面只能存放单一的数据类型
    let arr1: number[] = [12, 23, 34, 45, 56]
    let arr2: Array<Number> = [12, 23, 34, 45, 56]

    //元组的定义, 可以存放复杂数据类型, 一开始定义数据的时候里面的数据类型和个数就已经确定了
    //注意问题: 元组定义和使用的两边要保持类型和个数的一致
    let arr3: [string, number, boolean] = ['jacklu', 23.567, true]
    //四舍五入, 保留两位
    console.log(arr3[1].toFixed(2));


    console.log('=======================================================================');

    //枚举类型, 枚举里面每个元素都有自己的编号, 默认从零开始, 也可以给里面的元素赋值(赋值number类型)
    enum Color {
        red = 10, green, blue
    }

    let color: Color = Color.red
    console.log(color);//10
    console.log(Color[11]);//green

    //any类型, 当一个数组中要存储多个数据, 个数不确定, 此时也可以使用any类型来定义数组
    let anyArray: any[] = ['yangmin', 'don`t', 'like', 'jacklu', true, 520, 999]
    console.log(anyArray);

    //void类型
    function showMsg(): void {
        console.log('没有返回类型');
    }
    showMsg()

    //object类型
    function getObject(obj: Object): Object {
        return {
            name: 'jacklu',
            love: 'yangmin'
        }
    }
    console.log(getObject({}));

    //联合类型
    function getStr(str: Number | String): String | Number{
        return str
    }
    console.log( getStr(520));

    //类型断言, 简单的理解成类型转换
    function getLength(str: String | Number): Number{
        //如果是字符串
        if((<String>str).length){
            return (<String>str).length
        }else{
            //如果是数字
            return str.toString().length
        }

    }
    console.log(getLength('hello jacklu'));
    

    //类型推断
    let txt;//any型
    let txt1 = 'jacklu'//String型
    txt = 12
    txt = 'yangmin'
    // txt1 = 23//不被允许



})()
```



## 接口

接口的核心原则之一是对值所具有的结构进行类型检查, 我们使用接口(Interface)来定义对象的类型

> ==接口是对象的状态(属性)和行为(方法)的抽象描述==

```typescript
(() => {
    //定义一个接口, 该接口作为IPerson对象的类型使用, 限定或者是约束该对象中的属性数据
    interface IPerson {
        readonly id: Number,//只读属性
        name: String,
        age: Number,
        sex?: String//sex属性是可有可无的
    }

    //定义一个对象, 该对象的类型就是我们定义的接口IPerson, 不可以添加接口中没有的属性
    const person: IPerson = {
        id: 1,
        name: 'yangmin',
        age: 18,
    }
    //    person.id = 2//只读属性不可以写
    person.name = 'jacklu'
    // person.girlFriend = 'yangmin'//不被允许的
    console.log(person);
})()
```



## 函数类型

```typescript
/**
 * 为了使用接口表示函数类型, 我们需要给接口定义一个调用签名
 * 他就像是一个只有参数列表和返回值类型的函数定义. 参数列表里的每个参数都需要名字和类型
 */
(() => {

    //定义一个接口, 用来作为某个函数的类型使用, 只能定义一个函数式接口
    interface ISearchFun {
        (source: string, search: string): boolean
    }

    //定义一个函数, 该类型就是上面定义接口的类型
    const searchString: ISearchFun = function (source: string, search: string): boolean {
        //在source中查找subString这个字符串
        return source.search(search) != -1
    }

    console.log(searchString('love you yangmin', 'love'));//true

})()
```



## 类类型

```typescript
/**
 * 类类型: 类的类型可以通过接口来实现
 */
(() => {

    //定义一个接口
    interface IFly {
        //该方法没有任何的实现
        fly(): void
    }
    //定义一个类来实现这个接口
    class Person implements IFly {
        fly() {
            console.log('I can fly....I`m the supper man!')

        }
    }

    const p = new Person()
    p.fly()

    //定义一个接口
    interface ISwim {
        swim(): void
    }

    class Person2 implements IFly, ISwim {
        swim() {
            console.log('swim2...')
        }
        fly() {
            console.log('fly2...')
        }
    }

    const p2 = new Person2()
    p2.fly()
    p2.swim()

    //接口实现接口
    interface flyAmdSwim extends IFly, ISwim { }

    class Person3 implements flyAmdSwim {
        swim() {
            console.log('swim3...')
        }
        fly() {
            console.log('fly3...')
        }
    }

    let p3 = new Person3()
    p3.swim()
    p3.fly()

})()
```



## 类

```typescript
(()=>{

    class Person{
        name: string
        age: number
        gender: string

        constructor(name:string = 'yangmin', age:number = 22, gender: string = '女'){
            this.name = name
            this.age = age
            this.gender = gender
        }

        sayHi(str: string){
            console.log(`大家好, 我是${this.name}, 今年${this.age}岁, 喜欢${str}`);
        }
    }

    const person = new Person();
    person.sayHi('jacklu')

})()
```



## 继承

```typescript
(()=>{
    class Person{
        name:string
        age: number 
        gender: string 

        constructor(name:string = 'yangmin', age:number = 22, gender:string = '女'){
            this.name = name
            this.age = age 
            this.gender = gender 
        }
        sayHi(str:string){
            console.log(`我是${this.name},${str}`);
        }
    }

    /**
     *  定义一个类继承Person
     * 一个类中不可以有两个构造函数, 子类的构造函数势必要调用父类的构造函数(默认也会调用)
     */
    class Student extends Person{
        constructor(name:string,age:number,gender:string){
            //调用父类的构造函数
            super(name,age,gender);
        }
        sayHi(){
            super.sayHi('你是谁呀?')
        }
    }

    //进行实例化
    const person = new Person()
    person.sayHi('hahaha.....')

    const student = new Student('jacklu',23,'男')
    student.sayHi()

})()
```



## 多态

> **==ts中的多态与java的不一样, ts中子类调用属性还是子类, 但是在java中子类调用的属性是父类的==**

```typescript
(() => {

    //定义一个父类
    class Animal {
        name: string
        constructor(name: string = '动物') {
            this.name = name
        }
        run(distance: number = 0) {
            console.log(`跑了${distance}米远的距离  父类的方法`);
        }
    }
    //定义一个子类
    class Dog extends Animal {
        constructor(name: string) {
            super(name)
        }
        run(distance: number = 5) {
            console.log(`跑了${distance}米远的距离  ${this.name}`);
        }

    }
    //定义一个子类
    class Pig extends Animal {
        constructor(name: string) {
            super(name)
        }
      /*   run(distance: number = 10) {
            console.log(`跑了${distance}米远的距离  ${this.name}`);
        } */

    }

    //实例化父类对象
    let ani: Animal = new Dog('狗狗')
    //调用的是子类对象的方法
    ani.run()
    //属性也是调用子类对象的, 这点跟java的不一样, java调用的是父类的属性
    console.log(ani.name);

    ani = new Pig('猪猪')
    //没有重写则调用的是父类的方法, 重写了则调用的是子类的方法
    ani.run()


})()
```


# 《js面向对象及设计模式》    

## linux 设计哲学   


准则1：小即是美   
准则2：让每个程序做好一件事   
准则3：快速建立原型   
准则4：舍弃高效率而取可移植性   
准则5：采用纯文本来存储数据（可读性）   
准则6：充分利用软件杠杆效应（复用）   
准则7：使用shell复用（提出了具体的解决方案）      
准则8：避免强制性的用户界面     
准则9：让每个程序成为过滤器（流式一个处理一个）    

## 六大设计原则SOLID   


1.S-单一职责原则（single）   
做好一件事   

2.O-开放封闭元整(open)   
对于拓展开放，对于修改封闭    

3.l-里氏替换原则（Liskov Substitution Principle)   
子类能覆盖父类，父类能出现的地方子类就能出现

4.I-接口隔离原则(Interface Segregation Principle)   
保持接口独立，单独小而精

5.D-依赖倒转原则(Dependence Inversion Principle)
 面向抽象编程，不依赖具体实现
  
6.迪米特法则（最少知道原则）（Demeter Principle）
一个类对自己依赖的类知道的越少越好    

## 设计模式
二十三种设计模式   

创建型(5)
工厂方法模式、抽象工厂模式、单例模式、建造者模式、；

组合型(7)
适配器模式、装饰者模式、代理模式、外观模式、桥接模式、组合模式、享元模式

行为型(11)
策略模式，模板方法模式，观察者模式，迭代器模式，职责连模式，命令模式，备忘录模式，状态模式，访问者模式，中介者模式，解释器模式

### 1.工厂模式（创建）
对new进行封装。  
```js
function createPerson(person) {
    let {name,age} = person
    let o = new Object()
    o.name = name
    o.age = age
    o.sayName = function() {
    console.log(this.name)
    }
    return o
}
```
### 2.单例模式（创建）
该类负责创建自己的对象，同时确保只有单个对象被创建。这个类提供了一种访问其唯一的对象的方式，可以直接访问，不需要实例化该类的对象。

1. 单例类只能有一个实例。   
2. 单例类必须自己创建自己的唯一实例。   
3. 单例类必须给所有其他对象提供这一实例。   

```js
class Person {
    sayName() {
        console.log('我是小明！')
    }
}
Person.getInstance = (function() {
  let instance
  return function() {
     if (!instance) {
         instance = new Person()
     } 
     return instance
  }
})()
let person1 = Person.getInstance()
perso1.sayName()
```
场景    
1. jQuery 只有一个$   
2. 所有系统只有一个登陆框

### 3.适配器模式（组合）

就是充电插头，对电压进行转换   
适配器模式（Adapter Pattern）是作为两个不兼容的接口之间的桥梁。
```js
class Adapter {
    specificRequest () {
        return '德国插头'
    }
}
class Target {
    constructor () {
        this.adapter = new Adapter()
    }
    request () {
        let info = this.adapter.specificRequest()
        return `${info} 转换为 中国`
    }
}
```

### 4.装饰器模式
装饰器模式（Decorator Pattern）允许向一个现有的对象添加新的功能，同时又不改变其结构。这种类型的设计模式属于结构型模式，它是作为现有的类的一个包装。

```js
class Circle {
  draw () {
      console.log('画一个○')
  }
}
class RedCircle {
  constructor(circle){
      this.circle = circle
  }
  draw () {
      this.circle.draw()
      this.setRedCircle(this.circle)
  }
  setRedCircle () {
      console.log('这里画一个红○')
  }
}
```
ES7 装饰器
基本上，装饰器的行为就是下面这样。   
修饰类   
```js
@decorator
class A {}

// 等同于

class A {}
A = decorator(A) || A;

```
修饰方法   

装饰器第一个参数是类的原型对象，装饰器的本意是要“装饰”类的实例，但是这个时候实例还没生成，所以只能去装饰原型（这不同于类的装饰，那种情况时target参数指的是类本身）；第二个参数是所要装饰的属性名，第三个参数是该属性的描述对象。
```js
function x(target, name, descriptor) {
  return descriptor
}
```
不能修饰函数，因为存在变量提升
### 5.代理模式（组合）

无权访问对象，进行代理访问,
示例
1. 科学上网
2. 明星经纪人

一个类代表另一个类的功能.

场景
1. 网页事件代理
2. es6 proxy
3. $.proxy   
代理类与目标类隔离
### 6.外观模式（组合）

隐藏系统的复杂性，并向客户端提供了一个客户端可以访问系统的接口。   
子系统中的一组接口提供一个一致的界面，外观模式定义了一个高层接口，这个接口使得这一子系统更加容易使用。
### 7.观察者模式（行为）
观察者模式和发布订阅模式的区别，最大的区别是调度的地方（发布订阅模式）.  

虽然两种模式都存在订阅者和发布者（具体观察者可认为是订阅者、具体目标可认为是发布者），但是观察者模式是由具体目标调度的，而发布/订阅模式是统一由调度中心调的，所以观察者模式的订阅者与发布者之间是存在依赖的，而发布/订阅模式则不会。

```js
class Subject {
    constructor () {
        this.state = 0
        this.observers = []
    }
    getState () {
        return this.state
    }
    setState (state) {
        this.state = state
        this.notifyAllObservers()
    }
    notifyAllObservers () {
        this.observers.map((item) => {
            item.update()
        })
    }
    attach (observer) {
        this.observers.push(observer)
    }
}
class Observer {
  constructor(name, subject) {
      this.name = name
      this.subject = subject
      this.subject.attach(this)
  }
  update () {
      console.log('update')
  }
}
let s = new Subject()
let o =new Observer('O', s)
```
场景
1. 网页事件绑定
2. Promise
3. $.Callbacks() 听都没听过
4. node.js及各种框架的自定义事件

### 8.迭代器模式（行为）
这种模式用于顺序访问集合对象的元素，不需要知道集合对象的底层表示。
主要用来解决不同的方式来遍历整个整合对象。
```js
class Iterator {
    constructor () {
        this.list = container.list
        this.index = 0
    }
    next () {
        return this.list[this.index++]
    }
    hasNext () {
        if (this.index>=this.list.length) {
            return false
        }
        return true
    }
}
class Container {
    constructor (list) {
        this.list = list
    }
    getIterator () {
        return new Iterator(this)
    }
}

let c = new Container([1,2,3,4])
let i = c.getIterator()
while(i.hasNext()) {
    console.log(i.next())
}
```
场景
1. ES6 的迭代器
2. jQuery的each

有序数据集合（map,set,array,string,typeArray,arguments,NodeList）,以上都有Symbol.iterator,属性是一个函数，执行返回一个迭代器。
## 9.状态模式（行为）
类的行为是基于它的状态改变的。这种类型的设计模式属于行为型模式。
```js
// 交通灯 红绿黄
class State {
    constructor (color) {
        this.color = color
    }
    handle (l) {
        console.log('retrun light')
        context.setState(l)
    }
}
class Context  {
    constructor() {
        this.state = null
    }
    getState () {
        return this.state
    }
    setState (state) {
        this.state = state
    }
}
let context = new Context()
let green = new State('lv')
```
## 10.原型模式
用原型实例指定创建对象的种类，并且通过拷贝这些原型创建新的对象。
`Object.create(Instance)`
## 11.桥接模式
将抽象部分与实现部分分离，使它们都可以独立的变化。自由组合。
## 12.组合模式
生成属性结构，标识整体-部分关系，让整体和部分有统一的操作方式
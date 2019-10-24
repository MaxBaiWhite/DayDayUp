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

### 1.工厂模式
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
### 2.单例模式
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
1、创建jS对象的几种方式：
 
 1）工厂模式：
  ```
  function createPersion(name,age){
    var o = new Object();
    o.name = name；
    o.age = age;
    o.sayName = function(){
      console.log(this.name)
    }
    return o;
  }
  var person1 = createPersion('Nicholas','29');
  ```
  劣势：无法解决对象识别问题；
  
  2）构造函数模式：
  ```
  function Presion(name,age){
    this.name = name；
    this.age = age;
    this.sayName = function(){
      console.log(this.name)
    }
  }
  var person1 = new Persion('Nicholas','29');
  ```
  优势：解决了对象识别问题
  劣势：每个实例的方法均不同，浪费方法产出空间
  
  3）原型模式：
  ```
  function Presion(name,age){
  }
  Persion.prototype = {
    name :'nameEx',
    age :'29',
    sayName : function(){
      console.log(this.name)
    }
  }
  var person1 = new Persion();
  ```
  优势：解决了对象识别问题;每个实例的方法均不同，浪费方法产出空间的问题
  
  
  4）原型模式：
  ```
  function Preson(name,age){
    this.name = name
    this.age = age
  }
  Person.prototype = {
    constructor : Persion
    sayName : function(){
      console.log(this.name)
    }
  }
  var person1 = new Person();
  var persion2 = new Person();
  ```
  优势：最大限度的节省内存，集两种模式之长；
  
  5）动态原型模式：
  ```
  function Preson(name,age){
    this.name = name
    this.age = age
    if(typeof this.sayName != 'function'){
      Person.prototype.sayName = funtion(){
        console.log(this.name)
      }
    }   
  }
  var friend = new Person('Nicholas','29')
  friend.sayName()
  ```
 
 6）寄生构造函数
 ```
 function SpecialArray(){
    var values = new Array();
    values.push.apply(values,arguments);
    values.toPipedString = function(){
       return this.join('|')
    };
    return values;
 }
 
 var colos = new SpecialArray('red','blue','green');
 alert(colors.toPipedString());//'red|blue|green'
 ```

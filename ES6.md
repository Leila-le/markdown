疑问：
1. use strict
Generator 函数

# 1.类的由来
ES6 提供了更接近传统语言的写法，引入了 Class（类）这个概念，作为对象的模板。通过class关键字，可以定义类。
```javascript
class Point {
  constructor(x, y) {
    this.x = x;
    this.y = y;
  }

  toString() {
    return '(' + this.x + ', ' + this.y + ')';
  }
}
```

      - 上面代码定义了一个“类”，可以看到里面有一个constructor()方法，
        这就是构造方法，而this关键字则代表实例对象。
      - Point类除了构造方法，还定义了一个toString()方法。
        注意，定义toString()方法的时候，前面不需要加上function这个关键字，直接把函数定义放进去了就可以了。
      - 另外，方法与方法之间不需要逗号分隔，加了会报错。
ES6 的类，完全可以看作构造函数的另一种写法。

```js
class Point {
  // ...
}

typeof Point // "function"
Point === Point.prototype.constructor // true
```

    上面代码表明，类的数据类型就是函数，类本身就指向构造函数。
    使用的时候，也是直接对类使用new命令，跟构造函数的用法完全一致。
```js
class Bar {
  doStuff() {
    console.log('stuff');
  }
}

const b = new Bar();
b.doStuff() // "stuff"

```
 事实上，类的所有方法都定义在类的prototype属性上面。
**因此，在类的实例上面调用方法，其实就是调用原型上的方法。**
```JS
class B {}
const b = new B();

b.constructor === B.prototype.constructor // true

```

    上面代码中，b是B类的实例，它的constructor()方法就是B类原型的constructor()方法。

由于类的方法都定义在prototype对象上面，所以类的新方法可以添加在prototype对象上面。Object.assign()方法可以很方便地一次向类添加多个方法:
```JS
class Point {
  constructor(){
    // ...
  }
}

Object.assign(Point.prototype, {
  toString(){},
  toValue(){}
});

```

**另外，类的内部所有定义的方法，都是不可枚举的（non-enumerable）**
```JS
class Point {
  constructor(x, y) {
    // ...
  }

  toString() {
    // ...
  }
}

Object.keys(Point.prototype)
// []
Object.getOwnPropertyNames(Point.prototype)
// ["constructor","toString"]

```
*上面代码中，toString()方法是Point类内部定义的方法，它是不可枚举的。这一点与 ES5 的行为不一致。*
```JS
var Point = function (x, y) {
  // ...
};

Point.prototype.toString = function () {
  // ...
};

Object.keys(Point.prototype)
// ["toString"]
Object.getOwnPropertyNames(Point.prototype)
// ["constructor","toString"]

```
**上面代码采用 ES5 的写法，toString()方法就是可枚举的。**

# 2. constructor()方法

`constructor()方法`是类的默认方法，通过new命令生成对象实例时，自动调用该方法。一个类必须有`constructor()方法`，如果没有显式定义，一个空的`constructor()方法`会被默认添加。

**constructor()方法默认返回实例对象（即this），完全可以指定返回另外一个对象。**
类必须使用new调用，否则会报错。这是它跟普通构造函数的一个主要区别，后者不用new也可以执行。
```JS
class Foo {
  constructor() {
    return Object.create(null);
  }
}

Foo()
// TypeError: Class constructor Foo cannot be invoked without 'new'
```


```javascript
let commodityType = commodityHead.querySelector('.commodity-type h4').innerText;
                let commodityPrice = commodityHead.querySelector('.commodity-price .value').innerText;
                let order = {
                    'type': commodityType,
                    'price': commodityPrice,
                }
                let params = new URLSearchParams(order);// 使用 URLSearchParams 将对象转换为查询参数
                let url = 'api/business/package-order/' + params.toString();
                fetch(url, {
                    method: "POST",
                    headers: {
                        'Content-Type': 'application/json', // 告诉服务器发送的是 JSON 数据
                    },
                    body: JSON.stringify(order), // 将 order 对象转换为 JSON 字符串作为数据体
                })
```

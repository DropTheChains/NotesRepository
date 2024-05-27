ECMAScript是规范，而JavaScript是ES的实现。


## 1、let

```JavaScript
越域问题：
{
    var a = 1;
    let b = 1;
}

console.log(a)  //1
console.log(b)  //Uncaught ReferenceError: b is not defined


重复声明问题：
var a = 1;
var a = 2;
var a = '测试';

let b = 1;
let b = 2;   // SyntaxError: Identifier 'b' has already been declared 


变量提升：
console.log(a)  //undefined
var a = 1;
console.log(b)   //ReferenceError: Cannot access 'b' before initialization
let b = 1;
```

## 2、const

```JavaScript
const a = 1;
a = 2;  //Uncaught TypeError: Assignment to constant variable.
```

## 3、解构

```JavaScript
数组解构
let arr = [1,2,3]
console.log(arr[1])

let [x,y,z] = [1,2,3]
console.log(x,y,z)

对象解构
let person = {
    name: '张三',
    age: 18,
    email: '12345@admin.com'
}
let {name,age} = person;
console.log(name,age)

方法传参解构
function haha({name,age}){
    console.log(name)
    console.log(age)
}
haha(person)
```

## 4、链判断

```JavaScript
let message = {
    body: {
        user: {
            firstName: 'haha'
        }
    }
}
console.log(message?.body?.user?.firstName || 'default' )

```

## 5、参数默认值

```JavaScript
有默认值的参数尽量放到参数列表的最后
function add(a,c,b=5){
    return a + b + c;
}
console.log(add(1,2))
```

## 6、箭头函数

```JavaScript
function print(arg){
    console.log(arg)
}

let print1 = function(arg){
    console.log(arg)
}

let print2 = (arg) =>{
    return arg;
}

let sum = (a,b) =>{
    return a+b;
}
sum(1,2)
```

## 7、模板字符串

```JavaScript

let info = `你好，我的名字是：【${name}】,我的年龄是【${age}】,我的邮箱是【${person.email}】`;
console.log(info)

```

## 8、Promise
```JavaScript
let url = "https://mdn.github.io/learning-area/javascript/apis/fetching-data/can-store/products.json";

console.log(1)

let promise = fetch(url);

promise.then( (resp) => {

    resp.json().then( (data) =>{

        console.log(data)

    })

})

console.log(2)
```


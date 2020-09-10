# javascript
javascript学习
- 数组去重的方法 - splice()
```javascript
//创建一个数组
var arr = [1, 2, 3, 2, 2, 1, 3, 4, 2, 5];

//去除数组中重复的数字
//获取数组中的每一个元素
for (var i = 0; i < arr.length; i++) {
    //console.log(arr[i]);
    /*获取当前元素后的所有元素*/
    for (var j = i + 1; j < arr.length; j++) {
        //console.log("---->"+arr[j]);
        //判断两个元素的值是否相等
        if (arr[i] == arr[j]) {
            //如果相等则证明出现了重复的元素，则删除j对应的元素
            arr.splice(j, 1);
            //当删除了当前j所在的元素以后，后边的元素会自动补位
            //此时将不会在比较这个元素，我需要再比较一次j所在位置的元素
            //使j自减
            j--;
        }
    }
}
```
- map()方法
```javascript
const arr1 = [
    { name: '千古壹号', age: '28' },
    { name: '许嵩', age: '32' },
];

// 将数组 arr1 中的 name 属性，存储到 数组 arr2 中
const arr2 = arr1.map((item) => item.name);

// 将数组 arr1 中的 name、age这两个属性，改一下“键”的名字，存储到 arr3中
const arr3 = arr1.map((item) => ({
    myName: item.name,
    myAge: item.age,
})); // 将数组 arr1 中的 name 属性，存储到 数组 arr2 中
//打印结果
arr1:[{"name":"千古壹号","age":"28"},{"name":"许嵩","age":"32"}]

arr2:["千古壹号","许嵩"]

arr3:[{"myName":"千古壹号","myAge":"28"},{"myName":"许嵩","myAge":"32"}]
```
- 对象的操作
  - in运算符： 通过该运算符可以检查一个对象中是否含有指定的属性，如果有则返回true，没有则返回false。
  语法： '属性名' in 对象   例如: 'name' in obj
- ES6语法
  - 可以利用babel插件将ES6语法转变为ES5语法，这样可以适用于低版本的游览器
  - 数组的解构赋值：let [a, b,c] =[1,2,3] ,根据位置进行对应一一赋值
  - 对象的解构赋值： 将对象中的值按照属性匹配的方式提取出来，然后赋值给变量 
  ```javascript
  const person = { name: 'qianguyihao', age: 28, sex: '男' };
let { name, age, sex } = person; // 对象的结构赋值

console.log(name); // 打印结果：qianguyihao
console.log(age); // 打印结果：28
console.log(sex); // 打印结果：男
```
  - 字符串的解构： 字符串也可以解构，因为此时的字符串被转换为一个类似于数组的对象
  ```javascript
  const [a, b, c, d] = 'hello';
console.log(a);  //h
console.log(b);  // e
console.log(c);   // l
```
- 剩余参数：可以将不确定数量的剩余的元素放到一个数组中。
  - 为什么使用剩余参数：方法的参数是三个，但使用时是用到了四个参数，所以控制台会报错
   ``` javascript
   function fn(a, b, c) {
      console.log(a);
      console.log(b);
      console.log(c);
      console.log(d);
  }

  fn(1, 2, 3);
  ```
  - 剩余参数的写法：
  ```javascript
    const fn = (...args) => {
      //当不确定方法的参数时，可以使用剩余参数
      console.log(args[0]);
      console.log(args[1]);
      console.log(args[2]);
      console.log(args[3]);
  };

  fn(1, 2);
  fn(1, 2, 3); //方法的定义中了四个参数，但调用函数时只使用了三个参数，ES6 中并不会报错。
  ```
  - 代码举例
  ```javascript
  const sum = (...args) => {
    let total = 0;
    args.forEach(item => total += item); // 注意 forEach里面的代码，写得 很精简
    return total;
};
console.log(sum(10, 20, 30));
```
  - 扩展运算符（展开语法）：扩展运算符是将数组或者对象拆分成逗号分隔的参数序列
  ```javascript
  let arr1 = ['www', 'smyhvae', 'com'];
  let arr2 = arr1; //let arr2 = arr1;其实是让 arr2 指向 arr1 的地址。也就是说，二者指向的是同一个内存地址。
  let arr3 = [...arr1]; 
  arr2.push('你懂得');  //当arr2中新增元素时，arr1中也会新增元素，一起改变
  arr3.push('你懂得');   //arr3改变时arr1不会进行改变
 //合并数组
  let arr1 = ['王一', '王二', '王三'];
let arr2 = ['王四', '王五', '王六'];
// ...arr1  // '王一','王二','王三'
// ...arr2  // '王四','王五','王六'
// 方法1
let arr3 = [...arr1, ...arr2];
console.log(arr3); // ["王一", "王二", "王三", "王四", "王五", "王六"]
// 方法2
arr1.push(...arr2);
console.log(arr1); // ["王一", "王二", "王三", "王四", "王五", "王六"]
  ``` 
  - set数据结构：可以接收一个数组作为参数，实现数组去重
  ```javascript
  const set2 = new Set(['张三', '李四', '王五', '张三']); // 注意，这个数组里有重复的值

// 注意，这里的 set2 并不是数组，而是一个单纯的 Set 数据结构
console.log(set2); // {"张三", "李四", "王五"}

// 通过扩展运算符，拿到 set 中的元素（用逗号分隔的序列）
// ...set2 //  "张三", "李四", "王五"

// 注意，到这一步，才获取到了真正的数组
console.log([...set2]); // ["张三", "李四", "王五"]
```
  - promise: 解决回调地狱的问题，避免了层层嵌套的回调函数。
  - JavaScript 的执行环境是单线程。所谓单线程，是指 JS 引擎中负责解释和执行 JavaScript 代码的线程只有一个，也就是一次只能完成一项任务，这个任务执行完后才能执行下一个，它会「阻塞」其他任务。这个任务可称为主线程。异步模式可以一起执行多个任务
  - 常见的异步模式有以下几种： 定时器，接口调用，事件函数
  - js中常见的接口调用方式：原生ajax, 基于jQuery的ajax, Fetch, Promise, axios
  - async/await: 更加方便地进行异步操作。
  - 函数 
  - break、continue、return 的区别
    - break ：结束当前的循环体（如 for、while）
    - continue ：跳出本次循环，继续执行下次循环（如 for、while）
    - return ：1、退出循环。2、返回 return 语句中的值，同时结束当前的函数体内的代码，退出当前函数。
  - 闭包：如果这个作用域可以访问另外一个函数内部的局部变量，那就产生了闭包，而另外那个作用域所在的函数称为闭包函数。
   ```javascript
      function fn1() {
      let a = 10;

      function fn2() {
          console.log(a);
      }
      fn2();
  }

  fn1();
  ```

  
  
  
  
  
  
  






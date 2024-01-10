## 1. Object .运算符和[]运算符的区别
### 相同点：两个都可以访问对象的属性。
### 不同点：
#### 1. []运算符可以使用数字作为属性，.运算符不能。
```
const obj = {1:100};
console.log(obj.1);//报错
console.log(obj[1]);100
```
#### 2. []运算符可以使用字符串变量作为属性，.运算符不能。
```
const obj = {name:'rose'};
const str = 'name';
console.log(obj.str);//undefined
console.log(obj[str]);//'rose'
```
#### 3. []可以在程序运行时创建和修改属性，.运算符不能。
```
const list = [{name:'jack',age:18,hobby:'eat'},{name:'rose',age:19,hobby:'run'}];
const newList = list.map(item=>{
  const obj  ={};
  for(let a in item){
    obj[a] = item[a];//如果用.运算符，得到的obj只有属性a，该有的属性都不会有。因为这里a是变量，所以要用[]。
  };
  return obj;
});
console.log(newList);
```
#### 4. 对于一些可能导致语法错误的字符、关键字或保留字，都使用[]运算符，不要使用.运算符，会报错。
#### 5.对于以下代码可以怎么优化？
![image](https://github.com/Lujinghui1234/Javascript/assets/109168485/19e43a42-ea32-40fe-bdeb-d6116fe6a3dc)


### 1. Object .运算符和[]运算符的区别
#### 相同点：两个都可以访问对象的属性。
#### 不同点：
##### 1. []运算符可以使用数字作为属性，.运算符不能。
```
const obj = {1:100};
console.log(obj.1);//报错
console.log(obj[1]);100
```
##### 2. []运算符可以使用变量作为属性，.运算符不能。
```
const obj = {name:'rose'};
const str = 'name';
console.log(obj.str);//undefined
console.log(obj[str]);//'rose'
```
##### 3. []可以在程序运行时创建和修改属性，.运算符不能。
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
##### 4. 对于一些可能导致语法错误的字符、关键字或保留字，都使用[]运算符，不要使用.运算符，会报错。
### 2. Javascript shorthand coding techniquet
ex.1
```
//Longhand:
const fruits = ['mango', 'peach', 'banana'];
for (let i = 0; i < fruits.length; i++)

//Shorthand:
for (let fruit of fruits){
  console.log(fruit);//mango,peach,banana
}

//If you just wanted to access the index, do:
for (let key in fruits){
  console.log(key);//0,1,2
}
```
ex.2
```
const variable = xxx;
//Longhand:
const variable1 = variable ? variable : '';
//Shorthand:
const variable1 = variable || '';
```
### 3. ??运算符和||运算符的区别
#### 1，??运算符只会判断左边的变量是否为null或undefined；||运算符除了null和undefined还考虑到了空字符串/false/0等情况
#### 2，??运算符判断左边变量如果为null或undefined，返回右边变量；||运算符判断左边变量转换为Boolean类型时，如果为true返回左边变量，为false则返回右边变量
#### 3，开发中||运算符的使用场景比??运算符更多，因为||运算符除了null和undefined还考虑到了空字符串/false/0等情况。




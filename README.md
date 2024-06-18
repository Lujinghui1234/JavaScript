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
### 4. 页面跳转传递数据，为什么开发中极少使用localStorage?
    1, 假设换了个浏览器（考虑用户转发页面），不会有本地缓存数据
    2，数据可在控制台看到，容易被窃取和XSS攻击，这点可以通过https协议加密/数据加密/数据转义和过滤解决，但是比较麻烦
    3，由于数据是持久化存储，除非人为清除数据不然数据会一直存在，数据量过大容易导致存储空间不足
### 5. 页面跳转数据，通过url传递参数有什么优缺点？
```
//跳转传递参数：
import {useNavigate} from 'react-router-dom';
const navigate = useNavigate();
const data = {a:b:{1}};
const stringifyData = 写一个方法递归处理data，将每一层数据都处理成string,可使用qs第三方库qs.stringfy()辅助处理
navigate(`detail?${stringifyData}`)
```

```
//获取参数：
import {useLocation} from 'react-router-dom';
const location = useLocation();
const queryParams = location.search.replace(location.search[0],'');//[0]是个问号
const queryData = 写一个方法将string类型的queryParams转换成对象类型，可使用qs第三方库qs.parse()辅助处理
```
#### 优点：
    1.传参可以通过navigate跳转时直接在?后面拼接即可传参，使用方便
#### 缺点:
    1，参数较多时，url太长影响美观,而且如果长度过长，会受浏览器限制
    2，参数暴露在url上，数据容易被窃取且被随意更改！！！即使空格和特殊符号已经被转义，但也可以被识别

### 6. Javascript中k可通过Object.entries()同时处理对象的key和value
```
const obj = {
    input: { name: 'rose' },
    eyeList: [{ code: '123' }]
};
 for (const [key,value] of Object.entries(obj)) {
  console.log(key)//input、eyeList
  console.log(value)//{ name: 'rose' }、[{ code: '123' }]
}
```




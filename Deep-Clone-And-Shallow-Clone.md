## 1. Lodash/cloneDeep
  深克隆很方便，但是引入第三方库会消耗内存空间，如果项目多处引用多个库，会影响项目运行速度
## 2. JSON.parse(JSON.stringify(obj)) 
  这个是深克隆，但对于function和undefined会丢失、Date变成string类型、Map、Set会变成{}
## 3. 对象或数组的扩展运算符
### 情况①：对象或数组只有一层，且元素都是基本数据类型，属于深拷贝
 ```
const obj = {name:'rose',age:18};
const newObj = {...obj};
obj.age = 20
console.log(obj.age,newObj.age);//20,18
 ```
### 情况②：对象或数组里的元素是引用数据类型，属于浅拷贝
  ```
  const obj = {num:1,list:[1,2,3]};
  const newObj = {...obj};
  newObj.list.push(4);
  console.log(obj,newObj);//list都会变成[1,2,3,4]
  ```
## 4. structuredClone，这个是深克隆（https://www.builder.io/blog/structured-clone）
  ```
  const obj = {num:1,list:[1,2,3]};
  const newObj = structuredClone(obj);
  //优点：不用引入第三方库，节省内存空间
  //缺点：用在function和DOM上会报错，Property descriptors, setters, and getters也会报错；
  ```
### structuredClone用在类的实例对象上会有问题
  ```
  Class Far{
    name="rose"
    say(){
      return 'hello'
    }
   };
  const son = new Far();
  const newSon = structuredClone(son);
  console.log(newSon.instanceof Far);//false,用在类的实例身上，实例新克隆出来的对象不再是类的实例了
  ```
## 5. Object.assign 这个是浅克隆
```
const obj = {a:0,b:{c:0}};
const obj2 = Object.assign({},obj);
obj.a = 1;
console.log(obj.a,obj2.a);//1,0
```


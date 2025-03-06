## 1. 同一个api，页面call：cancel，但postman call：200
因为postman和浏览器的环境不同，postman会设置了某些东西，项目上线后用户使用环境也是浏览器，肯定要以浏览器为准。
## 2. 不要滥用可选链，看为什么是空数据，是api原因还是前端代码写错了？有些明知道不会是空数据的，就不要加可选链了。
## 3. git commit 报错：pidtree\lib\pidtree.js    new Error: no matching pid found
这个报错是因为本地进程太多了，解决方法是清理本地内存空间：清空回收站、关闭不使用的进程，关闭编辑器，直接用git bash操作。
## 4. 大数值精度问题
前言：在ES6以前，Javascript没有专门的整数类型，所有的数字都被表示为双精度64位浮点数，这就意味着Javascript能安全地处理的整数范围是有限的，超过16位数的大数字会失去精度。

场景：API返回数据：obj_id为18位数值

![image](https://github.com/Lujinghui1234/Coding-Common-Error/assets/109168485/d08c40e2-15de-4fb3-ba48-6a3f01b1e967)

问题：使用JSON.parse（obj_id）,变成了898186844400803800，失去了精度。

解决：判断数据类型，如果是大精度数据，就不要JSON.parse()了（这个方法会变成Number,大数据会丢失精度）。
```
if(typeof obj_id === 'string' && /^\d{16,}$/.test(obj_id)){
    return obj_id;
}else{
    return JSON.parse(obj_id)
};
```
## 5. 自己在本地新建了个项目，关联远程仓库时git push报错：The requested URL returned error: 403
  解决：https://blog.csdn.net/qq_40226073/article/details/119801341
  思路是生成仓库的token令牌，git绑定密码为这个令牌。
## 6.Vite脚手架npm i报错: A complete log of this run can be found in C:\users\AppData\local\npmm_cache\_log_***.jpg
解决思路：推荐第二种，安装依赖pnpm是优先于npm的，速度也更快

```
一，用npm
1、删除掉原有的node_modules
2、npm cache clean --force 清除缓存
3、重新运行 npm i 安装依赖
```

```
二，用pnpm
1、npm i pnpm -g
2、pnpm install
3、pnpm run dev
```
## 7.常见ts报错：

![image.png](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/912ef097268a48f780741251f314f871~tplv-k3u1fbpfcp-watermark.image?)
答案：https://blog.csdn.net/qq_40864647/article/details/125764130

最简单的方法是断言：

![image.png](https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/b13858456251461d879e5ee68fd8337a~tplv-k3u1fbpfcp-watermark.image?)

## 8.关于tailwindcss的使用注意事项
```
//html代码
<div className="searchTop min-w-[540px]">123</div>

//媒体查询css代码
.searchTop{
    min-width: 100%;//这里想要修改宽度，必须使用和tailwindcss一样的属性：min-width！！！！！！!而不是width
}
```
## 9. api返回的id为interger类型，前端拿着这个id再次请求api，id精度失真
原因：太大的数字用interger会丢失精度问题
解决：改为string

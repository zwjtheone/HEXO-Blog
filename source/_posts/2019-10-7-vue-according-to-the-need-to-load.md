---
title: vue-router 按需加载的 3 种方式
date: 2019/10/7 11:28
updated: 2019/10/7 11:28
tags:
	- vue

---

# 下列 3 种方式均可将组件打包成单文件异步加载

- vue 异步
- es 提案的 import
- webpack 的 require.ensure
- 
## vue 异步
```
{
    path: '/promisedemo',
    name: 'PromiseDemo',
    component: resolve => require(['../components/PromiseDemo'], resolve)
}
```


## es 提案 import

```
// 下面2行代码，没有指定webpackChunkName，每个组件打包成一个js文件。
const ImportFuncDemo1 = () => import('../components/ImportFuncDemo1')
const ImportFuncDemo2 = () => import('../components/ImportFuncDemo2')

// 下面2行代码，指定了相同的webpackChunkName，会合并打包成一个js文件。
// const ImportFuncDemo = () => import(/* webpackChunkName: 'ImportFuncDemo' */ '../components/ImportFuncDemo')
// const ImportFuncDemo2 = () => import(/* webpackChunkName: 'ImportFuncDemo' */ '../components/ImportFuncDemo2')
export default new Router({
    routes: [
       {
            path: '/importfuncdemo1',
            name: 'ImportFuncDemo1',
            component: ImportFuncDemo1
        },
        {
            path: '/importfuncdemo2',
            name: 'ImportFuncDemo2',
            component: ImportFuncDemo2
        }
    ]
})

```

## require.ensure
```
{
    path: '/promisedemo',
    name: 'PromiseDemo',
    component: resolve => require.ensure([], () => resolve(require('../components/PromiseDemo')), 'demo')
}

```

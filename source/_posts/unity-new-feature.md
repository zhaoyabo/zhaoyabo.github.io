---
title: unity new feature
date: 2021-04-27 14:15:45
tags: unity

---

# unity2018+ 新特性

1.Addressable 与 Assetbundle 的使用对比。

<!--more-->

参考文章

https://www.jianshu.com/p/8009c16fcab3

https://zhuanlan.zhihu.com/p/77600079

https://zhuanlan.zhihu.com/p/82247256

Addressable 加载资源是异步的，需要设置回调。

​	Addressables.LoadAssetAsync（url）.Completed += (AsyncOperationHandle<GameObject> obj) =>{

var go = Addressables.InstantiateAsync(url,parent).Result;

}

2.Timeline ,Cinemline 使用教程


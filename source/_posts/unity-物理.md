---
title: unity-物理
date: 2021-04-19 12:09:27
tags: unity 物理

---

## Unity 碰撞器（Collider）、触发器（Trigger）、刚体（Rigidbody）之间的关系

物体之间要产生碰撞必须为GameObject添加碰撞器(Collider)和刚体(Rigidbody)，GameObject只有添加刚体的时候才会收到物理影响。碰撞器是物理组件的一部分，需要同刚体一起添加到GameObject才能触发碰撞事件。GameObject只添加刚体，没有碰撞体，则会穿过彼此。

<!-- more -->

#### 物体发生碰撞的必要条件:

​		2个物体都必须带有Collider，其中1个物体还必须带有Rigidbody.

#### 检测碰撞发生的方式有2种,一种是利用碰撞器，一种是利用触发器

​		碰撞器：GameObject 添加的Collider，

​		触发器：GameObject 的Collider isTrigger 打开.

当2个GameObject的Collider isTrigger都未选中的时候，为碰撞器的事件。具体表现为：碰撞之后带有刚体的物体会受物理影响产生撞飞的效果

​		OnCollisionEnter, OnCollisionStay, OnCollisionExit 

其中1个GameObject的Collider isTrigger 选中的时候，物理引擎会被忽略，为触发器事件。具体表现为：2个物体会互相穿过

​		OnTriggerEnter，OnTriggerStay, OnTriggerExit.


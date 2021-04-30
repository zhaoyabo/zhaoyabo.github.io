---
title: unity NavMeshAgent
date: 2021-04-30 12:44:52
tags:unity NavMeshAgent
---

**NavMeshAgent**属于寻路系统，它也带有一个圆柱体形的碰撞体。

<!--more-->

如果两个这样的对象相遇，就会产生推动效果。寻路过程的计算细节并不清楚，但根据测试，应该也是用物理系统去模拟了一些计算（之所以会和物理系统产生冲突，可能就是因为这个原因）。具体如何运用：如果你的角色要寻路，那么添加了NavMeshAgent后就不要再添加Rigidbody或CharacterController，如果要对另外一个动态对象产生碰撞，就为那个对象加上Navmesh Obstacle组件。如果不进行寻路操作，那么CharacterController和Rigidbody也不要混用。如果对象之间需要产生真实的推力效果，就用Rigidbody；否则，用CharacterController。如果真有复杂的混用情况，也可以在代码中根据情况，启用或禁用相应组件。不过建议不要这样做，因为一旦出了问题，你无法调试。要从设计上就避免这些复杂的情况。备注 ：用Navigation系统，有时需要判断是否达到了目的地，需要进行如下判断：



```
if (!navAgent.pathPending)    
｛    
    if (navAgent.remainingDistance <= navAgent.stoppingDistance)    
    ｛    
        if (!navAgent.hasPath || navAgent.velocity.sqrMagnitude == 0f)    
        ｛    
            //find path done!    
        ｝    
    ｝    
｝    
```



最后有一个地方自己栽了好久，要提醒一下。如下代码：



```
void Update () ｛  
        if (Vector3.Distance(transform.position, player.position) < 1.3f)  
        ｛  
            agent.Stop();  
            anim.SetBool("Move", false);  
        ｝  
        else  
        ｛  
            agent.ResetPath();  
            anim.SetBool("Move", true);  
            agent.SetDestination(player.position);  
            agent.Resume();  
        ｝  
    ｝  
```



当寻路物体与寻路目标的距离小于既定目标距离时，调用了stop方法停止寻路后，距离又大于既定距离了，这时寻路物体不会自动寻路，通过调用agent.ResetPath()和agent.Resume()方法都可以让寻路物体恢复寻路，但是agent.ResetPath()方法会使得当你的寻路物体过多的时候，代码控制的新产生的寻路物体的agent.SetDestination()函数失效，效果就是新产生寻路物体的物体不会走了，只有当角色与新产生的寻路物体考得足够近时其才会寻路，走远后又不会寻路了。
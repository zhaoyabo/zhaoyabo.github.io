---
title: Unity3D Quaternion
date: 2021-05-13 15:02:36
tags: Unity 
---

1、Angle函数

```
public static float Angle(Quaternion a, Quaternion b);  
```

计算两个旋转之间的夹角。与Vector3.Angle()作用是一样的

<!-- more -->
2、AngleAxis函数

```
public static Quaternion AngleAxis(float angle, Vector3 axis);  
```

将物体绕axis旋转angle度


3、Dot函数

```
public static float Dot(Quaternion a, Quaternion b);  
```

两个旋转之间的点乘，通过点积，我们其实是可以计算两个向量的夹角的，另外通过点积的计算我们可以简单粗略的判断当前物体是否朝向另外一个物体: 只需要计算当前物体的transform.forward向量与(otherObj.transform.position – transform.position)的点积即可，大于0则面对，否则则背对着。当然这个计算也会有一点误差，但大致够用。

 
4、Euler函数

```
public static Quaternion Euler(Vector3 euler);   
public static Quaternion Euler(float x, float y, float z);  
```

把旋转角度变成对应的Quaternion，返回一个先沿z轴旋转z角度，然后沿x轴旋转x角度，最后沿y轴旋转y角度的旋转


5、Inverse函数



public static Quaternion Inverse(Quaternion rotation);

返回反向的旋转



6、Lerp和LerpUnclamped函数

public static Quaternion Lerp(Quaternion a, Quaternion b, float t); 

根据t值在四元数a和b之间进行插值，并将结果规范化与Slerp效果差不多，效率比Slerp高但是如果from和to相差过大效果会不好，会返回一个标准化的Quaternion。t取值范围[0,1]  

public static Quaternion LerpUnclamped(Quaternion a, Quaternion b, float t);

通过t值from向to之间插值，并且规范化结果，t的取值不受限制



7、Slerp和SlerpUnclamped

```
public static Quaternion Slerp(Quaternion a, Quaternion b, float t);  
public static Quaternion SlerpUnclamped(Quaternion a, Quaternion b, float t);  
```

同上





8、FromToRotation函数

public static Quaternion FromToRotation(Vector3 fromDirection, Vector3 toDirection); 

生成一个四元数表示fromDirection到toDirection的旋转,跟SetFromToRotation差不多，区别是可以返回一个Quaternion。



9、LookRotation函数

public static Quaternion LookRotation(Vector3 forward);

public static Quaternion LookRotation(Vector3 forward, Vector3 upwards = Vector3.up);

建立一个旋转，使z轴朝向forward y轴朝向upwards（默认upwards为Vector3.up）

```
public Transform target;  
 void Update()  
 ｛  
     Vector3 relativePos = target.position - transform.position;  
     Quaternion rotation = Quaternion.LookRotation(relativePos);  
     transform.rotation = rotation;  
 ｝  
```


10、RotateTowards函数



public static Quaternion RotateTowards(Quaternion from, Quaternion to, float maxDegreesDelta);

从from旋转到to.与Slerp基本相同，但这个函数的角速度永远不会超过maxDegreesDelta。负的maxDegreesDelta值将使旋转远离to



11、SetFromToRotation函数

```
public void SetFromToRotation(Vector3 fromDirection, Vector3 toDirection);  
```

设置一个四元数表示fromDirection到toDirection的旋转

```
private Vector3 _from = Vector3.one;  
private Vector3 _to = new Vector3(100f, 200f, 100f);  
private Quaternion q;  
private Vector3 headUpDir;  
void Start()  
｛  
    q.SetFromToRotation(_from, _to);  
    transform.rotation = q;  
    headUpDir = transform.TransformDirection(Vector3.forward);  
｝  
把物体的fromDirection旋转到toDirection  
输入：a=Vector3(0,0,1); b=Vector3(0,1,0)//把z轴朝向y轴    
输出： q=(-0.7,0,0,0.7); headUpDir=(0,1,0)    
输入：a=Vector3(0,0,1); b=Vector3(1,0,0)//把z轴朝向x轴    
输出： q=(0,0.7,0,0.7); headUpDir=(1,0,0)    
输入：a=Vector3(0,1,0); b=Vector3(1,0,0)//把y轴朝向x轴    
输出： q=(0,0,-0.7,0.7); headUpDir=(0,0,1)            
```

12、SetLookRotation函数

```
public void SetLookRotation(Vector3 view);  
public void SetLookRotation(Vector3 view, Vector3 up = Vector3.up);  
```

设置一个四元数表示朝向为view上方向为up的旋转

```
public Transform obj1;  
public Transform obj2;  
Quaternion q;  
void Update()  
｛  
    q.SetLookRotation(obj1.position, obj2.position);  
    transform.rotation = q;  
｝  
类似于LookAt()方法，使物体1始终注视着物体2  
```


13、ToAngleAxis函数

```
public void ToAngleAxis(out float angle, out Vector3 axis);  
```

将四元数转换成一个角-轴表示的旋转

```
public float angle = 0.0F;  
public Vector3 axis = Vector3.zero;  
void Start()  
｛  
    transform.eulerAngles = new Vector3(0, 90, 0);  
    transform.rotation.ToAngleAxis(out angle, out axis);  
    print(angle + " " + axis);  
｝  
将物体的旋转角度返回到angles和axis里（物体的z轴和世界坐标z轴的夹角）    
例：    
输入：transform.localEulerAngles=(0,0,0);    
输出：angle=0, axis=(1,0,0);    
输入：transform.localEulerAngles=(0,90,0);    
输出：angle=90,axis=(0,1,0);    
输入：transform.localEulerAngles=(270,0,0);    
输出：angle=90,axis=(-1,0,0)    
```
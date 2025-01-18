---
up: "[[Unity-Godot Game Tools]]"
related: 
created: 2024-03-16
tags:
  - domain/3d
---

## FromToRotation

一个向量到另外一个向量的 旋转 

```c#
// 创建一个从一个方向到另一个方向的旋转四元数 
Quaternion fromToRotation = Quaternion.FromToRotation(Vector3.forward, Vector3.up); 
Debug.Log("FromToRotation: " + fromToRotation);

```

## LookRotation

配合物体 transform.rotation

```c#
public Transform target;

    void Update()
    {
        Vector3 relativePos = target.position - transform.position;

        // the second argument, upwards, defaults to Vector3.up
        Quaternion rotation = Quaternion.LookRotation(relativePos, Vector3.up);
        transform.rotation = rotation;
    }
```

## AngleAxis

围绕一个向量选择一定角度



```c#
Quaternion angleAxis = Quaternion.AngleAxis(90f, Vector3.up); Debug.Log("AngleAxis: " + angleAxis);


```

## Quarternion.Slerp

球形差值

```c#
Quaternion slerpQuat = Quaternion.Slerp(Quaternion.identity, Quaternion.AngleAxis(90f, Vector3.up), 0.5f); 
Debug.Log("Slerp: " + slerpQuat);
```


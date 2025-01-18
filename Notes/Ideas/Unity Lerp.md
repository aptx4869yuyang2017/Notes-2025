---
up:
  - "[[Unity-Godot Game Tools]]"
related: 
tags:
  - domain/3d
type: "[[Streaming]]"
created: 2024-03-02
finished: 2024-03-03
URLs:
  - https://www.youtube.com/watch?v=RNccTrsgO9g&t=24s
---
[The right way to Lerp in Unity - YouTube](https://www.youtube.com/watch?v=RNccTrsgO9g&t=24s)


## 普通 Lerp

计算差值

## Dynamic Easing

动态缓动（Dynamic Easing）是一种用于动画和过渡效果的技术，它可以根据目标属性的变化速度动态调整缓动函数，以实现更自然和流畅的动画效果。通常，缓动函数是一个用于控制动画速度变化的数学函数，例如线性缓动、加速缓动、减速缓动等。

在动态缓动中，缓动函数会根据目标属性的变化速度进行调整，以确保动画过程中的加速度和减速度更符合物体运动的真实感觉。这样可以避免动画在开始和结束时突然加速或减速，从而产生更自然的过渡效果
### Mathf.SmoothDamp

[Unity - Scripting API: Mathf.SmoothDamp](https://docs.unity3d.com/ScriptReference/Mathf.SmoothDamp.html)

需要考虑
- 当前速度
- 与目标的距离
所以经常用于相机跟随

![400](https://s1.vika.cn/space/2024/03/03/23797769403c4de4ba0f3346bbaa6b2a)
参数中的 duration 其实不是一个准确时间，是个大概时间

```c#
public class TestLerp : MonoBehaviour
{
    //public Transform target;
    private Vector3 target;
    float timeElapsed = 0;
    public float smoothTime = 0.9f;
    Vector3 velocity=Vector3.zero;

    private void Start()
    {
        StartCoroutine(ChangeTarget());
    }

    void Update()
    {
        transform.position = Vector3.SmoothDamp(transform.position, target, ref velocity, smoothTime);
    }

    IEnumerator ChangeTarget()
    {
        // 在每隔 smoothTime 时长，执行一次ChangeTarget方法
        while (true)
        {
            yield return new WaitForSeconds(smoothTime);
            ChangeTargetValue();
        }
    }

    void ChangeTargetValue()
    {
        float randomX = Random.Range(-20f, 20f);
        float randomZ = Random.Range(-20f, 20f);
        target = new Vector3(randomX, 0f, randomZ);
        Debug.Log("Target changed: " + randomX + " " + randomZ);
    }
}
```

### 增加 一个 Easing 函数提前处理 t

其实可以理解 没有处理的就是 t = t

![400](https://s1.vika.cn/space/2024/03/03/b4b754746b1a4dd68e82368b60d0a5b6)



## MoveTowards 可以保持速率稳定

![600](https://s1.vika.cn/space/2024/03/03/7d3db88c05c840bd947170b1756fca33)

[Unity - Scripting API: Mathf.MoveTowards](https://docs.unity3d.com/ScriptReference/Mathf.MoveTowards.html)

```c#
void Update()
    {
        transform.position = Vector3.MoveTowards(transform.position, target, speed * Time.deltaTime);
    }
```


## 其他数据类型 Lerp


- Color.Lerp
- 

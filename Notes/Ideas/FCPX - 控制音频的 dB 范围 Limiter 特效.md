---
up: 
related:
  - "[[FCPX - Ali Abdaal 教程]]"
created: 2025-01-25
tags:
  - domain/media
---
[31. 限制器和EQ均衡器\_哔哩哔哩\_bilibili](https://www.bilibili.com/video/BV1Jo4y1a7Ex?spm_id_from=333.788.player.switch&vd_source=6d4ef5f8b8b73d69ea854cb9321a50ac&p=31)

# 单片段测试

![image.png](https://s1.vika.cn/space/2025/01/25/ab74d31af0c740f39b6a4733834608bc)

**将视频的声音控制在特定的dB范围内**

- Effect 
	- Audio - Levels
		- Limiter

![image.png](https://s1.vika.cn/space/2025/01/25/1b66f2514d0d449384172f2c478529a2)

点击进入控制台

![image.png](https://s1.vika.cn/space/2025/01/25/b575774b04e14d0697815888defc3297)

- Gain 增益
	- 给音量增大多少 dB
- Release 
	- 参数的作用
		- **恢复速度**：Release 决定限制器在多快的时间内停止对超限信号的处理，使其回到正常电平。
		- **音质影响**：较短的 Release 时间能让音频快速恢复，但可能导致失真或音质变化；较长的 Release 时间则使恢复更平缓，保持音质自然，但可能延长处理时间。
	- 使用建议
		- **短 Release**：适用于需要快速响应的场景，如打击乐器。
		- **长 Release**：适用于需要平滑处理的场景，如人声或弦乐。
		- 人声或平滑音频**
	- **Release: 100ms - 300ms**
	    - 较慢的恢复速度，适合保持人声或乐器的自然动态。


# 多片段应用


- 批量选择片段：选中第一个之后 `Shift + 最后一个`
- `commond + shift + v` 粘贴属性
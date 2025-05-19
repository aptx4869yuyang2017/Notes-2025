---
up:
  - "[[Media 媒体运营 MOC]]"
related: 
created: 2025-02-05
tags:
  - domain/media
aliases: 
---


- 找到了 Whisper Auto Caption 的字幕重叠问题原来是帧率问题
	- 我目前计划所有素材工程 保持60帧设定，主要是受到录屏软件 只有60帧的限制
- 还是 Captions 比 Titles 香，还是尝试使用 Captions 吧
	- 用 **Whisper Transcription** 貌似没有帧率问题，字幕分割的更短
	- 工作流
		- 导出 mp3
		- Whisper 转译 SRT 字幕
		- FCPX - File - Import - Caption


![image.png](https://s1.vika.cn/space/2025/02/05/f4789e8fb6004e2394acca8b3bfb7aa7)


![image.png](https://s1.vika.cn/space/2025/02/05/b32b093a1b314435bdf05f070d861cf5)

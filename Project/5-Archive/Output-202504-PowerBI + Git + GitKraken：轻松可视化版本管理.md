---
up:
  - "[[输出Output Map]]"
related:
  - "[[PowerBI MOC]]"
created: 2025-02-14
tags:
  - domain/powerbi
---

# 参考教程

- [World Class Power BI SOURCE CONTROL: End-to-End!!! - YouTube](https://youtu.be/IIvMkvpluVY?si=YoZ7uQjeF-NcqdUp)
- [Title Unavailable \| Site Unreachable](https://www.youtube.com/watch?v=khDFh98bX-I)

文稿主要参考这篇
[Title Unavailable \| Site Unreachable](https://www.youtube.com/watch?v=PDI3k4G4Dpk&t=18s)

- [[PowerBI PBIP 相关更新]]

# 大纲

[Excalidraw ](https://excalidraw.com/#json=5Eq483QG2U2phXw4LWOQU,iKCwVeuwK2T1ZATQo2O_Pw)



# 备选封面



- [Lelouch Vi Britannia \| Danbooru](https://danbooru.donmai.us/posts?page=7&tags=Lelouch)
- https://gbf.wiki/Lelouch_Lamperouge#/media/File:Npc_zoom_3040219000_01.png
- https://64.media.tumblr.com/cbbc8d59665b3b25cf355d2976b0887a/tumblr_inline_o6k7c563EF1u4y9h4_500.jpg 这张皇帝白衣最帅

![image.png|241](https://s1.vika.cn/space/2025/02/13/b0276d2061704f79a023ec2e0ab0cb9c)
![导出02.png|292](https://s1.vika.cn/space/2025/02/17/c15e8c87211540db8d11c87e5bcce5b9)

![image.png|330](https://s1.vika.cn/space/2025/02/24/f3ea4f10f7d84e42a6c7ca39e64407a0)

![image.png|283](https://s1.vika.cn/space/2025/02/18/5d32ae29825d4a7babba9340a873b430)


# Intro

在这个视频中，我想向大家展示如何在开发 PowerBI 报告的时候进行使用 Git 来操作版本控制。我们将从
- Git 的基础介绍开始
- 之后分享不使用命令行来操作 Git 的方案
- 最后介绍如何使用 Git 管理 PowerBI 

---

具体如何使用 GitHub 管理PowerBI 以及如何 联动 GitHub 与 Microsoft Fabric 的内容 ，将在后续的视频中介绍，不想错过的观众可以先点个关注，视频更新后将会第一时间向您推送。



---

目录：
- PBIP 的




大家好，我是禹洋，欢迎点开这个视频。我立志每周都会上传新的视频，分享 BI 与 数据可视化的领域的技巧与最佳实践，感兴趣的朋友可以帮忙点个关注，方便收到后续更新。

使用Git进行版本控制本质上是一种 追踪代码更改的方式，特别是在软件开发过程中。你可以把它想象成在开发过程中为代码拍摄快照。它让开发者能够协作，共同处理相同的代码，追踪错误，并在需要时回滚更改。这是程序员之间的常见做法，尤其是在大型的多人协作的项目中。

然而，在BI领域中，这一功能长期以来一直缺失。原因在于，常规的BI类的工具的文件并不是常规的文本格式。比如 PowerBI 的 PBIX & Tableau 的 tbwx。这些都是二进制文件，我们如果使用文本编辑器中打开中类型的文件，并想更新某个度量或添加某个视觉对象，你无法从文本中精确定位到这些更改的位置。因此，如果你想对Power BI报告进行版本控制，过去你需要对整个项目文件进行版本控制，而不是仅仅针对更改的部分。


然而，PowerBI 在 2024年-6月 的更新版本中引入了
[Power BI enhanced report format (PBIR) in Power BI Desktop developer mode (Preview) \| Microsoft Power BI Blog \| Microsoft Power BI](https://powerbi.microsoft.com/en-us/blog/power-bi-enhanced-report-format-pbir-in-power-bi-desktop-developer-mode-preview/)


# BI 软件的版本管理


- 常规的版本管理 Server 端
	- Tableau
	- QuickBI
- 本地的文件管理
	- Version XXX
	- SVN 二进制文件管理确实更好

![image.png|414](https://s1.vika.cn/space/2025/02/13/ae4a696cbf014d31832671a3988ed165)


PowerBI 想走出一条完全不一样的道路
- 尝试把 软件工程领域的版本控制




# VS Code 插件

![image.png|308](https://s1.vika.cn/space/2025/02/13/52d653556eb94f6398c7d9771fedfe78)



# 本地的版本管理 协作


- 简单案例来展示 Git 版本控制方式
	- 版本回溯
	- 模拟协作
- PowerBI 的版本控制
	- 版本回溯
	- 模拟协作
	- 删除




# 发布与 Github 集成





# 文稿



这是一个想要带你告别手工管理Power BI版本的视频。我会用草履虫都能听懂的方式 给您介绍 Git 是如何管理版本变化的，看看它和手工管理有什么区别。我们会用简单的图形化工具GitKraken，通过操作我们  熟悉的txt文件，演示Git最最基础 也是最最常用的两个功能：**版本创建**和**版本回滚**。

最后我们还是会回归到Power BI的主题，看看最新的Power BI项目格式是如何组织文件，完美适配Git这个版本管理工具的。

为了方便观看，我会把章节时间点放在置顶评论区，欢迎跳转到感兴趣的部分。视频开始前，别忘了**一键三连**，也欢迎关注本频道，希望能和您一起共同成长！


我们这次视频的演示就这么多，刚开始使用 Git 来管理 PowerBI 的版本， 这些基础操作足够简单，也足够用了。后续我们还会介绍 如何使用 Git 进行多人协作，以及如何 将 我们本地的文件 发布到服务端，感兴趣的朋友可以先点个关注，方便后续第一时间收到更新。


以上就是本期视频的所有内容，如果感觉本对您有帮助的话，欢迎点赞投币与分享。当然更欢迎您的留言交流，让我们下个视频再见。
---
up:
  - "[[输出Output Map]]"
related: 
created: 2025-01-19
---

[【像程序员一样使用PowerBI】使用TMDL批量编辑代码](https://www.bilibili.com/video/BV1r5w6ekEG3/?spm_id_from=333.999.0.0&vd_source=6d4ef5f8b8b73d69ea854cb9321a50ac)
#output/video/done 



25年1月 PowerBI 新发布TMDL预览功能。 在我眼里可以说是近几年我最喜欢的一个功能了，因为这个功能说实话能够非常大的提升我们日常工作的效率。

使用BI工具的用户可以说半个程序员啊，本质上也是在用逻辑和代码处理问题。市面大部分的BI工具都太原始了，没怎么认真从提升开发者效率方面思考过问题，就以 tableau 为例，我根本就不可能出一期相同主题的视频，据我所知 tableau 还没有类似功能或者插件能够实现批量化处理字段/度量值的功能。 可能我觉得工作中最痛苦的事情就是把写过10遍以上的逻辑，在新报表中再写一遍。 

这次我们就结合25年1月 PowerBI 新发布预览功能。 表格模型 定义语言 视图，后面简称 TMDL 视图功能，看一下 PowerBI 是怎么提升开发者的工作效率的。




# 批量迁移度量值





# 创建计算组

```
createOrReplace

    table 'Time Intelligence'      

        calculationGroup
            precedence: 1

            calculationItem YTD =
                    CALCULATE (
                        SELECTEDMEASURE (),
                        DATESYTD ( 'Calendar'[Date] )
                    )

            calculationItem QTD =
                    CALCULATE (
                        SELECTEDMEASURE (),
                        DATESQTD ( 'Calendar'[Date] )
                    )

            calculationItem MTD =
                    CALCULATE (
                        SELECTEDMEASURE (),
                        DATESMTD ( 'Calendar'[Date] )
                    )

            calculationItem Current = SELECTEDMEASURE()

        column 'Show as'
            dataType: string                        
            sourceColumn: Name
            sortByColumn: Ordinal          

        column Ordinal
            dataType: int64
            formatString: 0        
            summarizeBy: none
            sourceColumn: Ordinal
```


# 总结


我们做个简单的总结，我只是演示了两个非常简单的场景，我们就已经见识到了，TMDL视图的效率提升效果是多么惊人！

实际上这些功能早就是可以利用外部工具来实现的功能。但是 PowerBI 依旧在认真集成这些功能，而且这个其实功能并不是一个简单的功能提升，而是整个 Powerbi 宏大规划中的一个小环节，有机会我们讨论讨论我是怎么理解 PowerBI 的整体产品规划的，当然这个【像程序一样使用 Powerbi】将会是一个系列视频，可以帮忙点个关注，方便收到后续更新，也欢迎私信交流您的使用体验。


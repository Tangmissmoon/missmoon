---
title: 百本技术佬·第一本《Effective Python》
description: 种一棵树，最好的时间是十年前，其次是现在。
categories:
 - 记录
tags:
- 心得
- 笔记
- 阅读
- Python
---

> 刻意练习，每日精进. 找出闪光点.

<!-- more begin-out-is-great -->

📘基本信息
    书名：《Effective Python》编写高质量Python代码的90个有效方法
    
    作者：Brett Slatkin 爱飞翔译第2版
    类别：#编程技术 
    阅读时间：工作日每天晚上一个知识点
    重要信息：
    ｜ Python提升类的书籍，管理编程习惯
    相关阅读：
🔧阅读方式
    理解会用的，阅读细节，加深印象
    不太会的，略知一二，工匠手写笔记+手工练习（代码）

12. 特殊步进的切片方式：somelist[start:end:stride]，-1反转的用法，对bytes类型的字符串、Unicode类型的字符串都可以，不支持UTF-8的字节数据，尽量不要同时写满标记的三个参数，难以理解，如有需要，使用itertools内置模块里的islice方法

13. 用星号的unpacking操作捕获元素：one,two,*three=[1,2,3,4]

14. 用`sort`方法的key参数来表示复杂的排序逻辑
```python
Class Tool:
    def __init__(self, name, weight):
        self.name = name
        self.weight = weight
    
    def __repr__(self):
        return f"Tool({self.name!r}, {self.weight})"
# Traceback        
tools.sort()
power_tolls = [
    Tool('drill', 4),
    Tool('circular saw', 5),
    Tool('jackhammer', 40),
    Tool('sander', 4),
]
power_tools.sort(key=lambda x:(-x.weight, x.name))
power_tools.sort(key=lambda x:(-x.weight, x.name) reverse=True) # error
```
15. 第15条，不要过分依赖给字典添加条目时所用的顺序，`3.5`之前的版本，顺序不定，这跟字典类型以前跟哈希表实现有关，内置的`hash`函数和随机种子数来确定，因此`dict`相关的方法都不能保证固定的顺序，而`3.6`开始，字典会保留添加时所使用的顺序。

>内置的`Collections`模块提供的OrderedDict，行为和3.7版本后的标准dict很像，但性能有较到区别。实现LRU缓存，（least-recently-used缓存）OrderedDict比dict类型更合适。

>补充，如果不想把这种与标准字典相似的类型当作标准字典处理的话，可以考虑三种办法：
> - 不依赖插入时的顺序编码；
> - 在程序运行时，明确判断字典类型，可以使用`instance`方法；
> - 给代码添加类型注解并作静态分析。

>内置的`Collections`模块提供的OrderedDict，行为和3.7版本后的标准dict很像，但性能有较到区别。实现LRU缓存，（least-recently-used缓存）OrderedDict比dict类型更合适。


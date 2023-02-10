---
title: 如何赢得团队其他成员的尊重？
categories:
 - 心得
tags: 
 - 团队经验
---

# 念起

最近好像是水逆，有一首歌叫遇见你的时候所有星星都掉落下来，描述最近的情况是，最近遇到的东西都在坏掉，是磁场干扰的因素吗？比如，食堂干饭，刷卡机子坏掉了；喝水，饮水机坏掉了；手机，卡顿的时候强制关机发出奇怪的蜂鸣声；窗头的窗帘架子掉下来一半，吹风机从桌子上掉下来莫名打开了开关，自顾自开启了工作，再说下去就不和谐了。

# 工作总结

 开会-开会-定位问题-拆需求，平平无奇的一天。

# 今日专业阅读

《effective python》的第17条，用`defaultdict` 处理内部状态中缺失的元素，不使用`setdefault`，比如：
```python

visits = {
    'Mexico': {'Tulum', 'Puerto Vallarta'},
    'Japan': {'Hakone'},
}
visits.setdefault('France', set()).add('Arles') # short use

if (japan := visits.get('Japan')) is None : # Long use
    visits['Japan'] = japan = set()
japan.add('Kyoto')
print(visits)
```
展开讲了`setdefault` 方案 vs `defaultdict` 的区别，`python` 内置的 `collections` 模块提供了`defaultdict`类，它能够实现**键缺失的情况下，自动添加该键及键所对应的默认值**，区别 `setdefault` 方案的是，不再重复分配 `set`。
- 如果字典需要添加任意键，考虑使用内置的`collections`模块中的`defaultdict`实例来解决问题；
- 收到传入的字典键名较随意，没有用 `defauldict` 初始化，应该考虑用 `get` 完成访问，某些情况下也可以访问 `setdefault`。
  

## 灵感文献

-  github中文社区 https://www.githubs.cn/?ref=nicelinks.site

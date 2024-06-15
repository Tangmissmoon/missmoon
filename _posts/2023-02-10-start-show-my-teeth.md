---
title: 程序员每天在干什么？
categories:
 - 心得
tags: 
 - 团队经验
---

<iframe frameborder="no" border="0" marginwidth="0" marginheight="0" width=325 height=450 src="//music.163.com/outchain/player?type=0&id=5355712960&auto=0&height=430"></iframe>

# 念起

赵紫骅的《你还好吗》前奏是一段微信来电的音效，戴着耳机干活的我疯狂翻手机准备接电话，才发现上当的不只我一个，热评第一也是。昨天分完需求，今天是疯狂battle的一天。推进需求的可实现性，对接同事的排期，以及一些根据经验，判断可能存在坑的地方。

## 大部分程序员的工作流程

1. 整理大块功能，做好排期，按代码项目/功能块划分 ｜ **工作一张表**+排期文档，搭架子
2. 确认对应功能对接同事的技术可行性、排期、接口开发 ｜ 完善表+**沟通**，填钢筋
3. 根据功能出接口、数据库变更、方案，改动范围，成型技术方案、接口 ｜ **技术方案**+接口文档，成模型
4. 动手开发，确认对接同事的ddl，并在那之前给出 ｜ **coding**+接口文档，填砖瓦
5. 关注ddl，分配工作，阶段性同步+节点沟通，站在验收标准复查工作 ｜ **coding+mr**+联调+沟通，逐渐成型
6. 

# 今日专业阅读

由于今天是周五，需要学习两条。

《effective python》的第18条是，结合`__missing__` 构造依赖键的默认值，前面两条分别介绍了，内置`dict` 类型的两种方法，少数`setdefault` 方法用来处理缺失键，`defaultdict` 则是大多数情况会做的选择，18条介绍第三种方式，现引入一段代码：
```python
# 管理社交网络账号的图片：字典来关联图片的路径名和相关的文件句柄
pictures = {}
path = 'profile_1234.png'

if (handle := pictures.get(path)) is None:
    try:
        handle = open(path , 'a+b')
    except OSError:
        print(r'Failed to open path {path}')
        raise
else:
    pictures[path] = handle

handle.seek(0)
image_data = handle.read()
```
假设用`setdefault` 方法来实现，`get` 替换成`setdefault` ：
```python
# 关键步骤换一下
try:
    handle = pictures.setdefault(path, open(path , 'a+b'))
except OSError:
    print(r'Failed to open path {path}')
    raise
else:   # 还记得这个else的用法是，没有走异常来执行的语句，见第9和65条
    handle.seek(0)
    image_data = handle.read()
```
这样做的好处是代码变少了，阅读到`handle`这一行就能很快理解，这是在绑定路径和图片，制作文件的句柄，但有问题的是：无论路径名是否在字典里，`defaultdict` 的第二个参数 `open` 方法仍然会调用一次，就可能导致重复生成已经存在的文件句柄，引发冲突，如果`try` 代码块捕获到异常，难以定位到具体是哪个内方法引起的，一行要素过多，两次调用的报错，只会提示这一行代码。

于是，第三种方案来了，`defaultdict` 开始大展身手，
```python
# 同样是替换绑定的代码，增加一个辅助函数
from collections import default

def open_picture(profile_path):
    try:
    return open(profile_path , 'a+b')
except OSError:
    print(r'Failed to open path {path}')
    raise

pictures = defaultdict(open_picture)
handle = picture[path]
handle.seek(0)
image_data = handle.read()
```
运行以后，同样出错了，原来是`defaultdict` 函数，不支持输入带参数的方法，来作为参数，同样失败了，引入今天需要掌握的一种用法，我还没用过，也没碰见过：
```python
# 注意 open_picture方法保留了，同时，class的类型
class Pictures(dict):
    def __missing__(self, key):
        value = open_picture(key)
        self[key] = value
        return value

pictures = Pictures()
handle = pictures[path]
handle.seek(0)
image_data = handle.read()
```
`Python`内置的这种解决方案，继承了`dict`类型并实现`__missing__` 方法，字典中不存在的键就会执行这个方法，`pictures[path]` 字典访问时，字典里没有`path` 值就会调用`__missing__` 方法。
- 创建默认值需要较大开销 or 引起异常，不建议考虑`setdaultdict` 方法来解决问题；
- 方法作为参数传入`defauldict` 时，参数排不上用场，不支持；
- 默认值跟键名有关，可以定义dict子类并实现`__missing__` 方法。
  
噢，关于 seek https://www.tutorialspoint.com/python/file_seek.htm

## 灵感文献

-  github中文社区 https://www.ezindie.com/?ref=nicelinks.site

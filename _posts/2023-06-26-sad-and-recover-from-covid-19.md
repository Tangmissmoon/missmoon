---
title: 19-23还是🐏了，首阳后身体不如之前
categories:
 - 日结
tags: 
 - mac
 - 随笔
---
 
<iframe frameborder="no" border="0" marginwidth="0" marginheight="0" width=330 height=450 src="//music.163.com/outchain/player?type=0&id=8374925988&auto=1&height=430"></iframe>

## 起因
 
从武汉毕业后，跟新冠擦肩而过几次，都没有中招，在一个没有出行的周末后，突然中招了，恰逢工作2周年，中午终于请假了，加上1天半+双休的调养，周一又回到了工位，开始奋斗。但这次阳康后，身体明显不如之前，工作几个小时后，明显疲惫头晕。病毒对于人体的攻击强度还是要比预期的高。

回到久违的《Effective Python》的学习：
第25条，用只能关键字和只能按位置传入的参数来设计清晰的参数列表，`/`和`*`出现在参数列表里，分别代表左侧按照位置指定的参数，而星号右侧参数只能是按照关键字形式指定的参数，
对应的：
- Keyword-only argument 是一种只能通过关键字指定而不能通过位置指定的参数，位于*符号的右侧；
- Positional-only argument 是一种参数，不允许调用者通过关键字来指定，必须按照位置传递，位于/符号的左侧；
- 位于两者之间的参数，可以按照位置指定，也可以用关键字来指定。

## tips
最近在干爬虫，交付多章节多页面内容时，共用同一id的信息，使用特殊标识，在每段长文本的前面增加 “page##@@@” 的固定字符，之后再使用正则读取page，按顺序拼接起来，这种办法解决了，固定顺序拼接长文，检查遗漏的问题。
```bash
def find_missing_number(nums, max_page=None):
    # 将输入的数组转换成集合
    num_set = set(nums)

    max_page = max_page if max_page else list(nums)[-1]
    # 生成1-9的数字序列
    full_set = set(range(1, max_page))

    # 使用集合差集操作，得到缺失的数字
    missing_set = full_set - num_set
    missing_nums = sorted(list(missing_set))
    print("丢失的数字", missing_nums)
    return missing_nums
```

## 随笔
亲戚家的小朋友，让帮忙选下志愿，问计算机可不可以。问清楚毕业想做什么，小朋友回答想去国企；
于是，我得出结论计算机、电气、电子都可以，最理想的还是口腔医学，这是当初家人想让我去，没去，现在又推荐给新的人。
师公医，相对来说，社会地位高，前期积累，后期享福。经验和社会资源都足以，到退休，当时不懂，现在还是觉得诚不我欺。
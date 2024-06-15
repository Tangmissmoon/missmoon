---
title: Python多重继承以及方法解析顺序
categories:
 - 编程
tags: 
 - Python
 - 继承
---

<iframe frameborder="no" border="0" marginwidth="0" marginheight="0" width=330 height=450 src="//music.163.com/outchain/player?type=0&id=2105681544&auto=1&height=430"></iframe>

# 念起

今天高速写码四五个小时了，脑力略微不太够，仅学两个建议就撤退。处理继承问题，Tornado handler 方法复用。


# 今日专业阅读

继续《Effective Python》的学习： 

第20条：遇到意外情况时，应该抛出异常，而不是`None`，`utility fuction` 编写方法时，有时会返回`None` ，处理异常情况，应当选择对应的`Exception` 类的子类，而不是直接返回`None`，把执行方法出的异常保留在方法定义里，文中举了一个除数的例子：
```python
# 计算两数相除的辅助函数
def careful_divide(a, b):
    try:
        return a / b;
    except ZeroDivisionError:
        raise ValueError('Invalid inputs')

# 调用时，放入异常处理结构
x, y = 5, 2
try:
    result = careful_divide(x, y)
except ValueError:
    print('Ivalid inputs')
else:
    # print(f'Result is {result}')
    print('Result is%.1f' % result)
```
当然还有一种方法，就是限定返回值为`float` 类型，增加类型注解，而`Python` 采用的动态类型和静态类型相搭配的`gradual`类型系统，不能在函数的接口上指定函数可能抛出哪些异常，有些编程语言支持这种受检异常(`checked exception`)。可以在注释文档里，增补这部分说明：
```python
# 计算两数相除的辅助函数
def careful_divide(a, b):
    """Divides a by b.

    Raises:
        ValueError: When the inputs cannot be divided.
    """
    try:
        return a / b;
    except ZeroDivisionError:
        raise ValueError('Invalid inputs')
```
今天的要点就是：返回`None`来表示特殊情况，容易出错，无法区分开0和空白字符串之类的，因为用`if` 判断结果，这三类会得到一致的结果：`false`。

第21条：了解如何在闭包里面使用外围作用域中的变量。闭包(`closure`)的用法，之前掌握了，但不够熟悉，一般不会主动在项目中用到，提供了一个场景，如果需要给列表元素排序，而且需要置顶其中的某些元素，比如关键消息、特殊事件的靠前。

一种方案，辅助函数通过`key` 参数传给列表的`sort` 方法，排序方法根据辅助函数所返回的值来决定元素在列表中的先后顺序，辅助函数做的工作就是，确认当前元素是否需要置顶，需要，就返回0，直接排在非重要元素前面，比如：
```python
def sort_priority(values, group):
    def helper(x):
        if x in group:
            return (0, x)
        return (1, x)
    values.sort(key=helper)
```
方法可以实现像参数一样传递的原因是，函数在`Python` 里时头等对象，引用、赋给变量，当成参数传给其他函数，或者进行比较等，闭包函数也是一种函数，所以通常也可以直接传递。

`Python` 可以比较序列，包括元祖，它的规则是，从前往后一个一个位置比，直到得出结论。
引入一个变量的作用域(`scope`)的问题，引用变量时，解析（`resolve` ）方向是：

1.  当前函数的作用域；
2. 外围作用域，包含当前函数的其他函数对应的作用域；
3. 包含当前代码的模块对应作用域，通常也叫全局作用域，`global scope`；
4. 内置作用域（`build-in scope`， 一些内置方法的作用域）

通常在两个作用域引用同名的变量，容易引起作用域bug，是一种保护机制，防止函数中局部变量来污染外围模块，保证全局作用域的安全。那么如果非要跨域使用怎么办？

比如在闭包里的数据，给外面的变量，可以使用`nonlocal` 关键字，加一句`nonlocal 变量X`， 就可以去闭包外围操作了，即使这样，还是不能侵入模块级别的作用域，原因和上面一样，其他代码仍需要受到保护。

还有一种语句，`global`，如果需要放到模块作用域的话，使用这个。

## 灵感网站

- 新闻渠道，保持好奇心 https://medium.com/
- 产品的2022年64条建议 https://uxdesign.cc/a-product-managers-64-insights-from-2022-22e3bd78b8c9

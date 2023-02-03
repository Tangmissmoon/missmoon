---
title: 怎样参加到开源项目中去
categories:
 - 技能
 - 读帖心得
tags: 
 - 术之道
 - 个人发展
 - 输出
 - 吸型大法
---

# 前因

逛v2ex时候发现技术很关心的的一个问题：“**如何参与到开源项目中去？**”
下面有个各路神仙给出答案：

# 后果

关注+吸收+实践
 
## 具体操作

找到`daemon.json`文件，在大括号里添加

```json
"registry-mirrors": [
"https://registry.docker-cn.com"
],
```
因为我用的是colima，替代docker，所以主机上这个文件在colima下有一份，在`vim ~/.colima-docker/docker/daemon.json`，设置后没有解决问题，再次尝试后解决`vim ~/.colima/docker/daemon.json`，两个位置都试试。

[docker-cmd](https://docs.docker.com/engine/reference/commandline/dockerd/)
 
{% highlight ruby %}
def foo
  puts 'foo'
end
{% endhighlight %}

{% highlight ruby linenos %}
def foo
  puts 'foo'
end
{% endhighlight %}


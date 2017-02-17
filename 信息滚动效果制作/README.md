# 信息滚动效果制作

内容来自[信息滚动效果制作](http://www.imooc.com/learn/17)

## `marquee`标签实现信息滚动 

需要注意的是`marquee`标签在HTML5中以被废弃

`marquee`标签知识点

1.behavior滚动的方式

+ alternate:表示在两端之间来回滚动
+ scroll:表示由一端滚动到另一端，会重复
+ slide:表示由一端滚动到另一端，不会重复

2.direction滚动的方式down,up,left,right

3.loop滚动的次数(当loop=-1表示一直滚动下去，默认为-1)

4.scrollamount设定活动字幕的滚动速度

5.scolldelay设定活动字幕滚动两次之间的延迟时间

`marquee`标签`this.stop()`当前对象停止；`this.start()`当前对象开始运动。


## JS实现

### 无缝滚动原理

相当于再clone一个内容区域，两个区域交替滚动

![]()






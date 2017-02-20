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

### 无缝滚动

相当于再clone一个内容区域，两个区域交替滚动

![无缝滚动原理](https://github.com/windzencoder/JavaScript/blob/master/%E4%BF%A1%E6%81%AF%E6%BB%9A%E5%8A%A8%E6%95%88%E6%9E%9C%E5%88%B6%E4%BD%9C/images/principle.png)


javascript代码如下：

```
<script type="text/javascript">
    var area = document.getElementById('moocBox');
    var con1 = document.getElementById('con1');
    var con2 = document.getElementById('con2');
    var speed = 50;
    area.scrollTop = 0;
    //克隆内容
    con2.innerHTML = con1.innerHTML;
    function scrollUp() {
        if (area.scrollTop >= con1.scrollHeight) {
            area.scrollTop = 0;
        } else {
            area.scrollTop++;
        }
    }
    var myScroll = setInterval("scrollUp()", speed);
    area.onmouseover = function () {
        clearInterval(myScroll);
    }
    area.onmouseout = function () {
        myScroll = setInterval("scrollUp()", speed);
    }
</script>

```

效果如下：

![效果](https://github.com/windzencoder/JavaScript/blob/master/%E4%BF%A1%E6%81%AF%E6%BB%9A%E5%8A%A8%E6%95%88%E6%9E%9C%E5%88%B6%E4%BD%9C/images/result_01.gif)

### 间歇性滚动
 
就是滚动一下，停止一下。滚动一行或者多行
 
效果如下

![效果](https://github.com/windzencoder/JavaScript/blob/master/%E4%BF%A1%E6%81%AF%E6%BB%9A%E5%8A%A8%E6%95%88%E6%9E%9C%E5%88%B6%E4%BD%9C/images/result_02.gif)































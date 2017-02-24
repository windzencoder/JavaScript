# 图片展示特效

内容来自于[图片展示特效](http://www.imooc.com/learn/31)

## 图片展示上移效果

主要是添加鼠标移入和移出事件，改变top的值。具体的布局参见代码

js代码如下：

```
function showDetail(){
    var Div = document.getElementById('picList').getElementsByTagName('div');
	var divHeight = 160;
	for(var i =0 ;i<Div.length;i++){
		Div[i].onmouseover = showMeg;
		Div[i].onmouseout = hideMeg;
		}
	function showMeg(){
		this.getElementsByTagName('a')[0].style.top = 0;
		}
	function hideMeg(){
		this.getElementsByTagName('a')[0].style.top = divHeight+'px';
		}
}
```

效果如下：

## 图片侧位展示效果

这个... 效果一般

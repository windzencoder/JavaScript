# 固定边栏滚动

内容来自[固定边栏滚动特效](http://www.imooc.com/learn/52)

效果如下：

![result](https://github.com/windzencoder/JavaScript/blob/master/%E5%9B%BA%E5%AE%9A%E8%BE%B9%E6%A0%8F%E6%BB%9A%E5%8A%A8%E7%89%B9%E6%95%88/images/result.gif)

关键实现点：

1.CSS position fixed

当滚动左侧内容时，右侧的内容并不会随着滚动而滚动

2.监听window上的滚动事件

3.设置fixed条件判断

滚动高度+屏幕高度>边栏高度

**jQuery实现**

```
			var jWindow = $(window);
			//滚动事件
			jWindow.scroll(function () {
				//滚动的距离
				var scrollHeight = jWindow.scrollTop();
				//屏幕的高度
				var screenHeight = jWindow.height();
				//右侧边栏的高度
				var sideHeight = $('#J_BdSide').height();
				if(screenHeight+scrollHeight>sideHeight){
					$('#J_BdSide').css({
						'position':'fixed',
						'top':-(sideHeight-screenHeight),
						'right':0
					});
				} else {
					$('#J_BdSide').css({
						'position':'static'
					});
				}
			});

			window.onload = function() {
				//触发滚动事件
				jWindow.trigger('scroll');
			}

			jWindow.resize(function () {
				//触发滚动事件
				jWindow.trigger('scroll');
			})
```

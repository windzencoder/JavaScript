# 弹出层效果

内容来自[弹出层效果](http://www.imooc.com/learn/58)

效果如下![效果图](https://github.com/windzencoder/JavaScript/blob/master/%E5%BC%B9%E5%87%BA%E5%B1%82%E6%95%88%E6%9E%9C/img/result.png)

主要的知识点：
1.获取页面的高度和宽度

```
  var sWidth = document.body.scrollWidth;
  var sHeight = document.body.scrollHeight;
```

2.获取可见区域的高度和宽度


```
  var wHeight = document.documentElement.clientHeight;
```

3.获取元素的高度和宽度


```
  var dHeight = oLogin.offsetHeight;
  var dWidth = oLogin.offsetWidth;
```

4.创建元素和拼接元素和移出元素

```
var oMask = document.createElement("div");
document.body.appendChild(oMask);
document.body.removeChild(oLogin);
```


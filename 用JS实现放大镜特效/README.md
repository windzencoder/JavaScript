# 用JS实现放大镜特效

内容来自[用JS实现放大镜特效](http://www.imooc.com/learn/32)

**原理分析**

关键原理：鼠标在小图片上移动时，通过捕捉鼠标在小图片上的位置，定位大图片的相应位置。

当鼠标移动到图片上时，会出现一个半透明的区域，相当于是放大镜，显示要展示的范围，然后在右侧显示放大的图片

![原理1](https://github.com/windzencoder/JavaScript/blob/master/%E7%94%A8JS%E5%AE%9E%E7%8E%B0%E6%94%BE%E5%A4%A7%E9%95%9C%E7%89%B9%E6%95%88/images/principle_1.png)

当鼠标移动的时候，放大镜也会跟着移动，此时放大的图片也会跟随着移动，要注意的是，此时的大图片移动的方向是反的。

![原理2](https://github.com/windzencoder/JavaScript/blob/master/%E7%94%A8JS%E5%AE%9E%E7%8E%B0%E6%94%BE%E5%A4%A7%E9%95%9C%E7%89%B9%E6%95%88/images/principle_2.png)

**技术点**

所需要的鼠标事件：

+ onmouseover:会在鼠标指针移动到指定的对象上时发生

+ onmouseout:会在鼠标指针移出指定的对象时发生

+ onmousemove:会在鼠标指针移动时发生


定位相关

![定位](https://github.com/windzencoder/JavaScript/blob/master/%E7%94%A8JS%E5%AE%9E%E7%8E%B0%E6%94%BE%E5%A4%A7%E9%95%9C%E7%89%B9%E6%95%88/images/position.png)

**offsetLeft与style.left对比**

1.`style.left`返回的是字符串，如30px，`offsetLeft`返回的是数值30

2.`style.left`是可读写的，`offsetLeft`是只读的，所以要改变`div`的位置，只能修改`style.left`

3.`style.left`的值需要事先定义，否则取到的值为空。

主要JS代码如下：

```
    <script>
        
        window.onload = function () {
            var objDemo = document.getElementById("demo");
            var objSmallBox = document.getElementById("small-box");
            var objMark = document.getElementById("mark");
            var objFloatBox = document.getElementById("float-box");
            var objBigBox = document.getElementById("big-box");
            var objBigBoxImage = objBigBox.getElementsByTagName("img")[0];

            objMark.onmouseover = function () {
                objFloatBox.style.display = 'block';
                objBigBox.style.display = 'block';
            }

            objMark.onmouseout = function () {
                objFloatBox.style.display = 'none';
                objBigBox.style.display = 'none';
            }

            objMark.onmousemove = function (ev) {
                //兼容ie
                var _event = ev || window.event;
                var left = _event.clientX - objDemo.offsetLeft
                        - objSmallBox.offsetLeft - objFloatBox.offsetWidth / 2;
                var top = _event.clientY - objDemo.offsetTop - objSmallBox.offsetTop
                        - objFloatBox.offsetHeight / 2;

                if(left < 0){
                    left = 0;
                } else if(left > (objMark.offsetWidth - objFloatBox.offsetWidth)){
                    left = objMark.offsetWidth - objFloatBox.offsetWidth;
                }

                if(top < 0){
                    top = 0;
                }else if(top > (objMark.offsetHeight - objFloatBox.offsetHeight)) {
                    top = objMark.offsetHeight - objFloatBox.offsetHeight;
                }

                objFloatBox.style.left = left + 'px';
                objFloatBox.style.top = top + 'px';

                var percentX = left / (objMark.offsetWidth-objFloatBox.offsetWidth);
                var percentY = top / (objMark.offsetHeight-objFloatBox.offsetHeight);

                objBigBoxImage.style.left = -percentX * (objBigBoxImage.offsetWidth - objBigBox.offsetWidth)
                                        + 'px';
                objBigBoxImage.style.top = -percentY * (objBigBoxImage.offsetHeight - objBigBox.offsetHeight)
                        + 'px';

            }
        }
        
    </script>
```

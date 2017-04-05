# Tooltip浮动提示框效果

内容来自[Tooltip浮动提示框效果](http://www.imooc.com/learn/120)

## 特效分析

**四个关键点**：

**显示**：鼠标移动到ToolTip超链接上时，ToolTip提示框可以显示出来

**隐藏**：鼠标移开时，ToolTip提示框自动隐藏

**定位**：ToolTip提示框的位置需要根据ToolTip超链接的位置来设置

**可配置**：ToolTip提示框可以根据参数不同，改变尺寸和显示内容


**技术点**：

1.绝对定位：position: absolute

2.js创建dom：createElement与appendChild

3.鼠标事件：mouseenter与mouseleave setTimeout和clearTimeout

对于mouseenter与mouseover的区别，请参考[mouseenter 与 mouseover 的不同](http://www.w3school.com.cn/tiy/t.asp?f=jquery_event_mouseenter_mouseover)

>不论鼠标指针穿过被选元素或其子元素，都会触发 mouseover 事件。
只有在鼠标指针穿过被选元素时，才会触发 mouseenter 事件。


对`offsetLeft`和`offsetTop`的理解，请参考[CSS专题（二）：元素大小与位置offsetLeft offsetTop offsetWidth offsetHeight clientWidth clientHeight scrollWidth scrollHeight scrollLeft scrollTop](http://www.cnblogs.com/fangjins/archive/2012/08/02/2619835.html)


主要代码如下：

效果如下：

![效果](https://github.com/windzencoder/JavaScript/blob/master/Tooltip%E6%B5%AE%E5%8A%A8%E6%8F%90%E7%A4%BA%E6%A1%86%E6%95%88%E6%9E%9C%20/images/result.png)


```
    //优化事件绑定
    function addEvent(element, event, callbackFunction) {
        if(element.addEventListener) {
            element.addEventListener(event, callbackFunction, false);
        } else if (element.attachEvent){
            element.attachEvent('on' + event, callbackFunction);
        }
    }


    var toolTipBoxClass = 'tooltip-box';

    //是否为IE浏览器
    var isIE = navigator.userAgent.indexOf("MSIE") > -1;

    //优化getElementById方法
    var getEL = function (id) {
        return document.getElementById(id);
    }
    var demo = getEL("demo");

    //obj表示超链接元素 id提示框id，html提示框中的内容
    function showToolTip(obj, id, html, width, height) {
        if(getEL(id) == null) {
            //创建
            var toolTipBox;
            toolTipBox = document.createElement("div");
            toolTipBox.className = toolTipBoxClass;
            toolTipBox.id = id;
            toolTipBox.innerHTML = html;
            obj.appendChild(toolTipBox);

            toolTipBox.style.width = width ? width + 'px' : "auto";
            toolTipBox.style.height = height ? height + 'px' : "auto";

            if(!width && isIE){
                toolTipBox.style.width = toolTipBox.offsetWidth;
            }

            toolTipBox.style.position = "absolute";
            toolTipBox.style.display = "block";

            var left = obj.offsetLeft;
            var top = obj.offsetTop + 20;

            //left 在屏幕较小的时候 不让ToolTip提示框超出浏览器
            if(left+toolTipBox.offsetWidth>document.body.clientWidth){
                var demoLeft = demo.offsetLeft;
                left = document.body.clientWidth-toolTipBox.offsetWidth-demoLeft;
                if(left<0) {
                    left = 0;
                }
            }



            toolTipBox.style.left = left + "px";
            toolTipBox.style.top = top + "px";


            addEvent(obj,'mouseleave', function () {
                //延时隐藏
                setTimeout(function () {
                    getEL(id).style.display = "none";
                }, 300)
            });

        } else {
            //显示
            getEL(id).style.display = "block";
        }
    }

    //优化 利用冒泡
    addEvent(demo, 'mouseover', function (e) {
        var event = e || window.event;
        var target = event.target || event.srcElement;

        if(target.className == 'tooltip') {
            var _html;
            var _id;
            var _width = 200;

            switch (target.id){
                case 'tooltip1':
                    _id = "t1";
                    _html = "中华人民共和国";
                    break;
                case 'tooltip2':
                    _id = "t2";
                    _html = "美国篮球职业联赛";
                    break;
                case 'tooltip3':
                    _id = "t3";
                    _html = '<h2>春晓</h2><p>春眠不觉晓，</p><p>处处闻啼鸟。</p><p>夜来风雨声，</p><p>花落知多少。</p>';
                    _width = 100;
                    break;
            }
            showToolTip(target, _id, _html, _width);
        }

    })
    
   
 ```
    
    
    



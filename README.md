## TemperatureView: 自定义 View ，用来显示温度的变化
效果图：<br/>
![](https://github.com/ljuns/TemperatureView/blob/master/temperature/source/temp.gif)<br/>
当然，正常室温变化是没有这么快的，再来张截图：<br/>
![](https://github.com/ljuns/TemperatureView/blob/master/temperature/source/temp_1.png)<br/>
下面来说说这个过程，首先可以将它分为几个部分，分别为：<br/>
1、整个背景圆（可有可无）<br/>
2、进度弧（分为三段，颜色分别为绿黄红）<br/>
3、进度弧上的文字（正常，预警，警告）<br/>
4、刻度弧（紧靠着进度弧内侧的黑色弧）<br/>
5、刻度<br/>
6、中间的圆<br/>
7、指针<br/>
8、当前温度<br/>
同时这几个部分也是绘制的步骤。<br/>
那些自定义属性就不多说了，下面直接是绘制的过程：<br/>
首先是背景圆，当然，这个可有可无，全凭个人喜欢：<br/>
``` Java
/**
 * 背景圆
 * @param canvas
 */
private void drawOutCircle(Canvas canvas) {
  // 已经将画布移到中心，所以圆心为（0,0）
  canvas.drawCircle(0, 0, mSize /2-dp2px(1), outCirclePaint);
  canvas.save();
}
```
这里没什么好说的，直接画圆

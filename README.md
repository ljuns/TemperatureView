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
这里没什么好说的，直接画圆。接下来是第二部分了，进度弧:<br/>
``` Java
/**
 * 进度弧
 * @param canvas
 */
private void drawProgress(Canvas canvas) {
  // dp2px(10):留一点位置（可有可无）
  progressRadius = mSize /2 - dp2px(10);
  canvas.save();
  RectF rectF = new RectF(-progressRadius, -progressRadius, progressRadius, progressRadius);
  // 设置为圆角
  progressPaint.setStrokeCap(Paint.Cap.ROUND);
  progressPaint.setColor(Color.GREEN);
  // 从150度位置开始，经过120度
  canvas.drawArc(rectF, 150, 120, false, progressPaint);
  progressPaint.setColor(Color.RED);
  progressPaint.setStrokeCap(Paint.Cap.ROUND);
  canvas.drawArc(rectF, 330, 60, false, progressPaint);
  progressPaint.setColor(Color.YELLOW);
  progressPaint.setStrokeCap(Paint.Cap.BUTT);
  canvas.drawArc(rectF, 270, 60, false, progressPaint);
  canvas.restore();
}
```
整个进度从150度到30度，一共是240度，分为40份，所以刚好每份是6度。这部分也很简单，至于角度，自己在纸上画画算算就会瞬间明了<br/>
Paint.Cap.ROUND：用来设置 Paint 为圆角，因为进度的头尾两端个人觉得圆角好看点<br/>


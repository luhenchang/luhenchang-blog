---
theme: qklhk-chocolate
highlight: agate
---
# 一、自定义的必要性

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**绘制**的底层是强大的,我们所用的各端语言只是在现代UI追求的步伐中和用户喜好的交互中求同存异，抽取封装出自成个性风格的UI控件,当然面对万亿级别的客户各个平台的UI库出也不可能满足所有的客户需求,当然一门语言的可制定性也意味着其强大,几乎每个平台都提供了接口让开发者创造其UI的可能性,更可能的能满足客户需求。`ECharts`作为前端强大的图表K线等绘制工具可以说应有竟有,无比风骚。但用户和产品的需求永远是一个库满足不了的。当然作为技术人员自定义绘制也应该是需要掌握的技术。我们前端移动端作为产品的排面就应该让其独具特色,别具一格。所以自定义从我们的`技术岗位`、`技术本身`、`亿万用户不同需求`...出发，"自定义**很必要**"。

# 二、ECharts 
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[ECharts](https://echarts.apache.org/examples/zh/index.html)使用过的伙伴们都知道极其的丰富和花里胡哨了。对于库的使用没啥写的吧？我们今天的目的是学会自己分析和写出ECharts的效果,而不是使用Echarts库,虽然我没咋么写过前端,有API咋们就能一步步往下走。
如下:<br/>
**折线图**
![image.png](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/f4d54591ea2b48aba72038478638e884~tplv-k3u1fbpfcp-watermark.image)

**K线图**

![image.png](https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/923a9619ecd341bea96ac1d3d3cbe3eb~tplv-k3u1fbpfcp-watermark.image)

**K线图**

![image.png](https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/cf97d4b7bd734616a24ff7a58a6c7bd6~tplv-k3u1fbpfcp-watermark.image)

....当然还有很多。

# 三、画布的认识
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;不同于Android以及Flutter等。Canvas在HTML5中并不是实质的画布。**&lt;canvas&gt;** 元素本身并没有绘制能力（它仅仅是图形的容器） - 您必须使用脚本来完成实际的绘图任务。`getContext() 方法可返回一个对象`，该对象提供了用于在画布上绘图的方法和属性。HTML5中可以通过Canvas标签获取getContext("2d") 对象,它提供了很多绘制的属性和方法，可用于在画布上绘制文本、线条、矩形、圆形等等。

## 1、画布的创建
&nbsp;第一我们通过getElementById来获取Canvas容器标签,然后通过canvas.getContext("2d")来获取绘制对象。
```js
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
<canvas id="canvas"/>

<script>
    //getElementById() 来访问 canvas 元素
    const canvas = document.getElementById("canvas");
    const context = canvas.getContext("2d");
    
    
    context.fillStyle= 'rgb(222,155,155)';
    context.fillRect(0,0,canvas.width,canvas.height);
</script>
</body>
</html>
```
## 2、设置画布的宽高和背景色

&nbsp;通过canvas的width和height属性来设置画布的大小。通过fillStyle属性设置绘制区域的颜色。fillRect来设置绘制区域大小为坐标点为左上角固定宽高的距形。<br/>

**canvas.width设置画布的宽**<br/>
**canvas.height设置画布的高**<br/>
**context.fillStyle设置填充颜色**<br/>
**context.fillRect设置距形**

| 属性       | 作用                        |
| ---------- | --------------------------- |
| fillStyle  | 设置填充的样式,颜色、渐变等 |
| fillRect() | 定义被填充的矩形位置和大小  |



```js
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
<canvas id="canvas"/>

<script>
    //getElementById() 来访问 canvas 元素
    const canvas = document.getElementById("canvas");
     //设置画布的宽高
    canvas.width=400;
    canvas.height=200;
    //获取绘制的对象
    const context = canvas.getContext("2d");
    //设置填充的颜色是颜色渐变等
    context.fillStyle= 'rgb(222,155,155)';
    //填充区域为矩形,来定义位置和大小
    context.fillRect(0,0,canvas.width,canvas.height);
</script>
</body>
</html>
```

![image.png](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/9f8d265aaa214f49a3d5b96903eb3c32~tplv-k3u1fbpfcp-watermark.image)

**设置画布的宽高为width=1000;height=500;** <br/>
效果如下:

```js
 //画布宽高
 canvas.width=1000;
 canvas.height=5000;
 ...
 context.fillStyle= 'rgb(222,155,155)';
```

![image.png](https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/f4597740cce042058ab2cd7b5086b106~tplv-k3u1fbpfcp-watermark.image)

## 3、设置渐变色
&nbsp;渐变色一直是UI中极其多见的效果。不仅增添美感,更是高大上道路上的比不可少的秘诀。接下来咋们来体验一下前端的渐变。

### 线性渐变<br/>
##### createLinearGradient(x0: number, y0: number, x1: number, y1: number)<br/>
(x0,y0) 链接 (x1,y1)方向上进行渐变。如下(0,0)到(canvas.width,0)是水平方向上渐变。
##### addColorStop(offset: number, color: string): void;<br/>
用来设置渐变色起始的比例位置。<br/>
我们来看看效果<br/>

```js
const gradient = context.createLinearGradient(0, 0, canvas.width,0);
    gradient.addColorStop(0  ,"rgb(100,200,155)")
    gradient.addColorStop(0.5,"rgb(200,120,155)")
    gradient.addColorStop(1.0,"rgb(200,220,255)")
    context.fillStyle = gradient
```

![image.png](https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/5a361535abb0404497c6481f3d5aa2ec~tplv-k3u1fbpfcp-watermark.image)

如下(0,0)到(canvas.width,canvas.height)是对角线方向上渐变我们来看看效果<br/>

![image.png](https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/164b64427ec348f5985493955c73d22e~tplv-k3u1fbpfcp-watermark.image)

##### 任意方向上线性渐变

```js
const gradient = context.createLinearGradient(0, 0, canvas.width,canvas.height);

```
![image.png](https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/fd1ea70b7eef496db114cbe6b0e14c53~tplv-k3u1fbpfcp-watermark.image)

总结渐变色方向的确定通过(x0,y0)和(x1,y1)连线方向即可。通过addColorStop来进行比例设置渐变色值所起始范围。


### 径向渐变
##### createRadialGradient(x0: number, y0: number, r0: number, x1: number, y1: number, r1: number)
r0和r1半径比较那个大，那么就从那个到半径小的方向进行渐变,而不是从里到外或者从外到里。

```js
    //region 4.径向渐变色
    const canvas = document.getElementById("canvas");
    //设置画布的宽高
    canvas.width=1000;
    canvas.height=500;

    //绘制的对象获取
    const context = canvas.getContext("2d");
    //Radial（径向）
    //createRadialGradient(x0: number, y0: number, r0: number, x1: number, y1: number, r1: number)
    const gradient = context.createRadialGradient(canvas.width / 2, canvas.height / 2, 50, canvas.width / 2, canvas.height / 2, 20);
    gradient.addColorStop(0  ,"rgb(100,200,155)")
    gradient.addColorStop(0.8,"rgb(200,120,155)")
    gradient.addColorStop(1.0,"rgb(00,120,105)")

    context.fillStyle = gradient
    //设置填充的区域为巨形 fillRect(x: number, y: number, w: number, h: number)
    context.fillRect(0,0,canvas.width,canvas.height);
    //endregion
```

**半径50到20渐变-由外到内**过程如下

![image.png](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/eaa7369ee6d84de3aff0e90ee1d25ef9~tplv-k3u1fbpfcp-watermark.image)

**半径20到50渐变-由内到外**过程如下

![image.png](https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/168c72f85e9143e5832397270949a7c8~tplv-k3u1fbpfcp-watermark.image)

渐变就到这里...案例中会充分的使用渐变的。由于时间问题单独渐变案例就不写了。

# 三、画布的变换
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;画布通过translate、rotate、scale、skew等进行画布的变换,可以让我们绘制过程事半功倍,犹鱼得水。
默认情况画布的坐标系是左上角,我们可以在坐标(0,0)绘制到(100,100)且连线。如下代码和效果:<br/>

**context.beginPath()表示开始一段新的路径,下次填充只会修改此段路径内容**<br/>
**context.moveTo(x, y)路径的起始点**<br/>
**context.lineTo(x, y)链接到下一个点**<br/>
**context.strokeStyle = gradient 设置未闭合路径的颜色**<br/>
**context.stroke() 路径为线**<br/>


```js
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>canvas_change</title>
</head>
<body>
<canvas id="canvas"/>
</body>
<script>
    //region 1.变换traslate
    const canvas = document.getElementById("canvas");
    //设置画布的宽高
    canvas.width = 100;
    canvas.height = 100;
    //绘制的对象获取
    const context = canvas.getContext("2d");

    //此段路径绘制开始
    context.beginPath()
    context.moveTo(0, 0)
    context.lineTo(100, 100)

    //设置线的颜色为渐变色
    const gradient = context.createLinearGradient(
        0,
        0, canvas.width, canvas.height);
    gradient.addColorStop(0, "rgb(100,200,155)")
    gradient.addColorStop(0.8, "rgb(200,120,155)")
    gradient.addColorStop(1.0, "rgb(00,120,105)")
    context.strokeStyle = gradient

    //画不是闭合区域 fill是闭合区域
    context.stroke()
    
</script>
</html>
```

![image.png](https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/1ea246a0c4cb44b9b4a781b4e0b9beed~tplv-k3u1fbpfcp-watermark.image)

### 画布translate[平移]
我们常见的ECharts等图表都可以看到有坐标系,而我们的坐标系默认是左上角。大部分常见的坐标系都不是在左上角的。如果以左上角为圆点绘制起来也许比较费劲。最希望的是以(0,0)为我们想要的相对位置，这样处理很多事变的简单。

**折线图**
![image.png](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/f4d54591ea2b48aba72038478638e884~tplv-k3u1fbpfcp-watermark.image)

上面我们学会了绘制线条。那我们绘制出默认的坐标系,且在默认的圆心左上角绘制一个半径为50的圆圈。


```js
<script>
    //region 1.变换traslate
    const canvas = document.getElementById("canvas");
    //设置画布的宽高
    canvas.width = 400;
    canvas.height = 200;
    //绘制的对象获取
    const context = canvas.getContext("2d");

    //设置线的颜色为渐变色
    const gradient = context.createLinearGradient(
        0,
        0, canvas.width, canvas.height);
    gradient.addColorStop(0, "rgb(100,200,155)")
    gradient.addColorStop(0.8, "rgb(200,120,155)")
    gradient.addColorStop(1.0, "rgb(00,120,105)")
    context.strokeStyle = gradient



    //绘制X轴开始
    context.beginPath()
    context.moveTo(0, 0)
    context.lineTo(canvas.width, 0)
    context.closePath()
    //画不是闭合区域 fill是闭合区域
    context.stroke()

    //绘制Y轴
    context.beginPath()
    context.moveTo(0, 0)
    context.lineTo(0, canvas.height)
    context.closePath()
    //画不是闭合区域 fill是闭合区域
    context.stroke()

    context.beginPath()
    //绘制在圆心绘制圆圈
    context.arc(0, 0, 50, 0, Math.PI * 2, true);
    context.closePath()
    //画不是闭合区域 fill是闭合区域
    context.fillStyle = gradient
    context.fill()

</script>
```



![image.png](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/31367a343e9e4b308c5eacea2f3d3744~tplv-k3u1fbpfcp-watermark.image)

接下来我想将坐标远点放到画布中间,绘制之前加平移变换。我们可以看出绘制过程中圆的坐标轴是以画布中心为圆点绘制坐标轴和圆的,当然你可以任意的平移。

```js
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>canvas_change</title>
</head>
<body>
<canvas id="canvas"/>
</body>
<script>
    //region 1.变换traslate
    const canvas = document.getElementById("canvas");
    //设置画布的宽高
    canvas.width = 400;
    canvas.height = 200;
    //绘制的对象获取
    const context = canvas.getContext("2d");

    //设置线的颜色为渐变色
    const gradient = context.createLinearGradient(
        0,
        0, canvas.width, canvas.height);
    gradient.addColorStop(0, "rgb(100,200,155)")
    gradient.addColorStop(0.8, "rgb(200,120,155)")
    gradient.addColorStop(1.0, "rgb(00,120,105)")
    context.fillStyle = "rgba(100,200,155,0.2)"
    context.fillRect(0, 0, canvas.width, canvas.height);
    context.strokeStyle = gradient

    //平移画布
    context.translate(canvas.width/2,canvas.height/2)

    //绘制X轴开始
    context.beginPath()
    context.moveTo(0, 0)
    context.lineTo(canvas.width, 0)
    context.closePath()
    //画不是闭合区域 fill是闭合区域
    context.stroke()

    //绘制Y轴
    context.beginPath()
    context.moveTo(0, 0)
    context.lineTo(0, canvas.height)
    context.closePath()
    //画不是闭合区域 fill是闭合区域
    context.stroke()

    context.beginPath()
    //绘制在圆心绘制圆圈
    context.arc(0, 0, 50, 0, Math.PI * 2, true);
    context.closePath()
    //画不是闭合区域 fill是闭合区域
    context.fillStyle = "rgb(200,120,155)"
    context.fill()

</script>
</html>
```

![image.png](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/3035b30e11534c3b8d362433b018833b~tplv-k3u1fbpfcp-watermark.image)

### 画布rotate【旋转】

首先我们猜想一下画布的旋转,然后去证明是否正确。首先绘制一个线,然后旋转画布10度,再次绘制同样的线。绘图前后对比如下:


```js
//旋转画布
context.rotate(Math.PI/180*10)
```

![image.png](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/12c059f8114f4f8d916758cfefc4a2ce~tplv-k3u1fbpfcp-watermark.image)


### 画布scale【缩放】
画布Canvas通过scale(float sx, float sy)可以将绘制坐标系转换为我们希望的坐标系。例如默认坐标系是如下:
![](https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/12caccd9b62d41a3bffa66844837db1a~tplv-k3u1fbpfcp-watermark.image)

我心目中的坐标系并不是这样的而是这样那样的如下:


![](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/97abbe9ef9b14a6bb586c24c1dacffd1~tplv-k3u1fbpfcp-watermark.image)

接下来我们想要得到一个如下2一样的坐标系。

![](https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/879e0060c4f949b285011fd69435c623~tplv-k3u1fbpfcp-watermark.image)

>沿x轴镜像，就相当于canvas.scale(1, -1),沿y轴镜像，就相当于canvas.scale(-1, 1),沿原点镜像，就相当于canvas.scale(-1, -1)

分析图二坐标系可以看到圆点在左下角。y轴向上为正方向,x轴向右为正方向,和默认的坐标系左上角对比，只是y轴方向相反。这时候我们就可以利用canvas.scale(1,-1)镜像变换,再通过平移向下即可。<br/>
**沿x轴镜像scale(1,-1)**<br/>
**向下平移canvas.height即可---这里注意了因为坐标系被scale(1,-1)之后坐标系向上为正,向下平移需要-canvas.height**
代码部分

```js
<script>
    //region 1.变换rote
    const canvas = document.getElementById("canvas");
    //设置画布的宽高
    canvas.width = 400;
    canvas.height = 200;
    //绘制的对象获取
    const context = canvas.getContext("2d");

    //设置线的颜色为渐变色
    const gradient = context.createLinearGradient(
        0,
        0, canvas.width, canvas.height);
    gradient.addColorStop(0, "rgb(100,200,155)")
    gradient.addColorStop(0.8, "rgb(200,120,155)")
    gradient.addColorStop(1.0, "rgb(00,120,105)")
    context.fillStyle = "rgba(100,200,155,0.2)"
    context.fillRect(0, 0, canvas.width, canvas.height);
    context.strokeStyle = gradient

    //沿x轴镜像变换必须明白最重要的一点,这时候y坐标系向下为正，经过下面scale(1,-1)y轴坐标系乡下为负。
    context.scale(1,-1)
    //向下平移，注意这时候乡下是负方向哦
    context.translate(0,-canvas.height)

    //绘制X轴开始
    context.beginPath()
    context.moveTo(0, 0)
    context.lineTo(canvas.width, 0)
    context.closePath()
    //画不是闭合区域 fill是闭合区域
    context.stroke()

    //绘制Y轴
    context.beginPath()
    context.moveTo(0, 0)
    context.lineTo(0, canvas.height)
    context.closePath()
    //画不是闭合区域 fill是闭合区域
    context.stroke()

    context.beginPath()
    //绘制线
    context.moveTo(0,0);
    context.lineTo(100,100);
    context.closePath()
    //画不是闭合区域 fill是闭合区域
    context.strokeStyle = "rgb(200,120,155)"
    context.stroke()

</script>
```

![image.png](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/8ead168065be4201935b9b880274b817~tplv-k3u1fbpfcp-watermark.image)

好了,到这里我们学会了坐标系的变换,我相信大家应该觉得这么简单的东西,就这样么？当然了坐标变换有着极大的便利性和简化功能，我们逐步深入，画布的变换定会让你事半功倍,游刃有余。

# 四、手写ECharts案例

### 1、折线图

如下是[ECharts官方第一个案例](https://echarts.apache.org/examples/zh/index.html):都是文字和各种线圆组成,但是其中有很多跟我们的坐标变换有着千丝万缕的关系，咋们来一步步分析画布变换的重要性。
![image.png](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/2871d20a388f46a98a238f2e986b59b9~tplv-k3u1fbpfcp-watermark.image)

#### 分析绘制过程<br/>
**1.变换坐标系--为操作带来方便**<br/>
**2.绘制平行X轴的线条**<br/>
**3.绘制文字**<br/>
**4.绘制折线和圆**<br/>

**1.变换坐标系--为操作带来方便**<br/>

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;我们分析上图,基本是左下角为坐标圆心进行整个折线图的绘制。但我们坐标系默认是左上角,所以接下来变换坐标系圆点到左下角即可,上面案例中我们看到距离底部和坐标有一定的距离用来绘制文字我们设置距离下面50左边40。


```js
 //region 1.变换rote
    const marginBootom = 50;
    const marginLeft = 40;
    const canvas = document.getElementById("canvas");
    //设置画布的宽高
    canvas.width = 400;
    canvas.height = 200;
    //绘制的对象获取
    const context = canvas.getContext("2d");
    //渐变
    context.strokeStyle = "rgb(0,0,0,1)"
    context.lineWidth=0.2

    //沿x轴镜像对称变换画布
    context.scale(1, -1)
    //向下平移画布-marginBootom的高度
    context.translate(marginLeft, -canvas.height+marginBootom)
    
```
此时的坐标系是这样的，为了演示和观察方便我这里贴一下坐标系。接下来我们开始后面的绘制过程。

![image.png](https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/e3e7b674829a4ae48cb8aaa9d2c6ad3c~tplv-k3u1fbpfcp-watermark.image)

**2.绘制平行X轴的线条**<br/>
这个平行X轴的线条我们难道需要计算每条线的起点和终点么？这么麻烦？当然来画布的变换很好的解决了这个问题。我们的画布是有状态的每次的状态都可以进行保存也可以返回之前的状态。如下:我们绘制了最底下的一条线。


![image.png](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/276a7fcefd4448cc839909a9314b1fc7~tplv-k3u1fbpfcp-watermark.image)

那我们可以每次变换坐标系向Y轴方向向上平移固定高度再绘制这条线线。多次绘制就形成了平行X轴的多条线段。


```html

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Line</title>
</head>
<body>
<canvas id="canvas"/>
<script>
    //region 1.变换rote
    const marginBootom = 50;
    const marginLeft = 40;
    const canvas = document.getElementById("canvas");
    //设置画布的宽高
    canvas.width = 400;
    canvas.height = 300;
    //绘制的对象获取
    const context = canvas.getContext("2d");
    //渐变
    context.strokeStyle = "rgb(0,0,0,1)"
    context.lineWidth=0.08

    //沿x轴镜像对称变换画布
    context.scale(1, -1)
    //向下平移画布-marginBootom的高度
    context.translate(marginLeft, -canvas.height+marginBootom)
    
    //保存好当前画布的状态。因为我们的圆心在左下角，我们还需要返回到这个远点进行其他操作。
    context.save()
    const heightOfOne=30

    //绘制X轴开始
    for(let i=0; i<7; i++){
        context.beginPath()
        context.moveTo(0, 0)
        context.lineTo(canvas.width, 0)
        context.closePath()
        //画不是闭合区域 fill是闭合区域
        context.stroke()
        //每次绘制完之后继续往上平移
        context.translate(0,heightOfOne)
    }
    context.restore()

</script>
</body>
</html>
```
![image.png](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/09189c08f7af4c74acc49df44ac4d1e7~tplv-k3u1fbpfcp-watermark.image)


**3.绘制刻度**<br/>
同样的方法我们将X轴分为7等分，没以等分我们都要绘制一个刻度。代码如下

![image.png](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/fe58dd1687f2436792dad6f264c8c9c9~tplv-k3u1fbpfcp-watermark.image)

```js
 //绘制刻度开始
    context.save()
    context.lineWidth=0.2
    for(let i=0; i<8; i++){
        context.beginPath()
        context.moveTo(0, 0)
        context.lineTo(0, -5)
        context.closePath()
        //画不是闭合区域 fill是闭合区域
        context.stroke()
        //每次绘制完之后继续往上平移
        context.translate(widthOfOn,0)
    }
    context.restore()

```


![image.png](https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/eb82cfa869414156aea6dc481a832161~tplv-k3u1fbpfcp-watermark.image)

**绘制X轴下面文字**<br/>

如果非常精确,这里可能涉及到文字的测量。当然了我们需要精确,由于时间问题我这里也就不细细说明文字绘制测量的详细API。代码中有解释。


**context.fillText("文字",x,y);表示在（x,y）位置绘制文字**

![image.png](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/fe58dd1687f2436792dad6f264c8c9c9~tplv-k3u1fbpfcp-watermark.image)

```js
   //x轴绘制文字数组
    const xText = new Array("Mon", "Tue", "Wed","Thu","Fir","Sat","Sun");
    for(let i=0; i<xText.length; i++){
        //画不是闭合区域 fill是闭合区域
        context.stroke()
        //每次绘制完之后继续往上平移
        if(i===0){
            //分析之后第一次移动了单位长度的一半。后面的每次都平移一个刻度长度,坐标圆心就平移到了每个刻度的中间。y轴向下平移了5个像素。这样就和X轴不会重合。
            context.translate(widthOfOn/2,-5)
        }else{
            context.translate(widthOfOn,0)
        }
        context.fillText(xText[i],0,0);
    }
    context.restore()
```


![image.png](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/3f570c27aef34fb0b8756a318a9bfc7e~tplv-k3u1fbpfcp-watermark.image)

到这里我们发现字体是沿着X轴镜像变换的。因为默认右下方是正方向，我们经过变换右上方为正方向。所以这里绘制之前我们需要将坐标系还原即可。


```js
 //x轴绘制文字数组
    context.save()
    const xText = new Array("Mon", "Tue", "Wed","Thu","Fir","Sat","Sun");
    //这里沿着X轴镜像对称变换。那么Y轴向下为正，X没变向右为正。
    context.scale(1,-1)
    for(let i=0; i<xText.length; i++){
        //画不是闭合区域 fill是闭合区域
        context.stroke()
        //每次绘制完之后继续往上平移
        if(i===0){
            //分析之后第一次移动了单位长度的一半。后面的每次都平移一个刻度长度,坐标圆心就平移到了每个刻度的中间。y轴向下平移了5个像素。这样就和X轴不会重合。
            context.translate(widthOfOn/2,15)

        }else{
            context.translate(widthOfOn,0)
        }
        context.fillText(xText[i],0,0);
    }
    //还原到远点为左下角状态。
    context.restore()
```

![image.png](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/2833e0b299e74e0492fe2731faaaae3c~tplv-k3u1fbpfcp-watermark.image)

**绘制Y轴左边的文字**<br/>
还需要我BB么....

![image.png](https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/b910162b8d434e1dbc822b12149053d6~tplv-k3u1fbpfcp-watermark.image)
```js
    //保存左下角为坐标圆点状态。
    context.save()
    context.scale(1,-1)
    context.translate(-20,0)
    context.font = "7pt Calibri";
    //Y轴左边绘制文字
    for(let i=0; i<7; i++){
        //画不是闭合区域 fill是闭合区域
        context.stroke()
        //每次绘制完之后继续往上平移
        context.fillText((50*i).toString(),0,0);
        context.translate(0,-heightOfOne)

    }
    context.restore()
```

![image.png](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/522369c6c42343b9a37f1b67038b3981~tplv-k3u1fbpfcp-watermark.image)

字体看上图都绘制完成,但是对比原图我们的文字并不在每个刻度的正中间。如上图蓝色指向。
如下图上面是我们绘制的。下面是案例的对比之下我们绘制的文字中间位置不是单位刻度中间位置。我们只需要计算出文字的宽度即可。然后绘制的文字X减去位子宽度的一半即可。好好想想很简单的把？
![image.png](https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/475c6d69f6784238b85a2579a37f5b4d~tplv-k3u1fbpfcp-watermark.image)

**context.measureText("文本");测量文字**<br/>
**context.fillText(xText[i],-textWidth.width/2,0);**
```js
    //x轴绘制文字数组
    context.save()
    const xText = new Array("Mon", "Tue", "Wed","Thu","Fir","Sat","Sun");
    //这里沿着X轴镜像对称变换。那么Y轴向下为正，X没变向右为正。
    context.scale(1,-1)
    context.font = "7pt Calibri";
    for(let i=0; i<xText.length; i++){
        //画不是闭合区域 fill是闭合区域
        context.stroke()
        //每次绘制完之后继续往上平移
        if(i===0){
            //分析之后第一次移动了单位长度的一半。后面的每次都平移一个刻度长度,坐标圆心就平移到了每个刻度的中间。y轴向下平移了5个像素。这样就和X轴不会重合。
            context.translate(widthOfOn/2,15)

        }else{
            context.translate(widthOfOn,0)
        }
        const textWidth = context.measureText(xText[i]);
        context.fillText(xText[i],-textWidth.width/2,0);
    }
    //还原到远点为左下角状态。
    context.restore()
```

![image.png](https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/5c6209c96e484729b5775156b4f4a586~tplv-k3u1fbpfcp-watermark.image)
同样的Y轴文字自己感受一波？就不啰嗦了。

![image.png](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/4e1126a8710148c695892525ed0a093f~tplv-k3u1fbpfcp-watermark.image)

**4.绘制折线和圆**<br/>
所有的绘制有个小问题,不管那一端需要将我们实际的数据映射到我们的坐标系中。这个就简单的计算而已，这里提一下,例如我们的坐标系内部是按照画布的宽度来计算的，也就是像素,当时我们实际的数据可能是任意的数据。所以我们需要按照数据来进行映射到我们的坐标系。案例中的折线数据就是如此:

定义类进行坐标的储存，第一次使用前端的对象怪怪的.....
```js
const Point = {
    createNew: function (x,y) {
        const point = {};
        point.x = x;
        point.y = y;
        return point;
    }
};
```

```js
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Line</title>
    <script type="text/javascript" src="js/canvas..js"></script>
</head>

<body>
<canvas id="canvas"></canvas>
<script>
    //region 1.变换rote
    const marginBootom = 50;
    const marginLeft = 40;
    const canvas = document.getElementById("canvas");
    //设置画布的宽高
    canvas.width = 500;
    canvas.height = 300;
    //绘制的对象获取
    const context = canvas.getContext("2d");
    //渐变
    context.strokeStyle = "rgb(0,0,0,1)"
    context.lineWidth = 0.09

    //沿x轴镜像对称变换画布
    context.scale(1, -1)
    //向下平移画布-marginBootom的高度
    context.translate(marginLeft, -canvas.height + marginBootom)

    //绘制X轴和刻度
    drawX(context)
    //绘制文字
    drawText(context)
    //绘制折线和圆
    drawLine(context)
    //绘制圆
    drawCircle(context)
</script>

</body>
</html>
```
canvas.js文件

```js
//绘制折线
function drawLine(context) {
    //绘制折线段
    const widthOfOn = (canvas.width - marginLeft) / 7
    const danweiHeight=35/50;//每个数字占用的实际像素高度
    const point01 = Point.createNew(widthOfOn/2,150*danweiHeight);
    const point02 = Point.createNew(widthOfOn/2+widthOfOn,250*danweiHeight);
    const point03 = Point.createNew(widthOfOn/2+widthOfOn*2,225*danweiHeight);
    const point04 = Point.createNew(widthOfOn/2+widthOfOn*3,211*danweiHeight);
    const point05 = Point.createNew(widthOfOn/2+widthOfOn*4,140*danweiHeight);
    const point06 = Point.createNew(widthOfOn/2+widthOfOn*5,148*danweiHeight);
    const point07 = Point.createNew(widthOfOn/2+widthOfOn*6,260*danweiHeight);


    const points = [point01, point02, point03, point04, point05, point06, point07];
    context.save();

    context.beginPath();
    for (let index = 0; index < points.length; index++) {
        context.lineTo(points[index].x,points[index].y);
    }
    context.strokeStyle="rgb(93,111,194)"
    context.lineWidth=1
    context.shadowBlur = 5;
    context.stroke();
    context.closePath();
    context.restore();
}
//绘制圆圈
function drawCircle(context) {
    const widthOfOn = (canvas.width - marginLeft) / 7
    const danweiHeight=35/50;//每个数字占用的实际像素高度
    const point01 = Point.createNew(widthOfOn/2,150*danweiHeight);
    const point02 = Point.createNew(widthOfOn/2+widthOfOn,250*danweiHeight);
    const point03 = Point.createNew(widthOfOn/2+widthOfOn*2,225*danweiHeight);
    const point04 = Point.createNew(widthOfOn/2+widthOfOn*3,211*danweiHeight);
    const point05 = Point.createNew(widthOfOn/2+widthOfOn*4,140*danweiHeight);
    const point06 = Point.createNew(widthOfOn/2+widthOfOn*5,148*danweiHeight);
    const point07 = Point.createNew(widthOfOn/2+widthOfOn*6,260*danweiHeight);


    const points = [point01, point02, point03, point04, point05, point06, point07];
    context.save();
    context.beginPath();
    for (let index = 0; index < points.length; index++) {
        context.beginPath();
        context.arc(points[index].x,points[index].y,3, 0, Math.PI * 2, true);
        context.closePath();
        context.fillStyle = 'rgb(100,255,255)';
        context.shadowBlur = 5;
        context.shadowColor = 'rgb(100,255,255)';
        context.fill()
    }
    canvas.restore();
}
```
![image.png](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/a23578110b824e51986baa2c8875eadc~tplv-k3u1fbpfcp-watermark.image)

到这里,如果你一步步走下来对于不明白的百度搜索看API我相信只要你自己练习至少三个每个使用一下画布的变换,那么自定义你就已经达到不错的水平,当然对于各种骚操作,我们可以进一步学习`贝塞尔曲线`等和`动画`加`手势`等。


### 平滑的折线图

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;今天第一次接触HTML5的自定义,其实各端的自定义都是底层渲染绘制基础上的API封装,一个好的平台或者语言都会有完善的API,H5再我看来之所以有ECharts这样的库可以所很完善了API,所以这个章节我很有信心。

- `曲线`开发中时常出现在自定义图标里面,学会曲线绘制能让你的软件更具`创造性`和`无穷的魅力`。

#### 一、曲线认识与理解
- 由于之前Android写过一些概论和理解,所以这里就贴一下android的代码和理解，时间问题就这里可以看基本的理解即可

```
曲线常见的API
1.一阶曲线
2.二阶曲线
3.三阶曲线
```
我们在初中高中学习中学习了各种`直线`,`圆`,`椭圆`,`正玄`...`曲线`等对应的坐标系方程吧,接下来我们回顾一下我们的直线和曲线等方程。

-  第一步我们还是定义一个类新建坐标系,屏幕可旋转横屏显示
```kotlin
package com.example.android_draw.view

import android.content.Context
import android.graphics.Canvas
import android.util.AttributeSet
import android.view.View

/**
 *
 *  ┌─────────────────────────────────────────────────────────────┐
 *  │┌───┬───┬───┬───┬───┬───┬───┬───┬───┬───┬───┬───┬───┬───┬───┐│
 *  ││Esc│!1 │@2 │#3 │$4 │%5 │^6 │&7 │*8 │(9 │)0 │_- │+= │|\ │`~ ││
 *  │├───┴─┬─┴─┬─┴─┬─┴─┬─┴─┬─┴─┬─┴─┬─┴─┬─┴─┬─┴─┬─┴─┬─┴─┬─┴─┬─┴───┤│
 *  ││ Tab │ Q │ W │ E │ R │ T │ Y │ U │ I │ O │ P │{[ │}] │ BS  ││
 *  │├─────┴┬──┴┬──┴┬──┴┬──┴┬──┴┬──┴┬──┴┬──┴┬──┴┬──┴┬──┴┬──┴─────┤│
 *  ││ Ctrl │ A │ S │ D │ F │ G │ H │ J │ K │ L │: ;│" '│ Enter  ││
 *  │├──────┴─┬─┴─┬─┴─┬─┴─┬─┴─┬─┴─┬─┴─┬─┴─┬─┴─┬─┴─┬─┴─┬─┴────┬───┤│
 *  ││ Shift  │ Z │ X │ C │ V │ B │ N │ M │< ,│> .│? /│Shift │Fn ││
 *  │└─────┬──┴┬──┴──┬┴───┴───┴───┴───┴───┴──┬┴───┴┬──┴┬─────┴───┘│
 *  │      │Fn │ Alt │         Space         │ Alt │Win│   HHKB   │
 *  │      └───┴─────┴───────────────────────┴─────┴───┘          │
 *  └─────────────────────────────────────────────────────────────┘
 * 版权：渤海新能 版权所有
 *
 * @author feiWang
 * 版本：1.5
 * 创建日期：2/8/21
 * 描述：Android_Draw
 * E-mail : 1276998208@qq.com
 * CSDN:https://blog.csdn.net/m0_37667770/article
 * GitHub:https://github.com/luhenchang
 */
class LHC_Cubic_View @JvmOverloads constructor(
    context: Context?,
    attrs: AttributeSet? = null,
    defStyleAttr: Int = 0
) : View(context, attrs, defStyleAttr) {

    init {

    }

    override fun onDraw(canvas: Canvas?) {
        super.onDraw(canvas)
    }

}

```
为了方便观察和绘制进行了网格和坐标轴的绘制。我相信学过上一篇文章的对于画布的变换操作已经熟练掌握了,网格坐标轴的代码我就不再讲解,看图。

![](https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/6d1f6d5f46144983b96bfbe83cf1bde6~tplv-k3u1fbpfcp-watermark.image)
#### 1.方程式映射到坐标系
记得我们初中学过`Y(x)=ax+b`的直线方程吧。我们来看看这个方程映射到坐标系中的图像。
首先定义一个函数 `y=2x-80`获取一段点集合,为了看效果我们x偶数时候绘制,然后绘制点即可。代码如下:
```kotlin
    private var number=0..420
    //直线方程y=2x-80
    private fun drawzxLine(canvas: Canvas) {
        pointList= ArrayList()
        //绘制方程式y=10x+20
        val gPaint = getPaint()
        number.forEach { t ->
            val point=PointF()
            if (t%2==0) {//x轴偶数点进行绘制
                point.x = t.toFloat()
                point.y = 2f * t - 80
                pointList.add(point)
                canvas.drawPoint(point.x, point.y, gPaint)
            }
        }
    }

```
 ![](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/5f0c63ecc7a9402da4781add80dd34e5~tplv-k3u1fbpfcp-watermark.image)

>1.同样圆的方程,椭圆的方程等都可以这样进行映射到坐标系。   <br/>
>2.![](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/8ac54dec94e6425d8220ea3656a11615~tplv-k3u1fbpfcp-watermark.image)  所表示的曲线是以O(a，b)为圆心，以r为半径的圆。 <br/>
>3.例如:(x-10)<sup>2</sup>+(y-10)<sup>2</sup>=160<sup>2</sup>我们进行映射到坐标系内。<br>

- 解方程应该没问题吧。我们来变换为我们熟悉的方程式:

>(x-10)<sup>2</sup>+(y-10)<sup>2</sup>=160<sup>2</sup><br>
>1.移项 (y-10)<sup>2</sup>=160<sup>2</sup>-(x-10)<sup>2</sup><br/>
>2.开方 转换为函数Math方程式如下:<br/>
>开方之后有正负值需要注意
>1. y=sqrt(160.0.pow(2.0).toFloat() - ((point.x - 10).toDouble()).pow(2.0)).toFloat() + 10
>2. y=-sqrt(160.0.pow(2.0).toFloat() - ((pointDown.x - 10).toDouble()).pow(2.0)).toFloat() + 10

```kotlin
 //绘制圆圈
        number.forEach { t ->
            val point = PointF()
            val pointDown = PointF()

            //(x-10)2+（y-10）2=1602
            point.x = t.toFloat()
            pointDown.x = t.toFloat()
            //y计算应该不用我说吧。
            point.y =
                sqrt(160.0.pow(2.0).toFloat() - ((point.x - 10).toDouble()).pow(2.0)).toFloat() + 10
            pointDown.y = -sqrt(
                160.0.pow(2.0).toFloat() - ((pointDown.x - 10).toDouble()).pow(2.0)
            ).toFloat() + 10
            canvas.drawPoint(point.x, point.y, gPaint)
            canvas.drawPoint(pointDown.x, pointDown.y, gPaint)

        }
```
![](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/85b1149629e14db0ab37ae8dd2354696~tplv-k3u1fbpfcp-watermark.image)

#### 2.贝塞尔曲线

 通过上面我们发现凡是函数都可以和坐标系绘制进行一一映射,当然了`贝塞尔曲线`也是有方程式的。有如下:

`线性贝塞尔曲线`
- 给定点P0、P1，线性贝塞尔曲线只是一条两点之间的直线。这条线由下式给出：
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![](https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/5de192d012dd4ce9b268b152033c05f1~tplv-k3u1fbpfcp-watermark.image)

![](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/9d0140a2a76a46e6944e03be6807f18f~tplv-k3u1fbpfcp-watermark.image)

`二次方贝塞尔曲线`
- 二次方贝塞尔曲线的路径由给定点P0、P1、P2的函数B（t）追踪：
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/a42c6d589e87417ca71a2f10394e282a~tplv-k3u1fbpfcp-watermark.image)
![](https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/0c0af9736741499abe3cf097a7aa405c~tplv-k3u1fbpfcp-watermark.image)

`三次方贝塞尔曲线`

P0、P1、P2、P3四个点在平面或在三维空间中定义了三次方贝塞尔曲线。曲线起始于P0走向P1，并从P2的方向来到P3。一般不会经过P1或P2；公式如下：

![](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/5bfec94b20974c68aa888bf7d8f180e5~tplv-k3u1fbpfcp-watermark.image)

![](https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/bb2313ae6ba64064a91401f072d7002b~tplv-k3u1fbpfcp-watermark.image)

当然在Android端的Native层已经封装好了方法,`二次方贝塞尔曲线`和`三次方贝塞尔曲线`,已知函数当然可以进行封装。
```kotlin
在Android端提供了二阶和三阶
 `二次方贝塞尔曲线`：
    public void quadTo(float x1, float y1, float x2, float y2)
    public void rQuadTo(float dx1, float dy1, float dx2, float dy2) 
 `三次方贝塞尔曲线`：
    public void cubicTo(float x1, float y1, float x2, float y2,float x3, float y3)
    public void rCubicTo(float x1, float y1, float x2, float y2,float x3, float y3) 

```
接下来我们绘制一个二阶曲线，控制点可以随着手势的移动和下按进行对应的屏幕移动,对于`手势坐标系和屏幕坐标系的映射转换`[上节折线](https://juejin.cn/post/6922365337119916040)里面说很明白了,这里不多做解释。
- quadTo(float x1, float y1, float x2, float y2)
```kotlin
    //记录移动的canvas画布坐标,不是手势坐标，由手势坐标转换为canvas坐标进行刷新
    private var moveX: Float = 160f
    private var moveY: Float = 160f
   private fun drawQuz(canvas: Canvas) {
        controllRect = Rect(
            (moveX - 30f).toInt(),
            (moveY + 30f).toInt(),
            (moveX + 30).toInt(),
            (moveY - 30f).toInt()
        )
        val quePath = Path()
        canvas.drawCircle(0f, 0f, 10f, getPaintCir(Paint.Style.FILL))
        canvas.drawCircle(320f, 0f, 10f, getPaintCir(Paint.Style.FILL))
        //第一个点和控制点的连线到最后一个点链线。为了方便观察
        val lineLeft = Path()
        lineLeft.moveTo(0f, 0f)
        lineLeft.lineTo(moveX, moveY)
        lineLeft.lineTo(320f, 0f)
        canvas.drawPath(lineLeft, getPaint(Paint.Style.STROKE))
        //第一个p0处画一个圆。第二个p1处画一个控制点圆,最后画一个。
        canvas.drawCircle(moveX, moveY, 10f, getPaintCir(Paint.Style.FILL))
        quePath.quadTo(moveX, moveY, 320f, 0f)
        canvas.drawPath(quePath, getPaint(Paint.Style.STROKE))
    }

    override fun onTouchEvent(event: MotionEvent): Boolean {
        when (event.action) {
            ACTION_DOWN,
            ACTION_MOVE -> {
                //在控制点附近范围内部,进行移动
                Log.e("x=", "onTouchEvent: (x,y)"+(event.x - width / 2).toInt()+":"+(-(event.y - height / 2)).toInt())
                //将手势坐标转换为屏幕坐标
                moveX = event.x - width / 2
                moveY = -(event.y - height / 2)
                invalidate()
            }
        }
        return true
    }

```
![](https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/c86080490d2541bdb8edbbb5156aa8fc~tplv-k3u1fbpfcp-watermark.image)

上图可以拖动控制点,在起点和结尾之间的曲线随着控制点发生了变形。`控制点靠近那一侧弧度的凸起就偏向那一侧`,初步的认识这一个规律即可,而练习中不断的去调节控制点达到我们的需求。但是在上图中我们回发现弧度不够圆圈,在三阶函数里面可以很好的调节弧度。接下来我们来看看三阶函数

`三阶曲线`

- public void cubicTo(float x1, float y1, float x2, float y2,float x3, float y3)
同样我们在坐标系内绘制三阶曲线。
为了很好的看到效果我们这次进行来精细的控制,我们可以拖动`任意`我们想要拖动的`控制点`进行观察我们的三阶曲线。在上章节折线中`对于手势配合Rect的contains方法可以进行局部的点击`,当然了拖动也是没问题的。
如下图:我们只需要在控制点附近进行绘制`距形包裹住控制点`,手势滑动时时刷`新控制点`和`对应的距形`即可。

![](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/1ce7c24acbdf437fa4371328d0c5e281~tplv-k3u1fbpfcp-watermark.image)

![](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/f8d9617582fb4a0bba7c7394ec01e01b~tplv-k3u1fbpfcp-watermark.image)

到这里我想我们应该大概的明白二阶和三阶曲线对于弧度的`大致方向控制`了吧。你以为这样就结束了么。接下来下来开始正式的进入曲线应用。

![image.png](https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/0e223bd994474ac1baa394511428f816~tplv-k3u1fbpfcp-watermark.image)

曲线图分析<br/>

4.三阶曲线的拯救
![](https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/0d0a068441ec441486d4721f6251bda0~tplv-k3u1fbpfcp-watermark.image)
>当$y_1$<$y_2$如上图1.求出中点坐标x轴下部分控制点x+40px,上部分x-40px，y轴也可以调整来搞搞平滑度下部分控制点y-40x,上部分y+40。<br/>1.获取中点的坐标（$X_中$、$Y_中$）= (($x_1$+$x_2$)/2、($y_1$+$y_2$)/2)<br/>2.$x_1$到$X_中$之间的坐标=(($x_1$+$x_中$)/2、($y_1$+$y_中$)/2)<br/>3.$x_中$到$X_2$之间的坐标=(($x_中$+$x_2$)/2、($y_中$+$y_2$)/2)<br/><br/>当$y_1$>$y_2$如上图2.求出中点坐标x轴上部分+40px,下部分x-40px，y轴也可以调整，y轴也可以调整来搞搞平滑度上部分控制点y+40x,下部分y-40。<br/>1.获取中点的坐标（$X_中$、$Y_中$）= (($x_1$+$x_2$)/2、($y_1$+$y_2$)/2)<br/>2.$x_1$到$X_中$之间的坐标=(($x_1$+$x_中$)/2、($y_1$+$y_中$)/2)<br/>3.$x_中$到$X_2$之间的坐标=(($x_中$+$x_2$)/2、($y_中$+$y_2$)/2)<br/>

```js
/**
 * 绘制曲线
 * @param context
 */
function drawQuaraticLine(context) {
    //绘制折线段
    const widthOfOn = (canvas.width - marginLeft) / 7
    const danweiHeight=35/50;//每个数字占用的实际像素高度
    const point01 = Point.createNew(widthOfOn/2,150*danweiHeight);
    const point02 = Point.createNew(widthOfOn/2+widthOfOn,250*danweiHeight);
    const point03 = Point.createNew(widthOfOn/2+widthOfOn*2,225*danweiHeight);
    const point04 = Point.createNew(widthOfOn/2+widthOfOn*3,211*danweiHeight);
    const point05 = Point.createNew(widthOfOn/2+widthOfOn*4,140*danweiHeight);
    const point06 = Point.createNew(widthOfOn/2+widthOfOn*5,148*danweiHeight);
    const point07 = Point.createNew(widthOfOn/2+widthOfOn*6,260*danweiHeight);


    const dataList = [point01, point02, point03, point04, point05, point06, point07];
    context.save();
    context.beginPath();
    context.lineTo(point01.x,point01.y)
    //500=grid_width-40 每个单位的长度的=像素长度
    const danweiX = widthOfOn;
    const grid_width=widthOfOn;
    const xMoveDistance=20
    const yMoveDistance=30
    for (let index = 0;index < dataList.length-1;index++) {
        if (dataList[index] === dataList[index + 1]) {
            context.lineTo(danweiX*(index+1),0)
        } else if(dataList[index] < dataList[index + 1]){//y1<y2情况
            const centerX=(grid_width * index + grid_width * (1 + index)) / 2
            const centerY=(dataList[index].y + dataList[index + 1].y) / 2
            const controX0=(grid_width * index+centerX)/2
            const controY0=(dataList[index].y+centerY)/2
            const controX1=(centerX+ grid_width * (1 + index))/2
            const controY1=(centerY+dataList[index+1].y)/2
            context.bezierCurveTo(controX0+xMoveDistance,controY0-yMoveDistance,controX1-xMoveDistance,controY1+yMoveDistance,grid_width * (1 + index),dataList[index + 1].y)
        }else{
            const centerX=(grid_width * index + grid_width * (1 + index)) / 2
            const centerY=(dataList[index].y + dataList[index + 1].y) / 2
            const controX0=(grid_width * index+centerX)/2
            const controY0=(dataList[index].y+centerY)/2
            const controX1=(centerX+ grid_width * (1 + index))/2
            const controY1=(centerY+dataList[index+1].y)/2
            context.bezierCurveTo(controX0+xMoveDistance,controY0+yMoveDistance,controX1-xMoveDistance,controY1-yMoveDistance,grid_width * (1 + index),dataList[index + 1].y)
        }
    }
    context.strokeStyle="rgb(93,111,194)"
    context.lineWidth=2
    context.shadowBlur = 5;
    context.stroke();
    context.closePath();
    context.restore();
}
```
由于时间问题对于参数没有进行详细的调整,当然了X轴之间的间隙太小，所以看着比较尴尬。如果你有时间自己可以参看我之前的[android自定义曲线](https://juejin.cn/editor/drafts/6925686430811291662)博客来一波
![image.png](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/e4e266f38440432b83a3c0420187e827~tplv-k3u1fbpfcp-watermark.image)

### 3、填充的折线图

我们之前搞定了折线和曲线,但下面这种填充如何搞定？如何进行更骚的操作？我们接下来进行探究。

![image.png](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/b38d1188620b46c1a32c56ef18929f67~tplv-k3u1fbpfcp-watermark.image)

我们在之前的基础上进行，我们可以在之前的基础上进行绘制一个封闭的多边形进行填充即可。


```js
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Line</title>
  <script type="text/javascript" src="js/canvas..js"></script>
  <script type="text/javascript" src="js/canvas_fill.js"></script>
</head>

<body>
<canvas id="canvas"></canvas>
<script>
  //region 1.变换rote
  const marginBootom = 50;
  const marginLeft = 40;
  const canvas = document.getElementById("canvas");
  //设置画布的宽高
  canvas.width = 500;
  canvas.height = 300;
  //绘制的对象获取
  const context = canvas.getContext("2d");
  //渐变
  context.strokeStyle = "rgb(0,0,0,1)"
  context.lineWidth = 0.09

  //沿x轴镜像对称变换画布
  context.scale(1, -1)
  //向下平移画布-marginBootom的高度
  context.translate(marginLeft, -canvas.height + marginBootom)

  //绘制X轴和刻度
  drawX(context)
  //绘制文字
  drawText(context)
  //绘制折线和圆
  drawFillLine(context)
  //绘制圆
  drawCircle(context)




</script>

</body>
</html>
```

填充部分代码

```js
function drawFillLine(context) {
    //绘制折线段
    const widthOfOn = (canvas.width - marginLeft) / 7
    const danweiHeight=35/50;//每个数字占用的实际像素高度
    const point00 = Point.createNew(0,150*danweiHeight);
    const point01 = Point.createNew(widthOfOn/2,150*danweiHeight);
    const point02 = Point.createNew(widthOfOn/2+widthOfOn,250*danweiHeight);
    const point03 = Point.createNew(widthOfOn/2+widthOfOn*2,225*danweiHeight);
    const point04 = Point.createNew(widthOfOn/2+widthOfOn*3,211*danweiHeight);
    const point05 = Point.createNew(widthOfOn/2+widthOfOn*4,140*danweiHeight);
    const point06 = Point.createNew(widthOfOn/2+widthOfOn*5,148*danweiHeight);
    const point07 = Point.createNew(widthOfOn/2+widthOfOn*6,260*danweiHeight);


    const points = [point00,point01, point02, point03, point04, point05, point06, point07];
    context.save();
    context.beginPath();
    for (let index = 0; index < points.length; index++) {
        context.lineTo(points[index].x,points[index].y);
    }
    context.strokeStyle="rgb(93,111,194)"
    context.lineWidth=1
    context.shadowBlur = 5;
    context.stroke();
    context.closePath();

    context.beginPath();
    //绘制闭环多边形
    context.moveTo(0,0)
    for (let index = 0; index < points.length; index++) {
        context.lineTo(points[index].x,points[index].y);
    }
    context.lineTo(points[points.length-1].x,0);
    context.lineTo(0,0);
    context.closePath();
    context.fillStyle="rgba(93,111,194,0.5)"
    context.lineWidth=3
    context.shadowBlur = 5;
    context.fill();
    context.restore();


}
```
渐变色的使用让其更具有特点和魅力。当然了我不是一个标准的设计师,美不在于我们,在于设计，一个好的设计应该不会像我一样配色这么丑吧？

![image.png](https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/6566e2902fd741919c60c4fffbd556c7~tplv-k3u1fbpfcp-watermark.image)

![image.png](https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/8c95e1d0d7ba4c7f9e8b954f9cf66406~tplv-k3u1fbpfcp-watermark.image)


![image.png](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/e31a6b4340134a4ead2bc6b51b8ffa4e~tplv-k3u1fbpfcp-watermark.image)

### 3、多条折线图

如下多条折线图,我们搞定了一条还搞不定多条么？只需要同样的操作，只是数据集合不一样罢了。

![image.png](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/2c1cf982313248beada66f05e8a34ae5~tplv-k3u1fbpfcp-watermark.image)

由于时间问题，我们直接在之前的基础上进行操作

```js
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Line</title>
  <script type="text/javascript" src="js/canvas..js"></script>
  <script type="text/javascript" src="js/canvas_fill.js"></script>
</head>

<body>
<canvas id="canvas"></canvas>
<script>
  //region 1.变换rote
  const marginBootom = 50;
  const marginLeft = 40;
  const canvas = document.getElementById("canvas");
  //设置画布的宽高
  canvas.width = 500;
  canvas.height = 300;
  //绘制的对象获取
  const context = canvas.getContext("2d");
  //渐变
  context.strokeStyle = "rgb(0,0,0,1)"
  context.lineWidth = 0.09

  //沿x轴镜像对称变换画布
  context.scale(1, -1)
  //向下平移画布-marginBootom的高度
  context.translate(marginLeft, -canvas.height + marginBootom)

  //绘制X轴和刻度
  drawX(context)
  //绘制文字
  drawText(context)

  function drawMoreLine(context) {
    //绘制折线段
    const widthOfOn = (canvas.width - marginLeft) / 7
    const danweiHeight=35/50;//每个数字占用的实际像素高度
    const point01 = Point.createNew(widthOfOn/2,            200*danweiHeight);
    const point02 = Point.createNew(widthOfOn/2+widthOfOn,  250*danweiHeight);
    const point03 = Point.createNew(widthOfOn/2+widthOfOn*2,225*danweiHeight);
    const point04 = Point.createNew(widthOfOn/2+widthOfOn*3,211*danweiHeight);
    const point05 = Point.createNew(widthOfOn/2+widthOfOn*4,140*danweiHeight);
    const point06 = Point.createNew(widthOfOn/2+widthOfOn*5,148*danweiHeight);
    const point07 = Point.createNew(widthOfOn/2+widthOfOn*6,260*danweiHeight);


    const point011 = Point.createNew(widthOfOn/2,            150*danweiHeight);
    const point012 = Point.createNew(widthOfOn/2+widthOfOn,  200*danweiHeight);
    const point013 = Point.createNew(widthOfOn/2+widthOfOn*2,125*danweiHeight);
    const point014 = Point.createNew(widthOfOn/2+widthOfOn*3,181*danweiHeight);
    const point015 = Point.createNew(widthOfOn/2+widthOfOn*4,90*danweiHeight);
    const point016 = Point.createNew(widthOfOn/2+widthOfOn*5,98*danweiHeight);
    const point017 = Point.createNew(widthOfOn/2+widthOfOn*6,210*danweiHeight);


    const point021 = Point.createNew(widthOfOn/2,            60*danweiHeight);
    const point022 = Point.createNew(widthOfOn/2+widthOfOn,  65*danweiHeight);
    const point023 = Point.createNew(widthOfOn/2+widthOfOn*2,61*danweiHeight);
    const point024 = Point.createNew(widthOfOn/2+widthOfOn*3,70*danweiHeight);
    const point025 = Point.createNew(widthOfOn/2+widthOfOn*4,78*danweiHeight);
    const point026 = Point.createNew(widthOfOn/2+widthOfOn*5,68*danweiHeight);
    const point027 = Point.createNew(widthOfOn/2+widthOfOn*6,72*danweiHeight);


    const points = [point01, point02, point03, point04, point05, point06, point07];
    const point1s = [point011, point012, point013, point014, point015, point016, point017];
    const point2s = [point021, point022, point023, point024, point025, point026, point027];

    context.save();
    context.beginPath();
    for (let index = 0; index < points.length; index++) {
      context.lineTo(points[index].x,points[index].y);
    }
    context.strokeStyle="rgb(93,111,194)"
    context.lineWidth=1
    context.shadowBlur = 5;
    context.stroke();
    context.closePath();




    context.beginPath();
    for (let index = 0; index < point1s.length; index++) {
      context.lineTo(point1s[index].x,point1s[index].y);
    }
    context.strokeStyle="rgb(193,111,194)"
    context.lineWidth=1
    context.shadowBlur = 5;
    context.stroke();
    context.closePath();

    context.beginPath();
    for (let index = 0; index < point2s.length; index++) {
      context.lineTo(point2s[index].x,point2s[index].y);
    }
    context.strokeStyle="rgb(293,111,294)"
    context.lineWidth=1
    context.shadowBlur = 5;
    context.stroke();
    context.closePath();


    context.beginPath();
    for (let index = 0; index < point2s.length; index++) {
      context.lineTo(point2s[index].x,point2s[index].y-15);
    }
    context.strokeStyle="rgb(293,211,194)"
    context.lineWidth=1
    context.shadowBlur = 5;
    context.stroke();
    context.closePath();

    context.beginPath();
    for (let index = 0; index < point2s.length; index++) {
      context.lineTo(point2s[index].x,point2s[index].y-35);
    }
    context.strokeStyle="rgb(93,211,294)"
    context.lineWidth=1
    context.shadowBlur = 5;
    context.stroke();
    context.closePath();
    for (let index = 0; index < points.length; index++) {
      context.beginPath();
      context.arc(points[index].x,points[index].y, 3, 0, Math.PI * 2, true);
      context.closePath();
      context.fillStyle = 'rgb(100,255,255)';
      context.shadowBlur = 10;
      context.shadowColor = 'rgb(100,255,255)';
      context.fill()
    }

    //第一个上面的圆
    for (let index = 0; index < points.length; index++) {
      context.beginPath();
      context.arc(points[index].x,points[index].y, 3, 0, Math.PI * 2, true);
      context.closePath();
      context.fillStyle = "rgb(93,111,194)";
      context.shadowBlur = 10;
      context.shadowColor = "rgb(93,111,194)";
      context.fill()
    }
    //第二条线上面的圆
    for (let index = 0; index < point1s.length; index++) {
      context.beginPath();
      context.arc(point1s[index].x,point1s[index].y, 3, 0, Math.PI * 2, true);
      context.closePath();
      context.fillStyle = "rgb(193,111,194)"
      context.shadowBlur = 10;
      context.shadowColor ="rgb(193,111,194)"
      context.fill()
    }
    //第三条线的圆
    for (let index = 0; index < point2s.length; index++) {
      context.beginPath();
      context.arc(point2s[index].x,point2s[index].y, 3, 0, Math.PI * 2, true);
      context.closePath();
      context.fillStyle = "rgb(293,111,294)"
      context.shadowBlur = 10;
      context.shadowColor ="rgb(293,111,294)"
      context.fill()
    }
    //四...圆
    for (let index = 0; index < point2s.length; index++) {
      context.beginPath();
      context.arc(point2s[index].x,point2s[index].y-15, 3, 0, Math.PI * 2, true);
      context.closePath();
      context.fillStyle = "rgb(293,211,194)"
      context.shadowBlur = 1;
      context.shadowColor ="rgb(293,211,194)"
      context.fill()
    }
    //第五条线上面的圆圈
    for (let index = 0; index < point2s.length; index++) {
      context.beginPath();
      context.arc(point2s[index].x,point2s[index].y-35, 3, 0, Math.PI * 2, true);
      context.closePath();
      context.fillStyle = "rgb(93,211,294)"
      context.shadowBlur = 1;
      context.shadowColor ="rgb(93,211,294)"
      context.fill()
    }

    context.restore();
  }

  //绘制填充折线和圆
  drawMoreLine(context)
</script>

</body>
</html>
```
![image.png](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/495aa1e6fa20475aada0c95b44b086aa~tplv-k3u1fbpfcp-watermark.image)

### 4、多条折线填充图

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;由于时间问题这个就最后一个案例吧。后面的更好的特效案例请期待我的小册,一直在进步写作的路上，希望尽快和大家见面。

分析<br/>
**闭合区域的叠加而已**

![image.png](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/24aa54f7a97b40e79a078f6ac77d285a~tplv-k3u1fbpfcp-watermark.image)


```js
//第一条线闭合区域
    context.beginPath();
    context.moveTo(0,0)
    for (let index = 0; index < points.length; index++) {
      context.lineTo(points[index].x,points[index].y);
    }
    context.lineTo(points[points.length-1].x,0);
    context.closePath();

    context.fillStyle="rgba(93,111,194,0.5)"
    context.lineWidth=11
    context.shadowBlur = 5;
    context.fill();
    context.closePath();
```

![image.png](https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/43bbd73b948c45a8927db36ecb293f98~tplv-k3u1fbpfcp-watermark.image)

差几个文字


```js
//第一条线闭合区域
    context.beginPath();
    context.moveTo(0,0)
    for (let index = 0; index < points.length; index++) {
      context.lineTo(points[index].x,points[index].y);
      //这里由于文字反转所以需要变换坐标系。且为了方便操作每次都将坐标圆点移动到顶点跟家方便的操作
      context.save()
      context.translate(points[index].x,points[index].y)
      context.scale(1,-1)
      context.fillText(points[index].y+"",0,-10)
      //记得文字绘制完成还原坐标系，因为后面还要绘制线，不影响坐标系圆点是左下叫为圆形即可。
      context.restore()
    }
    context.lineTo(points[points.length-1].x,0);
    context.closePath();
```

![image.png](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/1cc9ad13eb044ee3a18d34bddae049a1~tplv-k3u1fbpfcp-watermark.image)

### 5、柱状图案例

群里有提到写柱状图的，下午一看前端大佬们人真的多，写了这篇水文居然这么多人点赞，于是我迫不及待的补上这个柱状图哈哈。非常感谢前端大佬们。第一次写js内容有问题地方多多指出多多见谅。

![image.png](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/2cfb8da86f044c2aa9043ede2fd7979c~tplv-k3u1fbpfcp-watermark.image)

#### 1、绘制X轴和刻度。看代码注释

```js
let marginLeft=80
let marginBootom=100
function translateCanvas(context) {
    //画布变换到左下角。
    context.translate(marginLeft,canvas.height-marginBootom)
    context.scale(1,-1)
}
//绘制X线和刻度等
function drawXLine(context) {
    //绘制X轴
    context.beginPath();
    //起始点
    context.moveTo(0,0)
    //X轴结束点
    context.lineTo(canvas.width-marginLeft*2,0)
    context.closePath();
    context.strokeStyle = 'rgb(0,0,0)';
    context.shadowBlur = 2;
    context.lineWidth=0.1
    context.shadowColor = 'rgb(100,255,255)';
    context.stroke()


    //绘制平行线
    context.save()
    //计算每一份单位宽度
    let heightOne=(canvas.height-marginBootom*2)/7
    for (let index=0; index<8; index++){
        context.beginPath();
        context.moveTo(0,0)
        context.lineTo(canvas.width-marginLeft*2,0)
        context.closePath();
        context.strokeStyle = 'rgb(0,0,0)';
        context.shadowBlur = 2;
        context.lineWidth=0.1
        context.shadowColor = 'rgb(100,255,255)';
        context.stroke()
        context.translate(0,heightOne)
    }
    context.restore()


    //绘制刻度
    context.save()
    //计算每一份单位宽度
    let widthOne=(canvas.width-marginLeft*2)/20
    for (let index=0; index<21; index++){
        context.beginPath();
        context.moveTo(0,0)
        context.lineTo(0,-5)
        context.closePath();
        context.strokeStyle = 'rgb(0,0,0)';
        context.lineWidth=0.1
        context.stroke()
        context.translate(widthOne,0)
    }
    context.closePath()
    context.restore()
}
```
效果如下:

![image.png](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/f82dc981d655462497df488cd0a9e2c6~tplv-k3u1fbpfcp-watermark.image)

#### 2、绘制X轴下面的文字。看代码注释
这里有多一点绘制文字通过measureText进行测量即可如何讲一个文字绘制到刻度中间呢?


![image.png](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/3378e4c49a4548f1955c88553aaa4c08~tplv-k3u1fbpfcp-watermark.image)


```js
let xText=["北京","天津","河北","山西","四川","广东","上海","深圳","江苏","河南","山西",
    "陕西","甘肃","内蒙","天塌","运城","哈尔滨","日本","台湾","香港"]
//绘制底部文字
function drawXDownText(context){
    //绘制刻度
    context.save()
    context.scale(1,-1)
    context.beginPath();
    //计算每一份单位宽度
    let widthOne=(canvas.width-marginLeft*2)/20
    for (let index=0; index<xText.length; index++){
        const textWidth = context.measureText(xText[index]);
        //计算文字的文字，自己画图看看很简单就是相对位置剪来剪去
        context.strokeStyle = 'rgb(111,11,111)';
        context.fillText(xText[index],widthOne/2-textWidth.width/2,textWidth.emHeightAscent)
        context.stroke()
        context.translate(widthOne,0)
    }
    context.restore()


    //绘制Y轴左边的文字
    context.save()
    //这里很重要,为了字体不反转
    context.scale(1, -1)
    context.translate(-30, 0)
    context.font = "7pt Calibri";
    let heightOne=(canvas.height-marginBootom*2)/7
    //Y轴左边绘制文字
    for (let i = 0; i < 8; i++) {
        //画不是闭合区域 fill是闭合区域
        context.stroke()
        //测量文字
        const textHeight = context.measureText((3000 * i).toString());
        //设置文字绘制的位置
        context.fillText((3000 * i).toString(), 0, textHeight.emHeightAscent / 2);
        //每次绘制完之后继续往上平移
        context.translate(0, -heightOne)
    }
    context.restore()


}
```

![image.png](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/5c348aae1e2248c19c503a8ee3fb115f~tplv-k3u1fbpfcp-watermark.image)

#### 3、绘制巨型和造数据
⭐️⭐️⭐️⭐️⭐️⭐️这里比较重要的一点，评论区也提到了，如何将实际的数据于坐标系结合。例如我们实际的数据来自于后台都是几千几万。而我们的坐标系高度紧紧500px。其实简单的运算也就是一个单位的数字占实际像素多高danwei=500/最大值(例如2000)即可。那12000*danwei就是12000应该在实际画布中的位置。


```js
let datas=[[100,2800,9000],[150,2900,600],[300,12000,400],[500,13333,4000],[1300,2000,122],[111,3333,1111],[1111,2111,1111],[111,1611,222],[444,4444,333],[222,11111,2222],[2222,2235,11],[111,1345,1111],[1111,11111,2234],[1122,12223,12],[121,1665,111],[234,334,21]
    ,[112,12134,1211],[1212,12111,134],[124,2021,112],[1222,20345,1212],[1412,17771,1111],[111,12222,1111],[1123,121333,1111],[11112,11212,111],]
//绘制巨型等条状物
function drawRect(context) {
    //绘制刻度
    context.save()
    context.beginPath();
    //计算每一份单位宽度
    let widthOne=(canvas.width-marginLeft*2)/20
    let widthOneRect=widthOne/3
    let heightOne=(canvas.height-marginBootom*2)/7
    let danwei=heightOne/3000
    for (let index=0; index<xText.length; index++){
        //计算文字的文字，自己画图看看很简单就是相对位置剪来剪去
        context.fillStyle = 'rgb(189,119,119)';
        context.fill()
        //第一个条纹
        context.fillRect(0,0,widthOneRect-1,datas[index][0]*danwei)
        context.fillStyle = 'rgb(19,172,172)';
        //第二个条纹
        context.fillRect(widthOneRect,0,widthOneRect-1,datas[index][1]*danwei)
        context.fillStyle = 'rgb(111,73,142)';
        //第三个条纹
        context.fillRect(widthOneRect*2,0,widthOneRect-1,datas[index][2]*danwei)
        context.translate(widthOne,0)
    }
    context.restore()
}
```

![image.png](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/f85bf1b249074e6bb77534c6863db799~tplv-k3u1fbpfcp-watermark.image)

后面有时间会多补上其他的.....

### 5、雷达系列图
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;如果上面你都按照我敲下来,我想自定义对你来说不再是难事,下面我们通过案例来看看自定义简单的API加初中简单的数学计算能给我们带来什么呢?
![image.png](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/1f185f8f1781452aa1c30d4c49aa1a60~tplv-k3u1fbpfcp-watermark.image)
#### 绘制之前的分析<br/>
**坐标变换到屏幕中心带来的方便**<br/>
**绘制多条骨架线段**<br/>
**如何实际数据映射到屏幕中**<br/>
**连线填充完成**<br/>
#### 1、坐标变换
如上图,如果圆点在屏幕中心会带来很方便的操作。直接上代码....不清楚看上面的坐标变换部分
```js
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>雷达图</title>
</head>
<body>
<canvas id="canvas" style="background: black"></canvas>
</body>
<script>
    const canvas = document.getElementById("canvas");
    canvas.width = 831;
    canvas.height = 706;
    //绘制的对象获取
    const context = canvas.getContext("2d")
    context.translate(canvas.width/2,canvas.height/2)
    context.scale(1,-1)
    //绘制圆
    context.arc(0,0,50,0,Math.PI*2,true)
    context.strokeStyle="rgb(189,142,16)"
    context.stroke()

</script>
</html>
```

![image.png](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/016d364778324793b85962909dda4667~tplv-k3u1fbpfcp-watermark.image)

#### 2、绘制多条骨架线段
我们看到总共有三条骨架直线将屏幕分为`六等分`,我们可以简单的求出三条线段的方程式吧？初中的数学我相信你能明白。<br/>

Y<sub>x<sub>=-tan30*x<br/>

Y<sub>x<sub>= tan30*x<br/>

![image.png](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/1f185f8f1781452aa1c30d4c49aa1a60~tplv-k3u1fbpfcp-watermark.image)

```js
 let y1= Math.tan(Math.PI/180*30)*(-300)
    let y2= Math.tan(Math.PI/180*30)*300
    context.moveTo(-300,y1)
    context.lineTo(300,y2)
    context.closePath();
    context.strokeStyle="rgb(189,142,16)"
    context.stroke()
```

![image.png](https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/d92d9552efad49789999af8e4df49d5c~tplv-k3u1fbpfcp-watermark.image)

补全了

```js
 context.beginPath();

    //左边一条骨架线段
    let y1= Math.tan(Math.PI/180*30)*(-300)
    let y2= Math.tan(Math.PI/180*30)*300
    context.moveTo(-300,y1)
    context.lineTo(300,y2)
    context.strokeStyle="rgb(189,142,16)"
    context.stroke()

    //中间骨架线
    context.moveTo(0,300)
    context.lineTo(0,-300)


    //右边一条骨架线段
    let y11= -Math.tan(Math.PI/180*30)*(-300)
    let y22= -Math.tan(Math.PI/180*30)*300
    context.moveTo(-300,y11)
    context.lineTo(300,y22)
    context.strokeStyle="rgb(189,142,16)"
    context.stroke()
    context.closePath();
```

![image.png](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/7f1695854de042688bcc353573e51ac2~tplv-k3u1fbpfcp-watermark.image)

发散的圆

```js
  for (let i = 0; i < 6; i++) {
        context.beginPath();
        //绘制圆
        context.arc(0,0,50*(i+1),0,Math.PI*2,true);
        context.strokeStyle="rgb(189,142,16)";
        context.stroke();
        context.closePath();
    }
```

![image.png](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/03930b7374a247449664b2feab60fcce~tplv-k3u1fbpfcp-watermark.image)
#### 3、如何实际数据映射到屏幕中
同样我们圆的半径可以看做是各个骨架坐标轴的长度,而我们实际数据是长度数据而已如何将长度数字映射到各个不规则的骨架坐标轴上呢？当然还是离不开简单的数学。
例如我们一个数字250如下图两个白色虚线相交地方。我们实际的250代表的是圆点到焦点部分的长度。但是我们需要在坐标系中定位那就需要求出(x,y)在坐标系中的虚拟坐标。同样的简单的初中数学,不难得出（x,y）=(length*cson30,lenght*sin30),如果你细心分析每个骨架坐标轴上的所有坐标都满足（x,y）=(length*cson30,lenght*sin30)。接下来我们上代码看效果

![image.png](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/1f185f8f1781452aa1c30d4c49aa1a60~tplv-k3u1fbpfcp-watermark.image)


```js
 //绘制网线填充
    const datas = [[70, 100, 20, 5, 21, 99],[100, 120,50, 75, 121, 99],[117,211,259,232,190,200],[217,240,259,282,190,120]];
    for (let i = 0; i < datas.length; i++) {
        for (let index=0;index<datas[i].length;index++){
            context.beginPath()
            //右上角开始顺时针开始绘制
            context.lineTo(datas[i][0]*Math.cos(Math.PI/180*30),datas[i][0]*Math.sin(Math.PI/180*30))
            context.lineTo(datas[i][1]*Math.cos(Math.PI/180*30),-datas[i][1]*Math.sin(Math.PI/180*30))
            context.lineTo(0,-datas[i][2])
            context.lineTo(-datas[i][3]*Math.cos(Math.PI/180*30),-datas[i][3]*Math.sin(Math.PI/180*30))
            context.lineTo(-datas[i][4]*Math.cos(Math.PI/180*30),datas[i][4]*Math.sin(Math.PI/180*30))
            context.lineTo(0,datas[i][5])
            context.fillStyle="rgba(189,142,16,0.09)"
            context.fill()
            context.closePath();
        }
    }
    //绘制网线边缘线条
    for (let i = 0; i < datas.length; i++) {
        for (let index=0;index<datas[i].length;index++){
            context.beginPath()
            //右上角开始顺时针开始绘制
            context.lineTo(datas[i][0]*Math.cos(Math.PI/180*30),datas[i][0]*Math.sin(Math.PI/180*30))
            context.lineTo(datas[i][1]*Math.cos(Math.PI/180*30),-datas[i][1]*Math.sin(Math.PI/180*30))
            context.lineTo(0,-datas[i][2])
            context.lineTo(-datas[i][3]*Math.cos(Math.PI/180*30),-datas[i][3]*Math.sin(Math.PI/180*30))
            context.lineTo(-datas[i][4]*Math.cos(Math.PI/180*30),datas[i][4]*Math.sin(Math.PI/180*30))
            context.lineTo(0,datas[i][5])
            context.strokeStyle="rgb(189,142,16)"
            context.stroke()
            context.closePath();
        }
    }

```

![image.png](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/674165eb12d04cf6aa69571da11cf7a0~tplv-k3u1fbpfcp-watermark.image)

# 掘金文字限制,会另起篇章!!!!!

# 五、总结
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;对于我一个基本没使用过HTML5和JS移动端人员来说一天的功夫就能够完成这些内容。对于前端的大佬们来说简单不过来,当然了奇怪的是我也问过很多前端开发人员,对于自定义也是一知半解,不够深入，当我问起图表，ECharts总是频频出口，可能有些公司的UI不是太严格，开发基本在Echarts里面寻找类似图表或者设计人员直接基于ECharts进行选择设计,可能是种种原因国内的UI基本趋向于同一,技术在变革,UI设计也应该别具一格，有所特色。当然了我们最好有自定义的能力岂不更好？当你遇到不常见的设计你可以随心所欲，那是一件多么美好的事情。

我想下面这些图表,无非巨型、弧度、等加画布变换、填充渐变、文字绘制吧？是时候展示你的技术了
![image.png](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/5346b292bbeb4f2f9a483dac6c705ae1~tplv-k3u1fbpfcp-watermark.image)

![image.png](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/7e36747a7d104fce875781b2931b87e4~tplv-k3u1fbpfcp-watermark.image)

当然了[ECharts](https://echarts.apache.org/examples/zh/index.html)里面有很多自定义的内容。如果你认真手敲了这篇文字，你就应该对于自定义内容胸有成竹。至于好的操作当然离不开手势和动画，后面我们来开始手势加动画来逐渐过渡到`K线`，没错就是K线。<br/>

![k线图](https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/7c6f30d394e2480b8f061be4cd2a9e61~tplv-k3u1fbpfcp-watermark.image?imageView2/2/w/480/h/480/q/85/interlace/1)
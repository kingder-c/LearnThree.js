# 坐标系
Threejs使用的是右手坐标系，这源于opengl默认情况下，也是右手坐标系。
![坐标系](http://ouewomi2z.bkt.clouddn.com/17-8-10/4596474.jpg)


# WebGL中的点线面
线条的深入理解

在Threejs中，一条线由点，材质和颜色组成。

点由THREE.Vector3表示，Threejs中没有提供单独画点的函数，它必须被放到一个THREE.Geometry形状中，这个结构中包含一个数组vertices，这个vertices就是存放无数的点（THREE.Vector3）的数组。这个表示可以如下图所示：three.js向量

![点的存储方式](http://ouewomi2z.bkt.clouddn.com/17-8-10/68130906.jpg)

为了绘制一条直线，首先我们需要定义两个点，如下代码所示：
```
var p1 = new THREE.Vector3( -100, 0, 100 );

var p2 = new THREE.Vector3( 100, 0, -100 );
```
请大家思考一下，这两个点在坐标系的什么位置，然后我们声明一个THREE.Geometry，并把点加进入，代码如下所示：

var geometry = new THREE.Geometry();

geometry.vertices.push(p1);

geometry.vertices.push(p2);

geometry.vertices的能够使用push方法，是因为geometry.vertices是一个数组。这样geometry 中就有了2个点了。

然后我们需要给线加一种材质，可以使用专为线准备的材质，THREE.LineBasicMaterial。

最终我们通过THREE.Line绘制了一条线，如下代码所示:

var line = new THREE.Line( geometry, material, THREE.LinePieces );

ok，line就是我们要的线条了。
6、画高中时深爱的坐标平面

我还深爱着高中时的那个坐标平面，它勾起了我关于前排同学的细细长发的回忆…

这个平面的效果如下所示：three.js画坐标系

它横竖分别绘制了20条线段，在摄像机的照射下，就形成了这般模样。
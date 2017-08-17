# 1.使用Three.js渲染导出的DAE

在Three.js中使用Collada(即.dae)文件的话，首先得要用到 ColladaLoader.js。

官方参考文档：#Reference/Loaders/ColladaLoader

但是这个ColladaLoader.js并不包含在three.js文件里面，需要你自己下载然后添加进来。

这个文件中three.js的repo里面的examples/js/loaders/ColladaLoader.js

如果你检出了three.js的源代码的话，在上面的位置就可以找到这个文件了。

然后在你的html里面载入这个文件就可以了。

 

其实一开始照着官方的文档去加载和展示dae是显示不出来的，

搜索了很多相关知识后才找到如下方式可以显示出来，

可能是camera视角原因和光照原因。

最后可以正常显示的页面主文件如下：
```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="utf-8">
    <title>Roulette</title>
    <style type="text/css">
        body {
            margin: 0;
        }
        canvas { width: 100%; height: 100% }
    </style>
    <script type="text/javascript" src="js/three.js"></script>
    <script type="text/javascript" src="js/ColladaLoader.js"></script>
    <script src="js/OrbitControls.js"></script>
    <script src="js/pumpStation1.js"></script>
</head>
<body onload="startGame();">

</body>
</html>
```

Js文件
```
var scene, camera, renderer, daeModel;

//初始化场景
function initScene() {
    scene = new THREE.Scene();
}

//初始化摄像机
function initcamera(){
    aspect = 980/ 490;
    D = 8;
    camera = new THREE.OrthographicCamera(-D*aspect, D*aspect, D, -D, 1, 1000);
    //camera = new THREE.PerspectiveCamera(75, window.innerWidth/window.innerHeight,0.1,200)
    camera.position.set( 300, -300, 300 );
    camera.lookAt( new THREE.Vector3( 0, 0, 0 ) );
    camera.up.x = 0;
    camera.up.y = 0;
    camera.up.z = 1;
    //camera.rotation.z = 1 / 6 * Math.PI;
    //camera.rotation.z = 5/6*Math.PI;
}
function initthree() {
    renderer = new THREE.WebGLRenderer();
    renderer.setSize( 980, 490 );
    renderer.setClearColor( 0xffffff );
    document.body.appendChild( renderer.domElement );
    /*
        var spotLight = new THREE.SpotLight( 0xffffff );
        spotLight.position.set( 100, 1000, 100 );
    
        spotLight.castShadow = true;
    
        spotLight.shadow.mapSize.width = 1024;
        spotLight.shadow.mapSize.height = 1024;
    
        spotLight.shadow.camera.near = 500;
        spotLight.shadow.camera.far = 4000;
        spotLight.shadow.camera.fov = 30;
    
        scene.add( spotLight );
    */
}

function initlight() {
    var light = new THREE.DirectionalLight( 0xffffff, 2 );
    light.position.set( 300, -300, 200 );
    scene.add( light );
}

function LoadModel() {
    var loader = new THREE.ColladaLoader();
    loader.load( "./model/pumpStation1.dae", function ( collada ) {
        daeModel = collada.scene;
        daeModel.scale.set( 0.1, 0.1, 0.1 );
        daeModel.position.set( -6, 0, 0 );
        scene.add( daeModel );
        //参考坐标轴
        var axisHelper = new THREE.AxisHelper(500);
        scene.add(axisHelper);
    },
    function ( xhr ) {
        console.log(( xhr.loaded / xhr.total * 100 ) + "% loaded" );
    } );
}

//初始化渲染器
function render() {
    requestAnimationFrame( render );

    renderer.clear();

    renderer.render( scene, camera );
    //if( daeModel ){
    //    daeModel.rotation.z++;
    //}
}

var Controls;
// 初始化控制器
function initControls() {
    Controls = new THREE.OrbitControls( camera );
}

function startGame(){
    console.log('Load Model started...');
    initScene();
    initcamera();
    initthree();
    initlight();
    LoadModel();
    render();
    initControls();
    
}
```
图片显示效果如下图所示
![](http://ouewomi2z.bkt.clouddn.com/17-8-17/56919267.jpg)



其中的这一段代码是用来控制鼠标拖动模型旋转的
```
var Controls;
// 初始化控制器
function initControls() {
    Controls = new THREE.OrbitControls( camera );
}
```

必须在主页中引用这个脚本

`<script src="js/OrbitControls.js"></script>`
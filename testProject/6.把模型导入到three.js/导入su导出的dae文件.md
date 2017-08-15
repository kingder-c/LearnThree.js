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

最后可以正常显示的主文件如下：
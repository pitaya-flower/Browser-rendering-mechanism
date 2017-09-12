# Browser-rendering-mechanism
浏览器渲染机制
大体分为以下步骤：
1.解析HTML标签，构建DOM树。
2.解析CSS标签，构建CSSOM树。
3.把DOM和CSSOM组合成渲染树（render tree）。
4.在渲染树的基础上进行布局，计算每个节点的几何结构。
5.把每个节点绘制到屏幕上（painting）。

DOM：Document Object Model，浏览器将HTML解析成树形的数据结构，简称DOM。CSSOM：CSS Object Model，浏览器将CSS解析成树形的数据结构，简称CSSOM。Render Tree: DOM和CSSOM合并后生成Render Tree

![4648608-1286ed541be5bae1.png](http://upload-images.jianshu.io/upload_images/7279690-da76f0e931f114e6.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

Layout: 计算出Render Tree每个节点的具体位置。
Painting:通过显卡，将Layout后的节点内容分别呈现到屏幕上。
下面我们来说说具体的流程。
当浏览器获得html文件后，会自上而下的加载，并在加载过程中进行解析和渲染。 加载说的就是获取资源文件的过程，如果在加载的过程中，遇到外部css文件和图片，浏览器会另外发出一个请求，来获取css文件和相应的图片，这个请求是异步的，并不会影响html文件。 但是如果遇到javascript文件，html文件会挂起渲染的线程，等待javascript加载完毕后，html文件再继续渲染。因为javascript可能会修改DOM，导致后续的html资源白白加载，所以html必须等待javascript文件加载完毕后，再继续渲染。这也就是为什么javascript文件要写在底部body标签前的原因。html的渲染过程就是将html代码按照深度优先遍历来生成DOM树。 css文件下载完后也会进行渲染，生成相应的CSSOM。 当所有的css文件下载完且所有的CSSOM构建结束后，就会和DOM一起生成Render Tree。 接下来，浏览器就会进入Layout环节，将所有的节点位置计算出来。 最后，通过Painting环节将所有的节点内容呈现到屏幕上。当然，每个浏览器对于渲染的实现机制都不相同，比如说chrome会在一开始就将不影响DOM结构的javascript也异步加载从而进一步提高性能等。

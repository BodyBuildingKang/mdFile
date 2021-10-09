# 优化相关前提



### 游戏安装包大，运行卡

1. U3D内置了Mono虚拟机，所以可以跨平台

2. U3D(开发) --->>> Mono --->>> 操作系统

### DrawCall是如何影响性能的

 1. DrawCall就是CPU对图形绘制接口的调用，CPU通过调用图形库(direct/opengl)接口，命令GPU进行渲染操作

 2. DrawCall造成卡顿最大元凶是CPU对图形库命令的频繁调用，造成GPU忙不过来，以至于卡顿

 3. 每次一次的绘制渲染，CPU需要准备检测渲染状态，提交渲染所需要的的数据，提交渲染所需要的状态

 4. 当DrawCall过多，CPU会额外开销用于准备工作，导致GPU可能处于空闲状态。

     1. 例： 拷贝1000个总大小1M的文件和单个大小为1M的文件，明显拷贝1000个文件要慢很多，DrawCall调用跟这个类似

        

### DrawCall优化：  减少DrawCall

1. 批处理思想： 尽量把小的DrawCall合并到一个大的DrawCall里去
2. 批处理注意点： 合并网格最好是同材质，同贴图，同shader，同网格定点格式
3. 避免使用大量小的网格，如必要时，要考虑是否要合并
4. 避免使用过多的材质，尽量共享材质
5. 合并尽量在编辑器下进行合并(合并也是需要计算的)
6. 合并时将动态和静态的物体分开：静态的合并一次即可，动态只要有物体发生变换就要重新合并



### Unity --- Profiler

看官方文档  http://docs.unity3d.com/Manual/Profiler.html

### Unity Statistics统计面板

	 1. FPS :  不能低于30帧率(越高越好)
	 2. CPU：main  进行时间计算的绝对值(越低越好) 
	 3. render thread(GPU) : GPU计算时间(越低越好) 
	 4. Batches: 批处理 （Unity内置的优化： 把DrawCall进行合并成一次，进行批次处理）
	 5. Verts:  摄像机内的顶点个数
	 6. Tris： 摄像机内的三角面个数
	 7. SetPass calls：渲染通道(GPU得到渲染请求把指令发送给对应物体的shader上，让其读取指令并通知相应的渲染通道进行渲染操作)



# 资源优化



### 资源优化标准

#### Mesh

	1. Mesh动态模型面片数 <= 3000
	2. 材质球 < 3
	3. 骨骼数 < 50
	4. 静态模型顶点数 < 500

#### Audio

   1. 长时间音乐(背景音乐) 压缩格式 MP3 (不是频繁加载)  ----- 减少包的大小

      ​    **https://blog.csdn.net/u012565990/article/details/51794486?spm=1001.2014.3001.5501**

          1. 导入文件的类型 Load Type ：
             1. Decompress On Load
             2. Compressed In Memory
             3. Streaming

   2. 短时间音乐(音效) 非压缩格式  wav  

#### Texture

 	1. 贴图长款 < 1024

#### Shader

	1. 尽量减少复杂数学运算
	2. 减少discard操作

### 模型优化

​	1. 减少面数，顶点数

### 贴图优化

​	1. 贴图 材质合并 --->>> 减少DrawCall的调用  

### 如何减少冗余资源和重复资源

	1. Resources目录下的资源不管是否被引用，都会被打进包里； 不使用的资源不要放在Resources目录下
	2. 不同目录下的相同资源文件，如果都被引用，那么都会被打进包里，造成冗余
	3. 保证同一个资源文件在项目中只存放在一个目录位置

### 资源监测与分析

​	1. https://www.uwa4d.com/product.html?t=RC

# 渲染优化(GPU)



	1. CPU/GPU分工 ------------ https://www.zhihu.com/question/21475727
	2. LOD 技术 （LOD Group）： 层级细节（根据距离显示） -------------- **在LOD2和LOD1可以修改贴图的品质，** **Cast Shadow和Receive Shadow可以移除**
	3. Occlusion Culling -- 遮挡剔除
	4. Lightmapping - 光照贴图
	5. 合并Mesh



# 代码优化(CPU)

### 资源池 -=-- Object Pooling





# 其他优化



### 优化工具

​	1. UWA Game Optimization Toolkit



### 文章

	1. [使用Unity开发安卓游戏，应该如何进行性能优化](https://gameinstitute.qq.com/community/detail/105016)



### 编辑性能优化

	1. [Unity加快代码编译速度](http://www.xuanyusong.com/archives/4474)































​	


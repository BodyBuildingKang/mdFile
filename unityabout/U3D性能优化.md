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

# 优化策略

## 一：遮挡剔除（Occlusion Culling）

1.当场景中包含大量模型时，造成渲染效率的降低（即帧速率FPS的降低），采用遮挡剔除技术，可以使得那些被阻挡的物体不被渲染提高渲染效率

2.原理：在场景空间中创建一个遮挡区域，该遮挡区域是有单元格（Cell）组成；每个单元格是构成整个场景遮挡区域的一部分，这些单元格会把整个场景拆分成多个部分，当摄像机能够看到该单元格时，表示该单元格的物体会被渲染出来，其他的不去渲染

3.遮挡剔除步骤：

(1)场景

(2)除了主角，摄像机，直线光，地面。把层级视图中的所有游戏对象标记为“遮挡静态”（Occluder Static/Occludee Static）

(3)执行菜单命令“Windows”—>“Occlusion Culling”,弹出“遮挡剔除”面板，单击下方的“Back”按钮，开始烘焙

(4)单击“遮挡剔除”（Occlusion）窗口的“Visualizatior”，运行程序

4.若场景中存在大量的小“物件”，使用“层消隐距离”来优化场景

(1):原理：较远距离将小物件剔除，减少绘图调用的数量

(2):方法：将小物件放入一个单独的层（Separate  Layer）中，并使用Camera.main.layerCullDistances函数设置层的消隐距离

(3)例如：void Start(){

​         Float[] distances=new float[32];

​         //这里定义的数组下标“8”表明第8层

​         distances[8]=10；

​         Camera.main.layerCullDistances=distances;

​    }

当摄像机距离这些小物件超过10m的时候，就不可见了

## 二：层级描述（LOD）

1.原理：当一个物体离摄像机远时使用复杂度底的模型，当物体离摄像机比较近时使用复杂度较高的模型，所以一定要制作好各个层级的模型，并按“模型名称_LOD0”“模型名称_LOD1”等；最后的数字序号越低表示复杂程度越高，这样的命名规则使Unity能够自动的为模型添加LOD组（LODGroup）

2.步骤:

(1)：新建一个空的游戏对象，命名为_LOD，并给它添加LODGroup组件

(2)：分别将游戏对象退拽到_LOD空对象的LODGroup组件的各个级别上

(3)：选中视图中的_LOD下的游戏对象将它们Reset

(4)：拖动摄像机改变距离就会发现，图形会随着摄像机距离改变而改变

## 三：项目调优工具数据分析器（Profiler）

提供了系统更加详细、具体的性能动态监测

1.CPU使用情况（CPU Usage）

2.GPU使用情况（GPU Usage）

3.系统渲染（Rendering）

4.内存（Memory）

5.音频（Audio）

6.3D物理（Physics 3D）

7.2D物理（Physics 2D）

8.脚本调用

##  四：项目优化策略

### 1.Draw Call

原理：一个模型的数据经过CPU传输到GPU,并命令GPU进行绘制，称为一个Draw Call

降低Draw Call的原理：基于Draw Call 是CPU调用底层图形接口，主要工作量就是尽量减少CPU在调用图形接口上的开销而努力。

降低Draw Call的思路：每个游戏对象尽量减少渲染的次数，多个游戏对象尽量一起渲染

降低Draw Call的主要途径：

####	(1):Draw Call 批处理技术(Draw Call Batching)

核心：在可见性测试之后，检查所有要绘制的对象材质，把相同材质分为一组，然后把它们组合成一个对象，这样一次Draw Call就可以处理对个对象

动态批处理：完全自动进行

静态批处理：需要指出哪些是静态的，再属性窗口中将“Static”复选框勾选

####	(2)：使用图集(Texture Packing 或者Texture Atlasing)减少材质的使用

尽量减少场景中使用的材质数量，尽量共享材质，对于仅纹理不同的材质，可以把纹理组合到一张更大的纹理中(称为图集Texture Packing 或者Texture Atlasing),然后把不会移动的物体标记为“Static”

####	(3):尽量减少使用反光，阴影，因为那会使物体多次渲染

####	(4)：视锥体合理剪辑(Frustum Culling )

 视锥体合理剪辑是Unity内建的功能，一般来说，对于大型场景中的大量游戏对象进行合理的分层，对于大型建筑物使用较大裁剪距离，而对于小游戏对象可以使用较小裁剪距离，场景中的粒子系统等可以使用更小的裁剪距离

####	(5) 遮挡剔除方法

####	(6)  网格渲染器

 只有处于摄像机视锥体内，且添加了网格渲染器（Mesh Renderer）组件的对象才会产生渲染的开销，其他不产生，这样我们可以对暂时无需显示的游戏对象通过脚本的方式进行控制，不进行渲染，需要的时候再渲染即可

#### (7) 减少游戏对象的缩放

 统一缩放的对象不会与非统一缩放的对象进行批处理

#### (8) 减少多通道Shader的使用

 多通道的Shader会妨碍批处理操作：几乎Unity中所有的着色器在前向渲染中都支持多个光源，因为它们开辟多个通道，所以对批处理有影响

#### (9) 脚本访问材质的方法

 如果需要脚本访问复用材质属性，如使用Renderer.material改变贴图，则将会造成一份材质。因此一般使用Renderer.ShaderMaterial来保证材质的共享状态

#### (10) 尽量多使用预设

 使用预设生成的对象会自动的使用相同的网格模型和材质，因此会自动被批处理

###  2.模型与图形方面

####  (1) 模型优化

 		A : 模型几何体的优化：模型的顶点、三角形面片数目等不要太多，如果可能，把相邻的对象(网格)合并为一个，且只用一个材质的对象(网格)

​		B : 蒙皮动画模型优化：主要针对添加骨骼的模型，建议在Unity中的每一个角色仅使用一个蒙皮网络渲染器来绘制，这样Unity会使用可见性裁剪和包围体更新的方法来优化角色的运动

​		C : 压缩面片(Mesh):模型导入后最好打开“Mesh Compression”、“Off”、“Low”、“Medium”、“High”这几项，具体分析，酌情选择。

​		D : 避免大量使用Unity自带的Sphere等内建游戏对象

####  (2) 贴图(纹理)优化

​	 A:使用贴图压缩优化

 	B:贴图压缩格式选择：不透明贴图的压缩格式为ETC4bit，透明贴图的格式，选择RGBA16bit或者RGBA32bit

 	C:选择支持Mipmap减少内存带宽需求

####  (3) 材质

 	尽量合并使用同贴图的材质球，合并使用相同材质球的对象，建议使用纹理图集，尽量减少AlphaTest和AlphaBlend材质的使用

####   (4) (模型)碰撞体

 	尽量不要使用MeshCollider，如果避免不了，尽可能的减少Mesh的面片数，或用较少的面片的代理体来代替

####  (5) 粒子系统

 	屏幕上的最大粒子数建议小于200，每个粒子发射器发射的最大粒子数建议不超过50个，粒子Size尽可能的小，对于非常小的粒子，建议粒子纹理去掉Alpha通道，尽量不要开启粒子的碰撞功能

####  (6) 其他

 	A:建议场景中尽可能多的使用预设体，尽可能多的使用预设的实例化以降低内存带宽的负担

 	B:建议将非均匀缩放都改为均匀缩放，不要在静态物体上附加Animation组件

###  3.光照与摄像机方面

####  (1) 渲染途径

​	决定灯光和阴影在场景中的计算方法，不同的渲染途径具有不同的性能特性和渲染效果，unity提供了3中渲染途径：

 			顶点光照:最低保真度光照，不支持实时阴影，只对所有对象渲染一遍

​			 前向渲染:基于着色器的渲染途径，系统默认的综合平衡选项

 			延时光照：具有较高的保真度和真实感的渲染途径，如果要开发绚丽多彩具有较多实时灯光与阴影效果的场景时，采用此种渲染

 	摄像机关于渲染途径的选项：“File”—>“Building Setting”—>“Player Setting”—>“Other Setting”中进行设置

####  	(2) 光照与阴影方面

 	像素的动态光照将对顶点变换增加显著的开销，对于静态物体，采用“光照烘焙”.如果硬阴影可以解决就不要用软阴影，允许的话在大场景中使用线性雾，实时阴影开销大，，阴影的显示距离设置：“Edit”—>“Project Setting”—>“Quality”中进行设置

####  	(3) 摄像机技巧

​	 我们可以根据距离来设置要显示的物体，根据设置层来设置距离

###  4. 程序优化方面

####  	(1) 程序整体优化方面

 	A:我们要删除脚本中为空或者不需要的默认方法，尽量少在Update里面做事情，脚本不用时把它禁用掉(Deactive)

​	 B:尽量不使用原生态的GUI方法，而是使用UGUI或者NGUI来代替

 	C:尽量的隐藏/显示或者实例化来回的切换对象，尽量少用SetActiveRecursively或Active，而是改为将对象移除相机范围和移回原位的做法，也可以选择使用脚本的方式开启与关闭游戏对象的“Mesh Renderer”组件来进行优化

 	D:不要频繁的获取组件，将其声明为全局变量

 	E:脚本不使用时禁用它，需要时再开启

 	F:尽量直接声明脚本变量，而不使用GetComponent来获取脚本

 	G:尽量少的使用Update、LateUpdate、FixedUpdate等每帧都处理的函数

 	H:使用C#中的委托与事件机制，比使用SendMessage机制效率更高

####  	(2) 事件函数方面

 	A:按照脚本生命周期的原理，对于“协程”与“调用函数”，一般在脚本禁用的时候，“协程”与调用函数，不会自动调用，需要使用脚本写明标识禁用，否者会出现空转现象，耗费资源

 	B:同一脚本中频繁使用的变量与脚本之间频繁调用的变量或方法，建议声明为全局的

 	C:尽量避免每帧处理，可以每隔几帧处理一次。

 	D:可以使用协同或者调用函数来代替不必每帧都执行的方法

 	E:避免在Update或者FixedUpdate中使用搜索方法

####  	 (3) 数学计算方面

 尽量使用int类型来代替float类型，尽量少用复杂的数学函数，改除法为乘法，尽量少用模运算和除法运算

####  	 (4) 垃圾回收机制

 	A:尽量主动回收垃圾

 	B:垃圾回收的时机：尽量放在游戏场景的加载和场景结束的时候主动卸载资，在战斗中不要主动卸载，否者造成非连续性卡顿等

 	C:避免频繁分配内存:应该经常重复使用数组合其他对象，不能分配新的数组或对象，采用“游戏对象缓存技术”提高系统效率

 	D:在较大场景中，距离摄像机较远的游戏对象可以将GameObject上不必要的脚本禁用(Disable)掉，如果需要开启，则再使用GameObject.setctive（）开启等，这样也可以配合事件中的OnBecameInvisible（）（当变为不可见）和OnBecameVisible（）(当变为可见)使得游戏对象在不可见的时候自动禁用，可见的时候再开启

 	E:善于使用OnBecameInvisible（）和OnBecameVisible（），控制物体Update（）函数的执行减少开销

 	F:资源预加载技术的运用。资源预加载技术就是以空间换取时间的方法，正式进入战斗场景前，可以在关卡之间的“战绩统计场景”中进行“预加载”操作（一般常用“协同”进行加载），这样游戏不会出现卡顿等现象

###   5. Unity系统设置方面

####  	(1) 限帧措施

​	在一手机为代表的移动设备上运行游戏，主动减少“帧速率”（FPS）可以显著地减少发热和耗电，以及稳定游戏FPS,减少出现卡顿的情况:	 “Edit”—>“ProjectSetting”—>“Quality”中的“VSync Count”参数会影响FPS,

####  	(2) 物理性能优化

 	A:增加固定时间步长：“Edit”—>“ProjectSetting”—>“Time”中调整FixedTimestep参数

 	B:设置“最大允许时钟步调”：物理计算和FixedUpdate（）执行不会超过该指定的时间

 	C:设置“时间缩放因子”：值为1游戏正常进行，值为0暂停允许，值为2游戏运行时间加快2倍，值为0.5则运行时间减慢到一半

####  	(3) 调整像素光数量

 	像素光可以让你的游戏看起来效果绚丽多彩，但是不要使用过多，可以使用质量管理器来调节像素光的数量

###  	6. 良好的开发与使用习惯

​	(1) 养成良好的标签(Tags)、层次(Hierratchy)和图层(Layer)的条理化习惯

​	(2) 项目研发过程中养成经常通过Stats和Profile查看对效率影响最大的方面或对象，或者是禁用部分模型的方法查看问题到底在哪里而不是项目发布后再进行这一步

 



























​	


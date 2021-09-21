DOD： Date Original Design 面向数据设计

1. 种数据驱动的设计。变得更加单纯纯粹



DOTS： Data-Oriented Tech Stack 面向数据技术栈

1. Entity Component System
   1.  实例化对象在内存中是紧密排列的，

2. Job System
   1. Unity对CPU多核编程的应用

3. Burst Compiler
   1. Unity 开发全新的快速编译器

ECS(主要是Entities的开发)：

1. 组件（Component）
2. 系统（System）
3. Entities 的管理器脚本（GameObjectEntity.cs）

![image-20210921160323543](E:\GitHub\mdFile\images\image-20210921160323543.png)



1. Entities
2. Hybrid Renderer
3. Mathematics

![OOD-DOD](E:\GitHub\mdFile\images\OOD-DOD.png)



什么是DOD
Unity实际上在做的大计划,是一个在程序届流行了一阵子,最近越来越火的概念DOD (Data Oriented Design) 即 面向数据设计. 他是与我们所熟知的OOD (Object Oriented Design) 即面向对象设计相对的概念. 

ECS
实例组件系统,是编程思想的改变,从基于对象的运作,改变为"流水线式运作"(我自己的比喻).虽然显然破坏了"程序对现实的模拟"这样美好的愿望,但是却大大的增强了解耦性,可测性,扩展性.并且天然是以下要描述的几个组件的好伙伴~

Job System
Job System是Unity对CPU多核编程的应用.通过把工作分散到CPU的各个核心上来大大提升运行效率.而ECS跟他之间的搭配则是由于ECS的System部分天然是以批量处理为核心的,因此只要稍加改动,就可以转变为批量的分Job交到多核去处理.实现性能的提升.

HPC#
HPC#(High Perform C#)是Unity开发的一个C#子集,通过抛弃对象,指针,等高级特性,从语言层面加速性能. 截图里没有直接列出这个,但是Native Container 是HPC#的一环. 而由于ECS本身的去对象化,可见又是天然的好伙伴.

Burst Compiler
这又是Unity自己开发的,一个全新的快速编译器,最重要的是由于不用考虑通用性,仅仅针对Unity,针对游戏,再配合HPC#, 使得性能有了更大的提升




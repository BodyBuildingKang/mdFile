# Unity--GUI 

1. OnGUI:OnGUI是Unity中通过代码驱动的GUI系统。
2. NGUI:第三方插件包，是Unity一直以来最流行的UI插件。
3. UGUI:从Unity4.6开始后，Unity找到NGUI的作者，用了一年开发了UGUI，变成内置于Unity中的包，集成到了编辑器中。

# OnGUI

主要用来创建调试工具、创建自定义属性面板、创建新的Editor窗口和工具达到扩展编辑器效果。
OnGUI不建议使用在项目UI中

![image-20210312001555611](..\images\image-20210312001555611.png)

# Text



![image-20210312001841801](..\images\image-20210312001841801.png)

1. Font:字体
2. Font Style：字体类型（Normal：正常
3. Bold：加粗；Italic：斜体；Bold And Italic）
4. Font Size:字体大小
5. Line Spacing：行间距
6. Rich Text：可以结合多种字体类型和大小

```html
1.  <b>Text</b> 
2.  <i>Text</i>
3. <size=15>Text</size>
4. <color=black>Text</color>
5. <color=#0500CD>Text</color>
```

			7. Alignment：对齐方式
			8. Align By Geometr：几何方向对齐
			9. Horizontal Oveflow：水平方向溢出方式（Wrap：自动换行；Overflow：溢出显示）
			10. Vertical Overflow：垂直方向溢出方式（TrunCate：截断不显示；Overflow：溢出显示）
			11. Best Fit：字体最佳适应大小
			12. Color：颜色与透明度
			13. 脚本上有Color、Color32的区别，Color类是Float类型的参数，大小为0 ~ 1，Color32是Int类型参数，大小为0 ~ 255；
			14. Material：材质
			15. Raycast Target:射线投射目标，是否能够响应图形射线

![image-20210312002114957](..\images\image-20210312002114957.png)

# Image

![image-20210312002125441](..\images\image-20210312002125441.png)

1. Source Image：源图像，Sprite图像资源
2. Color：颜色与透明度；
3. Material：材质
4. Raycast Target：射线投射目标；
5. Image Type：
   	1、Simple  默认，在拉伸区域内完全显示一张图片
   	2、Sliced 切片，九宫格应用，需要图片做过九宫格分割，四角在图片拉升时不会拉伸变形
   	3、Tiled 平铺，像铺地板一样填满整个控件
   	4、Filled 填充，技能冷却主要依靠这个属性
6. Preserve Aspect：保持长宽比
7. Set Native Size：设置原始尺寸
8. Filled 填充
9. Fill Method：切割方式，水平、垂直，90、180、360度圆形
10. Fill Origin：切割起始位置
11. Fill Amount：切割的量，0~1
12. Clockwise：顺时针方向
13. Preserve Aspect：保持长宽比

# Raw Image

![image-20210312002259415](..\images\image-20210312002259415.png)

1. Texture：纹理；区别于Sprite
2. Color：
3. Material：
4. Raycast Target：
5. UV Rect：UV矩阵，改变UV坐标，可实现一张图片切分，如果这一组图相互切换变成一个动画，例如动物跑动，就能实现动图的效果。
6. Set Native Size：
7. RawImage核心代码比Image少很多，Raw Image不支持交互，可用于显示任何图片而不仅仅是Sprite，一般用在背景、图标上,支持UV Rect(用来设置只显示图片的某一部分)，而Image不支持UV Rect。
8. 扩展：Outline/描边组件Shadow阴影组件
9. 使用RawImage加Texture实现分镜显示

![image-20210312002331718](..\images\image-20210312002331718.png)



# Button

![image-20210312002339119](..\images\image-20210312002339119.png)

1. Interactable:是否可交互
2. Transition: 确定控件以可视方式响应用户操作的方式的属性
3. Navigation: 在EventSystem中，存在一个当前被选中按钮，我们可以通过按下上下左右，使被选中按钮进行更改。
4. Visualize：显示控件之间的导航

![image-20210312002351922](..\images\image-20210312002351922.png)



# Toggle

![image-20210312002410266](..\images\image-20210312002410266.png)

1. Is On：默认是否选中。
2. Toggle Transition：切换是是否有过渡效果，Fade表示有，None表示没有。
3. Graphic：设置开关要起作用的图形对象，不一定非要是默认的对号。
4. Group：设置分组。把多个Toggle放在同一个物体下，在这个物体上添加Toggle Group，并给Toggle赋值，就可以实现单选。
5. On Value Change：当Toggle值改变时所调用的函数。

![image-20210312002448248](..\images\image-20210312002448248.png)



#  Slider

![image-20210312002509728](..\images\image-20210312002509728.png)

1. Fill Rect：填充矩形，滑块与最小值方向所构成的填充区域所要使用的填充矩形，如果滑动条的作用只是用于改变指定值，那么此选项建议置空，这个相比于Scrollbar所多出来的属性主要用于标识从最小值变化到当前值所经过的变化区域。
2. Handle Rect：操作条矩形，当前值处于最小值与最大值之间比例的显示范围，也就是整个滑条的最大可控制范围。
3. Direction：方向，滑动条的方向，从左至右，从上至下还是其他的。
4. Left To Right；Right To Left；Bottom To Top；Top To Bottom
5. Min Value：滑动条的可变化最小值。
6. Max Value：滑动条的可变化最大值。
7. Whole Numbers: 变化值为整型，勾选此项，拖动滑动条将按整型数（最小为1）进行改变指定值。
8. Value：当前滑动条对应的值。



# Scroll View

![image-20210312002549389](..\images\image-20210312002549389.png)

![image-20210312002553034](..\images\image-20210312002553034.png)

![image-20210312002558361](..\images\image-20210312002558361.png)

## 结构

1. 滚动视图，是一个能上下或者左右拖动的ui列表，用于展示图像、文本，按钮等，在需要展示比较多的内容的情况的时候会用到。例如背包，长文字。
2. 滚动视图需要Scroll Rect, Mask, Layout Group
3. 组成结构：
   Scroll View：挂载Scroll Rect 组件
   Viewport: 视口，挂载Mask 组件
   Content: 内容，挂载Layout Group组件,Layout Group组件有三种
   		1、Grid Layout Group
   		2、Horizontal Layout Group
   		3、Vertical Layout Group # Mask 组件

## Mask组件

1. Mask组件：遮罩，它不是一个可见的UI控件，只是一个用来限制子物体显示内容的组件。换句话说，挂载Mask组件的父物体，用来显示子物体的一部分

## Grid Layout Group

![image-20210312004714918](..\images\image-20210312004714918.png)



1. Pading：边距
2. Cell Size：网格中每个单元格的大小
3. Spacing：间距，X轴（水平）间距，Y（垂直）轴间距
4. Start Corner：始角，子元素排列开始的位置
5. Start Axis：始轴，子元素排列优先轴，水平优先，垂直优先
6. Child Alignment：子元素对齐
7. Constraint：行列约束
8. Flexible，无约束
9. FixedColumnCount，约束指定数量的列
10. FixedRowCount，约束指定数量的行

## Scroll Rect

![image-20210312004609991](..\images\image-20210312004609991.png)

1. Content: 滚动的内容，可以是Text文字内容，也可以是图片内容
2. Horizontal：允许水平方向滚动;Vertical：允许垂直方向滚动
3. Movement Type：滚动类型
4. Unrestricted 无限制
5. Elastic 弹性，弹性模式在到达滚动矩形的边缘时会反弹内容;（Elasticity:弹性/弹跳量） 
6. Clamped 固定；
7. Inertia: 惯性，拖动后释放指针，内容将继续移动。
8. Deceleration Rate: 惯性减速率，减速率将决定内容停止移动的速度。比率0将立即停止运动。值为1表示运动永远不会减速。
9. Scroll Sensitivity: 滚动灵敏度，滚轮和触控板滚动事件的敏感性。滚动的速度。
10. Viewport：视口，滚动内容的父物体，需要用到Mask遮罩，遮罩部分为滚动内容可视部分。
11. Horizontal Scrollbar：水平滚动
12. Visibility: 能见度，永久的；自动隐藏；自动隐藏并扩展视口
13. Spacing：间距
14. Vertical Scrollbar：垂直滚动，同Horizontal



# Dropdown

![image-20210312003011130](..\images\image-20210312003011130.png)

## 结构

1. Label：初始化的文字
2. Arrow：初始化的下拉箭头
3. Template： Dropdown的模板样式；滚动视图
4. Item Background：每一个Item的背景图片
5. Item Checkmark：每一个Item的选中标识图片
6. Item Label：每一个Item的文字显示内容
7. Scrollbar：滚动条

## 组件面板

1. Template：下拉列表的模板
2. Caption Text：下拉列表首选项文字
3. Caption Image：下拉列表首选项图片
4. Item Text：下拉列表中的item文本
5. Item Image：下拉列表中的item图像，需要添加
6. Value：当前所选选项的索引。0是第一个选项，1是第二个选项，依此类推。
7. Options：下拉列表的文本和图像内容。可以为每个选项指定文本和图像。

![image-20210312004512972](..\images\image-20210312004512972.png)

# Input Field

![image-20210312003154461](..\images\image-20210312003154461.png)

1. Line Type：换行方式，当输入的内容超过输入域边界时：
2. single Line：单行，不换行，继续延伸此行，输入域中的内容只有一行；
3. multi Line Submit：多行，超过边界则换行，输入域中内容有多行；
4. multi Line Newline：多行，超过边界则新建换行，输入域中内容有多行。
5. Placeholder：位置标示，此输入域的输入位控制符，任何带有Text组件的物体。
   注意：Placeholder对应的Text也为此输入框的提示语显示：（例如Enter text...为提示语，当输入框内容为空时，提示语可见，内容不为空时，提示语不可见）
6. Caret blink rate：光标闪烁速度，标示输入光标的闪烁速度。
7. Selection Color：选中文本的颜色
8. Hide mobile input：手机端隐藏输入 
9. Read Only：只读，不允许输入
10. On Value Changed： 值改变时事件
11. End Edit： 输入结束时事件
12. Input Field同样可以用ISelectHandler接口实现选中事件监听
13. On Value Changed： 值改变时事件
14. End Edit： 输入结束时事件
15. Input Field同样可以用ISelectHandler接口实现选中事件监听
16. On Value Changed： 值改变时事件
17. End Edit： 输入结束时事件
18. Input Field同样可以用ISelectHandler接口实现选中事件监听

![image-20210312004400820](..\images\image-20210312004400820.png)



# Scrollbar

![image-20210312002907578](..\images\image-20210312002907578.png)

1. Handle Rect：操作条矩形，当前值处于最小值与最大值之间比例的显示范围，也就是整个滑条的最大可控制范围。
2. Direction：方向，滚动条的方向，从左至右，从上至下还是其他的。
3. Value：当前滚动条对应的值。
4. Size：操作条矩形长度，操作条矩形对应的缩放长度。
5. Numbers Of Steps：指定可滚动的位置数量，滚动条可滚动的位置数目，为0和1时不生效（事实上只有0个可滚动位置或1个可滚动位置那还叫滚动条吗），例如设为2，则拖动滚动条时滚动条只会处在最小值的位置和最大值的位置，因为他的可滚动位置只有2个，例如设为3，则拖动滚动条时滚动条只会处在最小值的位置、最大值的位置以及中间位置，因为他的可滚动位置只有3个。





# Canvas 

画布，创建UI物体时，会自动创建，并且，所有UI物体都是Canvas的子物体。和Canvas一同创建的还有一个EventSystem，其是一个基于Input的事件系统，可以对键盘、触摸、鼠标、自定义输入进行监听处理。
绘制元素顺序
画布中的UI元素是以它们在层次结构中出现的顺序绘制的。首先绘制第一个孩子，然后绘制第二个孩子，依此类推。如果两个UI元素重叠，则后一个元素将出现在前一个元素的顶部。
要更改哪个元素显示在其他元素的顶部，只需拖动层次结构中的元素即可。

## Rend Mode

![image-20210312003823867](..\images\image-20210312003823867.png)

1. Screen Space - Overlay
   屏幕空间-叠加，表示 Canvas 下的所有的 UI 控件永远位于屏幕的前面 , 不管有没有相机 , UI元素永远在屏幕最前面 ，主要是2D效果。在这种模式下，在不同的屏幕分辨率下画布会自动适配屏幕的分辨率大小。
   Pixel Perfect：完美像素，UI元素精确到像素对齐，边缘更清晰
   Sort Order：排列顺序，多个Canvas存在的时候，数值越大，越优先显示

 2. Screen Space - Camera
屏幕空间-相机模式，Canvas 和 摄像机之间有一定的距离 , 可以在摄像机和 Canvas 之间播放一些粒子特效，主要是3D效果。
Pixel Perfect ：完美像素，UI元素精确到像素对齐，边缘更清晰
Render Camera ：指定一个相机，用于渲染Canvas
Plane Distance：Canvas平面与摄像机的距离
Sorting Layer：Canvas显示层级，存在多个Canvas时，层级越大，显示优先级越高 
Order in Layer：层级顺序，同 Sorting Layer下，Order越大，显示优先级越高
  3.  World Space
    世界空间，Canvas 就和普通的 3D 物体一样了 , 可以控制它的大小,旋转,缩放等 , 一般用来做血条。
    Event Camera：用于响应事件的相机
    Sorting Layer：Canvas显示层级，存在多个Canvas时，层级越大，显示优先级越高 
    Order in Layer：层级顺序，同 Sorting Layer下，Order越大，显示优先级越高

## Canvas Scale

![image-20210312003927194](..\images\image-20210312003927194.png)

1、Constant Pixel Size：无论屏幕大小如何，都使UI元素保持相同的像素大小
Scale Factor：以此比例缩放Canvas中的所有UI元素。
2、Scale With Screen Size：根据不同屏幕尺寸自动改变UI大小
3、Constant Physical Size：恒定物理尺寸
4、World Space：世界空间设置

## Graphic Raycaster

![image-20210312003958642](..\images\image-20210312003958642.png)

只有UI的元素才继承了Graphic基类，才能响应图形射线。Ignore Reversed Graphic：图片翻转后点击无效Blocking Objects：可以阻止射线的Object类型Blocking Mask：可以阻止射线的Mask类型

## Color

![image-20210312004025873](..\images\image-20210312004025873.png)![image-20210312004030362](..\images\image-20210312004030362.png)

Color：颜色与透明度
脚本上有Color、Color32的区别，Color类是Float类型的参数，大小为0 ~ 1，Color32是Int类型参数，大小为0 ~ 255；



# Rect Transform

![image-20210312003328409](..\images\image-20210312003328409.png)![image-20210312003331091](..\images\image-20210312003331091.png)![image-20210312003338660](..\images\image-20210312003338660.png)

UGUI对象所特有的组件，区别于Transform
Pivot：轴点，UI对象旋转的中心点
Anchors：锚，UI对象所特有的，由四个位于UI对象父物体矩形边框范围内的四个点组成（UGUI对象都是矩形边框），用来锚定UI对象。
(Min_x,Min_y)；(Min_x,Max_y)；(Max_x,Min_y)；(Max_x,Max_y)；
有三种形态：锚点，锚线，锚框
无论父物体的位置尺寸大小改变，UI子物体的Rect Transform四个参数的的值不变。不同情况，Rect Transform四个参数有不同的含义。

## 锚点

![image-20210312003518591](..\images\image-20210312003518591.png)![image-20210312003522376](..\images\image-20210312003522376.png)

锚点：四个点重合的情况。无论如何改变父物体的尺寸， UI子物体Rect Transform四个参数的的值不变，其含义分别为：
PosX：锚点到UI子物体左边框的垂直距离
PosY：锚点到UI子物体下边框的垂直距离
Width：UI子物体的宽度
Height：UI子物体的高度
也就表示UI子物体的尺寸大小不变，并且锚点与UI子物体左下角的点的方向距离不变；进而推断出轴点与锚点的方向距离也保持不变；

## 锚线

![image-20210312003550879](..\images\image-20210312003550879.png)![image-20210312003554102](..\images\image-20210312003554102.png)![image-20210312003557583](..\images\image-20210312003557583.png)

锚线：两个点重合的情况。改变父物体的尺寸，UI子物体Rect Transform四个参数的值不变，其含义分别为：
PosX：锚线与UI子物体左边框的垂直距离
Top：锚线上方端点与 UI子物体上边框的垂直距离
Width：UI子物体的宽度
Bottom：锚线下方端点与 UI子物体下边框的垂直距离
也就表示锚线到UI子物体轴点的垂直距离保持不变，但是UI子物体的高度会随着父物体的高度变化而变化

## 锚框

锚框：四个点分开的情况。改变父物体的尺寸，UI子物体Rect Transform四个参数的值不变，其含义分别为：

Left：左方锚线与UI子物体左边框的垂直距离
Top：上方锚线与 UI子物体上边框的垂直距离
Right：右方锚线与 UI子物体右边框的垂直距离
Bottom：下方锚线与 UI子物体下边框的垂直距离
也就表示UI子物体的尺寸大小包括高度宽度都会随着父物体的尺寸改变而改变

注意：UI父物体与UI子物体的尺寸大小变化会受两者Scale大小比例影响

# Raycast Target

Image/RawImage/Text组件上都会有Raycast  Target这个参数，用来表示是否响应射线。

![image-20210312004156648](..\images\image-20210312004156648.png)

![image-20210312004139900](..\images\image-20210312004139900.png)








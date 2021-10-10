# NGUI

##  1.使用NGUI注意的点：

1. 完整的NGUI系统，必须要有UI Root/UI Panel/UI Camera,在创建NGUI内容时，系统会帮助我们创建出来
2. UI Root：NGUI的内容都必须挂在在UI Root下面
3. UI Panel： 在NGUI中，UI Panel就像一个容器，只有在UI Panel中UI对象才能显示，可以有多个UI Panel，每个UI Panel显示自己包含的内容
4. UI Camera： NGUI中的检测事件都是通过UI Camera来实现
5. NGUI中的空间要发生事件必须要有Collider组件，Collider区分2D/3D

## 2. UI Root组件

​		![image-20210308234304814](..\images\image-20210308234304814.png)

1. Scaling Style： 缩放比例类型。 UI Root的尺寸会随着分辨率的设置改变进行缩放
2.  Flexible：灵活的，根据高度，在设置的最小高度到最大高度之间缩放
3. Constrained：约束的，可以指定高度和宽度，根据指定的高度或宽度进行缩放

## 3 . UI Panel组件

​		![image-20210308234612667](..\images\image-20210308234612667.png)

1. Alpha：透明度
2. Depth：深度，显示优先级，数值越大，显示游戏层级越高
3. Clipping： 裁剪方式
4. Texture Mask：纹理遮罩
5. Soft Clip：细致裁剪
6. Constrain but don‘t clip：约束但不裁剪

## 4. UI Camera组件

​		![image-20210308234904331](..\images\image-20210308234904331.png)

1. Debug：用于调试，显示与鼠标交互的对象信息
2. Command Click：在Mac电脑触控板上用command按键模拟右键操作
3. Allow Multi Touch：是否允许多点触摸
4. Auto Hide Cursor：当游戏控制器或者输入设备被检测到时NGUI是否自动隐藏光标
5. Sticky Tooltip：粘性提示，True：一直显示直到鼠标移开对象；False：鼠标移动立即隐藏
6. Long Press Tooltip：长按住对象，持续Tooltip Delay时间之后，显示提示消息
7. Tooltip Delay：提示消息延迟时间
8. Raycast Range：射线长度，默认-1，表示无限远
9. Event Sources：用来确定哪些事件类型会被处理。被勾选掉的事件就不会被处理。有些平台会强制关闭一些事件。比如使用手柄时会自动关掉鼠标和touch时事件。
10. Thresholds：是指事件误差的范围，比如Mouse Click是指鼠标的按下和抬起两个事件在UI上的偏移误差不能大于10pixels，当大于
11. 10pixels时，则认为不是点击事件！ 。以像素为单位。
12. Axes and Keys：是指方向键/摇杆，键盘绑定。这些名字需要和Input Manager里面的一致。
13. UI Camera的原理：UI Camera就是通过在触摸/鼠标移动的位置的地方发射射线（就是Unity的Raycast），然后获取射线撞击的碰撞体(collider)信息，然后发射消息（通过Unity的SendMessage函数）给该碰撞体关联的GameObject的所有脚本
14. OnHover (bool isOver)：鼠标悬停或移出时触发。悬停时传入true，移出时传入false。
15. OnPress (bool isDown)：鼠标或触摸按下或松开时触发，按下时传入true，松开时传入false。
16. OnClick()：鼠标或触摸单击（按下并释放）时触发。
17. OnDoubleClick () ：双击（双击时间间隔小于0.25秒）时触发。
18. OnSelect (bool selected)：类似单击，区别在于选中一次之后再选中将不再触发OnSelect事件，除非期间选择了其他控件。 
19. OnDrag (Vector2 delta)：鼠标或触摸按下并移动时触发。delta为传入的位移。
20. OnInput (string text)：只用于输入控件，每次输入完成后触发，text传入本次输入的信息，而非输入控件中的文本信息。 
21. OnTooltip (bool show)：鼠标悬停一段时间或移开时触发，悬停时传入true，移开时传入false。
22. OnScroll (float delta)：鼠标中键滚动时触发，delta为传入的滚动增量。
23. UICamera.currentTouchID  ：用于区分鼠标按下的键位，-1为左键，-2为右键，-3为中键
24. UICamera.lastHit   ：   RaycastHit类型。用于获取被触发的物体。
25. UICamera.lastTouchPosition ：   用于获取鼠标或触摸的位置。

## 5. Atlas Maker

​			**NGUI区别于UGUI，NGUI在使用2D图片时采用图集的形式，因此，在使用NGUI之前，我们需要学会如何使用图集制作器制作图集。**



## 6  NGUI控件

####  1. Sprite—精灵

​		![image-20210308235733837](..\images\image-20210308235733837.png)

1. Atlas：图集，选择事先创建的图集
2. Sprite：精灵，选择图集中的精灵图片
3. Type：图片类型，和UGUI中Image Type一样
4. Simple：简单的；Sliced：切片（需要Sprite进行九宫格分割）Tiled：平铺
5. Filled：填充；Advanced：高级
6. Flip：翻转
7. Gradient：梯度，或者说颜色渐变
8. Color Tint：颜色
9. Pivot：轴点
10. Depth：深度，同一Panel下， 深度值越大，显示优先级越高
11. Size：尺寸大小
12. Anchors：锚

#### 2. Label—文本

​			![image-20210309000115410](..\images\image-20210309000115410.png)

1. Font Size：字体大小
2. Text：文本内容
3. Modifier： To uppercase 变大写，To Lowercase 变小写， Custom 自定义
4. OverFlow：溢出方式。Shrink 当溢出之后，缩小内容字体；Clamp 溢出之后，剪切掉；Resize Freely 无限制的调整大小；Resize Height 宽度不变，调整高度，高度大于UI界面也会溢出 
5. Alignment：对齐方式
6. Gradient：梯度，或者说颜色渐变
7. Effect：效果。阴影，描边
8. Spacing：间距
9. Max Lines：最大行数
10. Color Tint：颜色
11. BB Code：富文本支持

#### 3. Tooltip—提示信息

​				![image-20210309000126082](..\images\image-20210309000126082.png)

1. UI Camera：事件监听相机
2. Text：提示信息Label
3. Tooltip Root：根
4. Background：背景sprite
5. Appear Speed：出现的速度
6. Scaling Transition：尺寸变化的过渡效果

#### 4. Texture—纹理

​				![image-20210309000221410](..\images\image-20210309000221410.png)



基本和Sprite相同，区别在于，可以渲染所有的格式的图片，不需要使用图集。另外，多了UV Rect矩阵，通过改变UV的值，可实现一张图片切分，如果这一组图相互切换变成一个动画，例如动物跑动，就能实现动图的效果。

#### 5. Input Field—输入框

![image-20210309000313695](..\images\image-20210309000313695.png)

![image-20210309000317812](..\images\image-20210309000317812.png)

![image-20210309000321101](..\images\image-20210309000321101.png)



1. Label：用于绑定的Label，即输入文本。
2. Starting Value：起始显示的值。
3. Saved As：内容指定保存的键值。PlayerPrefs存取
4. Active Text Color：文本激活的时候显示的颜色。
5. Inactive Color：未激活的时候显示的颜色。
6. Caret Color：闪硕光标的颜色。
7. Select Color：被选择文字的颜色。
8. Input Type：输入内容格式化，可以是密码显示*号。
9. Keyboard Type：键盘样式。
10. Validation：输入内容格式 验证，如数字，名字邮箱等。
11. Character Limit：输入字符个数限制。

#### 6. Button—按钮

![image-20210309000415555](..\images\image-20210309000415555.png)

![image-20210309000419394](..\images\image-20210309000419394.png)

1. Tween Target:
2. Drag Over:
3. Transition：过渡时间
4. Colors：颜色过渡
5. Sprites：sprite过渡
6. On Click：On Click事件绑定

#### 7. Check Box（Toggle)选框

1. Group：属于哪个组，用于实现单选
2. State of “None”：是否允许none值
3. Starting State：开始状态
4. Sprite：状态转换影响的Sprite
5. Invert Sprite：
6. Transition：转换方式。平滑过渡；瞬间过渡
7. On Value Change : On Value Change事件

#### 8. Popup List—弹出框/下拉列表

![image-20210309000541464](..\images\image-20210309000541464.png)

![image-20210309000544454](..\images\image-20210309000544454.png)

![image-20210309000547099](..\images\image-20210309000547099.png)

1. Options：选项集合
2. Position：位置
3. Selection：选择操作
4. Alignment：对齐方式
5. Open On：打开弹出框方式
6. On Top：显示层级最高
7. Localized：本地化
8. Keep Value：勾选之后可以选择首选项
9. Initial Value：首选项
10. Atlas：下拉框背景使用的图集
11. Font：下拉框选项使用的字体
12. On Value Change：绑定UILabel/SetCurrentSelection方法，替换label

#### 9. Slider—滑杆

![image-20210309000650745](..\images\image-20210309000650745.png)

![image-20210309000654145](..\images\image-20210309000654145.png)

![image-20210309000656599](..\images\image-20210309000656599.png)

1. Value:滑杆当前的值
2. Steps：把滑杆分成若干节，值按照一节一节的变化
3. Foreground：前景
4. Background：背景
5. Thumb：滑动块
6. Direction：滑动方向
7. On Value Change：On Value Change事件

#### 10. Scroll Bar—滚动条

![image-20210309000734500](..\images\image-20210309000734500.png)

![image-20210309000738293](..\images\image-20210309000738293.png)

![image-20210309000740817](..\images\image-20210309000740817.png)

1. Value：滚动条的值
2. Size：滚动条滚动块的尺寸
3. Alpha：滚动条透明度
4. Steps：把滚动条成若干节，值按照一节一节的变化
5. Foreground：前景，滚动范围以及滚动块
6. Background：背景
7. Thumb：transform对象，用来交互
8. Direction：滑动方向
9. On Value Change：On Value Change事件

#### 11. Scroll View—滚动视图

![image-20210309000843027](..\images\image-20210309000843027.png)

![image-20210309000850075](..\images\image-20210309000850075.png)

![image-20210309000854158](..\images\image-20210309000854158.png)

​									`**Scroll View必须要有UI Panel组件，UI Scroll View +UI Drag Scroll View + Collider**`

1. Content Origin：内容开始位置
2. Movement：活动方式，水平；垂直；不限制；自定义
3. Drag Effect：拖拽效果，Momentum，动量/惯性；Spring 弹性
4. Scroll Wheel Factor：鼠标滚轮滚动系数
5. Momentum Amount：动量大小
6. Restrict Within Panel：限制内容在Panel之内
7. Scroll Bars：滚动条，水平；垂直
8. Show Condition：滚动条显示条件，总是显示；需要时显示；拖拽时显示
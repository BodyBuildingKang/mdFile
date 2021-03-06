## 形而上的思想

# 六大设计原则(SOLID)

## 理解

​	建议性的原则，没有实际的招数

## 1. 单一职责原则(Single Responsibility Principle)

1. 优点 ： 简单  稳定 扩展性高
2. 缺点 ： 代码量多，类多，使用成本高，可读性低

## 2. 里氏替换原则(Liskov Substitution Principle)

## 3. 迪米特法则(Law of Demeter)

## 4. 开闭原则(Open Close Principle)

## 5. 接口隔离原则(Interface Segregation Principle)

## 6. 依赖倒置原则(Dependence Inversion Principle)

# 设计模式

## 理解

面向对象语言在开发过程中，遇到了各种各样的问题和困难时，提出的思路以及解决方案。久而久之，沉淀下来就形成了设计模式。

## 1.  创建型设计模式 - 关注对象的创建

### 单例模式：

​	套路 ：·公开。。。 私有化构造函数

1. why: 构造对象耗时耗资源，很多地方都需要去new,想要避免重复构造
2. what: 
   1. 懒汉式单例模式  
   2. 饿汉式单例模式
   3. 普通单例模式
3. todo:
   1. 提前构造
   2. 构造函数私有化
   3. 公开静态方法||属性||字段提供实例，保证全局唯一

### 原型模式

​	套路：换个方式创建对象，不走构造函数，而是内存拷贝

### 简单工厂

​	套路：不直接new , 把对象创建转移到工厂类

### 工厂方法

 	套路：屏蔽对象的创建；留下来扩展空间

### 抽象工厂

​	 套路：屏蔽对象的创建；约束强制保障产品簇

## 2. 结构型设计模式

###  套路 ：关注类与类之间的关系

## 3. 行为型设计模式

### 套路 ：关注对象与行为的分离


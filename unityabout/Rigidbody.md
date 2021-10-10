# ***\*Rigidbody\*******\*继承\****[Component](https://docs.unity.cn/cn/2020.1/ScriptReference/Component.html)

## ***\*描述\****

## ***\*通过物理模拟控制对象的位置。\****

向对象添加 Rigidbody 组件后，其运动将受到 Unity 物理引擎的控制。即使不添加任何代码，Rigidbody 对象也受到向下的重力，并在与其他对象碰撞时作出反应（如果也存在适当的 [Collider](https://docs.unity.cn/cn/2020.1/ScriptReference/Collider.html) 组件）。
Rigidbody 还有一个脚本 API，让您能够向对象施加力，并以逼真的物理效果对其进行控制。例如，可以根据车轮施加的力来指定汽车的行为。根据这些信息，物理引擎可以处理汽车运动的大多数其他方面，因此汽车可进行逼真的加速并适当地响应碰撞。
在脚本中，建议使用 [FixedUpdate](https://docs.unity.cn/cn/2020.1/ScriptReference/MonoBehaviour.FixedUpdate.html) 函数来施加力和更改 Rigidbody 设置（而不是使用 [Update](https://docs.unity.cn/cn/2020.1/ScriptReference/MonoBehaviour.Update.html)，Update 用于大多数其他帧更新任务）。这样做的原因是物理更新在测量的时间步骤中执行，而时间步骤与帧更新不一致。FixedUpdate 在每次进行物理更新前调用，因此在该函数中做出的任何更改都将直接处理。
刚开始使用 Rigidbody 时，新手常常会遇到游戏物理效果似乎以“慢动作”运行的问题。这实际上是您的模型使用了不适当的缩放导致的。默认的重力设置假定一个世界单位对应于一米的距离。对于非物理游戏，如果您的模型长度都为 100 个单位，则不会有太大的差别；但在使用物理引擎时，它们将被视为非常大的对象。如果为本应较小的对象使用较大的缩放，它们下落时的视觉速度就会相当缓慢 - 物理引擎认为它们是非常大的物体，正在很远的距离处下落。因此，请确保您的对象缩放后与现实世界的对象差不多（例如，汽车的长度应为 4 个单位 = 4 米左右）。

## ***\*变量\****

| [angularDrag](https://docs.unity.cn/cn/2020.1/ScriptReference/Rigidbody-angularDrag.html) | 对象的角阻力。                                               |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [angularVelocity](https://docs.unity.cn/cn/2020.1/ScriptReference/Rigidbody-angularVelocity.html) | 刚体的角速度矢量（以弧度/秒为单位）。                        |
| [centerOfMass](https://docs.unity.cn/cn/2020.1/ScriptReference/Rigidbody-centerOfMass.html) | 相对于变换原点的质心。                                       |
| [collisionDetectionMode](https://docs.unity.cn/cn/2020.1/ScriptReference/Rigidbody-collisionDetectionMode.html) | 刚体的碰撞检测模式。                                         |
| [constraints](https://docs.unity.cn/cn/2020.1/ScriptReference/Rigidbody-constraints.html) | 控制该刚体的模拟自由度。                                     |
| [detectCollisions](https://docs.unity.cn/cn/2020.1/ScriptReference/Rigidbody-detectCollisions.html) | 是否应启用碰撞检测？（默认情况下始终启用）。                 |
| [drag](https://docs.unity.cn/cn/2020.1/ScriptReference/Rigidbody-drag.html) | 对象的阻力。                                                 |
| [freezeRotation](https://docs.unity.cn/cn/2020.1/ScriptReference/Rigidbody-freezeRotation.html) | 控制物理是否会更改对象的旋转。                               |
| [inertiaTensor](https://docs.unity.cn/cn/2020.1/ScriptReference/Rigidbody-inertiaTensor.html) | 质量相对于质心的对角惯性张量。                               |
| [inertiaTensorRotation](https://docs.unity.cn/cn/2020.1/ScriptReference/Rigidbody-inertiaTensorRotation.html) | 惯性张量的旋转。                                             |
| [interpolation](https://docs.unity.cn/cn/2020.1/ScriptReference/Rigidbody-interpolation.html) | 插值可以平滑消除固定帧率运行物理导致的现象。                 |
| [isKinematic](https://docs.unity.cn/cn/2020.1/ScriptReference/Rigidbody-isKinematic.html) | 控制物理是否影响刚体。                                       |
| [mass](https://docs.unity.cn/cn/2020.1/ScriptReference/Rigidbody-mass.html) | 刚体的质量。                                                 |
| [maxAngularVelocity](https://docs.unity.cn/cn/2020.1/ScriptReference/Rigidbody-maxAngularVelocity.html) | 刚体的最大角速率（以弧度/秒为单位）。（默认值为 7）范围为 { 0, 无穷大 }。 |
| [maxDepenetrationVelocity](https://docs.unity.cn/cn/2020.1/ScriptReference/Rigidbody-maxDepenetrationVelocity.html) | 离开穿透状态时刚体的最大速度。                               |
| [position](https://docs.unity.cn/cn/2020.1/ScriptReference/Rigidbody-position.html) | 刚体的位置。                                                 |
| [rotation](https://docs.unity.cn/cn/2020.1/ScriptReference/Rigidbody-rotation.html) | 刚体的旋转。                                                 |
| [sleepThreshold](https://docs.unity.cn/cn/2020.1/ScriptReference/Rigidbody-sleepThreshold.html) | 经过质量标准化的能量阈值 - 当低于该阈值时，对象开始进入睡眠状态。 |
| [solverIterations](https://docs.unity.cn/cn/2020.1/ScriptReference/Rigidbody-solverIterations.html) | solverIterations 确定刚体关节与碰撞接触点的解析精确度。它将重写 Physics.defaultSolverIterations。必须为正值。 |
| [solverVelocityIterations](https://docs.unity.cn/cn/2020.1/ScriptReference/Rigidbody-solverVelocityIterations.html) | solverVelocityIterations 影响刚体关节与碰撞接触点的解析精确度。它将重写 Physics.defaultSolverVelocityIterations。必须为正值。 |
| [useGravity](https://docs.unity.cn/cn/2020.1/ScriptReference/Rigidbody-useGravity.html) | 控制重力是否影响该刚体。                                     |
| [velocity](https://docs.unity.cn/cn/2020.1/ScriptReference/Rigidbody-velocity.html) | 刚体的速度矢量。它表示刚体位置的变化率。                     |
| [worldCenterOfMass](https://docs.unity.cn/cn/2020.1/ScriptReference/Rigidbody-worldCenterOfMass.html) | 刚体在世界空间中的质心（只读）。                             |

## ***\*公共函数\****

| [AddExplosionForce](https://docs.unity.cn/cn/2020.1/ScriptReference/Rigidbody.AddExplosionForce.html) | 向模拟爆炸效果的刚体施加力。                           |
| ------------------------------------------------------------ | ------------------------------------------------------ |
| [AddForce](https://docs.unity.cn/cn/2020.1/ScriptReference/Rigidbody.AddForce.html) | 向 Rigidbody 添加力。                                  |
| [AddForceAtPosition](https://docs.unity.cn/cn/2020.1/ScriptReference/Rigidbody.AddForceAtPosition.html) | 在 position 处施加 /force/。这将向对象施加扭矩和力。   |
| [AddRelativeForce](https://docs.unity.cn/cn/2020.1/ScriptReference/Rigidbody.AddRelativeForce.html) | 向刚体添加力（相对于其坐标系）。                       |
| [AddRelativeTorque](https://docs.unity.cn/cn/2020.1/ScriptReference/Rigidbody.AddRelativeTorque.html) | 向刚体添加扭矩（相对于其坐标系）。                     |
| [AddTorque](https://docs.unity.cn/cn/2020.1/ScriptReference/Rigidbody.AddTorque.html) | 向刚体添加扭矩。                                       |
| [ClosestPointOnBounds](https://docs.unity.cn/cn/2020.1/ScriptReference/Rigidbody.ClosestPointOnBounds.html) | 与附加碰撞体的包围盒最接近的点。                       |
| [GetPointVelocity](https://docs.unity.cn/cn/2020.1/ScriptReference/Rigidbody.GetPointVelocity.html) | 点 /worldPoint/（全局空间）处刚体的速度。              |
| [GetRelativePointVelocity](https://docs.unity.cn/cn/2020.1/ScriptReference/Rigidbody.GetRelativePointVelocity.html) | 相对于点 relativePoint 处的刚体的速度。                |
| [IsSleeping](https://docs.unity.cn/cn/2020.1/ScriptReference/Rigidbody.IsSleeping.html) | 刚体是否处于睡眠状态？                                 |
| [MovePosition](https://docs.unity.cn/cn/2020.1/ScriptReference/Rigidbody.MovePosition.html) | 将运动 Rigidbody 向 position 移动。                    |
| [MoveRotation](https://docs.unity.cn/cn/2020.1/ScriptReference/Rigidbody.MoveRotation.html) | 将刚体旋转到 /rotation/。                              |
| [ResetCenterOfMass](https://docs.unity.cn/cn/2020.1/ScriptReference/Rigidbody.ResetCenterOfMass.html) | 重置刚体的质心。                                       |
| [ResetInertiaTensor](https://docs.unity.cn/cn/2020.1/ScriptReference/Rigidbody.ResetInertiaTensor.html) | 重置惯性张量的值和旋转。                               |
| [SetDensity](https://docs.unity.cn/cn/2020.1/ScriptReference/Rigidbody.SetDensity.html) | 根据附加的碰撞体设置质量（假设密度恒定）。             |
| [Sleep](https://docs.unity.cn/cn/2020.1/ScriptReference/Rigidbody.Sleep.html) | 强制刚体进入睡眠状态至少一帧。                         |
| [SweepTest](https://docs.unity.cn/cn/2020.1/ScriptReference/Rigidbody.SweepTest.html) | 测试如果刚体在场景中移动时，是否会与任何对象发生碰撞。 |
| [SweepTestAll](https://docs.unity.cn/cn/2020.1/ScriptReference/Rigidbody.SweepTestAll.html) | 与 Rigidbody.SweepTest 类似，但返回所有命中对象。      |
| [WakeUp](https://docs.unity.cn/cn/2020.1/ScriptReference/Rigidbody.WakeUp.html) | 强制唤醒刚体。                                         |

## ***\*消息\****

| [OnCollisionEnter](https://docs.unity.cn/cn/2020.1/ScriptReference/Rigidbody.OnCollisionEnter.html) | 当该碰撞体/刚体已开始接触另一个刚体/碰撞体时，调用 OnCollisionEnter。 |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [OnCollisionExit](https://docs.unity.cn/cn/2020.1/ScriptReference/Rigidbody.OnCollisionExit.html) | 当该碰撞体/刚体已停止接触另一个刚体/碰撞体时，调用 OnCollisionExit。 |
| [OnCollisionStay](https://docs.unity.cn/cn/2020.1/ScriptReference/Rigidbody.OnCollisionStay.html) | 对应正在接触刚体/碰撞体的每一个碰撞体/刚体，每帧调用一次 OnCollisionStay。 |

## ***\*继承的成员\****

## ***\*变量\****

| [gameObject](https://docs.unity.cn/cn/2020.1/ScriptReference/Component-gameObject.html) | 此组件附加到的游戏对象。始终将组件附加到游戏对象。 |
| ------------------------------------------------------------ | -------------------------------------------------- |
| [tag](https://docs.unity.cn/cn/2020.1/ScriptReference/Component-tag.html) | 此游戏对象的标签。                                 |
| [transform](https://docs.unity.cn/cn/2020.1/ScriptReference/Component-transform.html) | 附加到此 GameObject 的 Transform。                 |
| [hideFlags](https://docs.unity.cn/cn/2020.1/ScriptReference/Object-hideFlags.html) | 该对象应该隐藏、随场景一起保存还是由用户修改？     |
| [name](https://docs.unity.cn/cn/2020.1/ScriptReference/Object-name.html) | 对象的名称。                                       |

## ***\*公共函数\****

| [BroadcastMessage](https://docs.unity.cn/cn/2020.1/ScriptReference/Component.BroadcastMessage.html) | 调用此游戏对象或其任何子项中的每个 MonoBehaviour 上名为 methodName 的方法。 |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [CompareTag](https://docs.unity.cn/cn/2020.1/ScriptReference/Component.CompareTag.html) | 此游戏对象是否使用 tag 进行了标记？                          |
| [GetComponent](https://docs.unity.cn/cn/2020.1/ScriptReference/Component.GetComponent.html) | Returns the component of Type type if the GameObject has one attached, null if it doesn't. Will also return disabled components. |
| [GetComponentInChildren](https://docs.unity.cn/cn/2020.1/ScriptReference/Component.GetComponentInChildren.html) | 使用深度首次搜索返回 GameObject 或其任何子项中类型为 type 的组件。 |
| [GetComponentInParent](https://docs.unity.cn/cn/2020.1/ScriptReference/Component.GetComponentInParent.html) | 返回 GameObject 或其任何父项中类型为 type 的组件。           |
| [GetComponents](https://docs.unity.cn/cn/2020.1/ScriptReference/Component.GetComponents.html) | 返回 GameObject 中类型为 type 的所有组件。                   |
| [GetComponentsInChildren](https://docs.unity.cn/cn/2020.1/ScriptReference/Component.GetComponentsInChildren.html) | 返回 GameObject 或其任何子项中类型为 type 的所有组件。       |
| [GetComponentsInParent](https://docs.unity.cn/cn/2020.1/ScriptReference/Component.GetComponentsInParent.html) | 返回 GameObject 或其任何父项中类型为 type 的所有组件。       |
| [SendMessage](https://docs.unity.cn/cn/2020.1/ScriptReference/Component.SendMessage.html) | 调用此游戏对象中的每个 MonoBehaviour 上名为 methodName 的方法。 |
| [SendMessageUpwards](https://docs.unity.cn/cn/2020.1/ScriptReference/Component.SendMessageUpwards.html) | 调用此游戏对象中的每个 MonoBehaviour 上或此行为的每个父级上名为 methodName 的方法。 |
| [TryGetComponent](https://docs.unity.cn/cn/2020.1/ScriptReference/Component.TryGetComponent.html) | 获取指定类型的组件（如果存在）。                             |
| [GetInstanceID](https://docs.unity.cn/cn/2020.1/ScriptReference/Object.GetInstanceID.html) | 返回对象的实例 ID。                                          |
| [ToString](https://docs.unity.cn/cn/2020.1/ScriptReference/Object.ToString.html) | 返回对象的名称。                                             |

## ***\*静态函数\****

| [Destroy](https://docs.unity.cn/cn/2020.1/ScriptReference/Object.Destroy.html) | 移除 GameObject、组件或资源。                   |
| ------------------------------------------------------------ | ----------------------------------------------- |
| [DestroyImmediate](https://docs.unity.cn/cn/2020.1/ScriptReference/Object.DestroyImmediate.html) | 立即销毁对象 /obj/。强烈建议您改用 Destroy。    |
| [DontDestroyOnLoad](https://docs.unity.cn/cn/2020.1/ScriptReference/Object.DontDestroyOnLoad.html) | 在加载新的 Scene 时，请勿销毁 Object。          |
| [FindObjectOfType](https://docs.unity.cn/cn/2020.1/ScriptReference/Object.FindObjectOfType.html) | 返回第一个类型为 type 的已加载的激活对象。      |
| [FindObjectsOfType](https://docs.unity.cn/cn/2020.1/ScriptReference/Object.FindObjectsOfType.html) | Gets a list of all loaded objects of Type type. |
| [Instantiate](https://docs.unity.cn/cn/2020.1/ScriptReference/Object.Instantiate.html) | 克隆 original 对象并返回克隆对象。              |

## ***\*运算符\****

| [bool](https://docs.unity.cn/cn/2020.1/ScriptReference/Object-operator_Object.html) | 该对象是否存在？                               |
| ------------------------------------------------------------ | ---------------------------------------------- |
| [operator !=](https://docs.unity.cn/cn/2020.1/ScriptReference/Object-operator_ne.html) | 比较两个对象是否引用不同的对象。               |
| [operator ==](https://docs.unity.cn/cn/2020.1/ScriptReference/Object-operator_eq.html) | 比较两个对象引用，判断它们是否引用同一个对象。 |
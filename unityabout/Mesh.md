# ***\*Mesh\*******\*继承\**** [Object](https://docs.unity.cn/cn/2020.1/ScriptReference/Object.html)

## ***\*描述\****

用于通过脚本创建或修改网格的类。

Meshes contain vertices and multiple triangle arrays.
三角形数组是顶点数组的简单索引；每个三角形三个索引。

您可能需要将可修改的网格接口用于 3 种用途：
有三种常见任务可能需要使用网格 API：

***\*1.从头开始构建网格\****： 应始终按以下顺序进行：
a) 分配 [vertices](https://docs.unity.cn/cn/2020.1/ScriptReference/Mesh-vertices.html)
b) 分配 [triangles](https://docs.unity.cn/cn/2020.1/ScriptReference/Mesh-triangles.html)。

using UnityEngine;

public class Example : MonoBehaviour

{

  Vector3[] newVertices;

  Vector2[] newUV;

  int[] newTriangles;

  void Start()

  {

​    Mesh mesh = new Mesh();

​    GetComponent<MeshFilter>().mesh = mesh;

​    mesh.vertices = newVertices;

​    mesh.uv = newUV;

​    mesh.triangles = newTriangles;

  }

}

***\*2.每一帧都修改顶点属性\****：
a) 获取顶点
b) 修改它们
c) 将它们分配回网格。

using UnityEngine;

public class Example : MonoBehaviour

{

  void Update()

  {

​    Mesh mesh = GetComponent<MeshFilter>().mesh;

​    Vector3[] vertices = mesh.vertices;

​    Vector3[] normals = mesh.normals;

​    for (var i = 0; i < vertices.Length; i++)

​    {

​      vertices[i] += normals[i] * Mathf.Sin(Time.time);

​    }

​    mesh.vertices = vertices;

  }

}
***\*3.连续更改网格三角形和顶点\****：
a) 调用 [Clear](https://docs.unity.cn/cn/2020.1/ScriptReference/Mesh.Clear.html) 以开始刷新
b) 分配顶点和其他属性
c) 分配三角形索引。


using UnityEngine;

public class ExampleClass : MonoBehaviour

{

  Vector3[] newVertices;

  Vector2[] newUV;

  int[] newTriangles;

  void Start()

  {

​    Mesh mesh = GetComponent<MeshFilter>().mesh;

​    mesh.Clear();

​    // Do some calculations...

​    mesh.vertices = newVertices;

​    mesh.uv = newUV;

​    mesh.triangles = newTriangles;

  }

}

## ***\*变量\****

| [bindposes](https://docs.unity.cn/cn/2020.1/ScriptReference/Mesh-bindposes.html) | 绑定姿势。每个索引处的绑定姿势引用索引相同的骨骼。 |
| ------------------------------------------------------------ | -------------------------------------------------- |
| [blendShapeCount](https://docs.unity.cn/cn/2020.1/ScriptReference/Mesh-blendShapeCount.html) | 返回此网格上的 BlendShape 计数。                   |
| [boneWeights](https://docs.unity.cn/cn/2020.1/ScriptReference/Mesh-boneWeights.html) | 网格中每个顶点的骨骼权重，最大值为 4。             |
| [bounds](https://docs.unity.cn/cn/2020.1/ScriptReference/Mesh-bounds.html) | 网格的包围体。                                     |
| [colors](https://docs.unity.cn/cn/2020.1/ScriptReference/Mesh-colors.html) | 网格的顶点颜色。                                   |
| [colors32](https://docs.unity.cn/cn/2020.1/ScriptReference/Mesh-colors32.html) | 网格的顶点颜色。                                   |
| [indexFormat](https://docs.unity.cn/cn/2020.1/ScriptReference/Mesh-indexFormat.html) | 网格索引缓冲区数据的格式。                         |
| [isReadable](https://docs.unity.cn/cn/2020.1/ScriptReference/Mesh-isReadable.html) | 如果网格支持读/写，则返回 true，否则返回 false。   |
| [normals](https://docs.unity.cn/cn/2020.1/ScriptReference/Mesh-normals.html) | 网格的法线。                                       |
| [subMeshCount](https://docs.unity.cn/cn/2020.1/ScriptReference/Mesh-subMeshCount.html) | Mesh 对象中的子网格数。                            |
| [tangents](https://docs.unity.cn/cn/2020.1/ScriptReference/Mesh-tangents.html) | 网格的切线。                                       |
| [triangles](https://docs.unity.cn/cn/2020.1/ScriptReference/Mesh-triangles.html) | 包含网格中所有三角形的数组。                       |
| [uv](https://docs.unity.cn/cn/2020.1/ScriptReference/Mesh-uv.html) | 网格的基础纹理坐标。                               |
| [uv2](https://docs.unity.cn/cn/2020.1/ScriptReference/Mesh-uv2.html) | 网格的第二个纹理坐标集（如果存在）。               |
| [uv3](https://docs.unity.cn/cn/2020.1/ScriptReference/Mesh-uv3.html) | 网格的第三个纹理坐标集（如果存在）。               |
| [uv4](https://docs.unity.cn/cn/2020.1/ScriptReference/Mesh-uv4.html) | 网格的第四个纹理坐标集（如果存在）。               |
| [uv5](https://docs.unity.cn/cn/2020.1/ScriptReference/Mesh-uv5.html) | 网格的第五个纹理坐标集（如果存在）。               |
| [uv6](https://docs.unity.cn/cn/2020.1/ScriptReference/Mesh-uv6.html) | 网格的第六个纹理坐标集（如果存在）。               |
| [uv7](https://docs.unity.cn/cn/2020.1/ScriptReference/Mesh-uv7.html) | 网格的第七个纹理坐标集（如果存在）。               |
| [uv8](https://docs.unity.cn/cn/2020.1/ScriptReference/Mesh-uv8.html) | 网格的第八个纹理坐标集（如果存在）。               |
| [vertexAttributeCount](https://docs.unity.cn/cn/2020.1/ScriptReference/Mesh-vertexAttributeCount.html) | 返回网格所具有的顶点属性数。（只读）               |
| [vertexBufferCount](https://docs.unity.cn/cn/2020.1/ScriptReference/Mesh-vertexBufferCount.html) | 获取网格中存在的顶点缓冲区数。（只读）             |
| [vertexCount](https://docs.unity.cn/cn/2020.1/ScriptReference/Mesh-vertexCount.html) | 返回网格中的顶点数（只读）。                       |
| [vertices](https://docs.unity.cn/cn/2020.1/ScriptReference/Mesh-vertices.html) | 返回顶点位置的副本或分配新顶点位置数组。           |

## ***\*构造函数\****

| [Mesh](https://docs.unity.cn/cn/2020.1/ScriptReference/Mesh-ctor.html) | 创建空网格。 |
| ------------------------------------------------------------ | ------------ |
|                                                              |              |

## ***\*公共函数\****

| [AddBlendShapeFrame](https://docs.unity.cn/cn/2020.1/ScriptReference/Mesh.AddBlendShapeFrame.html) | 添加新的混合形状帧。                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [Clear](https://docs.unity.cn/cn/2020.1/ScriptReference/Mesh.Clear.html) | 清除所有顶点数据和所有三角形索引。                           |
| [ClearBlendShapes](https://docs.unity.cn/cn/2020.1/ScriptReference/Mesh.ClearBlendShapes.html) | 从网格中清除所有混合形状。                                   |
| [CombineMeshes](https://docs.unity.cn/cn/2020.1/ScriptReference/Mesh.CombineMeshes.html) | 将多个网格合并到此网格中。                                   |
| [GetAllBoneWeights](https://docs.unity.cn/cn/2020.1/ScriptReference/Mesh.GetAllBoneWeights.html) | 获取网格的骨骼权重。                                         |
| [GetBaseVertex](https://docs.unity.cn/cn/2020.1/ScriptReference/Mesh.GetBaseVertex.html) | 获取给定 sub-mesh 的基顶点索引。                             |
| [GetBindposes](https://docs.unity.cn/cn/2020.1/ScriptReference/Mesh.GetBindposes.html) | 获取网格的绑定姿势。                                         |
| [GetBlendShapeFrameCount](https://docs.unity.cn/cn/2020.1/ScriptReference/Mesh.GetBlendShapeFrameCount.html) | 返回混合形状的帧计数。                                       |
| [GetBlendShapeFrameVertices](https://docs.unity.cn/cn/2020.1/ScriptReference/Mesh.GetBlendShapeFrameVertices.html) | 检索混合形状帧的 deltaNormals、deltaNormals 和 /deltaTangents/。 |
| [GetBlendShapeFrameWeight](https://docs.unity.cn/cn/2020.1/ScriptReference/Mesh.GetBlendShapeFrameWeight.html) | 返回混合形状帧的权重。                                       |
| [GetBlendShapeIndex](https://docs.unity.cn/cn/2020.1/ScriptReference/Mesh.GetBlendShapeIndex.html) | 按给定名称返回 BlendShape 的索引。                           |
| [GetBlendShapeName](https://docs.unity.cn/cn/2020.1/ScriptReference/Mesh.GetBlendShapeName.html) | 按给定索引返回 BlendShape 的名称。                           |
| [GetBonesPerVertex](https://docs.unity.cn/cn/2020.1/ScriptReference/Mesh.GetBonesPerVertex.html) | 每个顶点的非零骨骼权重数量。                                 |
| [GetBoneWeights](https://docs.unity.cn/cn/2020.1/ScriptReference/Mesh.GetBoneWeights.html) | 获取网格的骨骼权重。                                         |
| [GetColors](https://docs.unity.cn/cn/2020.1/ScriptReference/Mesh.GetColors.html) | 获取网格的顶点颜色。                                         |
| [GetIndexCount](https://docs.unity.cn/cn/2020.1/ScriptReference/Mesh.GetIndexCount.html) | 获取给定 sub-mesh 的索引计数。                               |
| [GetIndexStart](https://docs.unity.cn/cn/2020.1/ScriptReference/Mesh.GetIndexStart.html) | 对于给定 /sub-mesh/，获取网格索引缓冲区中的起始索引位置。    |
| [GetIndices](https://docs.unity.cn/cn/2020.1/ScriptReference/Mesh.GetIndices.html) | 获取指定子网格的索引列表。                                   |
| [GetNativeIndexBufferPtr](https://docs.unity.cn/cn/2020.1/ScriptReference/Mesh.GetNativeIndexBufferPtr.html) | 检索指向索引缓冲区的原生（底层图形 API）指针。               |
| [GetNativeVertexBufferPtr](https://docs.unity.cn/cn/2020.1/ScriptReference/Mesh.GetNativeVertexBufferPtr.html) | 检索指向顶点缓冲区的原生（底层图形 API）指针。               |
| [GetNormals](https://docs.unity.cn/cn/2020.1/ScriptReference/Mesh.GetNormals.html) | 获取网格的顶点法线。                                         |
| [GetSubMesh](https://docs.unity.cn/cn/2020.1/ScriptReference/Mesh.GetSubMesh.html) | 获取有关网格的子网格的信息。                                 |
| [GetTangents](https://docs.unity.cn/cn/2020.1/ScriptReference/Mesh.GetTangents.html) | 获取网格的切线。                                             |
| [GetTopology](https://docs.unity.cn/cn/2020.1/ScriptReference/Mesh.GetTopology.html) | 获取子网格的拓扑。                                           |
| [GetTriangles](https://docs.unity.cn/cn/2020.1/ScriptReference/Mesh.GetTriangles.html) | 获取此对象上指定子网格的切线列表。                           |
| [GetUVDistributionMetric](https://docs.unity.cn/cn/2020.1/ScriptReference/Mesh.GetUVDistributionMetric.html) | UV 分布指标可用于根据摄像机的位置计算所需的 Mipmap 级别。    |
| [GetUVs](https://docs.unity.cn/cn/2020.1/ScriptReference/Mesh.GetUVs.html) | 获取网格的 UV。                                              |
| [GetVertexAttribute](https://docs.unity.cn/cn/2020.1/ScriptReference/Mesh.GetVertexAttribute.html) | 基于索引返回有关顶点属性的信息。                             |
| [GetVertexAttributeDimension](https://docs.unity.cn/cn/2020.1/ScriptReference/Mesh.GetVertexAttributeDimension.html) | 获取此网格上特定顶点数据属性的尺寸。                         |
| [GetVertexAttributeFormat](https://docs.unity.cn/cn/2020.1/ScriptReference/Mesh.GetVertexAttributeFormat.html) | 获取此网格上特定顶点数据属性的格式。                         |
| [GetVertexAttributes](https://docs.unity.cn/cn/2020.1/ScriptReference/Mesh.GetVertexAttributes.html) | 获取有关网格的顶点属性的信息。                               |
| [GetVertices](https://docs.unity.cn/cn/2020.1/ScriptReference/Mesh.GetVertices.html) | 获取网格的顶点位置。                                         |
| [HasVertexAttribute](https://docs.unity.cn/cn/2020.1/ScriptReference/Mesh.HasVertexAttribute.html) | 检查特定顶点数据属性是否在此网格上存在。                     |
| [MarkDynamic](https://docs.unity.cn/cn/2020.1/ScriptReference/Mesh.MarkDynamic.html) | 优化网格以便频繁更新。                                       |
| [MarkModified](https://docs.unity.cn/cn/2020.1/ScriptReference/Mesh.MarkModified.html) | 向 Renderer 组件通知网格几何体更改。                         |
| [Optimize](https://docs.unity.cn/cn/2020.1/ScriptReference/Mesh.Optimize.html) | 优化网格数据以提高渲染性能。                                 |
| [OptimizeIndexBuffers](https://docs.unity.cn/cn/2020.1/ScriptReference/Mesh.OptimizeIndexBuffers.html) | 优化网格几何体以提高渲染性能。                               |
| [OptimizeReorderVertexBuffer](https://docs.unity.cn/cn/2020.1/ScriptReference/Mesh.OptimizeReorderVertexBuffer.html) | 优化网格顶点以提高渲染性能。                                 |
| [RecalculateBounds](https://docs.unity.cn/cn/2020.1/ScriptReference/Mesh.RecalculateBounds.html) | 从顶点重新计算网格的包围体。                                 |
| [RecalculateNormals](https://docs.unity.cn/cn/2020.1/ScriptReference/Mesh.RecalculateNormals.html) | 从三角形和顶点重新计算网格的法线。                           |
| [RecalculateTangents](https://docs.unity.cn/cn/2020.1/ScriptReference/Mesh.RecalculateTangents.html) | 从法线和纹理坐标重新计算网格的切线。                         |
| [SetBoneWeights](https://docs.unity.cn/cn/2020.1/ScriptReference/Mesh.SetBoneWeights.html) | 设置网格的骨骼权重。                                         |
| [SetColors](https://docs.unity.cn/cn/2020.1/ScriptReference/Mesh.SetColors.html) | 设置网格的每顶点颜色。                                       |
| [SetIndexBufferData](https://docs.unity.cn/cn/2020.1/ScriptReference/Mesh.SetIndexBufferData.html) | 设置网格索引缓冲区的数据。                                   |
| [SetIndexBufferParams](https://docs.unity.cn/cn/2020.1/ScriptReference/Mesh.SetIndexBufferParams.html) | 设置索引缓冲区大小和格式。                                   |
| [SetIndices](https://docs.unity.cn/cn/2020.1/ScriptReference/Mesh.SetIndices.html) | 为子网格设置索引缓冲区。                                     |
| [SetNormals](https://docs.unity.cn/cn/2020.1/ScriptReference/Mesh.SetNormals.html) | 设置网格的法线。                                             |
| [SetSubMesh](https://docs.unity.cn/cn/2020.1/ScriptReference/Mesh.SetSubMesh.html) | 设置有关网格的子网格的信息。                                 |
| [SetTangents](https://docs.unity.cn/cn/2020.1/ScriptReference/Mesh.SetTangents.html) | 设置网格的切线。                                             |
| [SetTriangles](https://docs.unity.cn/cn/2020.1/ScriptReference/Mesh.SetTriangles.html) | 为子网格设置三角形列表。                                     |
| [SetUVs](https://docs.unity.cn/cn/2020.1/ScriptReference/Mesh.SetUVs.html) | 设置网格的 UV。                                              |
| [SetVertexBufferData](https://docs.unity.cn/cn/2020.1/ScriptReference/Mesh.SetVertexBufferData.html) | 设置网格顶点缓冲区的数据。                                   |
| [SetVertexBufferParams](https://docs.unity.cn/cn/2020.1/ScriptReference/Mesh.SetVertexBufferParams.html) | 设置顶点缓冲区大小和布局。                                   |
| [SetVertices](https://docs.unity.cn/cn/2020.1/ScriptReference/Mesh.SetVertices.html) | 分配新的顶点位置数组。                                       |
| [UploadMeshData](https://docs.unity.cn/cn/2020.1/ScriptReference/Mesh.UploadMeshData.html) | 将以前进行的网格修改上传到图形 API。                         |

## ***\*静态函数\****

| [AcquireReadOnlyMeshData](https://docs.unity.cn/cn/2020.1/ScriptReference/Mesh.AcquireReadOnlyMeshData.html) | Gets a snapshot of Mesh data for read-only access.         |
| ------------------------------------------------------------ | ---------------------------------------------------------- |
| [AllocateWritableMeshData](https://docs.unity.cn/cn/2020.1/ScriptReference/Mesh.AllocateWritableMeshData.html) | Allocates data structures for Mesh creation using C# Jobs. |
| [ApplyAndDisposeWritableMeshData](https://docs.unity.cn/cn/2020.1/ScriptReference/Mesh.ApplyAndDisposeWritableMeshData.html) | Applies data defined in MeshData structs to Mesh objects.  |

## ***\*继承的成员\****

## ***\*变量\****

| [hideFlags](https://docs.unity.cn/cn/2020.1/ScriptReference/Object-hideFlags.html) | 该对象应该隐藏、随场景一起保存还是由用户修改？ |
| ------------------------------------------------------------ | ---------------------------------------------- |
| [name](https://docs.unity.cn/cn/2020.1/ScriptReference/Object-name.html) | 对象的名称。                                   |

## ***\*公共函数\****

| [GetInstanceID](https://docs.unity.cn/cn/2020.1/ScriptReference/Object.GetInstanceID.html) | 返回对象的实例 ID。 |
| ------------------------------------------------------------ | ------------------- |
| [ToString](https://docs.unity.cn/cn/2020.1/ScriptReference/Object.ToString.html) | 返回对象的名称。    |

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
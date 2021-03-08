#  1. AB的定义和作用



###  1. 定义

1. 它是一个存在于硬盘上的文件。可以称之为压缩包。这个压缩包可以认为是一个文件夹，里面包含了多个文件。这些文件可以分为两类：serialized file 和 resource files。（序列化文件和源文件）
   	1. serialized file：资源被打碎放在一个对象中，最后统一被写进一个单独的文件（只有一个）
    	2. resource files：某些二进制资源（图片、声音）被单独保存，方便快速加载

![image-20210306161555040](C:\Users\12746\AppData\Roaming\Typora\typora-user-images\image-20210306161555040.png)



2. 它是一个AssetBundle对象，我们可以通过代码从一个特定的压缩包加载出来的对象。这个对象包含了所有我们当初添加到这个压缩包里面的内容，我们可以通过这个对象加载出来使用。

### 2. 作用

1. AssetBundle是一个压缩包包含模型、贴图、预制体、声音、甚至整个场景，可以在游戏运行的时候被加载；
2. AssetBundle自身保存着互相的依赖关系；
3. 压缩包可以使用LZMA和LZ4压缩算法，减少包大小，更快的进行网络传输；
4. 把一些可以下载内容放在AssetBundle里面，可以减少安装包的大小；



# 2. AssetBundle流程

​													![image-20210309001837135](C:\Users\12746\AppData\Roaming\Typora\typora-user-images\image-20210309001837135.png)



![image-20210309001841237](C:\Users\12746\AppData\Roaming\Typora\typora-user-images\image-20210309001841237.png)



 1. 指定资源的AssetBundle属性

     	1. （xxxa/xxx） 这里的xxxa会生成目录，名字为xxx

	2. 构建AssetBundle包

       ```c#
        using UnityEditor; 
        using System.IO; 
        public class CreateAssetBundles {    
            [MenuItem("Assets/Build AssetBundles")]    
            static void BuildAllAssetBundles()    
            {        
                string assetBundleDirectory = "Assets/AssetBundles";        										if(!Directory.Exists(assetBundleDirectory))        
                {            
                    Directory.CreateDirectory(assetBundleDirectory);        
                }
                BuildPipeline.BuildAssetBundles(assetBundleDirectory,BuildAssetBundleOptions.None, 					BuildTarget.StandaloneWindows);
            } 
        }
        ```
   
     
3. 上传AssetBundle包
	
    	1. 
    
4. 加载AB包和包里面的资源
	
    ```c#
       public class LoadFromFileExample : MonoBehaviour {
            function Start() {
                var myLoadedAssetBundle 
                    = AssetBundle.LoadFromFile(Path.Combine(Application.streamingAssetsPath, "myassetBundle"));
                if (myLoadedAssetBundle == null) {
                    Debug.Log("Failed to load AssetBundle!");
                    return;
                }
                var prefab = myLoadedAssetBundle.LoadAsset<GameObject>("MyObject");
                Instantiate(prefab);
            }
        }
        ```
     ```c#
   IEnumerator InstantiateObject()
       {
            string url = "file:///" + Application.dataPath + "/AssetBundles/" + assetBundleName;        
            UnityEngine.Networking.UnityWebRequest request 
                = UnityEngine.Networking.UnityWebRequest.GetAssetBundle(url, 0);
            yield return request.Send();
            AssetBundle bundle = DownloadHandlerAssetBundle.GetContent(request);
            GameObject cube = bundle.LoadAsset<GameObject>("Cube");
            GameObject sprite = bundle.LoadAsset<GameObject>("Sprite");
            Instantiate(cube);
            Instantiate(sprite);
        }
        ```
        

5.  AssetBundle使用相关API
   1. BuildPipeline.BuildAssetBundles(dir, BuildAssetBundleOptions.None, BuildTarget.StandaloneWindows64);
   2. AssetBundle ab = AssetBundle.LoadFromFile("AssetBundles/scene/wall.unity3d");
   3. GameObject wallPrefab = ab.LoadAsset<GameObject>("CubeWall");
   4. Instantiate(wallPrefab);



# 3. AssetBundle分组策略

1. 逻辑实体分组(UI界面，角色， 所有场景的共享部分)
2. 类型分组(声音， shader，material)
3. 使用分组(按照关卡，场景)

==============================================

1. 把经常更新的资源放在一个单独的包里面，跟不经常更新的包分离
2. 把需要同时加载的资源放在一个包里面
3. 可以把其他包共享的资源放在一个单独的包里面
4. 把一些需要同时加载的小资源打包成一个包
5. 如果对于一个同一个资源有两个版本，可以考虑通过后缀来区分 

# 4. 依赖打包

![image-20210306171124188](C:\Users\12746\AppData\Roaming\Typora\typora-user-images\image-20210306171124188.png)

# 5. Build AssetBundles

1. Build的路径（随意只要是在硬盘上都可以的）

2. BuildAssetBundleOptions :

   1. BuildAssetBundleOptions.None：使用LZMA算法压缩，压缩的包更小，但是加载时间更长。使用之前需要整体解压。一旦被解压，这个包会使用LZ4重新压缩。使用资源的时候不需要整体解压。在下载的时候可以使用LZMA算法，一旦它被下载了之后，它会使用LZ4算法保存到本地上。

   2. BuildAssetBundleOptions.UncompressedAssetBundle：不压缩，包大，加载快

   3. BuildAssetBundleOptions.ChunkBasedCompression：使用LZ4压缩，压缩率没有LZMA高，但是我们可以加载指定资源而不用解压全部。

      **注意使用LZ4压缩，可以获得可以跟不压缩想媲美的加载速度，而且比不压缩文件要小。**

   4. BuildTarget : 选择build出来的AB包要使用的平台

![image-20210309002517751](C:\Users\12746\AppData\Roaming\Typora\typora-user-images\image-20210309002517751.png)

# 6. The Manifest File



![image-20210309002551043](C:\Users\12746\AppData\Roaming\Typora\typora-user-images\image-20210309002551043.png)

# 7. AB依赖

![image-20210309002745427](C:\Users\12746\AppData\Roaming\Typora\typora-user-images\image-20210309002745427.png)

# 8. AssetBundles的使用

1. AssetBundle.LoadFromMemoryAsync

![image-20210309002945937](C:\Users\12746\AppData\Roaming\Typora\typora-user-images\image-20210309002945937.png)

2. AssetBundle.LoadFromFile

![image-20210309002951819](C:\Users\12746\AppData\Roaming\Typora\typora-user-images\image-20210309002951819.png)

3. WWW.LoadFromCacheOrDownload

![image-20210309003001803](C:\Users\12746\AppData\Roaming\Typora\typora-user-images\image-20210309003001803.png)

4. UnityWebRequest

![image-20210309003008639](C:\Users\12746\AppData\Roaming\Typora\typora-user-images\image-20210309003008639.png)

# 9. Loading Assets from AssetBundles

1. 一般

```c#
T objectFromBundle = bundleObject.LoadAsset<T>(assetName);
```

2. GameObject

```c#
GameObject gameObject = loadedAssetBundle.LoadAsset<GameObject>(assetName);
```

3. 所有资源

```c#
Unity.Object[] objectArray = loadedAssetBundle.LoadAllAssets();
```

4. 加载Manifests文件可以处理资源的依赖

```c#
AssetBundle assetBundle = AssetBundle.LoadFromFile(manifestFilePath);
AssetBundleManifest manifest = assetBundle.LoadAsset<AssetBundleManifest>("AssetBundleManifest");
string[] dependencies = manifest.GetAllDependencies("assetBundle"); //Pass the name of the bundle you want the dependencies for.
foreach(string dependency in dependencies)
{
    AssetBundle.LoadFromFile(Path.Combine(assetBundlePath, dependency));
}
```

# 10. 卸载AB包资源

1. 两个作用
   1. 减少内存使用
   2. 有可能导致丢失

2. 卸载资源时机

   1. AssetBundle.Unload(true)  ：卸载所有资源  ： 即使有资源被使用着也会被卸载

      1. 在关卡切换、场景切换 
      2. 资源没被用的时候 调用 

   2. AssetBundle.Unload(false) ： 卸载所有没用被使用的资源	

   3. 个别资源怎么卸载

      1. 通过 Resources.UnloadUnusedAssets.	

      2. 场景切换的时候

# 11.文件校验(CRC MD5 SHA1)

1. 相同点：
   1. CRC、MD5、SHA1都是通过对数据进行计算，来生成一个校验值，该校验值用来校验数据的完整性。
2. 不同点：
   1. 算法不同。CRC采用多项式除法，MD5和SHA1使用的是替换、轮转等方法；
   2. 校验值的长度不同。CRC校验位的长度跟其多项式有关系，一般为16位或32位；MD5是16个字节（128位）；SHA1是20个字节（160位）；
   3.  校验值的称呼不同。CRC一般叫做CRC值；MD5和SHA1一般叫做哈希值（Hash）或散列值；
   4.  安全性不同。这里的安全性是指检错的能力，即数据的错误能通过校验位检测出来。CRC的安全性跟多项式有很大关系，相对于MD5和SHA1要弱很多；MD5的安全性很高，不过大概在04年的时候被山东大学的王小云破解了；SHA1的安全性最高。
   5. 效率不同，CRC的计算效率很高；MD5和SHA1比较慢。
   6. 用途不同。CRC一般用作通信数据的校验；MD5和SHA1用于安全（Security）领域，比如文件校验、数字签名等。

# 12. 其他问题

1.  依赖包重复问题
   1. 把需要共享的资源打包到一起
   2. 分割包，这些包不是在同一时间使用的
   3. 把共享部分打包成一个单独的包
2.  图集重复问题
3.  Android贴图问题
4. iOS文件处理重复fixed in Unity 5.3.2p2


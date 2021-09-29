1. 冒泡排序
   1. 思路(从小到大)： 比较相邻的元素。如果第一个比第二个大，就交换他们两个。
   2. ![bubbleSort](images/bubbleSort.gif)

```c#
public static void BubbleSort(int[] array)
{
    int temp;
    bool Swap;
    for(int i = 0; i < array.Length; i++)
    {
        Swap = false;
        for(int j = 0; j < array.Length - i; j++)
        {
            if(array[j] > arrary[j+1])
            {
                temp = array[j];
                array[j] = array[j+1];
                array[j+1] = temp;
                if(!Swap)
                    Swap = true;
            }
        }
        if(!Swap)
            return
    }
}
```

2. 选择排序

   a.  首先找到最大(小)数，然后存放起始位置，然后再用剩余未排序数找到最大(小)数，如此反复进行到最后(内层循环找到最大(小)数的索引进行保存,结束一次内循环后进行位置交换)
   
   b.  任何时候的时间复杂度都O(n2),数据规模越小越好
   
   ![selectionSort](images/selectionSort.gif)
   
   ~~~c#
   public static void SelectSort(int[] array)
   {
       int minIndex;
       int temp;
       for(int i = 0; i < array.Length; i++)
       {
           minIndex = i;
           for(int j = i + 1; j < array.Length; j++)
           {
               if(array[minIndex] > array[j])
               {
                   minIndex = j;
               }
           }
           temp = array[i];
           array[i] = array[minIndex];
           array[minIndex] = temp;

       }
   }
   ~~~


   3. 插入排序

    a.  
    
    b.

   ![insertionSort](images/insertionSort.gif)


   ~~~c#
   public static void InsertionSort(int[] array)
   {
       
   }
   ~~~
   
   
   


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

   a.  


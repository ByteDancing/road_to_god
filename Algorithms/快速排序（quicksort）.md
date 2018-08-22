### 快排思想
>   参考资料：[快速排序](https://baike.baidu.com/item/%E5%BF%AB%E9%80%9F%E6%8E%92%E5%BA%8F%E7%AE%97%E6%B3%95/369842?fromtitle=%E5%BF%AB%E9%80%9F%E6%8E%92%E5%BA%8F&fromid=2084344&fr=aladdin#6_3)

*快速排序是对冒泡排序的一种改进*

##### 算法思想：
`通过一趟排序将要排序的数据分割成独立的两部分，其中一部分的所有数据都比另外一部分的所有数据都要小，然后再按此方法对这两部分数据分别进行快速排序，整个排序过程可以递归进行，以此达到整个数据变成有序序列。`

#####   一趟快速排序的算法是：
- 1）设置两个变量i、j，排序开始的时候：i=0，j=N-1；
- 2）以第一个数组元素作为关键数据，赋值给key，即key=A[0]；
- 3）从j开始向前搜索，即由后开始向前搜索(j--)，找到第一个小于key的值A[j]，将A[j]和A[i]互换；
- 4）从i开始向后搜索，即由前开始向后搜索(i++)，找到第一个大于key的A[i]，将A[i]和A[j]互换；
- 5）重复第3、4步，直到i=j； (3,4步中，没找到符合条件的值，即3中A[j]不小于key,4中A[i]不大于key的时候改变j、i的值，使得j=j-1，i=i+1，直至找到为止。找到符合条件的值，进行交换的时候i， j指针位置不变。另外，i==j这一过程一定正好是i+或j-完成的时候，此时令循环结束）。

#####   快速排序-java代码实现
```
package com.chengxiang.algorithm;

/**
 * 快速排序
 *<p>Title:QuickSort.java</p>
 *<p>Description</p>
 *@author    Mr.Cheng
 *@date      2018年8月22日
 *@version   1.0
 */
public class QuickSort {

	/**
	 * 递归分治
	 *Titel:quickSort
	 *Description:
	 * @param array		数组
	 * @param low		开始位置
	 * @param height	结束位置
	 */
	public static void quickSort(int[] array, int low, int height) {
		if (low < height) {
			// 将数组一份为二
			int middle = getMiddle(array, low, height);
			// 对低端递归排序
			quickSort(array, low, middle - 1);
			// 对高端递归排序
			quickSort(array, middle + 1, height);
		}
	}

	/**
	 * 查找中轴(最低位作为中轴值) 
	 *Titel:getMiddle
	 *Description:
	 * @param array		数组
	 * @param low		开始位置
	 * @param height	结束位置
	 * @return	返回中轴所在位置
	 */
	public static int getMiddle(int[] array, int low, int height) {
		// 数组的第一个作为中轴数
		int temp = array[low];
		while (low < height) {
			while (low < height && array[height] >= temp) {
				height--;
			}
			// 比中轴数小的移到左边（低端）
			array[low] = array[height];
			while (low < height && array[low] < temp) {
				low++;
			}
			// 比中轴大的移到右边（高端）
			array[height] = array[low];
		}
		// 中轴记录到尾
		array[height] = temp;
		// 返回中轴位置
		return low;
	}

	public static void show(int[] array) {
		for (int i = 0; i < array.length; i++) {
			System.out.print(array[i] + "	");
		}
		System.out.println();
	}

}


```

---



#####    快排测试

```
package com.chengxiang.algorithm;

public class QuickSortTest {

	public static void main(String[] args) {
		int[] array = {1,7,9,8,6,4,3,5,2};
		System.out.println("排序前");
		QuickSort.show(array);
		System.out.println("排序后：");
		QuickSort.quickSort(array, 0, array.length-1);
		QuickSort.show(array);
	}

}

```
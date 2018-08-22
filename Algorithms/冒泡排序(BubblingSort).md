```
package com.chengxiang.algorithm;

/**
 * 冒泡算法
 * 两两相邻元素比较，如果左边比右边大，交换位置，每轮比较初最大的元素到顶端
 * n个数字完成排序，总共进行(n-1)躺排序,每i次的排序次数为(n-i)次
 *<p>Title:BubblingSort.java</p>
 *<p>Description</p>
 *@author    Mr.Cheng
 *@date      2018年8月22日
 *@version   1.0
 */
public class BubblingSort {
	public static int[]  sort(int array[]) {
		//外循环控制
		for(int i=1;i<array.length;i++) {
			//内循环控制循环次数
			for(int j=0;j<array.length-1;j++) {
				if(array[j]>array[j+1]) {
					int temp = array[j];
					array[j] = array[j+1];
					array[j+1] = temp;
				}
			}
			
			System.out.print("第"+i+"轮排序后的结果");
			show(array);
		}
		return array;
	}
	
	
	public static void show(int[] array) {
		for (int i = 0; i < array.length; i++) {
			System.out.print(array[i]+"	");
		}
		System.out.println();
	}
}

```

---

```
package com.chengxiang.algorithm;

public class SortTest {

	public static void main(String[] args) {
		int[] array = {4,2,8,9,5,7,6,1,3};
		System.out.println("排序前");
		BubblingSort.show(array);
		System.out.println("****************");
		System.out.println("排序后：");
		BubblingSort.sort(array);
		BubblingSort.show(array);
	}

	

}

```


####    结果
```
排序前
1	7	9	8	6	4	3	5	2	
******每轮排序结果**********
第1轮排序后的结果1	7	8	6	4	3	5	2	9	
第2轮排序后的结果1	7	6	4	3	5	2	8	9	
第3轮排序后的结果1	6	4	3	5	2	7	8	9	
第4轮排序后的结果1	4	3	5	2	6	7	8	9	
第5轮排序后的结果1	3	4	2	5	6	7	8	9	
第6轮排序后的结果1	3	2	4	5	6	7	8	9	
第7轮排序后的结果1	2	3	4	5	6	7	8	9	
第8轮排序后的结果1	2	3	4	5	6	7	8	9	
排序后：
1	2	3	4	5	6	7	8	9	

```

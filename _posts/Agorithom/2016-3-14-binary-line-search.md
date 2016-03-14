---
layout: post
title: 线性查找和二分查找
categories: Algorithm
description: 有序数组的快速查找
keywords: 算法，查找
---

## 线性查找和二分查找 

　　对于有序数组我们一般可以采用线性查找和二分查找这两个经典的算法来完成我们想要寻找的结果，关于这两个算法来进行查找的时候，二分查找的时间复杂度是优与线性查找的。

* 线性查找时间复杂度为：　Ｏ(N)
* 二分查找时间复杂度为：　Ｏ(logN)

　　线性查找是与N成正比，二分查找是与log(N)成正比的，可以看到在时间复杂度上二分查找是优于线性查找的，再用大Ｏ表示的时间复杂度方法中：Ｏ(1)可以算是优秀的，Ｏ(logN)则可以算是良好，Ｏ(N)还行就算还凑合吧，Ｏ(N^2)则就算在不咋滴的行列了。

## Java　代码实现线性查找

* 线性查找就是从有序数组的头开始查找，就是一个循环遍历整个数组的过程

```java
public class Lsearch {
	public static int count = 1;
	public static int LineSearch( int a[], int Searchnum){
		for(int i=0; i < a.length;i++){　　　　//实现线性查找
			if(a[i] == Searchnum){
				System.out.println("find result is :"+a[i]);
			    break;
			}
			 if(i == a.length-1){
			    System.out.println("not found");
			 }
			 count++; 
		}
		System.out.println("count is:" + count);
		return count;
	}
	//主函数验证线性查找
	public static void main(String[] args) {
		int b[] = {0,1,2,3,4,5,6,7,8,9};
		LineSearch(b, 0);
		}


}
```

## Java　代码实现二分查找

* 二分查找需要将所要查找的数组一分为二的方法来来查找，判断中间那个数 `(low+high)/2` 和需要查找的数大小，若中间的数大于查找的数的话，由于数组是有序的，那么一分为二的后半部分全部都是大于所查找的那个数，所以只需要在前半部分继续二分查找就好了。


```java
public class Binarychop {
	public static int found(int[] data,int k){
		int low = 0;
		int high = data.length-1;
		while(true){
			int mid = (low+high)/2; 　//在这里实现二分查找的
			if(data[mid] == k){
				System.out.println("found it is:" +data[mid]);
				return mid;
			}
			else if(low>high){
				System.out.println("can't found "+k);
				return data.length;
			}
			else{
				if(data[mid]<k)
					low = mid +1;
				else
					high = mid -1;
			}
		}
	}
	//主函数来验证二分查找
	public static void main(String[] args) {
		int b[] = {0,1,2,3,4,5,6,7,8,9};
		found(b, 3);
	}
}
```

###　参考书籍
[data structure && algorithm in java](http://rineshpk.weebly.com/uploads/1/8/2/0/1820991/data_structures_and_algorithms_in_javatqw_darksiderg.pdf)
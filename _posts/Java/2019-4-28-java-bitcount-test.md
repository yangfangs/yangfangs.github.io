---
layout: post
title: 计算1亿对Hamming distance仅需5ms的Java源码bitCount解析
categories: Java
description: bitCount
keywords: 汉明距离，二进制，Java，bitCount
---

  汉明距离（[Hamming Distance](https://en.wikipedia.org/wiki/Hamming_distance)）的基本思想很简单，就是找不同。当求由01二进制组成
  的向量间的汉明距离可以由位运算直接进行，速度非常快。好的算法能让计算速度达到极快，Java内置bitCount源码就实现了一种速度极快的算法。在Linux机器
  （CPU: i7-4790 @ 3.6GHz）测试了1亿对汉明距离只用0.5ms，是普通算法的196倍。


#  测试1亿对汉明距离结果

测试基于32位的01二进制数进行的。

测试类：

```java

import java.util.Arrays;
import java.util.Random;

public class testHammingDistance {

    //生成1亿个随机32位的Int类型数
    public static int[] randomInt(int num, int seed) {
        int[] a = new int[num];
        Random r = new Random(seed);
        Arrays.setAll(a, w -> r.nextInt());
        return a;
    }

    //调用Java bitCount 求汉明距离
    public static int hammingDistance1(int hash1, int hash2) {
        int i = hash1 ^ hash2;
        return Integer.bitCount(i);
    }

    //求解正数的二进制汉明距离
    public static int hammingDistance2(int hash1, int hash2){
        int num = hash1 ^ hash2;
        int count = 0;
        for(; num > 0; count++)
        {
            num &= (num - 1);
        }
        return count;
    }

    //主函数测试1亿对
    public static void main(String[] args) {

        int tem = 4324523;
        int[] all = randomInt(100000000,123);
        long startTime = System.currentTimeMillis();

        for (int x:all){
            int tem1 = hammingDistance1(tem,x);
        }
        long endTime = System.currentTimeMillis();


        long startTime2 = System.currentTimeMillis();
        for (int x:all){
            int tem2 = hammingDistance2(tem,x);
        }
        long endTime2 = System.currentTimeMillis();

        System.out.println("hammingDistance1 time used: " + (endTime-startTime) + "ms");
        System.out.println("hammingDistance2 time used: " + (endTime2-startTime2) + "ms");

    }
}

```
结果：

```bash

hammingDistance1 time used: 5ms
hammingDistance2 time used: 980ms

Process finished with exit code 0

```

#  一般算法

  求汉明距离的核心是在数两个二进制数求`&`运算后1的个数，求1的个数最容易想到的是循环整个二进制获得1的个数。如下算法:

```java

public int numberOf1(int hash1, int hash2){

    int num = hash1 ^ hash2;
	int count = 0;

	while(n!=0){

		if((num & 1) == 1){
			++count;
		}
		n = n >> 1;
	}
	return count;

```

* 这种方法很容易理解，就是每次循环的时候对1取`&`操作，若结果等于1就统计出了一个1，然后每次循环后右移`>>`使高位的0或1移动到低位。这种算法的
时间复杂度为`O(n)`,其中n表示bit的位数。

# 优化算法

```java

    public int hammingDistance2(int hash1, int hash2){

        int num = hash1 ^ hash2;

        int count = 0;

        for(; num > 0; count++)
        {
            num &= (num - 1);
        }

        return count;
    }

```
* 优化后的方法通过二进制的运算法则进行优化，优化后的时间复杂度仍然为`O(n)`，但是这里的n代表着1的个数最差的结果n才代表bit位，比第一个算法n代表bit位要好。
二进制的运算原则是逢二进一，每次循环时候我都让num减去1通过跟自身&操作消除低位1，最后num<0循环停止。有多少个1就循环多少次。


例如，二进制`0b1110`统计为3个1的过程如下：

```java

// 第一次迭代:
0b1110 - 1 = 0b1110 - 0b0001 = 0b1101
0b1110 & 0b1101 = 0b1100

// 第二次迭代：
0b1100 - 1 = 0b1100 - 0b0001 = 0b1011
0b1100 & 0b1011 = 0b1000

// 第三次迭代：
0b1000 - 1 = 0b1000 - 0b0001 = 0b0111
0b1000 & 0b0111 = 0b0000

```

#  Java源码bitCount算法

* Java的32位二进制Integer.bitCount源码如下：

```java

    public static int bitCount(int i) {
    i = i - ((i >>> 1) & 0x55555555);
    i = (i & 0x33333333) + ((i >>> 2) & 0x33333333);
    i = (i + (i >>> 4)) & 0x0f0f0f0f;
    i = i + (i >>> 8);
    i = i + (i >>> 16);
    return i & 0x3f;
    }

```

## Java源码实现了复杂度为O(1)的算法

* 当我们想知道一个二进制数中有多少个1时候最容易想到的方法就如前两种方法一个一个的数，数一下一共多少个1就完事了。但是Java源码使用的方法是
先两个一对儿数一下有多少个1，存到原来的位置。然后对上面的数的结果再成对统计以此类推。

以8位为例，算法思想如下：

```bash

       二进制                         十进制(count个数)
1  0   1  1   1  1   0  1      1  0   1  1   1  1   0  1
 \/     \/     \/     \/        \/     \/     \/     \/
 01     10     10     01        1      2       2      1
   \   /         \   /           \    /        \    /
   0011           0011             3              3
      \          /                 \             /
          0110                             6

```

这种count方法就如一个倒立的二叉树一样。每一层的节点个数为2^(n-1)个，也就是说对于32位的二进制2^(n-1)=32，n=5。所以，我们只需要数5次，对于64位二进制只需要
数6次就能知道二进制中有多少个1了，这种方法实现了时间复杂度为O(1)优秀算法。


## Java源码算法实现机理

* Java源码中每次`&`运算各个数的二进制，主要是为了抹除成对统计时候的左位（进行右移位运算时候高位对低位产生的影响）。

```java

0x55555555  ‭0b01010101010101010101010101010101‬
0x33333333  ‭0b00110011001100110011001100110011‬
0x0f0f0f0f  ‭0b00001111000011110000111100001111‬
0x00ff00ff  0b00000000111111110000000011111111
0x0000ffff  ‭0b00000000000000001111111111111111‬
0x3f        ‭0b00111111‬

```


* 算法实现

> i & 0x55555555实现整数i抹除左一位，然后错位相加。
> (i >>> 1) & 0x55555555表示：左位移到右边，再把左位抹除，这样就可以计算两个bit位上1的个数了：0b1011=>0b0001 + 0b0101 = 0b0110左两位有1个1，右两位有2个1。
> 这时i中存储了每两位的统计结果，可以进行两两相加，最后求和



> ```java
> 0b11 11 11 11 11    (i & 0x55555555) + ((i >>> 1) & 0x55555555)  = 0b0101010101‬ + 0b0101010101 = 0b1010101010
> 0b10 10 10 10 10    (i & 0x33333333) + ((i >>> 2) & 0x33333333) = 0b1000100010 + 0b00100010 = 0b1001000100
> 0b10 01 00 01 00    (i & 0x0f0f0f0f) + ((i >>> 4) & 0x0f0f0f0f) = 0b1000000100 + 0b0100 = 0b1000001000
> 0b10 00 00 10 00    (i & 0x00ff00ff) + ((i >>> 8) & 0x00ff00ff) = 0b1000 + 0b10 = 0b1010
> 0b00 00 00 10 10    (i & 0x0000ffff) + ((i >>> 16) & 0x0000ffff) = 0b1010 + 0 = 0b1010
> dec           10
> ```

* 算法原型

>```java
>public static int bitCount(int i) {
>   i = (i & 0x55555555) + ((i >>> 1) & 0x55555555);
>    i = (i & 0x33333333) + ((i >>> 2) & 0x33333333);
>    i = (i & 0x0f0f0f0f) + ((i >>> 4) & 0x0f0f0f0f);
>    i = (i & 0x00ff00ff) + ((i >>> 8) & 0x00ff00ff);
>    i = (i & 0x0000ffff) + ((i >>> 16) & 0x0000ffff);
>    return i;
>}
>
>```

* 原型优化

1.算法第一步可以优化为：i = i - ((i >>> 1) & 0x55555555); 减少一次位运算。原理如下：

* 对于两位二进制有如下规律：

```bash

00 = 00 - 00;
01 = 01 - 00;
01 = 10 - 01;
10 = 11 - 01;

```

所以，在统计两位中1的个数的时候可以由算法i = i - (i>>>1)得到，如果大于两位，为了避免高位右移时候对低位产生的影响，可以通过对01进行`&`运算
的方法抹除这种影响。

两位`&`运算如下:

```bash

i = i - (i>>>1&01)

```

推广到32位：

```bash

i = i - ((i >>> 1) & 0x55555555)

```
2.算法第二步没有优化方法

3.算法第三步：实际是计算每个byte中的1的数量，最多8（0b1000）个，占4bit，可以最后进行位与运算消位，减少一次&运算：i = (i + (i >>> 4)) & 0x0f0f0f0f

4.第四,五步：同上理由，可以最后消位。但是由于int最多32（0b100000）个1，所以这两步可以不消位，最后一步把不需要的bit位抹除就可以了：i & 0x3f

最后得到Java源码最简洁的写法。

# Java位运算符

|操作符	|描述|
|--------|----------|
|＆	|如果相对应位都是1，则结果为1，否则为0	|
| \\| |	如果相对应位都是0，则结果为0，否则为1|
|^	|如果相对应位值相同，则结果为0，否则为1	|
|〜	|按位取反运算符翻转操作数的每一位，即0变成1，1变成0。	|
|<< 	|按位左移运算符。各二进制位全部左移 若干位，高位丢弃，低位补0	|
|>> 	|按位右移运算符。各二进制位全部右移 若干位，高位补符号位	|
|>>> 	|按位右移补零操作符。左操作数的值按右操作数指定的位数右移，移动得到的空位以零填充。|


* 参考：

[java源码Integer.bitCount算法解析](https://segmentfault.com/a/1190000015763941?utm_source=tag-newest)



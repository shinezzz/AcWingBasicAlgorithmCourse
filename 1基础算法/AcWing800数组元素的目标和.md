# AcWing 算法基础课 -- 基础算法

## AcWing 800. 数组元素的目标和 

`难度：简单`

### 题目描述

给定两个升序排序的有序数组A和B，以及一个目标值x。数组下标从0开始。
请你求出满足A[i] + B[j] = x的数对(i, j)。

数据保证有唯一解。

**输入格式**

第一行包含三个整数n，m，x，分别表示A的长度，B的长度以及目标值x。

第二行包含n个整数，表示数组A。

第三行包含m个整数，表示数组B。

**输出格式**

共一行，包含两个整数 i 和 j。

```r
数据范围

数组长度不超过100000。
同一数组内元素各不相同。
1≤数组元素≤109

输入样例：

4 5 6
1 2 4 7
3 4 6 8 9

输出样例：

1 1
```

### Solution

```java
import java.util.*;
import java.io.*;

public class Main{
    public static void main(String[] args) throws IOException{
        BufferedReader in = new BufferedReader(new InputStreamReader(System.in));
        String[] s = in.readLine().split(" ");
        int n = Integer.parseInt(s[0]);
        int m = Integer.parseInt(s[1]);
        int x = Integer.parseInt(s[2]);
        int[] a = new int[n + 10];
        int[] b = new int[m + 10];
        s = in.readLine().split(" ");
        for(int i = 0; i < n; i++){
            a[i] = Integer.parseInt(s[i]);
        }
        s = in.readLine().split(" ");
        for(int i = 0; i < m; i++){
            b[i] = Integer.parseInt(s[i]);
        }
        // A 数组正序遍历
        // B 数组倒序遍历
        for(int i = 0, j = m - 1; i < n; i++){
            while(j > 0 && a[i] + b[j] > x) j--;
            if(a[i] + b[j] == x){
                System.out.println(i + " " + j);
            }
        }
        
    }
}
```
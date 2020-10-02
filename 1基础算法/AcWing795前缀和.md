# AcWing 算法基础课 -- 基础算法

## AcWing 795. 前缀和 

`难度：简单`

### 题目描述

输入一个长度为n的整数序列。

接下来再输入m个询问，每个询问输入一对l, r。

对于每个询问，输出原序列中从第l个数到第r个数的和。

**输入格式**

第一行包含两个整数n和m。

第二行包含n个整数，表示整数数列。

接下来m行，每行包含两个整数l和r，表示一个询问的区间范围。

**输出格式**

共m行，每行输出一个询问的结果。

```r
数据范围

1≤l≤r≤n,
1≤n,m≤100000,
−1000≤数列中元素的值≤1000

输入样例：

5 3
2 1 3 6 4
1 2
1 3
2 4

输出样例：

3
6
10
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
        s = in.readLine().split(" ");
        int[] a = new int[n];
        int[] p = new int[n + 1];
        // 计算前缀和：前i个元素的前缀和
        // 下标领先一个数组小标，为了表示出前 0 个前缀和为 0
        for(int i = 0; i < n; i++){
            a[i] = Integer.parseInt(s[i]);
            p[i + 1] = p[i] + a[i];
        }
        while(m>0){
            m--;
            s = in.readLine().split(" ");
            int l = Integer.parseInt(s[0]);
            int r = Integer.parseInt(s[1]);
            System.out.println(p[r] - p[l - 1]);
        }
    }
}
```
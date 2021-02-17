# AcWing 算法基础课 -- 数据结构

## AcWing 830. 单调栈 

`难度：简单`

### 题目描述

给定一个长度为N的整数数列，输出每个数左边第一个比它小的数，如果不存在则输出-1。

**输入格式**

第一行包含整数N，表示数列长度。

第二行包含N个整数，表示整数数列。

**输出格式**

共一行，包含N个整数，其中第i个数表示第i个数的左边第一个比它小的数，如果不存在则输出-1。

```r
数据范围

1≤N≤105

1≤数列中元素≤109

输入样例：

5
3 4 2 7 5

输出样例：

-1 3 -1 2 2
```

### Solution

```java
import java.util.*;
import java.io.*;

class Main{
    static final int N = 100010;
    static int[] a = new int[N];
    static int[] stk = new int[N];
    static int hh = 0;
    public static void main(String[] args) throws IOException{
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
        String[] s = br.readLine().split(" ");
        int n = Integer.parseInt(s[0]);
        s = br.readLine().split(" ");
        for(int i = 0; i < n; i ++) a[i] = Integer.parseInt(s[i]);
        // 输出每个数左边第一个比它小的数
        // 单调递增的栈
        for(int i = 0; i < n; i++){
            while(hh > 0 && a[stk[hh]] >= a[i]) hh--;
            if(hh == 0) bw.write("-1 ");
            else bw.write(a[stk[hh]] + " ");
            hh++;
            stk[hh] = i;
        }
        bw.close();
        br.close();
    }
}
```
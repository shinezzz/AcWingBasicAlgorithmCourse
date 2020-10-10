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

public class Main{
    public static void main(String[] args) throws IOException{
        int N = 100010;
        int[] stk = new int[N];
        int tt = 0;
        BufferedReader in = new BufferedReader(new InputStreamReader(System.in));
        int n = Integer.parseInt(in.readLine());
        String[] s = in.readLine().split(" ");
        for(int i = 0; i < n; i++){
            int x = Integer.parseInt(s[i]);
            while(tt > 0 && stk[tt] >= x) tt--;
            if(tt > 0) System.out.print(stk[tt] + " ");
            else System.out.print(-1 + " ");
            tt++;
            stk[tt] = x;
        }
    }
}
```
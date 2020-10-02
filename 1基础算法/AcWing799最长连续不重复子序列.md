# AcWing 算法基础课 -- 基础算法

## AcWing 799. 最长连续不重复子序列

`难度：简单`

### 题目描述

给定一个长度为n的整数序列，请找出最长的不包含重复的数的连续区间，输出它的长度。

**输入格式**

第一行包含整数n。

第二行包含n个整数（均在0~100000范围内），表示整数序列。

**输出格式**

共一行，包含一个整数，表示最长的不包含重复的数的连续区间的长度。

```r
数据范围

1≤n≤100000

输入样例：

5
1 2 2 3 5

输出样例：

3
```

### Solution

```java
import java.util.*;
import java.io.*;

public class Main{
    public static void main(String[] args) throws IOException{
        BufferedReader in = new BufferedReader(new InputStreamReader(System.in));
        BufferedWriter out = new BufferedWriter(new OutputStreamWriter(System.out));
        int n = Integer.parseInt(in.readLine());
        String[] s = in.readLine().split(" ");
        int[] a = new int[n + 10];
        for(int i = 0; i < n; i++){
            a[i] = Integer.parseInt(s[i]);
        }
        int[] q = new int[100010];
        int res = 0;
        // 区间 [i, j] 为不包含重复元素的区间
        // 遍历每一个元素，找到以该元素为结尾的最长不重复字符串
        // 当结尾元素往后移
        // 1. 如果出现了重复字符，开始元素往后移动
        // 2. 如果没有出现重复元素，开始元素不动
        // 可以发现开始元素的移动具有单调性
        // 这种场景适合双指针
        for(int i = 0, j = 0; j < n; j++){
            q[a[j]]++;
            while(i < j && q[a[j]] > 1){
                q[a[i]]--;
                i++;
            }
            res = Math.max(res, j - i + 1);
        }
        out.write(String.valueOf(res));
        out.flush();
    }
}
```
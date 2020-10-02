# AcWing 算法基础课 -- 基础算法

## AcWing 797. 差分 

`难度：简单`

### 题目描述

输入一个长度为n的整数序列。

接下来输入m个操作，每个操作包含三个整数l, r, c，表示将序列中[l, r]之间的每个数加上c。

请你输出进行完所有操作后的序列。

**输入格式**

第一行包含两个整数n和m。

第二行包含n个整数，表示整数序列。

接下来m行，每行包含三个整数l，r，c，表示一个操作。

**输出格式**

共一行，包含n个整数，表示最终序列。


```r
数据范围

1≤n,m≤100000,
1≤l≤r≤n,
−1000≤c≤1000,
−1000≤整数序列中元素的值≤1000

输入样例：

6 3
1 2 2 1 2 1
1 3 1
3 5 1
1 6 1

输出样例：

3 4 5 3 4 2
```

### Solution

```java
import java.util.*;
import java.io.*;

public class Main{
    public static void main(String[] args) throws IOException{
        BufferedReader in = new BufferedReader(new InputStreamReader(System.in));
        String[] s = in.readLine().split(" ");
        // 整数序列 n 个整数
        int n = Integer.parseInt(s[0]);
        // m 个插入操作
        // 插入操作对于数组的索引是从 1 开始的
        // 所以建立差分数组也是从从 1 开始，比较不容易出错
        int m = Integer.parseInt(s[1]);
        s = in.readLine().split(" ");
        int[] a = new int[n + 10];
        for(int i = 1; i <= n; i++){
            int c = Integer.parseInt(s[i - 1]);
            // 插入 c
            insert(a, i, i, c);
        }
        while(m > 0){
            m--;
            s = in.readLine().split(" ");
            int l = Integer.parseInt(s[0]);
            int r = Integer.parseInt(s[1]);
            int c = Integer.parseInt(s[2]);
            insert(a, l, r, c);
        }
        for(int i = 1; i <= n; i++){
            a[i] += a[i - 1];
            System.out.print(a[i] + " ");
        }
        
    }
    
    public static void insert(int[] a, int l, int r, int c){
        a[l] += c;
        a[r + 1] -= c;
    }
    
}
```
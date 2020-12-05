# AcWing 算法基础课 -- 数据结构

## AcWing 143. 最大异或对

`难度：简单`

### 题目描述

在给定的N个整数A1，A2……AN

中选出两个进行xor（异或）运算，得到的结果最大是多少？

**输入格式**

第一行输入一个整数N。

第二行输入N个整数A1～AN。

**输出格式**

输出一个整数表示答案。

**数据范围**

$1≤N≤10^5,$
$0≤Ai<2^31$

```r
输入样例：

3
1 2 3

输出样例：

3
```

### Solution

```java
import java.util.*;
import java.io.*;

class Main{
    static final int N = 100010;
    static final int M = 31 * N;
    static int[][] son = new int[M][2];
    static int[] a = new int[N];
    static int idx = 0;
    public static void insert(int x){
        int p = 0;
        for(int i = 30; i >= 0; i--){
            int t = x >> i & 1;
            if(son[p][t] == 0) son[p][t] = ++idx;
            p = son[p][t];
        }
    }
    public static int query(int x){
        int res = 0;
        int p = 0;
        for(int i = 30; i >= 0; i--){
            int t = x >> i & 1;
            if(son[p][t ^ 1] != 0) {
                p = son[p][t ^ 1];
                res = res * 2 + (t ^ 1);
            }
            else {
                p = son[p][t];
                res = res * 2 + t;
            }
        }
        return res;
    }
    public static void main(String[] args) throws IOException{
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        String[] s = br.readLine().split(" ");
        int n = Integer.parseInt(s[0]);
        s = br.readLine().split(" ");
        for(int i = 0; i < n; i++) a[i] = Integer.parseInt(s[i]);
        int res = 0;
        for(int i = 0; i < n; i++){
            insert(a[i]);
            int t = query(a[i]);
            res = Math.max(res, a[i] ^ t);
        }
        System.out.println(res);
    }
} 
```
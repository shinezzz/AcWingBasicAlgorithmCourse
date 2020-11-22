# AcWing 算法基础课 -- 基础算法

## AcWing 786. 第k个数 

`难度：简单`

### 题目描述

给定一个长度为n的整数数列，以及一个整数k，请用快速选择算法求出数列从小到大排序后的第k个数。

**输入格式**

输入共两行，第一行包含两个整数 n 和 k。

第二行包含 n 个整数（所有整数均在$1~10^9$范围内），表示整个数列。

**输出格式**

输出一个整数，表示数列的第k小数。

**数据范围**

1 ≤ n ≤ 100000
1 ≤ k ≤ n

**输入样例**：

```
5 3
2 4 1 5 3
```

**输出样例**：

```
3
```

### Solution

```java 
import java.util.*;
import java.io.*;

class Main{
    static int N = 100010;
    static int[] q = new int[N];
    public static void main(String[] args) throws IOException{
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        String[] s = br.readLine().split(" ");
        int n = Integer.parseInt(s[0]);
        int k = Integer.parseInt(s[1]);
        s = br.readLine().split(" ");
        for(int i = 0; i < n; i++){
            q[i] = Integer.parseInt(s[i]);
        }
        quickSort(0, n - 1, k);
        System.out.println(q[k - 1]);
    }
    public static void quickSort(int l, int r, int k){
        if(l >= r) return;
        int i = l - 1, j = r + 1, x = q[l + r >> 1];
        while(i < j){
            do i++; while(q[i] < x);
            do j--; while(q[j] > x);
            if(i < j){
                int t = q[i];
                q[i] = q[j];
                q[j] = t;
            }

        }
        // 第 k 数字的下标为 k - 1
        // 如果第 k 个数字在 j 的右边就递归右边
        // 否则递归左边
        // 这样可以把时间复杂度优化为  O(n)
        if(k - 1 > j) quickSort(j + 1, r, k);
        else quickSort(l, j, k);
    }
}
```


# AcWing 算法基础课 -- 基础算法

## AcWing 787. 归并排序

`难度：简单`

### 题目描述

给定你一个长度为n的整数数列。

请你使用快速排序对这个数列按照从小到大进行排序。

并将排好序的数列按顺序输出。

**输入格式**

输入共两行，第一行包含整数 n。

第二行包含 n 个整数（所有整数均在$1~10^9$范围内），表示整个数列。

**输出格式**

输出共一行，包含 n 个整数，表示排好序的数列。

**数据范围**

1 ≤ n ≤ 100000

**输入样例**：

```
5
3 1 2 4 5
```

**输出样例**：

```
1 2 3 4 5
```

### Solution

```java
import java.util.*;
import java.io.*;

public class Main{
    public static void main(String[] args) throws IOException{
        BufferedReader in = new BufferedReader(new InputStreamReader(System.in));
        int n = Integer.parseInt(in.readLine());
        int[] q = new int[n];
        int[] tmp = new int[n];
        String[] s = in.readLine().split(" ");
        for(int i = 0; i < n; i++){
            q[i] = Integer.parseInt(s[i]);
        }
        mergeSort(q, 0, n - 1, tmp);
        for(int num : q){
            System.out.print(num + " ");
        }
    }
    
    public static void mergeSort(int[] q, int l, int r, int[] tmp){
        if(l >= r) return;
        int mid = l + r >> 1;
        mergeSort(q, l, mid, tmp);
        mergeSort(q, mid + 1, r, tmp);
        int k = 0, i = l, j = mid + 1;
        while(i <= mid && j <= r){
            if(q[i] <= q[j]) tmp[k++] = q[i++];
            else tmp[k++] = q[j++];
        }
        while(i <= mid) tmp[k++] = q[i++];
        while(j <= r) tmp[k++] = q[j++];
        for(i = l, j = 0; i <= r; i++, j++) q[i] = tmp[j];
    }
}
```
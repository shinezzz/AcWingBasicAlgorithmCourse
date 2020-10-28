# AcWing 算法基础课 -- 搜索与图论
## AcWing 842. 排列数字 

`难度：简单`

### 题目描述

给定一个整数n，将数字1~n排成一排，将会有很多种排列方法。

现在，请你按照字典序将所有的排列方法输出。

**输入格式**

共一行，包含一个整数n。

**输出格式**

按字典序输出所有排列方案，每个方案占一行。

**数据范围**

$1≤n≤7$

```r
输入样例：

3

输出样例：

1 2 3
1 3 2
2 1 3
2 3 1
3 1 2
3 2 1
```

### Solution

```java
import java.util.*;
import java.io.*;

class Main{
    public static int N = 10;
    public static int[] a = new int[N];
    public static boolean[] flag = new boolean[N];
    public static void main(String[] args) throws IOException{
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();
        dfs(1, n);
    }
    public static void dfs(int u, int n){
        // 满足结束条件，打印输出
        if(u == n + 1){
            for(int i = 1; i <= n; i++){
                System.out.print(a[i] + " ");
            }
            System.out.println();
            return;
        }
        // 遍历选择列表
        for(int i = 1; i <= n; i++){
            // 如果这个选项还没有选择
            if(!flag[i]){
                // 标记
                flag[i] = true;
                // 选择放进路径
                a[u] = i;
                // 递归
                dfs(u + 1, n);
                // 恢复现场
                flag[i] = false;
                a[u] = 0;
            }
        }
    }
}
```
# AcWing 算法基础课 -- 动态规划

## AcWing 898. 数字三角形 

`难度：简单`

### 题目描述

给定一个如下图所示的数字三角形，从顶部出发，在每一结点可以选择移动至其左下方的结点或移动至其右下方的结点，一直走到底层，要求找出一条路径，使路径上的数字的和最大。

```r
        7
      3   8
    8   1   0
  2   7   4   4
4   5   2   6   5
```

**输入格式**

第一行包含整数n，表示数字三角形的层数。

接下来n行，每行包含若干整数，其中第 i 行表示数字三角形第 i 层包含的整数。

**输出格式**

输出一个整数，表示最大的路径数字和。

**数据范围**

1≤n≤500,
−10000≤三角形中的整数≤10000

```r
输入样例：

5
7
3 8
8 1 0 
2 7 4 4
4 5 2 6 5

输出样例：

30
```

### Solution

1. 自顶向下动态规划

```java
import java.util.*;

class Main{
    public static void main(String[] args){
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();
        int INF = 0x3f3f3f3f;
        int[][] a = new int[n + 10][n + 10];
        int[][] dp = new int[n + 10][n + 10];
        // 整数中有负数，dp 数组还是初始化为负无穷，第 0 行初始化为0就行了
        for(int i = 1; i <= n; i++){
            Arrays.fill(dp[i], -INF);
            for(int j = 1; j <= i; j++)
                a[i][j] = sc.nextInt();
        }
        // 自顶向下
        // 状态表示：集合：dp[i][j] 自顶向下到达 ij 的路径和；属性：最大值
        // 状态计算：dp[i][j] = Math.max(dp[i - 1][j], dp[i - 1][j - 1]) + a[i][j];
        for(int i = 1; i <= n; i++){
            for(int j = 1; j <= i; j++)
                dp[i][j] = Math.max(dp[i - 1][j], dp[i - 1][j - 1]) + a[i][j];
        }
        int res = -INF;
        for(int k = 0; k <= n; k++) res = Math.max(res, dp[n][k]);
        System.out.println(res);
    }
}
```

2. 自底向上动态规划

```java
import java.util.*;

class Main{
    public static void main(String[] args){
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();
        int INF = 0x3f3f3f3f;
        int[][] a = new int[n + 10][n + 10];
        int[][] dp = new int[n + 10][n + 10];
        // 整数中有负数，dp 数组还是初始化为负无穷，第 0 行初始化为0就行了
        for(int i = 1; i <= n; i++){
            Arrays.fill(dp[i], -INF);
            for(int j = 1; j <= i; j++)
                a[i][j] = sc.nextInt();
        }
        // 自底向上
        // 状态表示：集合：dp[i][j] 自底向上到达 ij 的路径和；属性：最大值
        // 状态计算：dp[i][j] = Math.max(dp[i + 1][j], dp[i + 1][j + 1]) + a[i][j];
        for(int i = n; i >= 1; i--){
            for(int j = 1; j <= i; j++)
                dp[i][j] = Math.max(dp[i + 1][j], dp[i + 1][j + 1]) + a[i][j];
        }
        System.out.println(dp[1][1]);
    }
}
```
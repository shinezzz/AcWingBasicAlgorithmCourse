# LeetCode 专题 -- 背包专题

## AcWing 3. 完全背包问题

`难度：简单`

### 题目描述

有 N 种物品和一个容量是 V 的背包，每种物品都有无限件可用。

第 i 种物品的体积是 vi，价值是 wi。

求解将哪些物品装入背包，可使这些物品的总体积不超过背包容量，且总价值最大。
输出最大价值。

**输入格式**

第一行两个整数，N，V，用空格隔开，分别表示物品种数和背包容积。

接下来有 N 行，每行两个整数 vi,wi，用空格隔开，分别表示第 i 种物品的体积和价值。

**输出格式**

输出一个整数，表示最大价值。

**数据范围**：

- $0 < N,V ≤ 1000$
- $0 < vi,wi ≤ 1000$

```r
输入样例
4 5
1 2
2 4
3 4
4 5
输出样例：
10
```

**进阶**：

> 一维dp数组

**链接**：
> <https://www.acwing.com/problem/content/3/>

### Solution


> **结论**：
>
> 将0-1背包中j的循环顺序改成从小到大，就变成了完全背包。
>
> 0-1背包：`dp[i][j] = max(dp[i-1][j], dp[i-1][j-vi]+wi)`
>
> 完全背包：`dp[i][j] = max(dp[i-1][j], dp[i][j-vi]+wi)`

- 状态：`dp[i][j]`表示只看前`i`种物品，总体积不超过`j`的情况下，背包中物品的最大价值

- 状态转移方程：

    和0-1背包的区别在于每种物品有无限个，则划分子集的时候不再是分成两个子集（取和不取第i件物品），而是分成多个子集（不取第i件，第i件取1个，第i件取2个，...)

    推导：

    `dp[i][j] = max(dp[i-1][j], dp[i-1][j-vi]+wi, dp[i-1][j-2vi]+2wi,...)`

    把`j`用`j-vi`替代，可得

    `dp[i][j-vi] = max(dp[i-1][j-vi], dp[i-1][j-2vi]+wi, dp[i-1][j-3vi]+2wi,...)`

    则`dp[i][j] = max(dp[i-1][j], dp[i][j-vi]+wi)`

**普通版**：

```java
import java.util.*;

public class Main{
    public static void main(String[] args){
        Scanner scan = new Scanner(System.in);
        int N = scan.nextInt();
        int V = scan.nextInt();

        int[] v = new int[N + 10];
        int[] w = new int[N + 10];
        for(int i = 1; i <= N; i++){
            v[i] = scan.nextInt();
            w[i] = scan.nextInt();
        }
        scan.close();
        // 开始dp
        int[][] dp = new int[N + 10][V + 10];
        for(int i = 1; i <= N; i++){
            for(int j = 0; j <= V; j++){
                dp[i][j] = dp[i - 1][j];
                if(j >= v[i])
                    dp[i][j] = Math.max(dp[i][j], dp[i][j - v[i]] + w[i]);
            }
        }
        System.out.println(dp[N][V]);
    }
}
```

**进阶版**：

```java
import java.util.*;

public class Main{
    public static void main(String[] args){
        Scanner scan = new Scanner(System.in);
        int N = scan.nextInt();
        int V = scan.nextInt();
        int[] v = new int[N + 10];
        int[] w = new int[N + 10];
        for(int i = 1; i <= N; i++){
            v[i] = scan.nextInt();
            w[i] = scan.nextInt();
        }
        scan.close();
        // 开始dp
        int[] dp = new int[V + 10];
        for(int i = 1; i <= N; i++){
            for(int j = v[i]; j <= V; j++){
                dp[j] = Math.max(dp[j], dp[j - v[i]] + w[i]);
            }
        }
        System.out.println(dp[V]);
    }
}
```

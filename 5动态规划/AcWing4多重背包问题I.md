# LeetCode 专题 -- 背包专题

## AcWing 4. 多重背包问题 I

`难度：简单`

### 题目描述

有 N 种物品和一个容量是 V 的背包。

第 i 种物品最多有 si 件，每件体积是 vi，价值是 wi。

求解将哪些物品装入背包，可使物品体积总和不超过背包容量，且价值总和最大。
输出最大价值。

**输入格式**:

第一行两个整数，N，V，用空格隔开，分别表示物品种数和背包容积。

接下来有 N 行，每行三个整数 vi,wi,si，用空格隔开，分别表示第 i 种物品的体积、价值和数量。

**输出格式**
输出一个整数，表示最大价值。

**数据范围**：

- 0 < N,V ≤ 100
- 0 < vi,wi,si ≤ 100

```matlab
输入样例
4 5
1 2 3
2 4 1
3 4 3
4 5 2
输出样例：
10
```

**进阶**：

> 一维dp数组

**链接**：
> <https://www.acwing.com/problem/content/4/>

### Solution


**普通版**：

```java
import java.util.*;

class Main{
    public static void main(String[] args){
        Scanner sc = new Scanner(System.in);
        int N = sc.nextInt();
        int V = sc.nextInt();
        int[] v = new int[N + 10];
        int[] w = new int[N + 10];
        int[] s = new int[N + 10];
        for(int i = 1; i <= N; i++){
            v[i] = sc.nextInt();
            w[i] = sc.nextInt();
            s[i] = sc.nextInt();
        }
        int[][] dp = new int[N + 10][V + 10];
        for(int i = 1; i <= N; i++){
            for(int j = 1; j <= V; j++){
                dp[i][j] = dp[i - 1][j];
                // 前面跟01背包一样
                // 01背包可以看成每种只有1个的多重背包
                // 那多重背包就是遍历 k 个,
                // 循环条件是 k <= s[i] && k * v[i] <= j 
                for(int k = 1; k <= s[i] && k * v[i] <= j; k++){
                    dp[i][j] = Math.max(dp[i][j], dp[i - 1][j - k * v[i]] + k * w[i]);
                }
            }
        }
        System.out.println(dp[N][V]);
    }
}
```

**进阶版**：

```java
import java.util.*;

class Main{
    public static void main(String[] args){
        Scanner sc = new Scanner(System.in);
        int N = sc.nextInt();
        int V = sc.nextInt();
        int[] v = new int[N + 10];
        int[] w = new int[N + 10];
        int[] s = new int[N + 10];
        for(int i = 1; i <= N; i++){
            v[i] = sc.nextInt();
            w[i] = sc.nextInt();
            s[i] = sc.nextInt();
        }
        int[] dp = new int[V + 10];
        for(int i = 1; i <= N; i++){
            for(int j = V; j >= v[i]; j--){
                for(int k = 0; k <= s[i] && k * v[i] <= j; k++){
                    dp[j] = Math.max(dp[j], dp[j - k * v[i]] + k * w[i]);
                }
            }
        }
        System.out.println(dp[V]);
    }
}
```

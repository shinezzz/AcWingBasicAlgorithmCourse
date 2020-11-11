# LeetCode 专题 -- 背包专题

## AcWing 5. 多重背包问题 II 

`难度：中等`

### 题目描述

有 N 种物品和一个容量是 V 的背包。

第 i 种物品最多有 si 件，每件体积是 vi，价值是 wi。

求解将哪些物品装入背包，可使物品体积总和不超过背包容量，且价值总和最大。

输出最大价值。

**输入格式**

第一行两个整数，N，V，用空格隔开，分别表示物品种数和背包容积。

接下来有 N 行，每行三个整数 vi,wi,si，用空格隔开，分别表示第 i 种物品的体积、价值和数量。

**输出格式**
输出一个整数，表示最大价值。

**数据范围**：

- $0 < N ≤ 1000$
- $0 < V ≤ 2000$
- $0 < vi,wi,si ≤ 2000$

```r
输入样例
4 5
1 2 3
2 4 1
3 4 3
4 5 2
输出样例：
10
```

**提示**：

本题考查多重背包的二进制优化方法。

**进阶**：

> 一维dp数组

**链接**：
> <https://www.acwing.com/problem/content/5/>

### Solution

数据范围为1000，所以`O(N*V*s)`的复杂度会超时。

因此通过二进制优化降低复杂度。

**二进制优化**：

比如$10 =2^0 + 2^1 + 2^2+3$

将多重背包问题转化为0-1背包问题。即通过二进制转化的方式，将物品数量转化为多种物品数量的组合。比如假设物品有10个，即可转化为`1,2,4,3`，这四种无论如何组合，组合成的状态都在10以内，就可以转化为0-1背包问题。

**重点是理解二进制优化的思想**：

```java
import java.util.*;

class Main{
    static int M = 11010;
    public static void main(String[] args){
        Scanner sc = new Scanner(System.in);
        int N = sc.nextInt();
        int V = sc.nextInt();
        int M = 11 * N + 10;
        int[] v = new int[M];
        int[] w = new int[M];
        int idx = 0;
        // 二进制处理
        // 比如 10 可以拆分为 1，2，4，3
        // 用二进制拆分，最后不够的单独一项
        // 转化为 01 背包问题
        for(int i = 1; i <= N; i++){
            int a = sc.nextInt();
            int b = sc.nextInt();
            int s = sc.nextInt();
            int k = 1;
            while(k <= s){
                idx++;
                v[idx] = k * a;
                w[idx] = k * b;
                s -= k;
                k = k << 1;
            }
            if(s > 0){
                idx++;
                v[idx] = s * a;
                w[idx] = s * b;
            }
        }
        int[] dp = new int[V + 10];
        for(int i = 1; i <= idx; i++){
            for(int j = V; j >= v[i]; j--){
                dp[j] = Math.max(dp[j], dp[j - v[i]] + w[i]);
            }
        }
        System.out.println(dp[V]);
    }
}
```

# AcWing 算法基础课 -- 动态规划

## AcWing 2. 01背包问题 

`难度：简单`

### 题目描述

有 N 件物品和一个容量是 V 的背包。每件物品只能使用一次。

第 i 件物品的体积是 vi，价值是 wi。

求解将哪些物品装入背包，可使这些物品的总体积不超过背包容量，且总价值最大。
输出最大价值。

**输入格式**：

第一行两个整数，N，V，用空格隔开，分别表示物品数量和背包容积。

接下来有 N 行，每行两个整数 vi,wi，用空格隔开，分别表示第 i 件物品的体积和价值。

**输出格式**：

输出一个整数，表示最大价值。

**数据范围**：

- $0 < N,V ≤ 1000$
- $0<vi,wi≤1000$

```matlab
输入样例
4 5
1 2
2 4
3 4
4 5
输出样例：
8
```

**进阶**：

> 一维dp数组

**链接**：
> <https://www.acwing.com/problem/content/2/>

### Solution


**思路**：

- 状态：`dp[i][j]`表示只看前`i`个物品，总体积不超过`j`的情况下，背包中物品的最大价值

    最后答案就是`dp[N][V]`

- 状态转移：找最后一个不同点，也就是选最后一个物品的不同方案。对于`dp[i][j]`有两种情况：

  1. 不选择当前的第件物品/第i件物品比背包容量要大

     则`dp[i][j] = dp[i-1][j]`

  2. 选择当前的第i件物品（潜在要求第i件物品体积小于等于背包总容量,即`v[i] >= j`）

     则`dp[i][j] = dp[i-1][j-v[i]] + w[i]`

    上面两种情况取max作为当前的最优解。

- 边界：`dp[0][0] = 0`

- **注意一些细节：**

  1. 如果` j `表示体积正好是` j `的话，那么答案就需要遍历求`max`。如果表示的是 不超过` j `的话，答案就是` dp[N][V] `。
  2. 如果题目要求背包必须放满，那么 `dp[0] [0…V]` 中仅仅有` dp[0][0]` 为0，其余值需被设置为`-INF`，返回dp[V]。
  3. 如果并没有要求必须把背包装满，而是只希望总价值尽量大，初始化时应该将`dp[0...V ]`全部设为0, 返回dp[V]。
  4. `i`和`j`从1开始循环。

**普通版**：

```java
import java.util.*;

class Main{
    public static void main(String[] args){
        // 输入数据
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
            for(int j = 1; j <= V; j++){
                // 放进去和不放进去取最大值
                dp[i][j] = dp[i - 1][j];
                if(j >= v[i])
                    dp[i][j] = Math.max(dp[i][j], dp[i - 1][j - v[i]] + w[i]);

            }
        }
        // int res = 0;
        // for(int i = 0; i <= V; i++) res = Math.max(res, dp[N][i]);
        // System.out.println(res);
        // 或者
        System.out.println(dp[N][V]);
    }
}
```

**进阶版**：

1. `dp[j]`表示体积不超过`j`的情况下的最大价值。
2. `dp[i][j] = max(dp[i-1][j], dp[i-1][j-v[i]] + w[i])`，看`j`，第二维要不就是用`j`，要不是就是用比`j`小的数。
3. 如果j从小往大循环，后面的dp[j]可能已经被前面的更新了，相当于dp[i][j - v[i]]
4. 所以让`j`从大到小循环。把第一维去掉，变成了`dp[j] = max(dp[j], dp[j-v[i] + w[i])`，比如计算第二层的时候，`dp[j-v[i]]`还没有在第二层被更新过（因为`j-v[i]`比`j`小），所以这个时候的`dp[j-v[i]]`存的是上一层的状态，也就是`dp[i-1][j-v[i]]`

```java
import java.util.*;

class Main{
    public static void main(String[] args){
        // 输入数据
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
            for(int j = V; j >= v[i]; j--){
                // 放进去和不放进去取最大值
                dp[j] = Math.max(dp[j], dp[j - v[i]] + w[i]);
            }
        }
        // 如果初始化：dp[0]为0，其他为负无穷，就要遍历取最大值。
        // 这种情况对应体积恰好为V的价值，保证所有的状态从0转移来
        //
        // 如果初始化：dp[i]都为0，dp[V]也是最大值。假设dp[k]为最大值。
        // dp[k]从0转移过来，那dp[V]从dp[V-k]转移过来，是一样的
        System.out.println(dp[V]);
    }
}
```

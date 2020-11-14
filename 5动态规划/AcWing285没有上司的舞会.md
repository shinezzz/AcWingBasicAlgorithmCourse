# AcWing 算法基础课 -- 动态规划

## AcWing 285. 没有上司的舞会

`难度：简单`

### 题目描述


Ural大学有N名职员，编号为1~N。

他们的关系就像一棵以校长为根的树，父节点就是子节点的直接上司。

每个职员有一个快乐指数，用整数 Hi 给出，其中 1≤i≤N。

现在要召开一场周年庆宴会，不过，没有职员愿意和直接上司一起参会。

在满足这个条件的前提下，主办方希望邀请一部分职员参会，使得所有参会职员的快乐指数总和最大，求这个最大值。

**输入格式**

第一行一个整数N。

接下来N行，第 i 行表示 i 号职员的快乐指数Hi。

接下来N-1行，每行输入一对整数L, K,表示K是L的直接上司。

**输出格式**

输出最大的快乐指数。

**数据范围**

1≤N≤6000,

−128≤Hi≤127

```r
输入样例：

7
1
1
1
1
1
1
1
1 3
2 3
6 4
7 4
4 5
3 5

输出样例：

5
```

### Solution

```java
import java.util.*;

class Main{
    static int N = 6010;
    // w[i] i 号职员的快乐指数
    static int[] w = new int[N];
    // 建树
    static int[] e = new int[N];
    static int[] ne = new int[N];
    static int[] h = new int[N];
    static int idx = 1;
    // 记录有没有父节点
    static boolean[] hasF = new boolean[N];
    // 添加一条 a 指向 b 的边
    public static void add(int a, int b){
        e[idx] = b;
        ne[idx] = h[a];
        h[a] = idx++;
    }
    public static void dfs(int u, int[][] dp){
        // 不需要递归结束条件
        dp[u][1] = w[u];
        for(int i = h[u]; i != 0; i = ne[i]){
            int j = e[i];
            // 递归到叶子节点,然后往树根走
            dfs(j, dp);
            dp[u][0] += Math.max(dp[j][0], dp[j][1]);
            dp[u][1] += dp[j][0];
        }
    }
    public static void main(String[] args){
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();
        for(int i = 1; i <= n; i++) w[i] = sc.nextInt();
        // 建树
        for(int i = 1; i < n; i++) {
            int l = sc.nextInt();
            int k = sc.nextInt();
            // k 是 l 的上司，添加一条 k 指向 l 的边
            add(k, l);
            hasF[l] = true;
        }
        // 找根节点
        int root = 1;
        while(hasF[root]) root++;
        // 从根节点开始递归
        // 状态表示：
        // dp[u][0] 表示是不偷 u 的最大值
        // dp[u][1] 表示偷 u 的最大值
        // 状态计算：
        // 遍历当前节点的所有子节点
        // for(int i = h[u]; i != 0; i = ne[i]) j = e[i]
        // dp[i][0] += Math.max(dp[j][0], dp[j][1])
        // dp[i][1] += dp[j][0]
        // 初始化
        // dp[u][1] = w[u]
        int[][] dp = new int[N][2];
        dfs(root, dp);
        System.out.println(Math.max(dp[root][0], dp[root][1]));
    }
}
```
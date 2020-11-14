# AcWing 算法基础课 -- 动态规划

## AcWing 901. 滑雪

`难度：简单`

### 题目描述

给定一个R行C列的矩阵，表示一个矩形网格滑雪场。

矩阵中第 i 行第 j 列的点表示滑雪场的第 i 行第 j 列区域的高度。

一个人从滑雪场中的某个区域内出发，每次可以向上下左右任意一个方向滑动一个单位距离。

当然，一个人能够滑动到某相邻区域的前提是该区域的高度低于自己目前所在区域的高度。

```r
下面给出一个矩阵作为例子：

 1  2  3  4 5

16 17 18 19 6

15 24 25 20 7

14 23 22 21 8

13 12 11 10 9
```

在给定矩阵中，一条可行的滑行轨迹为24-17-2-1。

在给定矩阵中，最长的滑行轨迹为25-24-23-…-3-2-1，沿途共经过25个区域。

现在给定你一个二维矩阵表示滑雪场各区域的高度，请你找出在该滑雪场中能够完成的最长滑雪轨迹，并输出其长度(可经过最大区域数)。

**输入格式**

第一行包含两个整数R和C。

接下来R行，每行包含C个整数，表示完整的二维矩阵。

**输出格式**

输出一个整数，表示可完成的最长滑雪长度。

**数据范围**

1≤R,C≤300,
0≤矩阵中整数≤10000

```r
输入样例：

5 5
1 2 3 4 5
16 17 18 19 6
15 24 25 20 7
14 23 22 21 8
13 12 11 10 9

输出样例：

25
```

### Solution

```java
import java.util.*;
import java.io.*;

class Main{
    static int N = 310;
    static int[][] g = new int[N][N];
    static int[][] dp = new int[N][N];
    // 四个方向
    static int[] dx = {-1, 0, 1, 0}, dy = {0, -1, 0, 1};
    static int R, C;
    public static int dfs(int x, int y){
        // 剪枝:判断这个点是否已经计算过
        if(dp[x][y] != -1) return dp[x][y];
        // 一个点走不通了,最少有 1 ;
        dp[x][y] = 1;
        // 朝四个方向递归
        for(int i = 0; i < 4; i++){
            int a = x + dx[i];
            int b = y + dy[i];
            // 判断 (a, b) 是否合法, 在滑雪场内 且 a[x][y] > g[a][b]
            if(a >= 1 && a <= R && b >= 1 && b <= C && g[x][y] > g[a][b])
                dp[x][y] = Math.max(dp[x][y], dfs(a, b) + 1);
        }
        return dp[x][y];
    }
    public static void main(String[] args) throws IOException{
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        String[] s = br.readLine().split(" ");
        R = Integer.parseInt(s[0]);
        C = Integer.parseInt(s[1]);
        for(int i = 1; i <= R; i++){
            s = br.readLine().split(" ");
            for(int j = 1; j <= C; j++){
                g[i][j] = Integer.parseInt(s[j - 1]);
            }
        }
        // 初始化DP数组为 -1
        for(int i = 0; i < N; i++) Arrays.fill(dp[i], -1);
        // 状态表示: dp[i][j] 表示从 (i,j) 出发的点滑雪路径的最大和
        // 状态计算: 递归,判断 (i,j) 是否可以继续走下去
        // dp[i][j] = Math.max(dp[x][y], dfs(x, y) + 1);
        // 初始化: dp[i][j] = -1;如果能够走到那个点 dp[x][y] = 1;
        int res = 0;
        for(int i = 1; i <= R; i++)
            for(int j = 1; j <= C; j++)
                res = Math.max(res, dfs(i, j));
        System.out.println(res);
    }
}
```
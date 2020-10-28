# AcWing 算法基础课 -- 搜索与图论

## AcWing 843. n-皇后问题 

`难度：中等`

### 题目描述

n-皇后问题是指将 n 个皇后放在 n∗n 的国际象棋棋盘上，使得皇后不能相互攻击到，即任意两个皇后都不能处于同一行、同一列或同一斜线上。

现在给定整数n，请你输出所有的满足条件的棋子摆法。

**输入格式**

共一行，包含整数n。

**输出格式**

每个解决方案占n行，每行输出一个长度为n的字符串，用来表示完整的棋盘状态。

其中”.”表示某一个位置的方格状态为空，”Q”表示某一个位置的方格上摆着皇后。

每个方案输出完成后，输出一个空行。

输出方案的顺序任意，只要不重复且没有遗漏即可。

**数据范围**

$1≤n≤9$

```r
输入样例：

4

输出样例：

.Q..
...Q
Q...
..Q. 

..Q.
Q...
...Q
.Q..
```

### Solution

```java
import java.util.*;
import java.io.*;

class Main{
    public static int N = 15;
    // 存储结果
    public static char[][] res = new char[N][N];
    // 标记是否冲突，列，主对角线，副对角线
    // 因为是一行一行递归，所以行不会有冲突
    public static boolean[] col = new boolean[N];
    public static boolean[] dg = new boolean[2*N];
    public static boolean[] sdg = new boolean[2*N];
    public static void main(String[] args){
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();
        for(int i = 0; i < n; i++){
            for(int j =  0; j < n; j++){
                res[i][j] = '.';
            }
        }
        // DFS 的是行，从第 0 行开始
        dfs(0, n);
    }
    public static void dfs(int u, int n){
        // 如果已经遍历完所有行，输出答案
        if(u == n){
            for(int i = 0; i < n; i++){
                for(int j = 0; j < n; j++)
                    System.out.print(res[i][j]);
                System.out.println();
            }
            System.out.println();
            return;
        }
        // 遍历每一列，看是否可以放皇后
        for(int i = 0; i < n; i++){
            // 主对角线和为定值,副对角线差为定值,防止差为负数,加个N
            if(!col[i] && !dg[u + i] && !sdg[u - i + N]){
                col[i] = dg[u + i] = sdg[u - i + N] = true;
                res[u][i] = 'Q';
                dfs(u + 1, n);
                res[u][i] = '.';
                col[i] = dg[u + i] = sdg[u - i + N] = false;
            }
        }
    }
}
```
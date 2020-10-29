# AcWing 算法基础课 -- 搜索与图论

## AcWing 849. Dijkstra求最短路 I  

`难度：简单`

### 题目描述

给定一个n个点m条边的有向图，图中可能存在重边和自环，所有边权均为正值。

请你求出1号点到n号点的最短距离，如果无法从1号点走到n号点，则输出-1。

**输入格式**

第一行包含整数n和m。

接下来m行每行包含三个整数x，y，z，表示存在一条从点x到点y的有向边，边长为z。

**输出格式**

输出一个整数，表示1号点到n号点的最短距离。

如果路径不存在，则输出-1。

**数据范围**

$1≤n≤500,$
$1≤m≤10^5,$

图中涉及边长均不超过10000。

```r
输入样例：

3 3
1 2 2
2 3 1
1 3 4

输出样例：

3
```

### Solution

```java
import java.util.*;
import java.io.*;

class Main{
    public static final int N = 510;
    public static final int INF = 0x3f3f3f3f;
    // 稠密图，用邻接矩阵来存
    public static int[][] g = new int[N][N];
    public static int[] d = new int[N];
    public static boolean[] flag = new boolean[N];
    public static void main(String[] args) throws IOException{
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        String[] s = br.readLine().split(" ");
        int n = Integer.parseInt(s[0]);
        int m = Integer.parseInt(s[1]);
        // 初始化为 INF
        for(int i = 0; i < N; i++){
            Arrays.fill(g[i], INF);
        }
        Arrays.fill(d, INF);
        while(m-- > 0){
            s = br.readLine().split(" ");
            int x = Integer.parseInt(s[0]);
            int y = Integer.parseInt(s[1]);
            int z = Integer.parseInt(s[2]);
            // 如果有重边或者自环，就选较小的
            g[x][y] = Math.min(g[x][y], z);
        }
        System.out.println(dijkstra(n));
    }
    public static int dijkstra(int n){
        d[1] = 0;
        // 迭代 n 次
        // 每次找当前没有确定最短路长度的点当中距离最小的一个
        for(int i = 1; i <= n; i++){
            int t = -1;
            // 遍历 1-n 个点，找到还没处理的且距离最小的
            for(int j = 1; j <= n; j++){
                if(!flag[j] && (t == -1 || d[t] > d[j]))
                    t = j;
            }
            // 找到 t，打标记
            flag[t] = true;
            // 已经找到了最短 d[t]，更新一波
            for(int j = 1; j <= n; j++){
                d[j] = Math.min(d[j], d[t] + g[t][j]);
            }
        }
        if(d[n] == 0x3f3f3f3f) return -1;
        return d[n];
    }
}
```
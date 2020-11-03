# AcWing 算法基础课 -- 搜索与图论

## AcWing 858. Prim算法求最小生成树 

`难度：简单`

### 题目描述

给定一个n个点m条边的无向图，图中可能存在重边和自环，边权可能为负数。

求最小生成树的树边权重之和，如果最小生成树不存在则输出impossible。

给定一张边带权的无向图G=(V, E)，其中V表示图中点的集合，E表示图中边的集合，n=|V|，m=|E|。

由V中的全部n个顶点和E中n-1条边构成的无向连通子图被称为G的一棵生成树，其中边的权值之和最小的生成树被称为无向图G的最小生成树。

**输入格式**

第一行包含两个整数n和m。

接下来m行，每行包含三个整数u，v，w，表示点u和点v之间存在一条权值为w的边。

**输出格式**

共一行，若存在最小生成树，则输出一个整数，表示最小生成树的树边权重之和，如果最小生成树不存在则输出impossible。

**数据范围**

$1≤n≤500,$
$1≤m≤105,$
图中涉及边的边权的绝对值均不超过10000。

```r
输入样例：

4 5
1 2 1
1 3 2
1 4 3
2 3 2
3 4 4

输出样例：

6
```

### Solution

```java
import java.util.*;
import java.io.*;

class Main{
    static final int INF = 0x3f3f3f3f;
    static final int N = 510;
    // 邻接矩阵存图
    static int[][] g = new int[N][N];
    // 记录 i 点到当前最小生成树的距离
    static int[] dist = new int[N];
    // 标记 i 点是否已经在最小生成树中
    static boolean[] flag = new boolean[N];
    // 存储最小生成树的距离
    static int res = 0;
    public static int prim(int n){
        Arrays.fill(dist, INF);
        dist[1] = 0;
        // 迭代 n 次
        for(int i = 1; i <= n; i++){
            // 找集合外距离集合最近的点
            // 用 t 来存储该点的序号
            int t = -1;
            for(int j = 1; j <= n; j++){
                if(!flag[j] &&(t == -1 || dist[j] < dist[t]))
                    t = j;
            }
            flag[t] = true;
            // 如果所有点距离集合的距离都为INF，即不可达，则说明没有最小生成树
            if(dist[t] == INF) return INF;
            res += dist[t];
            // 更新所有点到集合的距离
            // 因为就新加了 t 点，所以就比较一下各个点到 t 的距离与原来的dist就行了
            // 注意这一句要放在 res += dist[t]之后
            // 因为如果有自环 dist[t] = Math.min(dist[t], g[t][t]);这样距离就变了
            for(int j = 1; j <= n; j++) dist[j] = Math.min(dist[j], g[t][j]);
        }
        return res;
    }
    
    public static void main(String[] args) throws IOException{
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        String[] s = br.readLine().split(" ");
        int n = Integer.parseInt(s[0]);
        int m = Integer.parseInt(s[1]);
        for(int i = 0; i < N; i++){
            Arrays.fill(g[i], INF);
        }
        while(m-- > 0){
            s = br.readLine().split(" ");
            int u = Integer.parseInt(s[0]);
            int v = Integer.parseInt(s[1]);
            int w = Integer.parseInt(s[2]);
            // 稠密图用邻接矩阵来存
            g[u][v] = g[v][u] = Math.min(g[u][v], w);
        }
        if(prim(n) == INF) System.out.println("impossible");
        else System.out.println(res);
        
    }
}

```
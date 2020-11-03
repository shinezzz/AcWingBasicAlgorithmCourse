# AcWing 算法基础课 -- 搜索与图论

## AcWing 

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

$1≤n≤10^5,$
$1≤m≤2∗10^5,$
图中涉及边的边权的绝对值均不超过1000。

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
    static final int N = 100010;
    static final int INF = 0x3f3f3f3f;
    // 并查集在 O(1) 复杂度来检测a，b是否连通
    static int[] p = new int[N];
    // 最小生成树的长度
    static int res = 0;
    static class Edge{
        int u, v, w;
        public Edge(int u, int v, int w){
            this.u = u;
            this.v = v;
            this.w = w;
        }
    }
    public static int kruskal(int n, int m, Edge[] edges){
        Arrays.sort(edges, (Edge e1, Edge e2) -> e1.w - e2.w);
        // 初始化并查集
        for(int i = 1; i <= n; i++) p[i] = i;
        int cnt = 0;
        for(int i = 0; i < m; i++){
            int u = edges[i].u, v = edges[i].v, w = edges[i].w;
            // 并查集操作检查一条边的两个点是否连通
            // 找 u，v 的根节点
            u = find(u);
            v = find(v);
            // 两个连通块不连通，就合并
            if(u != v){
                p[u] = v;
                res += w;
                cnt++;
            }
        }
        if(cnt < n - 1) return INF;
        else return res;
    }
    public static int find(int x){
        if(p[x] != x) p[x] = find(p[x]);
        return p[x];
    }
    public static void main(String[] args) throws IOException{
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        String[] s = br.readLine().split(" ");
        int n = Integer.parseInt(s[0]);
        int m = Integer.parseInt(s[1]);
        // 存边
        Edge[] edges = new Edge[m];
        // 要排序还是从 0 开始
        for(int i = 0; i < m; i++){
            s = br.readLine().split(" ");
            int u = Integer.parseInt(s[0]);
            int v = Integer.parseInt(s[1]);
            int w = Integer.parseInt(s[2]);
            // 枚举每条边，就不用邻接表了，直接一个数组
            edges[i] = new Edge(u, v, w);
        }
        
        int t = kruskal(n, m, edges);
        if(t == INF) System.out.println("impossible");
        else System.out.println(res);
    }
}
```
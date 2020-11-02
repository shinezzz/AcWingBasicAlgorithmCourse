# AcWing 算法基础课 -- 搜索与图论

## AcWing 853. 有边数限制的最短路

`难度：简单`

### 题目描述

给定一个n个点m条边的有向图，图中可能存在重边和自环， 边权可能为负数。

请你求出从1号点到n号点的最多经过k条边的最短距离，如果无法从1号点走到n号点，输出impossible。

注意：图中可能 存在负权回路 。

**输入格式**

第一行包含三个整数n，m，k。

接下来m行，每行包含三个整数x，y，z，表示存在一条从点x到点y的有向边，边长为z。

**输出格式**

输出一个整数，表示从1号点到n号点的最多经过k条边的最短距离。

如果不存在满足条件的路径，则输出“impossible”。

**数据范围**

$1≤n,k≤500,$
$1≤m≤10000,$

任意边长的绝对值不超过10000。

```r
输入样例：

3 3 1
1 2 1
2 3 1
1 3 3

输出样例：

3
```

### Solution

Bellman-Ford算法

时间复杂度 $O(nm)$, n 表示点数，m 表示边数

**一般 spfa 性能比 Bellman-Ford 好，只有特殊情况下用 Bellman-Ford 算法，比如这题有边的数量的限制**

1. 思路
```r
for n 次
    for 所有边 a,b,w
        dist[b] = min(dist[b], dist[a] + w)
```

2. 解题代码

```java
import java.util.*;
import java.io.*;

class Main{
    // 稀疏图用邻接表来存储
    static int N = 510;
    static int M = 10010;
    // 存储所有边
    static Node[] e = new Node[M];
    // 存储距离起点的距离
    static int[] d = new int[N];
    // 备份 d 数组
    static int[] b = new int[N];
    static int idx = 1;
    // 初始化值
    static final int INF = 0x3f3f3f3f;
    public static void main(String[] args) throws IOException{
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        String[] s = br.readLine().split(" ");
        int n = Integer.parseInt(s[0]);
        int m = Integer.parseInt(s[1]);
        int k = Integer.parseInt(s[2]);
        for(int i = 1; i <= m; i++){
            s = br.readLine().split(" ");
            int x = Integer.parseInt(s[0]);
            int y = Integer.parseInt(s[1]);
            int z = Integer.parseInt(s[2]);
            e[i] = new Node(x, y, z);
        }
        bellmanFord(n, m, k);
    }
    public static void bellmanFord(int n, int m, int k){
        Arrays.fill(d, INF);
        // 起点初始化为 0
        d[1] = 0;
        // 最多 k 条边,循环限制 k 次
        for(int i = 0; i < k; i++){
            // 拷贝数组,否则会有串联问题,导致计算边的数量不准确
            b = Arrays.copyOf(d, N);
            for(int j = 1; j <= m; j++){
                 int x = e[j].x, y = e[j].y, z = e[j].z;
                 d[y] = Math.min(d[y], b[x] + z);
            }
        }
        if(d[n] > INF / 2){
            System.out.println("impossible");
        }else{
            System.out.println(d[n]);
        }
    }
    static class Node{
        int x, y, z;
        public Node(int x, int y, int z){
            this.x = x;
            this.y = y;
            this.z = z;
        }
    }
}
```
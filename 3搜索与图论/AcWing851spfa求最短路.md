# AcWing 算法基础课 -- 搜索与图论

## AcWing 851. spfa求最短路

`难度：简单`

### 题目描述

给定一个n个点m条边的有向图，图中可能存在重边和自环， 边权可能为负数。

请你求出1号点到n号点的最短距离，如果无法从1号点走到n号点，则输出impossible。

数据保证不存在负权回路。

**输入格式**

第一行包含整数n和m。

接下来m行每行包含三个整数x，y，z，表示存在一条从点x到点y的有向边，边长为z。

**输出格式**

输出一个整数，表示1号点到n号点的最短距离。

如果路径不存在，则输出”impossible”。

**数据范围**

$1≤n,m≤105,$

图中涉及边长绝对值均不超过10000。

```r
输入样例：

3 3
1 2 5
2 3 -3
1 3 4

输出样例：

2
```

### Solution

```java
import java.util.*;
import java.io.*;

class Main{
    static int INF = 0x3f3f3f3f;
    // 稀疏图用邻接表来存储
    static int N = 100010;
    static int[] e = new int[N];
    static int[] ne = new int[N];
    static int[] h = new int[N];
    static int[] w = new int[N];
    static int idx = 1;
    // 记录与起点的距离
    static int[] d = new int[N];
    // 记录队列里是否已经有了
    static boolean[] flag = new boolean[N];
    public static void add(int x, int y, int z){
        e[idx] = y;
        w[idx] = z;
        ne[idx] = h[x];
        h[x] = idx++;
    }
    public static int spfa(int n){
        // 初始化
        Arrays.fill(d, INF);
        d[1] = 0;
        Queue<Integer> q = new ArrayDeque<>();
        q.add(1);
        flag[1] = true;
        while(!q.isEmpty()){
            int t = q.remove();
            flag[t] = false;
            // 遍历所有以 t 为出发点的边
            for(int i = h[t]; i != 0; i = ne[i]){
                int j = e[i];
                if(d[j] > d[t] + w[i]){
                    d[j] = d[t] + w[i];
                    // 如果队列中没有 j,就将 j 入队
                    if(!flag[j]){
                        q.add(j);
                        flag[j] = true;
                    }
                }
            }
        }
        return d[n];
        
    }
    public static void main(String[] args) throws IOException{
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        String[] s = br.readLine().split(" ");
        int n = Integer.parseInt(s[0]);
        int m = Integer.parseInt(s[1]);
        while(m-- > 0){
            s = br.readLine().split(" ");
            int x = Integer.parseInt(s[0]);
            int y = Integer.parseInt(s[1]);
            int z = Integer.parseInt(s[2]);
            add(x, y, z);
        }
        if(spfa(n) < INF/2) System.out.println(d[n]);
        else System.out.println("impossible");
    }

}
```
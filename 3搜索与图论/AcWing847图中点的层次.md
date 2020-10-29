# AcWing 算法基础课 -- 搜索与图论

## AcWing 847. 图中点的层次 

`难度：简单`

### 题目描述

给定一个n个点m条边的有向图，图中可能存在重边和自环。

所有边的长度都是1，点的编号为1~n。

请你求出1号点到n号点的最短距离，如果从1号点无法走到n号点，输出-1。

**输入格式**

第一行包含两个整数n和m。

接下来m行，每行包含两个整数a和b，表示存在一条从a走到b的长度为1的边。

**输出格式**

输出一个整数，表示1号点到n号点的最短距离。

**数据范围**

$1≤n,m≤10^5$

```r
输入样例：

4 5
1 2
2 3
3 4
1 3
1 4

输出样例：

1
```

### Solution

```java
import java.util.*;
import java.io.*;

public class Main{
    public static final int N = 100010;
    // 建图
    public static int[] e = new int[N];
    public static int[] ne = new int[N];
    public static int[] h = new int[N];
    public static int idx = 1;
    // 记录 1 到 j 点的距离
    public static int[] dist = new int[N];
    // 存储结果
    public static int res = 0;
    public static void main(String[] args) throws IOException{
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
        String[] s = br.readLine().split(" ");
        int n = Integer.parseInt(s[0]);
        int m = Integer.parseInt(s[1]);
        while(m-- > 0){
            s = br.readLine().split(" ");
            int a = Integer.parseInt(s[0]);
            int b = Integer.parseInt(s[1]);
            add(a, b);
        }
        bfs();
        System.out.println(dist[n] - 1);
    }
    public static void add(int a, int b){
        e[idx] = b;
        ne[idx] = h[a];
        h[a] = idx;
        idx++;
    }
    public static void bfs(){
        Queue<Integer> q = new ArrayDeque<>();
        q.add(1);
        // dist[1] 初始化为 1，这样只要碰到 0，就认为没有遍历过
        // 可以省去一个标记数组
        dist[1] = 1;
        
        while(!q.isEmpty()){
            int t = q.remove();
            for(int i = h[t]; i != 0; i = ne[i]){
                int j = e[i];
                
                if(dist[j] == 0){
                    q.add(j);
                    dist[j] = dist[t] + 1;
                }
            }
        }
    }
}
```
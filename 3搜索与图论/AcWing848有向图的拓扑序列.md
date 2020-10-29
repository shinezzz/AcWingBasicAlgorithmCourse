# AcWing 算法基础课 -- 搜索与图论

## AcWing 848. 有向图的拓扑序列 

`难度：简单`

### 题目描述

给定一个n个点m条边的有向图，点的编号是1到n，图中可能存在重边和自环。

请输出任意一个该有向图的拓扑序列，如果拓扑序列不存在，则输出-1。

若一个由图中所有点构成的序列A满足：对于图中的每条边(x, y)，x在A中都出现在y之前，则称A是该图的一个拓扑序列。

**输入格式**

第一行包含两个整数n和m

接下来m行，每行包含两个整数x和y，表示存在一条从点x到点y的有向边(x, y)。

**输出格式**

共一行，如果存在拓扑序列，则输出任意一个合法的拓扑序列即可。

否则输出-1。

**数据范围**

$1≤n,m≤10^5$

```
输入样例：

3 3
1 2
2 3
1 3

输出样例：

1 2 3
```

### Solution

有向无环图也叫拓扑图

```java
import java.util.*;
import java.io.*;

class Main{
    // 建图
    public static final int N = 100010;
    public static int[] e = new int[N];
    public static int[] ne = new int[N];
    public static int[] h = new int[N];
    public static int idx = 1;
    // 数组模拟队列
    public static int[] q = new int[N];
    // 记录每个点的入度
    public static int[] d = new int[N];
    public static void main(String[] args) throws IOException{
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        String[] s = br.readLine().split(" ");
        int n = Integer.parseInt(s[0]);
        int m = Integer.parseInt(s[1]);
        while(m-- > 0){
            s = br.readLine().split(" ");
            int a = Integer.parseInt(s[0]);
            int b = Integer.parseInt(s[1]);
            add(a, b);
            // 加入一条 a->b 边，b 的入度加 1
            d[b]++;
        }
        if(topsort(n)){
            for(int i = 0; i < n; i++){
                System.out.print(q[i] + " ");
            }
        }
        else System.out.println(-1);
    }
    public static void add(int a, int b){
        e[idx] = b;
        ne[idx] = h[a];
        h[a] = idx;
        idx++;
    }
    public static boolean topsort(int n){
        // hh 队列头部；tt 队列尾部
        // 队列 头部出队，尾部入队
        int hh = 0, tt = -1;
        for(int i = 1; i <= n; i++){
            // d[i] == 0 表示 i 的入度为 0，就把 i 入队
            if(d[i] == 0){
                q[++tt] = i;
            }
        }
        while(hh <= tt){
            int t = q[hh++];
            for(int i = h[t]; i != 0; i = ne[i]){
                int j = e[i];
                if(--d[j] == 0) q[++tt] = j;
            }
        }
        // 队列从 0 开始，如果队尾的下标为 n - 1，表示遍历所有元素了
        return tt == n - 1;
    }
}
```
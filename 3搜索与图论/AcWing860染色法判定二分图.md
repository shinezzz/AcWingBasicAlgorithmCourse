# AcWing 算法基础课 -- 搜索与图论

## AcWing 860. 染色法判定二分图 

`难度：简单`

### 题目描述

给定一个n个点m条边的无向图，图中可能存在重边和自环。

请你判断这个图是否是二分图。

**输入格式**

第一行包含两个整数n和m。

接下来m行，每行包含两个整数u和v，表示点u和点v之间存在一条边。

**输出格式**

如果给定图是二分图，则输出“Yes”，否则输出“No”。

**数据范围**

$1≤n,m≤10^5$

```r
输入样例：

4 4
1 3
1 4
2 3
2 4

输出样例：

Yes
```

### Solution

```java
import java.util.*;
import java.io.*;

class Main{
    static final int N = 100010;
    static int[] e = new int[2 * N];
    static int[] ne = new int[2 * N];
    static int[] h = new int[N];
    static int idx = 1;
    // 标记颜色
    static int[] color = new int[N];
    public static void add(int u, int v){
        e[idx] = v;
        ne[idx] = h[u];
        h[u] = idx++;
    }
    // u 代表点的编号，c 代表颜色，值为1，2
    // dfs(u,c)表示把u号点染色成c颜色，并且判断从u号点开始染其他相连的点是否染成功
    public static boolean dfs(int u, int c){
        color[u] = c;
        for(int i = h[u]; i != 0; i = ne[i]){
            int j = e[i];
            if(color[j] == 0){
                // 还没染色，染上色，c是1就染成2，c是2就染成1，所以用3-c
                if(!dfs(j, 3 - c)) return false;
            }
            // 如果j已经染色，并且和u一样，就产生矛盾了
            else if(color[j] == c) return false;
        }
        return true;
    }
    public static void main(String[] args) throws IOException{
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        String[] s = br.readLine().split(" ");
        int n = Integer.parseInt(s[0]);
        int m = Integer.parseInt(s[1]);
        // 递归，用邻接表来存
        while(m-- > 0){
            s = br.readLine().split(" ");
            int u = Integer.parseInt(s[0]);
            int v = Integer.parseInt(s[1]);
            add(u, v);
            add(v, u);
        }
        boolean flag = true;
        // 遍历 n 个点
        for(int i = 1; i <= n; i++){
            // 如果没有染色，递归染色
            if(color[i] == 0){
                // 如果返回flase，说明染色出现矛盾，就说明不是二分图
                if(!dfs(i, 1)){
                    flag = false;
                    break;
                }
            }
        }
        if(flag) System.out.println("Yes");
        else System.out.println("No");
    }
}
```
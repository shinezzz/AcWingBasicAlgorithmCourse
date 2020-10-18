# AcWing 算法基础课 -- 数据结构

## AcWing 837. 连通块中点的数量 

`难度：简单`

### 题目描述

给定一个包含n个点（编号为1~n）的无向图，初始时图中没有边。

现在要进行m个操作，操作共有三种：

- “C a b”，在点a和点b之间连一条边，a和b可能相等；
- “Q1 a b”，询问点a和点b是否在同一个连通块中，a和b可能相等；
- “Q2 a”，询问点a所在连通块中点的数量；

**输入格式**

第一行输入整数n和m。

接下来m行，每行包含一个操作指令，指令为“C a b”，“Q1 a b”或“Q2 a”中的一种。

**输出格式**

对于每个询问指令”Q1 a b”，如果a和b在同一个连通块中，则输出“Yes”，否则输出“No”。

对于每个询问指令“Q2 a”，输出一个整数表示点a所在连通块中点的数量

每个结果占一行。

**数据范围**

$1≤n,m≤10^5$

```r
输入样例：

5 5
C 1 2
Q1 1 2
Q2 1
C 2 5
Q2 5

输出样例：

Yes
2
3
```

### Solution

这道题在并查集的基础上，还有一个计算每个连通块的点的数量。

每个连通块的点的数量也就是这个连通块根节点所在连通块中点的数量。
```java
import java.util.*;
import java.io.*;

public class Main{
    public static int N = 100010;
    public static int[] cnt = new int[N];
    public static int[] p = new int[N];
    public static void main(String[] args) throws IOException{
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
        String[] s = br.readLine().split(" ");
        int n = Integer.parseInt(s[0]);
        // 初始化,每个节点的父节点是自己
        for(int i = 1; i <= n; i++){
            p[i] = i;
            cnt[i] = 1;
        }
        int m = Integer.parseInt(s[1]);
        while(m-- > 0){
            s = br.readLine().split(" ");
            // 合并连通块
            if(s[0].equals("C")){
                int a = Integer.parseInt(s[1]);
                int b = Integer.parseInt(s[2]);
                a = find(a);
                b = find(b);
                if(a != b){
                    p[a] = b;
                    cnt[b] = cnt[a] + cnt[b];
                }
            }
            // 两个点是否在一个连通块
            else if(s[0].equals("Q1")){
                int a = Integer.parseInt(s[1]);
                int b = Integer.parseInt(s[2]);
                if(find(a) == find(b)) bw.write("Yes\n");
                else bw.write("No\n");
            }
            // 点 a 所在连通块的点的数量
            else if(s[0].equals("Q2")){
                int a = Integer.parseInt(s[1]);
                bw.write(cnt[find(a)] + "\n");
            }
            bw.flush();
        }
        bw.close();
        br.close();
    }
    public static int find(int x){
        if(p[x] != x) p[x] = find(p[x]);
        return p[x];
    }
}
```
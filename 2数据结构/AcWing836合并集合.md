# AcWing 算法基础课 -- 数据结构

## AcWing 836. 合并集合

`难度：简单`

### 题目描述

一共有n个数，编号是1~n，最开始每个数各自在一个集合中。

现在要进行m个操作，操作共有两种：

-  “M a b”，将编号为a和b的两个数所在的集合合并，如果两个数已经在同一个集合中，则忽略这个操作；
-  “Q a b”，询问编号为a和b的两个数是否在同一个集合中；

**输入格式**

第一行输入整数n和m。

接下来m行，每行包含一个操作指令，指令为“M a b”或“Q a b”中的一种。

**输出格式**

对于每个询问指令”Q a b”，都要输出一个结果，如果a和b在同一集合内，则输出“Yes”，否则输出“No”。

每个结果占一行。

**数据范围**

$1≤n,m≤10^5$

```r
输入样例：

4 5
M 1 2
M 3 4
Q 1 2
Q 1 3
Q 3 4

输出样例：

Yes
No
Yes
```

### Solution

并查集结构：1. 快速合并两个集合，快速查询两个元素是否在同一个集合中

注意 `find(int x)` 函数中的路径压缩 `p[x] = find[x]`

```java
import java.util.*;
import java.io.*;

public class Main{
    public static int N = 100010;
    // 存储每个节点的父节点
    public static int[] p = new int[N];
    public static void main(String[] args) throws IOException{
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
        String[] s = br.readLine().split(" ");
        int n = Integer.parseInt(s[0]);
        int m = Integer.parseInt(s[1]);
        // 先初始化每个节点为自己的父节点
        for(int i = 0; i < n; i++){
            p[i] = i;
        }
        while(m-- > 0){
            s = br.readLine().split(" ");
            int a = Integer.parseInt(s[1]);
            int b = Integer.parseInt(s[2]);
            if(s[0].equals("M")){
                p[find(a)] = find(b);
            }else{
                if(find(a) == find(b)){
                    bw.write("Yes" + "\n");
                }else{
                    bw.write("No" + "\n");
                }
            }
        }
        bw.close();
        br.close();
    }
    // 找到 x 的最后的父节点也就是根节点
    // 路径压缩:每个节点都指向根节点
    public static int find(int x){
        if(p[x] != x) p[x] = find(p[x]);
        return p[x];
    }
}

```
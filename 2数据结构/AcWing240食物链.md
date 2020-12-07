# AcWing 算法基础课 -- 数据结构

## AcWing 240. 食物链 

`难度：中等`

### 题目描述

动物王国中有三类动物A,B,C，这三类动物的食物链构成了有趣的环形。

A吃B， B吃C，C吃A。

现有N个动物，以1－N编号。

每个动物都是A,B,C中的一种，但是我们并不知道它到底是哪一种。

有人用两种说法对这N个动物所构成的食物链关系进行描述：

第一种说法是”1 X Y”，表示X和Y是同类。

第二种说法是”2 X Y”，表示X吃Y。

此人对N个动物，用上述两种说法，一句接一句地说出K句话，这K句话有的是真的，有的是假的。

当一句话满足下列三条之一时，这句话就是假话，否则就是真话。

1. 当前的话与前面的某些真的话冲突，就是假话；
2. 当前的话中X或Y比N大，就是假话；
3. 当前的话表示X吃X，就是假话。

你的任务是根据给定的N和K句话，输出假话的总数。

**输入格式**

第一行是两个整数N和K，以一个空格分隔。

以下K行每行是三个正整数 D，X，Y，两数之间用一个空格隔开，其中D表示说法的种类。

若D=1，则表示X和Y是同类。

若D=2，则表示X吃Y。

**输出格式**

只有一个整数，表示假话的数目。

**数据范围**

$1≤N≤50000,$
$0≤K≤100000$

```r
输入样例：

100 7
1 101 1 
2 1 2
2 2 3 
2 3 3 
1 1 3 
2 3 1 
1 5 5

输出样例：

3
```

### Solution

并查集的题目。

主要思想是维护每个节点到根节点的距离，详细看注释。

```java
// 思想：维护每个节点到共同根节点的距离，
import java.util.*;
import java.io.*;

class Main{
    static final int N = 50010;
    static int[] p = new int[N];
    static int[] dist = new int[N];
    public static int find(int x){
        if(p[x] != x) {
            // 重点是怎么更新 dist[x]
            // d[x]存储的是x到p[x]的距离，find(x)之后p[x]就是根节点了，所以d[x]存的就是到根节点的距离了
            int t = p[x];
            p[x] = find(p[x]);
            dist[x] = dist[t] + dist[x];
        }
        // return p[x];
        // if(p[x] != x){//不是祖宗节点的话
        //     int t = find(p[x]);
        //     dist[x] += dist[p[x]];
        //     p[x] = t;
        // }
        return p[x];
    }
    public static void main(String[] args) throws IOException{
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        String[] s = br.readLine().split(" ");
        int n = Integer.parseInt(s[0]);
        int k = Integer.parseInt(s[1]);
        for(int i = 1; i <= n; i++) p[i] = i;
        int res = 0;
        while(k -- > 0){
            s = br.readLine().split(" ");
            int d = Integer.parseInt(s[0]);
            int x = Integer.parseInt(s[1]);
            int y = Integer.parseInt(s[2]);
            if(x > n || y > n) res++;
            else{
                // 先找 x，y 的根节点
                int px = find(x), py = find(y);
                // 判断是不是同类关系
                if(d == 1){
                    // 如果 x 和 y 在一个集合中，判断两者距离根节点的距离是否刚好被 3 整除
                    if(px == py && (dist[x] - dist[y]) % 3 != 0) res ++;
                    // 如果 x 和 y 不在一个集合中，就把两者连起来
                    // 连起来要保证 dist[x] - dist[y] 能够被 3 整除
                    else if(px != py){
                        p[px] = py;
                        dist[px] = dist[y] - dist[x];
                    }
                }
                // 判断是不是吃与被吃的关系
                else if(d == 2){
                    // 如果在一个集合中，就要判断是否关系属实，就是差 1
                    // 如果不在一个集合中，就建立关系
                    // x 吃 y
                    // 我们定义 
                    // y - x 模 3 为 1 表示 y 吃 x
                    // y - x 模 3 为 2 表示 x 吃 y
                    // 防止出现取模出现负数不好判断，就先减去相应的值，看最后的模是否为 0
                    if(x == y) res ++;
                    else if(px == py && (dist[x] - dist[y] - 1) % 3 != 0) res++;
                    else if(px != py){
                        p[px] = p[y];
                        dist[px] = dist[y] + 1 - dist[x];
                    }
                }
            }
        }
        System.out.println(res);
    }
}
```
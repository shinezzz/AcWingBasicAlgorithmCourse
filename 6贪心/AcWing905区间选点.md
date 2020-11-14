# AcWing 算法基础课 -- 贪心专题

## AcWing 905. 区间选点 

`难度：简单`

### 题目描述

给定N个闭区间[ai,bi]，请你在数轴上选择尽量少的点，使得每个区间内至少包含一个选出的点。

输出选择的点的最小数量。

位于区间端点上的点也算作区间内。

**输入格式**

第一行包含整数N，表示区间数。

接下来N行，每行包含两个整数ai,bi，表示一个区间的两个端点。

**输出格式**

输出一个整数，表示所需的点的最小数量。

**数据范围**

$1≤N≤10^5,$
$−10^9≤ai≤bi≤10^9$

```r
输入样例：

3
-1 1
2 4
3 5

输出样例：

2
```

### Solution

```java
import java.util.*;

class Main{
    static class Pair{
        int a, b;
        public Pair(int a, int b){
            this.a = a;
            this.b = b;
        }
    }
    static int N = 100010;
    static int INF = 0x3f3f3f3f;
    static Pair[] g = new Pair[N];
    public static void main(String[] args){
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();
        for(int i = 1; i <= n; i++){
            int a = sc.nextInt();
            int b = sc.nextInt();
            g[i] = new Pair(a, b);
        }
        Arrays.sort(g, 1, n + 1, (Pair p1, Pair p2) -> p1.b - p2.b);
        int res = 0;
        int right = -INF;
        for(int i = 1; i <= n; i++){
            // 如果这个区间的左端点大于上一次的右边界,就加一个点,更新右边界
            if(g[i].a > right){
                res ++;
                right = g[i].b; 
            }
        }
        System.out.println(res);
    }
}
```
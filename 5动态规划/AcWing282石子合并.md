# AcWing 算法基础课 -- 动态规划

## AcWing 282. 石子合并

`难度：简单`

### 题目描述

设有N堆石子排成一排，其编号为1，2，3，…，N。

每堆石子有一定的质量，可以用一个整数来描述，现在要将这N堆石子合并成为一堆。

每次只能合并相邻的两堆，合并的代价为这两堆石子的质量之和，合并后与这两堆石子相邻的石子将和新堆相邻，合并时由于选择的顺序不同，合并的总代价也不相同。

例如有4堆石子分别为 1 3 5 2， 我们可以先合并1、2堆，代价为4，得到4 5 2， 又合并 1，2堆，代价为9，得到9 2 ，再合并得到11，总代价为4+9+11=24；

如果第二步是先合并2，3堆，则代价为7，得到4 7，最后一次合并代价为11，总代价为4+7+11=22。

问题是：找出一种合理的方法，使总的代价最小，输出最小代价。

**输入格式**

第一行一个数N表示石子的堆数N。

第二行N个数，表示每堆石子的质量(均不超过1000)。

**输出格式**

输出一个整数，表示最小代价。

**数据范围**

1≤N≤300

```r
输入样例：

4
1 3 5 2

输出样例：

22
```

### Solution

```java
import java.util.*;

class Main{
    public static void main(String[] args){
        Scanner sc = new Scanner(System.in);
        int N = sc.nextInt();
        int INF = 0x3f3f3f3f;
        int[] a = new int[N + 10];
        for(int i = 1; i <= N; i++) a[i] = sc.nextInt();
        int[][] dp = new int[N + 10][N + 10];
        // 先算一下前缀和 s
        int[] s = new int[N + 10];
        for(int i = 1; i <= N; i++) s[i] = s[i - 1] + a[i];
        // 状态表示：dp[i][j] 表示合并 i 到 j 的集合
        // 状态计算：(i,j) 取其中一点 k，可以分成两段 (i,k) 和 (k+1,j)，dp[i][j] = dp[i][k] + dp[k+1][j] + s[j] - s[i-1]
        // 从相邻 2 个合并，一直到所有合并
        // 区间 dp，第一重 循环区间长度，第二重 循环左端点，根据区间长度和左端点确定右端点
        for(int len = 2; len <= N; len++){
            for(int i = 1; i + len - 1 <= N; i++){
                int j = i + len - 1;
                dp[i][j] = INF;
                for(int k = i; k < j; k++){
                    dp[i][j] = Math.min(dp[i][j], dp[i][k] + dp[k + 1][j] + s[j] - s[i - 1]);
                }
            }
        }
        System.out.println(dp[1][N]);
    }
}
```
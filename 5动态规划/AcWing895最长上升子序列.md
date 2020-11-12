# AcWing 算法基础课 -- 动态规划

## AcWing 895. 最长上升子序列

`难度：简单`

### 题目描述

给定一个长度为N的数列，求数值严格单调递增的子序列的长度最长是多少。

**输入格式**

第一行包含整数N。

第二行包含N个整数，表示完整序列。

**输出格式**

输出一个整数，表示最大长度。

**数据范围**

$1≤N≤1000，$
$−10^9≤数列中的数≤10^9$

```r
输入样例：

7
3 1 2 1 8 5 6

输出样例：

4
```

### Solution

```java
import java.util.*;

class Main{
    public static void main(String[] args){
        Scanner sc = new Scanner(System.in);
        int N = sc.nextInt();
        int[] a = new int[N + 10];
        int[] dp = new int[N + 10];
        // 全部初始化为 1,因为每个字母都是一个上升子序列
        Arrays.fill(dp, 1);
        // N 的范围是 1000，可以用 n 方复杂度的做法
        // 两层循环
        // 状态表示: dp[i] 表示以 a[i] 结尾的上升子序列的长度;属性:最大值
        // 状态计算: 考虑倒数第二数字是否比当前数字小
        // 如果是 dp[i] = Math.max(dp[i],dp[j] + 1);
        for(int i = 1; i <= N; i++){
            a[i] = sc.nextInt();
            for(int j = 1; j <= i; j++){
                if(a[j] < a[i]) dp[i] = Math.max(dp[i], dp[j] + 1);
            }
        }
        // 遍历一遍
        int res = 1;
        for(int d : dp) res = Math.max(res, d);
        System.out.println(res);
    }
}
```
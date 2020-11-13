# AcWing 算法基础课 -- 动态规划

## AcWing 897. 最长公共子序列

`难度：简单`

### 题目描述

给定两个长度分别为N和M的字符串A和B，求既是A的子序列又是B的子序列的字符串长度最长是多少。
输入格式

第一行包含两个整数N和M。

第二行包含一个长度为N的字符串，表示字符串A。

第三行包含一个长度为M的字符串，表示字符串B。

字符串均由小写字母构成。

**输出格式**

输出一个整数，表示最大长度。

**数据范围**

1≤N,M≤1000

```r
输入样例：

4 5
acbd
abedc

输出样例：

3
```

### Solution

```java
import java.util.*;

class Main{
    public static void main(String[] args){
        Scanner sc = new Scanner(System.in);
        int N = sc.nextInt();
        int M = sc.nextInt();
        String a = sc.next();
        String b = sc.next();
        int[][] dp = new int[N + 10][M + 10];
        // 状态表示：dp[i][j]代表S1中的前i个字符，S2中的前j个字符的最长公共子序列
        // 状态转移：
        // 如果S1[i]==S2[j],那么最长公共子序列必然包含S1[i]/S2[j]这个元素，可以先找到不包含S1[i]和S2[j]的最长公共子序列,再加上这个元素即可，不包含S1[i]和S2[j]的最长公共子序列就是f[i-1][j-1]
        // 如果S1[i]!=S2[j],最长的公共子序列中可能不包含S1[i](dp[i-1][j]),也可能不包含S2[j](dp[i][j-1]),也可能都不包含dp[i-1][j-1]
        for(int i = 1; i <= N; i++){
            for(int j = 1; j <= M; j++){
                dp[i][j] = Math.max(dp[i - 1][j], dp[i][j - 1]);
                if(a.charAt(i - 1) == b.charAt(j - 1)) dp[i][j] = Math.max(dp[i][j], dp[i - 1][j - 1] + 1);
            }
        }
        System.out.println(dp[N][M]);
    }
}
```
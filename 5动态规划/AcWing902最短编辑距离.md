# AcWing 算法基础课 -- 动态规划

## AcWing 902. 最短编辑距离

`难度：简单`

### 题目描述

给定两个字符串A和B，现在要将A经过若干操作变为B，可进行的操作有：

1. 删除–将字符串A中的某个字符删除。
2. 插入–在字符串A的某个位置插入某个字符。
3. 替换–将字符串A中的某个字符替换为另一个字符。

现在请你求出，将A变为B至少需要进行多少次操作。

**输入格式**

第一行包含整数n，表示字符串A的长度。

第二行包含一个长度为n的字符串A。

第三行包含整数m，表示字符串B的长度。

第四行包含一个长度为m的字符串B。

字符串中均只包含大写字母。

**输出格式**

输出一个整数，表示最少操作次数。

**数据范围**

1≤n,m≤1000

```r
输入样例：

10 
AGTCTGACGC
11 
AGTAAGTAGGC

输出样例：

4
```

### Solution

```java
import java.util.*;

class Main{
    public static void main(String[] args){
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();
        String a = sc.next();
        int m = sc.nextInt();
        String b = sc.next();
        // 状态表示：dp[i][j] 表示 a 字符串的前 i 个字符与 b 字符串的前 j 个字符的最短编辑距离
        // 状态计算：就针对 a 字符串进行增，删，改
        // 增：dp[i][j] = dp[i][j - 1] + 1;
        // 删：dp[i][j] = dp[i - 1][j] + 1;
        // 改：if(a[i] == b[j]) dp[i][j] = dp[i - 1][j - 1]
        //     if(a[i] != b[j]) dp[i][j] = dp[i - 1][j - 1] + 1;
        // 初始化：dp[0][j] = j, dp[i][0] = i;
        int[][] dp =  new int[n + 10][m + 10];
        for(int i = 0; i <= n; i++) dp[i][0] = i;
        for(int j = 0; j <= m; j++) dp[0][j] = j;
        for(int i = 1; i <= n; i++){
            for(int j = 1; j <= m; j++){
                dp[i][j] = Math.min(dp[i][j - 1], dp[i - 1][j]) + 1;
                if(a.charAt(i - 1) == b.charAt(j - 1)) dp[i][j] = Math.min(dp[i][j], dp[i - 1][j - 1]);
                else dp[i][j] = Math.min(dp[i][j], dp[i - 1][j - 1] + 1);
            }
        }
        System.out.println(dp[n][m]);
    }
}
```
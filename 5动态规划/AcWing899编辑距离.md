# AcWing 算法基础课 -- 动态规划

## AcWing 899. 编辑距离 

`难度：简单`

### 题目描述

给定n个长度不超过10的字符串以及m次询问，每次询问给出一个字符串和一个操作次数上限。

对于每次询问，请你求出给定的n个字符串中有多少个字符串可以在上限操作次数内经过操作变成询问给出的字符串。

每个对字符串进行的单个字符的插入、删除或替换算作一次操作。

**输入格式**

第一行包含两个整数n和m。

接下来n行，每行包含一个字符串，表示给定的字符串。

再接下来m行，每行包含一个字符串和一个整数，表示一次询问。

字符串中只包含小写字母，且长度均不超过10。

**输出格式**

输出共m行，每行输出一个整数作为结果，表示一次询问中满足条件的字符串个数。

**数据范围**

1≤n,m≤1000,

```r
输入样例：

3 2
abc
acd
bcd
ab 1
acbd 2

输出样例：

1
3
```

### Solution

```java
import java.util.*;

class Main{
    public static void main(String[] args){
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();
        int m = sc.nextInt();
        String[] s = new String[n + 10];
        String[] q = new String[m + 10];
        int[] num = new int[m + 10];
        for(int i = 1; i <= n; i++) s[i] = sc.next();
        for(int i = 1; i <= m; i++){
            q[i] = sc.next();
            num[i] = sc.nextInt();
            int cnt = 0;
            for(int j = 1; j <= n; j++){
                if(find(s[j], q[i]) <= num[i]) cnt++;
            }
            System.out.println(cnt);
        }
    }
    public static int find(String a, String b){
        int n = a.length(), m = b.length();
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
        return dp[n][m];
    }
}
```
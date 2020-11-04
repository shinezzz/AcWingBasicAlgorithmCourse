# AcWing 算法基础课 -- 数学知识

## AcWing 872. 最大公约数 

`难度：简单`

### 题目描述

给定n对正整数ai,bi，请你求出每对数的最大公约数。

**输入格式**

第一行包含整数n。

接下来n行，每行包含一个整数对ai,bi。

**输出格式**

输出共n行，每行输出一个整数对的最大公约数。

**数据范围**

$1≤n≤10^5,$
$1≤ai,bi≤2∗10^9$

```r
输入样例：

2
3 6
4 6

输出样例：

3
2
```

### Solution

```java
import java.util.*;

class Main{
    public static int gcd(int a, int b){
        return b > 0 ? gcd(b, a % b) : a;
    }
    public static void main(String[] args){
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();
        while(n-- > 0){
            int a = sc.nextInt();
            int b = sc.nextInt();
            System.out.println(gcd(a, b));
        }
    }
}
```
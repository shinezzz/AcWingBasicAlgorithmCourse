# AcWing 算法基础课 -- 数学知识

## AcWing 866. 试除法判定质数

`难度：简单`

### 题目描述

给定n个正整数ai，判定每个数是否是质数。

**输入格式**

第一行包含整数n。

接下来n行，每行包含一个正整数ai。

**输出格式**

共n行，其中第 i 行输出第 i 个正整数ai

是否为质数，是则输出“Yes”，否则输出“No”。

**数据范围**

$1≤n≤100,$
$1≤ai≤2∗10^9$

```r
输入样例：

2
2
6

输出样例：

Yes
No
```

### Solution

```java
import java.util.*;

class Main{
    public static boolean isPrime(int a){
        if(a < 2) return false;
        // i <= x / i 很重要
        // i <= sqrt(n) 比较慢
        // i * i <= n 可能溢出
        for(int i = 2; i <= a / i; i++){
            if(a % i == 0) return false;
        }
        return true;
    }
    public static void main(String[] args){
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();
        while(n-- > 0){
            int a = sc.nextInt();
            if(isPrime(a)) System.out.println("Yes");
            else System.out.println("No");
        }
    }
}
```
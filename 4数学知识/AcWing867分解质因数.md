# AcWing 算法基础课 -- 数学知识

## AcWing 867. 分解质因数 

`难度：简单`

### 题目描述

给定n个正整数ai，将每个数分解质因数，并按照质因数从小到大的顺序输出每个质因数的底数和指数。

**输入格式**

第一行包含整数n。

接下来n行，每行包含一个正整数ai。

**输出格式**

对于每个正整数ai,按照从小到大的顺序输出其分解质因数后，每个质因数的底数和指数，每个底数和指数占一行。

每个正整数的质因数全部输出完毕后，输出一个空行。

**数据范围**

$1≤n≤100,$
$1≤ai≤2∗10^9$

```r
输入样例：

2
6
8

输出样例：

2 1
3 1

2 3
```

### Solution

```java
import java.util.*;

class Main{
    public static void divide(int a){
        // i <= x / i 很重要
        // i <= sqrt(n) 比较慢
        // i * i <= n 可能溢出
        for(int i = 2; i <= a / i; i++){
            if(a % i == 0){
                int cnt = 0;
                while(a % i == 0){
                    a /= i;
                    cnt++;
                }
                System.out.println(i + " " + cnt);
            }
        }
        // 一个数只会有一个大于 a/i 的质因数
        if(a > 1) System.out.println(a + " " + 1);
        System.out.println();
    }
    public static void main(String[] args){
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();
        while(n-- > 0){
            int a = sc.nextInt();
            divide(a);
        }
    }
}
```
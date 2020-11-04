# AcWing 算法基础课 -- 数学知识

## AcWing 868. 筛质数 

`难度：简单`

### 题目描述

给定一个正整数n，请你求出1~n中质数的个数。

**输入格式**

共一行，包含整数n。

**输出格式**

共一行，包含一个整数，表示1~n中质数的个数。

**数据范围**

$1≤n≤10^6$

```r
输入样例：

8

输出样例：

4
```

### Solution

1. 埃氏筛法，时间复杂度O(nloglogn)

**用质数筛去所有质数的倍数。**

```java
import java.util.*;

class Main{
    public static int getPrime(int n){
        int cnt = 0;
        // flag 表示 i 是否是合数
        boolean[] flag = new boolean[n + 10];
        // 用质数来筛合数
        int[] p = new int[n + 10];
        for(int i = 2; i <=n; i++){
            if(flag[i]) continue;
            p[cnt++] = i;
            // i 是质数，筛掉 i 的所有倍数
            for(int j = i + i; j <= n; j = j + i){
                flag[j] = true;
            }
        }
        return cnt;
    }
    public static void main(String[] args){
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();
        int cnt = getPrime(n);
        System.out.println(cnt);
    }
}
```

2. 线性筛法，时间复杂度O(n)

每个合数只会被最小质数筛掉。

```java
import java.util.*;

class Main{
    public static int getPrime(int n){
        int cnt = 0;
        // flag 表示 i 是否是合数
        boolean[] flag = new boolean[n + 10];
        // 用质数来筛合数
        int[] p = new int[n + 10];
        for(int i = 2; i <=n; i++){
            // 每个i都要遍历，不能跳过
            // 如果 i 是质数的花，加入数组
            if(!flag[i]) p[cnt++] = i;
            // i 是质数，筛掉 i 的所有倍数
            for(int j = 0; p[j] <= n / i; j ++){
                // 用质数筛去合数
                flag[i * p[j]] = true;
                // i % p[j] == 0 表示 p[j] 是 i 的最小质因子 当然也是 i * p[j] 的最小质因子
                // 这个啥时候就要break了，否则就用不是最小的质因子来筛合数了
                // i % p[j] != 0 表示 p[j] 小于 i 的最小质因子，当然是 i * p[j] 的最小质因子
                if(i % p[j] == 0) break;
            }
        }
        return cnt;
    }
    public static void main(String[] args){
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();
        int cnt = getPrime(n);
        System.out.println(cnt);
    }
}
```
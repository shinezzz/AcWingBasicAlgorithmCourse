# AcWing 算法基础课 -- 数学知识

## AcWing 871. 约数之和 

`难度：简单`

### 题目描述

给定n个正整数ai，请你输出这些数的乘积的约数之和，答案对$10^9+7$取模。

**输入格式**

第一行包含整数n。

接下来n行，每行包含一个整数ai。

**输出格式**

输出一个整数，表示所给正整数的乘积的约数个数，答案需对$10^9+7$取模。

**数据范围**

$1≤n≤100,$
$1≤ai≤2∗10^9$

```
输入样例：

3
2
6
8

输出样例：

252
```


### Solution

```java
import java.util.*;

class Main{
    static final int MOD =1000000007;
    static Map<Integer, Integer> map = new HashMap<>();
    public static void prime(int a){
        for(int i = 2; i <= a / i; i++){
            while(a % i == 0){
                a /= i;
                map.put(i, map.getOrDefault(i, 0) + 1);
            }
        }
        if(a > 1) map.put(a, map.getOrDefault(a, 0) + 1);
    }
    public static void main(String[] args){
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();
        for(int i = 0; i < n; i++){
            int a = sc.nextInt();
            prime(a);
        }
        long res = 1;
        for (int key : map.keySet()){
            long c = 1;
            for(int i = 0; i < map.get(key); i++){
                c = (c * key + 1) % MOD;
            }
            res = res * c % MOD;
        }
        System.out.println(res);
    }
}
```
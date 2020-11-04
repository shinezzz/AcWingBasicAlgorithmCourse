# AcWing 算法基础课 -- 数学知识

## AcWing 869. 试除法求约数 

`难度：简单`

### 题目描述

给定n个正整数ai，对于每个整数ai,请你按照从小到大的顺序输出它的所有约数。

**输入格式**

第一行包含整数n。

接下来n行，每行包含一个整数ai。

**输出格式**

输出共n行，其中第 i 行输出第 i 个整数ai的所有约数。

**数据范围**

$1≤n≤100,$
$2≤ai≤2∗10^9$

```r
输入样例：

2
6
8

输出样例：

1 2 3 6 
1 2 4 8 
```

### Solution

```java
import java.util.*;

class Main{
    public static void getDivisor(int a){
        List<Integer> p = new ArrayList<>();
        for(int i = 1; i <= a / i; i++){
            if(a % i == 0){
                p.add(i);
                if(i != a / i) p.add(a / i);
            }
        }
        Collections.sort(p);
        for(int i = 0; i < p.size(); i++)
            System.out.print(p.get(i) + " ");
        System.out.println();
    }
    public static void main(String[] args){
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();
        while(n-- > 0){
            int a = sc.nextInt();
            getDivisor(a);
        }
    }
}
```
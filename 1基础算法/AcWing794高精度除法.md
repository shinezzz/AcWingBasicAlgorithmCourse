# AcWing 算法基础课 -- 基础算法

## AcWing 794. 高精度除法 

`难度：简单`

### 题目描述

给定两个非负整数A，B，请你计算 A / B的商和余数。

**输入格式**

共两行，第一行包含整数A，第二行包含整数B。

**输出格式**

共两行，第一行输出所求的商，第二行输出所求余数。


数据范围

$1≤A的长度≤100000,$
$0≤B≤10000$

```r
输入样例：

7
2

输出样例：

3
1
```
### Solution

```java
import java.util.*;

class Main{
    public static void main(String[] args){
        Scanner sc = new Scanner(System.in);
        String sa = sc.next();
        int la = sa.length();
        int[] a = new int[la];
        for(int i = 0, j = 0; i < la; i++, j++) a[i] = sa.charAt(j) - '0';
        int b = sc.nextInt();
        Deque<Integer> c = new ArrayDeque<>();
        // 商用 c 存储，返回余数
        int t = div(a, b, c);
        while(!c.isEmpty()) System.out.print(c.pollFirst());
        System.out.print("\n" + t);
    }
    public static int div(int[] a, int b, Deque<Integer> c){
        int t = 0;
        for(int i = 0; i < a.length; i++){
            t = t * 10 + a[i];
            c.addLast(t / b);
            t = t % b;
        }
        while(c.size() > 1 && c.peekFirst() == 0) c.pollFirst();
        return t;
    }
}
```
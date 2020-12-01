# AcWing 算法基础课 -- 基础算法

## AcWing 793. 高精度乘法 

`难度：简单`

### 题目描述

给定两个正整数A和B，请你计算A * B的值。

**输入格式**

共两行，第一行包含整数A，第二行包含整数B。

**输出格式**

共一行，包含A * B的值。


数据范围

$1≤A的长度≤100000,$
$0≤B≤10000$

```r
输入样例：

2
3

输出样例：

6
```
### Solution

```java
import java.util.*;

class Main{
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        String sa = sc.next();
        int la = sa.length();
        int[] a = new int[la];
        // b 比较小，可以用 int 存
        int b = sc.nextInt();
        for(int i = la - 1, j = 0; i >= 0; i--, j++)    a[j] = sa.charAt(i) - '0';
        Deque<Integer> c = new ArrayDeque<>();
        mul(a, b, c);
        while(!c.isEmpty()) System.out.print(c.pop());
    }
    public static void mul(int[] a, int b, Deque<Integer> c){
        int t = 0;
        for(int i = 0; i < a.length; i++){
            t = t + a[i] * b;
            c.push(t % 10);
            t = t / 10;
        }
        // 因为 t 可能很大，所以也要把 t 加到 c 中
        while(t > 0){
            c.push(t % 10);
            t /= 10;
        }
        // 以防是 0 去除前导 0
        while(c.size() > 1 && c.peek() == 0) c.pop();
    }
}
```
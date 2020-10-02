# AcWing 算法基础课 -- 基础算法

## AcWing 792. 高精度减法 

`难度：简单`

### 题目描述

给定两个正整数，计算它们的差，计算结果可能为负数。

**输入格式**

共两行，每行包含一个整数。

**输出格式**

共一行，包含所求的差。

```r
数据范围

1≤整数长度≤100000

输入样例：

32
11

输出样例：

21
```
### Solution

```java
import java.util.*;
import java.io.*;

public class Main{
    public static void main(String[] args) throws IOException{
        BufferedReader in = new BufferedReader(new InputStreamReader(System.in));
        // 字符串读取两个数字
        String a = in.readLine(), b = in.readLine();
        // 用数组保存数字，数组的0位对应数字的个位，所以倒序遍历字符串
        List<Integer> x = new ArrayList<>();
        List<Integer> y = new ArrayList<>();
        for(int i = a.length() - 1; i >= 0; i--) x.add(a.charAt(i) - '0');
        for(int i = b.length() - 1; i >= 0; i--) y.add(b.charAt(i) - '0');
        // 用栈来存储，存的话先存个位，打印的话先打印高位
        Deque<Integer> c = new ArrayDeque<>();
        // 如果 x 大于等于 y， 就用 x - y
        // 如果 x 小于 y，先打印负号，再计算 y - x
        if(cmp(x, y)) c = sub(x, y);
        else{
            System.out.print("-");
            c = sub(y, x);
        }
        while(!c.isEmpty()){
            System.out.print(c.pop());
        }
    }
    public static boolean cmp(List<Integer> x, List<Integer> y){
        if(x.size() != y.size()) return x.size() > y.size();
        for(int i = x.size() - 1; i >= 0; i--){
            if(x.get(i) != y.get(i)) return x.get(i) > y.get(i);
        }
        return true;
    }
    public static Deque<Integer> sub(List<Integer> x, List<Integer> y){
        Deque<Integer> c =new ArrayDeque<>();
        // t 记录借位
        int t = 0;
        for(int i = 0; i < x.size(); i++){
            t = x.get(i) - t;
            if(i < y.size()) t = t - y.get(i);
            c.push((t + 10) % 10);
            // 如果 t 为负数，就借一位，否则不用借位
            t = t < 0 ? 1 : 0;
        }
        // 去除前导 0
        while( c.size() > 1 && c.peek() == 0) c.pop();
        return c;
    }
}
```
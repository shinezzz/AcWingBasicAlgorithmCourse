# AcWing 算法基础课 -- 基础算法

## AcWing 791. 高精度加法

`难度：简单`

### 题目描述

给定两个正整数，计算它们的和

**输入格式**

共两行，每行包含一个整数。

**输出格式**

共一行，包含所求的和。

**数据范围**：
```r
1≤整数长度≤100000
```
**输入样例**：

```r
12
23
```

**输出样例**：

```r
35
```

### Solution

1. 用BitInteger来处理

```java
import java.math.BigInteger;
import java.io.*;

public class Main {

    public static void main(String[] args) throws IOException {
        BufferedReader in = new BufferedReader(new InputStreamReader(System.in));
        BigInteger a = new BigInteger(in.readLine());
        BigInteger b = new BigInteger(in.readLine());
        System.out.println(a.add(b));
        
    }

}
```

2. 用字符串形式来，会比BigInteger的时间快一倍

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
        c = add(x, y);
        while(!c.isEmpty()){
            System.out.print(c.pop());
        }
    }
    // 人为规定 x > y
    public static Deque<Integer> add(List<Integer> x, List<Integer> y){
        if(x.size() < y.size()) return add(y, x);
        Deque<Integer> c =new ArrayDeque<>();
        // t 记录进位
        int t = 0;
        for(int i = 0; i < x.size(); i++){
            t += x.get(i);
            if(i < y.size()) t += y.get(i);
            c.push(t % 10);
            t = t / 10;
        }
        // 最后还有一个进位，别忽略
        if(t > 0) c.push(t);
        return c;
    }
}
```

3. 用数组存的方法，感觉比 List 灵活一点

```
import java.util.*;

class Main{
    public static void main(String[] args){
        Scanner sc = new Scanner(System.in);
        String sa = sc.next();
        String sb = sc.next();
        int la = sa.length();
        int lb = sb.length();
        int[] a = new int[la];
        int[] b = new int[lb];
        List<Integer> c = new ArrayList<>();
        for(int i = la - 1, k = 0; i >= 0; i--, k++){
            a[k] = sa.charAt(i) - '0';
        }
        for(int i = lb - 1, k = 0; i >= 0; i--, k++){
            b[k] = sb.charAt(i) - '0';
        }
        // 加法中 a 的长度 大于等于 b 的长度
        if(la > lb) c = add(a, b);
        else c = add(b, a);
        for(int i = c.size() - 1; i >= 0; i--){
            System.out.print(c.get(i));
        }
        
    }
    public static List<Integer> add(int[] a, int[] b){
        List<Integer> c = new ArrayList<>();
        // 加法，只需要记录进位
        int t = 0;
        for(int i = 0; i < a.length; i++){
            t += a[i];
            if(i < b.length) t += b[i];
            c.add(t % 10);
            t /= 10;
        }
        // 最后以防还有进位
        if(t > 0) c.add(t);
        return c;
    }
}
```
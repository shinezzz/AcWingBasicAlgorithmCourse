# AcWing 算法基础课 -- 基础算法

## AcWing 790. 数的三次方根

`难度：简单`

### 题目描述

给定一个浮点数n，求它的三次方根。

**输入格式**

共一行，包含一个浮点数n。

**输出格式**

共一行，包含一个浮点数，表示问题的解。

注意，结果保留6位小数。

**数据范围**：
```r
−10000≤n≤10000
```
**输入样例**：

```r
1000.00
```

**输出样例**：

```r
10.000000
```

### Solution

```java
import java.io.*;

public class Main{
    public static void main(String[] args) throws IOException{
        final double ACC = 1e-8;
        BufferedReader in = new BufferedReader(new InputStreamReader(System.in));
        double x = Double.parseDouble(in.readLine());
        double l = -100, r = 100;
        while(r - l > ACC){
            double mid  = (l + r) / 2;
            if(mid * mid * mid > x) r = mid;
            else l = mid;
        }
        System.out.printf("%.6f", l);
    }
}
```
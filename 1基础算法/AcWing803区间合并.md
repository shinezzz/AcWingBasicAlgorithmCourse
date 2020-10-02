# AcWing 算法基础课 -- 基础算法

## AcWing 803. 区间合并 

`难度：简单`

### 题目描述

给定 n 个区间 $[l_i,r_i]$，要求合并所有有交集的区间。

注意如果在端点处相交，也算有交集。

输出合并完成后的区间个数。

例如：[1,3]和[2,6]可以合并为一个区间[1,6]。

**输入格式**

第一行包含整数n。

接下来n行，每行包含两个整数 l 和 r。

**输出格式**

共一行，包含一个整数，表示合并区间完成后的区间个数。

**数据范围**:

$1≤n≤100000,$
$−10^9≤l_i≤r_i≤10^9$

```r
输入样例：

5
1 2
2 4
5 6
7 8
7 9

输出样例：

3
```

### Solution

```java
import java.util.*;
import java.io.*;

public class Main{
    public static class Pairs{
        int l, r;
        public Pairs(int l, int r){
            this.l = l;
            this.r = r;
        }
    }
    public static void main(String[] args) throws IOException{
        BufferedReader in = new BufferedReader(new InputStreamReader(System.in));
        int n = Integer.parseInt(in.readLine());
        List<Pairs> alls = new ArrayList<>();
        for(int i = 0; i < n; i++){
            String[] s = in.readLine().split(" ");
            int l = Integer.parseInt(s[0]);
            int r = Integer.parseInt(s[1]);
            alls.add(new Pairs(l, r));
        }
        // 利用 lambda 表达式重写比较器
        // 根据 左边界 升序排列
        Collections.sort(alls, (Pairs a1, Pairs a2) -> a1.l - a2.l);
        int res = 1;
        Pairs p = new Pairs(alls.get(0).l, alls.get(0).r);
        for(int i = 1; i < n; i++){
            int l = alls.get(i).l;
            int r = alls.get(i).r;
            if(l > p.r){
                res++;
                p.l = alls.get(i).l;
                p.r = alls.get(i).r;
            }
            else{
                if(r > p.r){
                    p.r = alls.get(i).r;
                }
            }
        }
        System.out.println(res);
    }
}
```
# AcWing 算法基础课 -- 贪心专题

## AcWing 2816. 判断子序列 

`难度：简单`

### 题目描述

给定一个长度为 n 的整数序列 a1,a2,…,an 以及一个长度为 m 的整数序列 b1,b2,…,bm。

请你判断 a 序列是否为 b 序列的子序列。

子序列指序列的一部分项按原有次序排列而得的序列，例如序列 {a1,a3,a5} 是序列 {a1,a2,a3,a4,a5}的一个子序列。

**输入格式**

第一行包含两个整数 n,m。

第二行包含 n 个整数，表示 a1,a2,…,an。

第三行包含 m 个整数，表示 b1,b2,…,bm。

**输出格式**

如果 a 序列是 b 序列的子序列，输出一行 Yes。

否则，输出 No。

**数据范围**

$1≤n≤m≤10^5,$
$−10^9≤ai,bi≤10^9$

```
输入样例：

3 5
1 3 5
1 2 3 4 5

输出样例：

Yes
```

### Solution

```java
import java.util.*;
import java.io.*;

class Main{
    static int N = 100010;
    static int[] a = new int[N];
    static int[] b = new int[N];
    public static void main(String[] args) throws IOException{
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        String[] s = br.readLine().split(" ");
        int n = Integer.parseInt(s[0]), m = Integer.parseInt(s[1]);
        s = br.readLine().split(" ");
        for(int i = 1; i <= n; i++) a[i] = Integer.parseInt(s[i - 1]);
        s = br.readLine().split(" ");
        for(int i = 1; i <= m; i++) b[i] = Integer.parseInt(s[i - 1]);
        int i = 1, j = 1;
        // a 是否是 b 的子序列
        // 从 b 里按顺序找 a 的每一个字符
        while(i <= n && j <= m){
            // 找到了 i 往前走
            if(a[i] == b[j]) i++;
            j++;
        }
        if(i == n + 1) System.out.println("Yes");
        else System.out.println("No");
    }
}
```

双指针，感觉这样写会看着舒服些

```java
import java.util.*;
import java.io.*;

class Main{
    static final int N = 100010;
    static int[] a = new int[N];
    static int[] b = new int[N];
    public static void main(String[] args) throws IOException{
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        String[] s = br.readLine().split(" ");
        int n = Integer.parseInt(s[0]);
        int m = Integer.parseInt(s[1]);
        s = br.readLine().split(" ");
        for(int i = 0; i < n; i++) a[i] = Integer.parseInt(s[i]);
        s = br.readLine().split(" ");
        for(int i = 0; i < m; i++) b[i] = Integer.parseInt(s[i]);
        int i = 0, j = 0;
        for(; i < n; i++, j++){
            while(j < m && a[i] != b[j]) j++;
            if(j == m){
                break;
            }
        }
        if(i == n) System.out.println("Yes");
        else System.out.println("No");
    }
}
```
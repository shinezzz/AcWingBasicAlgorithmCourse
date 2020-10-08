# AcWing 算法基础课 -- 数据结构

## AcWing 828. 模拟栈 

`难度：简单`

### 题目描述

实现一个栈，栈初始为空，支持四种操作：

(1) “push x” – 向栈顶插入一个数x；

(2) “pop” – 从栈顶弹出一个数；

(3) “empty” – 判断栈是否为空；

(4) “query” – 查询栈顶元素。

现在要对栈进行M个操作，其中的每个操作3和操作4都要输出相应的结果。

**输入格式**

第一行包含整数M，表示操作次数。

接下来M行，每行包含一个操作命令，操作命令为”push x”，”pop”，”empty”，”query”中的一种。

**输出格式**

对于每个”empty”和”query”操作都要输出一个查询结果，每个结果占一行。

其中，”empty”操作的查询结果为“YES”或“NO”，”query”操作的查询结果为一个整数，表示栈顶元素的值。

```r
数据范围

1≤M≤100000,
1≤x≤109


所有操作保证合法。
输入样例：

10
push 5
query
push 6
pop
query
pop
empty
push 4
query
empty

输出样例：

5
5
YES
4
NO
```

### Solution

```java
import java.util.*;
import java.io.*;

public class Main{
    public static final int N = 100010;
    public static int[] stk = new int[N];
    public static int tt = 0;
    public static void main(String[] args) throws IOException{
        BufferedReader in = new BufferedReader(new InputStreamReader(System.in));
        int m = Integer.parseInt(in.readLine());
        while(m > 0){
            m--;
            String[] s = in.readLine().split(" ");
            if(s[0].equals("push")){
                int x = Integer.parseInt(s[1]);
                stk[tt] = x;
                tt++;
            }else if(s[0].equals("pop")){
                tt--;
            }else if(s[0].equals("empty")){
                String res = tt == 0 ? "YES" : "NO";
                System.out.println(res);
            }else if(s[0].equals("query")){
                System.out.println(stk[tt - 1]);
            }
        }
    }
}
```
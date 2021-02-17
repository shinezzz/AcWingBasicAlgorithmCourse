# AcWing 算法基础课 -- 数据结构

## AcWing 827. 双链表 

`难度：简单`

### 题目描述

实现一个双链表，双链表初始为空，支持5种操作：

(1) 在最左侧插入一个数；

(2) 在最右侧插入一个数；

(3) 将第k个插入的数删除；

(4) 在第k个插入的数左侧插入一个数；

(5) 在第k个插入的数右侧插入一个数

现在要对该链表进行M次操作，进行完所有操作后，从左到右输出整个链表。

**注意**:题目中第k个插入的数并不是指当前链表的第k个数。例如操作过程中一共插入了n个数，则按照插入的时间顺序，这n个数依次为：第1个插入的数，第2个插入的数，…第n个插入的数。

**输入格式**

第一行包含整数M，表示操作次数。

接下来M行，每行包含一个操作命令，操作命令可能为以下几种：

(1) “L x”，表示在链表的最左端插入数x。

(2) “R x”，表示在链表的最右端插入数x。

(3) “D k”，表示将第k个插入的数删除。

(4) “IL k x”，表示在第k个插入的数左侧插入一个数。

(5) “IR k x”，表示在第k个插入的数右侧插入一个数。

**输出格式**

共一行，将整个链表从左到右输出。

```r
数据范围

1≤M≤100000


所有操作保证合法。
输入样例：

10
R 7
D 1
L 3
IL 2 10
D 3
IL 2 7
L 8
R 9
IL 4 7
IR 2 2

输出样例：

8 7 7 3 2 9
```

### Solution

```java
import java.util.*;
import java.io.*;

class Main{
    static final int N = 100010;
    static int[] e = new int[N];
    static int[] l = new int[N];
    static int[] r = new int[N];
    static int idx = 1;
    static int R = 100005;
    static int L = 0;
    public static void main(String[] args) throws IOException{
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
        String[] s = br.readLine().split(" ");
        int m = Integer.parseInt(s[0]);
        // 先把两个哨兵节点连上
        l[R] = L;
        r[L] = R;
        while(m > 0){
            m--;
            s = br.readLine().split(" ");
            if(s[0].equals("L")){
                int x = Integer.parseInt(s[1]);
                // 链表的最左端等价在 0 的右端
                add(0, x);
            }
            else if(s[0].equals("R")){
                int x = Integer.parseInt(s[1]);
                // 链表的最右端等价 l[R] 的右端
                add(l[R], x);
            }
            else if(s[0].equals("D")){
                int k = Integer.parseInt(s[1]);
                delete(k);
            }
            else if(s[0].equals("IL")){
                int k = Integer.parseInt(s[1]);
                int x = Integer.parseInt(s[2]);
                // k 的左侧等价于 l[k] 的右侧
                add(l[k], x);
            }
            else if(s[0].equals("IR")){
                int k = Integer.parseInt(s[1]);
                int x = Integer.parseInt(s[2]);
                // 就是在 k 的右侧
                add(k, x);
            }
        }
        // System.out.println(e[1]);
        for(int i = r[L]; i != R; i = r[i]) bw.write(e[i] + " ");
        bw.close();
    }
    public static void add(int k, int x){
        e[idx] = x;
        r[idx] = r[k];
        l[idx] = l[r[k]];
        l[r[k]] = idx;
        r[k] = idx;
        idx++;
    }
    public static void delete(int k) {
        r[l[k]] = r[k];
        l[r[k]] = l[k];
    }

}
```
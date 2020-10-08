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

public class Main{
    public static final int N = 100010;
    public static int[] e = new int[N];
    public static int[] l = new int[N];
    public static int[] r = new int[N];
    public static int idx;
    // 规定双向链表的头的位置（最左侧）为0，尾的位置（最右侧）为 100005
    // 插入的第 1 个结点只能从 1 开始

    public static void main(String[] args) throws IOException{
        BufferedReader in = new BufferedReader(new InputStreamReader(System.in));
        int m = Integer.parseInt(in.readLine());
        init();
        int x, k;
        while(m > 0){
            m--;
            String[] s = in.readLine().split(" ");  
            switch(s[0]){
                case "L" :
                    // 在链表最左端插入数 x
                    // 也就是在头结点的右边插入数 x
                    x = Integer.parseInt(s[1]);
                    add(0, x);
                    break;
                case "R" :
                    // 在链表的最右端插入数 x
                    // 也就是在尾结点的左边插入数 x
                    x = Integer.parseInt(s[1]);
                    add(l[100005], x);
                    break;
                case "D" :
                    // 将第 k 个插入的数删除
                    k = Integer.parseInt(s[1]);
                    remove(k);
                    break;
                case "IL" :
                    // 在第 k 个插入的数左侧插入一个数字
                    k = Integer.parseInt(s[1]);
                    x = Integer.parseInt(s[2]);
                    add(l[k], x);
                    break;
                case "IR" :
                    // 在第 k 个插入的数右侧插入一个数字
                    k = Integer.parseInt(s[1]);
                    x = Integer.parseInt(s[2]);
                    add(k, x);
                    break;
            }
            // for(int i = r[0]; i != 100005; i = r[i]){
            //     System.out.print(e[i] + " ");
            // }
            // System.out.println();
        }
        for(int i = r[0]; i != 100005; i = r[i]){
            System.out.print(e[i] + " ");
        }
    }
    public static void init(){
        r[0] = 100005;
        l[100005] = 0;
        idx = 1;
    }
    public static void add(int k, int x){
        e[idx] = x;
        r[idx] = r[k];
        l[idx] = k;
        l[r[k]] = idx;
        r[k] = idx;
        idx++;
        
    }
    public static void remove(int k){
        // System.out.println("r[l[k]]: " + r[l[k]] + " l[r[k]]:" + l[r[k]]);
        r[l[k]] = r[k];
        l[r[k]] = l[k];
        // System.out.println("r[l[k]]: " + r[l[k]] + " l[r[k]]:" + l[r[k]]);
    }
}
```
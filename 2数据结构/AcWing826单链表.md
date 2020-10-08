# AcWing 算法基础课 -- 数据结构

## AcWing 826. 单链表

`难度：简单`

### 题目描述

实现一个单链表，链表初始为空，支持三种操作：

(1) 向链表头插入一个数；

(2) 删除第k个插入的数后面的数；

(3) 在第k个插入的数后插入一个数

现在要对该链表进行M次操作，进行完所有操作后，从头到尾输出整个链表。

注意:题目中第k个插入的数并不是指当前链表的第k个数。例如操作过程中一共插入了n个数，则按照插入的时间顺序，这n个数依次为：第1个插入的数，第2个插入的数，…第n个插入的数。

**输入格式**

第一行包含整数M，表示操作次数。

接下来M行，每行包含一个操作命令，操作命令可能为以下几种：

(1) “H x”，表示向链表头插入一个数x。

(2) “D k”，表示删除第k个输入的数后面的数（当k为0时，表示删除头结点）。

(3) “I k x”，表示在第k个输入的数后面插入一个数x（此操作中k均大于0）。

**输出格式**

共一行，将整个链表从头到尾输出。

```r
数据范围

1≤M≤100000


所有操作保证合法。
输入样例：

10
H 9
I 1 1
D 1
D 0
H 6
I 3 6
I 4 5
I 4 5
I 3 4
D 6

输出样例：

6 4 6 5
```

### Solution

```java
import java.util.*;
import java.io.*;

public class Main{
    public static int N = 100010;
    public static int[] e = new int[N];
    public static int[] ne = new int[N];
    public static int head = 0;
    public static int idx = 1;
    public static void main(String[] args) throws IOException{
        BufferedReader in = new BufferedReader(new InputStreamReader(System.in));
        int m = Integer.parseInt(in.readLine());
        while(m > 0){
            m--;
            String[] s = in.readLine().split(" ");
            if(s[0].equals("H")){
                int x = Integer.parseInt(s[1]);
                addHead(x);
            }else if(s[0].equals("D")){
                int k = Integer.parseInt(s[1]);
                remove(k);
            }else{
                int k = Integer.parseInt(s[1]);
                int x = Integer.parseInt(s[2]);
                add(k, x);
            }
        }
        for(int i = head; i != 0; i = ne[i]) System.out.print(e[i] + " ");
        
    }
    public static void addHead(int x){
        // 先记录 idx 的值
        // 然后让 idx 指向头结点指向的结点
        // 修改头结点的指向为 idx
        // idx 加 1
        e[idx] = x;
        ne[idx] = head;
        head = idx;
        idx++;
    }
    public static void remove(int k){
        // 如果 k 为 0，删除头结点
        if(k == 0)  head = ne[head];
        // 第 k 个结点指向 next 的 next
        else    ne[k] = ne[ne[k]];
    }
    public static void add(int k, int x){
        // 先记录 idx 的值
        // 然后让 idx 指向第 k 指向的结点
        // 修改第 k 个结点的指向为 idx
        // idx 加 1
        e[idx] = x;
        ne[idx] = ne[k];
        ne[k] = idx;
        idx++;
    }
}
```
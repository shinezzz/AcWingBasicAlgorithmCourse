# AcWing 算法基础课 -- 数据结构

## AcWing 154. 滑动窗口 

`难度：简单`

### 题目描述

给定一个大小为n≤106

的数组。

有一个大小为k的滑动窗口，它从数组的最左边移动到最右边。

您只能在窗口中看到k个数字。

每次滑动窗口向右移动一个位置。

以下是一个例子：

该数组为[1 3 -1 -3 5 3 6 7]，k为3。

```r
窗口位置 	最小值 	最大值
[1 3 -1] -3 5 3 6 7 	-1 	3
1 [3 -1 -3] 5 3 6 7 	-3 	3
1 3 [-1 -3 5] 3 6 7 	-3 	5
1 3 -1 [-3 5 3] 6 7 	-3 	5
1 3 -1 -3 [5 3 6] 7 	3 	6
1 3 -1 -3 5 [3 6 7] 	3 	7
```

您的任务是确定滑动窗口位于每个位置时，窗口中的最大值和最小值。

**输入格式**

输入包含两行。

第一行包含两个整数n和k，分别代表数组长度和滑动窗口的长度。

第二行有n个整数，代表数组的具体数值。

同行数据之间用空格隔开。

**输出格式**

输出包含两个。

第一行输出，从左至右，每个位置滑动窗口中的最小值。

第二行输出，从左至右，每个位置滑动窗口中的最大值。

```r
输入样例：

8 3
1 3 -1 -3 5 3 6 7

输出样例：

-1 -3 -3 -3 3 3
3 3 5 5 6 7
```

### Solution

```java
import java.util.*;
import java.io.*;

public class Main{
    public static void main(String[] args) throws IOException{
        BufferedReader in = new BufferedReader(new InputStreamReader(System.in));
        String[] s = in.readLine().split(" ");
        int n = Integer.parseInt(s[0]);
        int k = Integer.parseInt(s[1]);
        // 数组 a 保存原始数据
        int[] a = new int[n + 10];
        // 数组 q 保存每一个滑动窗口处理之后的严格单调队列元素的下标
        // 注意 保存的是下标
        int[] q = new int[n + 10];
        s = in.readLine().split(" ");
        for(int i = 0; i < n; i++){
            a[i] = Integer.parseInt(s[i]);
        }
        // 1. 找滑动窗口的最小值
        // 滑动窗口的队列：队尾插入，队首弹出
        // hh 代表队首，tt 代表队尾
        // 分别初始化为 0 和 -1，保证滑动窗口为空的时候 tt < hh
        int hh = 0, tt = -1;
        for(int i = 0; i < n; i++){
            // 判断是否需要弹出队首元素
            // 当窗口队列不为空 且 当前下标和队首元素下标的差值大于 k - 1
            if(hh <= tt && i - q[hh] > k - 1) hh++;
            // 从队尾开始,弹出不大于当前元素的值
            while(hh <= tt && a[q[tt]] >= a[i]) tt--;
            // 插入当前元素
            tt++;
            q[tt] = i;
            // 队首元素即是当前窗口的最大值,打印出来
            // 当窗口元素个数达到 k 个时再输出
            if(i >= k - 1) System.out.print(a[q[hh]] + " ");
        }
        System.out.println();
        // 2. 找滑动窗口的最大值
        hh = 0;
        tt = -1;
        for(int i = 0; i < n; i++){
            if(hh <= tt && i - q[hh] > k - 1)  hh++;
            while(hh <= tt && a[q[tt]] <= a[i]) tt--;
            tt++;
            q[tt] = i;
            if(i >= k - 1) System.out.print(a[q[hh]] + " ");
        }
        System.out.println();
    }
}
```
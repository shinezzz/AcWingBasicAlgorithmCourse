# AcWing 算法基础课 -- 基础算法

## AcWing 796. 子矩阵的和 

`难度：简单`

### 题目描述

输入一个n行m列的整数矩阵，再输入q个询问，每个询问包含四个整数x1, y1, x2, y2，表示一个子矩阵的左上角坐标和右下角坐标。

对于每个询问输出子矩阵中所有数的和。

**输入格式**

第一行包含三个整数n，m，q。

接下来n行，每行包含m个整数，表示整数矩阵。

接下来q行，每行包含四个整数x1, y1, x2, y2，表示一组询问。

**输出格式**

共q行，每行输出一个询问的结果。

```r
数据范围

1≤n,m≤1000,
1≤q≤200000,
1≤x1≤x2≤n,
1≤y1≤y2≤m,
−1000≤矩阵内元素的值≤1000

输入样例：

3 4 3
1 7 2 4
3 6 2 8
2 1 2 3
1 1 2 2
2 1 3 4
1 3 3 4

输出样例：

17
27
21
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
        int m = Integer.parseInt(s[1]);
        int q = Integer.parseInt(s[2]);
        int[][] a = new int[n][m];
        int[][] p = new int[n + 1][m + 1];
        for(int i = 0; i < n; i++){
            s = in.readLine().split(" ");
            for(int j = 0; j < m; j++){
                a[i][j] = Integer.parseInt(s[j]);
                p[i + 1][j + 1] = a[i][j] + p[i][j + 1] + p[i + 1][j] - p[i][j];
            }
        }
        while(q > 0){
            q--;
            s = in.readLine().split(" ");
            int x1 = Integer.parseInt(s[0]);
            int y1 = Integer.parseInt(s[1]);
            int x2 = Integer.parseInt(s[2]);
            int y2 = Integer.parseInt(s[3]);
            System.out.println(p[x2][y2] - p[x2][y1 - 1] - p[x1 - 1][y2] + p[x1 - 1][y1 - 1]);
        }
    }
}
```
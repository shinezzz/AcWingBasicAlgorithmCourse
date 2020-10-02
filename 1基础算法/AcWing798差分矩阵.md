# AcWing 算法基础课 -- 基础算法

## AcWing 798. 差分矩阵

`难度：简单`

### 题目描述

输入一个n行m列的整数矩阵，再输入q个操作，每个操作包含五个整数x1, y1, x2, y2, c，其中(x1, y1)和(x2, y2)表示一个子矩阵的左上角坐标和右下角坐标。

每个操作都要将选中的子矩阵中的每个元素的值加上c。

请你将进行完所有操作后的矩阵输出。

**输入格式**

第一行包含整数n,m,q。

接下来n行，每行包含m个整数，表示整数矩阵。

接下来q行，每行包含5个整数x1, y1, x2, y2, c，表示一个操作。

**输出格式**

共 n 行，每行 m 个整数，表示所有操作进行完毕后的最终矩阵。

```r
数据范围

1≤n,m≤1000,
1≤q≤100000,
1≤x1≤x2≤n,
1≤y1≤y2≤m,
−1000≤c≤1000,
−1000≤矩阵内元素的值≤1000

输入样例：

3 4 3
1 2 2 1
3 2 2 1
1 1 1 1
1 1 2 2 1
1 3 2 3 2
3 1 3 4 1

输出样例：

2 3 4 1
4 3 4 1
2 2 2 2
```

### Solution

```java
import java.util.*;
import java.io.*;

public class Main{
    public static void main(String[] args) throws IOException{
        BufferedReader in = new BufferedReader(new InputStreamReader(System.in));
        BufferedWriter out = new BufferedWriter(new OutputStreamWriter(System.out)); 
        String[] s = in.readLine().split(" ");
        int n = Integer.parseInt(s[0]);
        int m = Integer.parseInt(s[1]);
        int q = Integer.parseInt(s[2]);
        int[][] a = new int[n + 10][m + 10];
        int[][] b = new int[n + 10][m + 10];
        for(int i = 1; i <= n; i++){
            s = in.readLine().split(" ");
            for(int j = 1; j <= m; j++){
                int c = Integer.parseInt(s[j - 1].trim());
                insert(a, i, j, i, j, c);
            }
        }
        while(q > 0){
            q--;
            s = in.readLine().split(" ");
            int x1 = Integer.parseInt(s[0]);
            int y1 = Integer.parseInt(s[1]);
            int x2 = Integer.parseInt(s[2]);
            int y2 = Integer.parseInt(s[3]);
            int c = Integer.parseInt(s[4]);
            insert(a, x1, y1, x2, y2, c);
        }
        for(int i = 1; i <= n; i++){
            for(int j = 1; j <= m; j++){
                b[i][j] = a[i][j] + b[i - 1][j] + b[i][j - 1] - b[i - 1][j - 1];
                // 如果不是以字符串的形式输出，就输出不了数字
                out.write(b[i][j] + " ");
                if(j == m){
                    out.write("\n");
                }
                
            }
            out.flush();

        }
        
    }
    public static void insert(int[][] a, int x1, int y1, int x2, int y2, int c){
        a[x1][y1] += c;
        a[x2 + 1][y1] -= c;
        a[x1][y2 + 1] -= c;
        a[x2 + 1][y2 + 1] += c;
    }
}
```
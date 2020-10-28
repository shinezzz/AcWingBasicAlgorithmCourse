# AcWing 算法基础课 -- 搜索与图论

## AcWing 844. 走迷宫  

`难度：简单`

### 题目描述

给定一个n*m的二维整数数组，用来表示一个迷宫，数组中只包含0或1，其中0表示可以走的路，1表示不可通过的墙壁。

最初，有一个人位于左上角(1, 1)处，已知该人每次可以向上、下、左、右任意一个方向移动一个位置。

请问，该人从左上角移动至右下角(n, m)处，至少需要移动多少次。

数据保证(1, 1)处和(n, m)处的数字为0，且一定至少存在一条通路。

**输入格式**

第一行包含两个整数n和m。

接下来n行，每行包含m个整数（0或1），表示完整的二维数组迷宫。

**输出格式**

输出一个整数，表示从左上角移动至右下角的最少移动次数。

**数据范围**

$1≤n,m≤100$

```r
输入样例：

5 5
0 1 0 0 0
0 1 0 1 0
0 0 0 0 0
0 1 1 1 0
0 0 0 1 0

输出样例：

8
```
### Solution

```java
import java.util.*;

class Main{
    public static final int N = 110;
    // a 数组保存地图
    public static int[][] a = new int[N][N];
    // d 数组表示从起点到 (x, y) 的距离,如没有走过为-1
    public static int[][] d = new int[N][N];
    public static int[] dy = {0, -1, 0, 1};
    public static int[] dx = {-1, 0, 1, 0};
    public static void main(String[] args){
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();
        int m = sc.nextInt();
        for(int i = 1; i <= n; i++){
            for(int j = 1; j <= m; j++){
                a[i][j] = sc.nextInt();
            }
        }
        // 从(1,1)走到(n,m)
        // 把起始点初始化为 1,这样 d[x][y] 为 0 的点就是没有到达的点
        d[1][1] = 1;
        Queue<Pair> q = new ArrayDeque<>();
        q.add(new Pair(1, 1));
        while(!q.isEmpty()){
            Pair p = q.poll();
            // 朝四个方向走
            for(int i = 0; i < 4; i++){
                int x = p.x + dx[i], y = p.y + dy[i];
                // 如果(x,y)在范围内且没有障碍物,则代表可走,放入队列;
                if(x >= 1 && x <= n && y >= 1 && y <= m && a[x][y] == 0 && d[x][y] == 0){
                    d[x][y] = d[p.x][p.y] + 1;
                    q.add(new Pair(x, y));
                }
            }
        }
        System.out.print(d[n][m] - 1);
    }
    static class Pair{
        int x, y;
        public Pair(int x, int y){
            this.x = x;
            this.y = y;
        }
    }
}
```
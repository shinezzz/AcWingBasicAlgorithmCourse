# AcWing 算法基础课 -- 搜索与图论

## AcWing 845. 八数码

`难度：简单`

### 题目描述

在一个3×3的网格中，1~8这8个数字和一个“x”恰好不重不漏地分布在这3×3的网格中。

例如：

```r
1 2 3
x 4 6
7 5 8
```

在游戏过程中，可以把“x”与其上、下、左、右四个方向之一的数字交换（如果存在）。

我们的目的是通过交换，使得网格变为如下排列（称为正确排列）：

```r
1 2 3
4 5 6
7 8 x
```

例如，示例中图形就可以通过让“x”先后与右、下、右三个方向的数字交换成功得到正确排列。

交换过程如下：

```r
1 2 3   1 2 3   1 2 3   1 2 3
x 4 6   4 x 6   4 5 6   4 5 6
7 5 8   7 5 8   7 x 8   7 8 x
```

现在，给你一个初始网格，请你求出得到正确排列至少需要进行多少次交换。


**输入格式**

输入占一行，将3×3的初始网格描绘出来。

例如，如果初始网格如下所示：

```r
1 2 3

x 4 6

7 5 8

则输入为：1 2 3 x 4 6 7 5 8
```

**输出格式**

输出占一行，包含一个整数，表示最少交换次数。

如果不存在解决方案，则输出”-1”。

```r
输入样例：

2  3  4  1  5  x  7  6  8 

输出样例

19
```

### Solution

字符串处理差劲，这部分还要优化。

```java
import java.util.*;

class Main{
    public static void main(String[] args){
        Scanner sc = new Scanner(System.in);
        StringBuilder state = new StringBuilder();
        for(int i = 0; i < 9; i++){
            state.append(sc.next());
        }
        System.out.println(bfs(state));
    }
    public static int bfs(StringBuilder state){
        String end = "12345678x";
        Queue<StringBuilder> q = new ArrayDeque<>();
        Map<String, Integer> map = new HashMap<>();
        map.put(state.toString(),0);
        q.add(state);
        
        int[] dx = {-1, 0, 1, 0};
        int[] dy = {0, -1, 0, 1};
        
        while(!q.isEmpty()){
            StringBuilder t = q.poll();
            if(t.toString().equals(end)){
                 return map.get(t.toString());
            }
            int dist = map.get(t.toString());
            int idx = t.indexOf("x");
            // x 转化为九宫格的位置
            int x = idx / 3;
            int y = idx % 3;
            // 找到可以和 x 交换的位置
            for(int i = 0; i < 4; i++){
                int a = x + dx[i], b = y + dy[i];
                // 判断坐标是否在九宫格内
                if(a >= 0 && a < 3 && b >= 0 && b < 3){
                    swap(t, a * 3 + b, x * 3 + y);
                    if(!map.containsKey(t.toString())){
                        map.put(t.toString(), dist + 1);
                        q.add(new StringBuilder(t));
                    }
                    swap(t, a * 3 + b, x * 3 + y);
                }
            }
        }
        return -1;
    }
    public static void swap(StringBuilder t, int m, int n){
        char c = t.charAt(m);
        t.setCharAt(m, t.charAt(n));
        t.setCharAt(n, c);
    }
}
```
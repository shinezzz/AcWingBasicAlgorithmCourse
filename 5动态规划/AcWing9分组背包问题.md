# LeetCode 专题 -- 背包专题

## AcWing 9. 分组背包问题

`难度：中等`

### 题目描述

有 N 组物品和一个容量是 V 的背包。

每组物品有若干个，同一组内的物品最多只能选一个。

每件物品的体积是 vij，价值是 wij，其中 i 是组号，j 是组内编号。

求解将哪些物品装入背包，可使物品总体积不超过背包容量，且总价值最大。

输出最大价值。

**输入格式**：

第一行有两个整数 N，V，用空格隔开，分别表示物品组数和背包容量。

接下来有 N 组数据：

- 每组数据第一行有一个整数 Si，表示第 i 个物品组的物品数量；
- 每组数据接下来有 Si 行，每行有两个整数 vij,wij，用空格隔开，分别表示第 i 个物品组的第 j 个物品的体积和价值；

**输出格式**：

输出一个整数，表示最大价值。

**数据范围**：

- 0 < N,V ≤ 100
- 0 < Si ≤ 100
- 0 < vij,wij ≤ 100

**示例 1**:

```r
3 5
2
1 2
2 4
1
3 4
1
4 5

输出样例：

8
```


**链接**：

> <https://www.acwing.com/problem/content/9/>

### Solution


**思路**：

背包问题，循环的顺序**物品-->体积-->决策**。

**进阶版**：

```java
import java.util.*;

class Main{
    public static void main(String[] args){
        Scanner sc = new Scanner(System.in);
        int N = sc.nextInt();
        int V = sc.nextInt();
        int[] dp = new int[V + 10];
        // 循环顺序为 物品种类 -> 体积 -> 决策
        // 还是 01 背包的思想，只不过 01 背包是放或者不放
        // 分组背包就是多一层循环，放或者不放第 i 个，一组里只能放一个
        for(int i = 1; i <= N; i++){
            int s = sc.nextInt();
            int[] v = new int[s];
            int[] w = new int[s];
            for(int k = 0; k < s; k++){
                v[k] = sc.nextInt();
                w[k] = sc.nextInt();
            }
            for(int j = V; j >= 0; j--){
                for(int k = 0; k < s; k++){
                    if(j >= v[k])  dp[j] = Math.max(dp[j], dp[j - v[k]] + w[k]);
                }
            }
        }
        sc.close();
        System.out.println(dp[V]);
    }
}
```

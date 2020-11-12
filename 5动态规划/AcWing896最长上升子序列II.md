# AcWing 算法基础课 -- 动态规划

## AcWing 896. 最长上升子序列II

`难度：简单`

### 题目描述

给定一个长度为N的数列，求数值严格单调递增的子序列的长度最长是多少。

**输入格式**

第一行包含整数N。

第二行包含N个整数，表示完整序列。

**输出格式**

输出一个整数，表示最大长度。

**数据范围**

$1≤N≤100000，$
$−10^9≤数列中的数≤10^9$

```r
输入样例：

7
3 1 2 1 8 5 6

输出样例：

4
```

### Solution

```java
import java.util.*;

class Main{
    public static void main(String[] args){
        Scanner sc = new Scanner(System.in);
        int N = sc.nextInt();
        // N 为 100000, n 方的做法会 TLE
        int[] a = new int[N + 10];
        // res[i] 数组记录长度为 i 时,所有子序列中结尾最小的元素
        int[] q = new int[N + 10];
        // 初始化为 0
        int len = 0;
        for(int i = 1; i <= N; i++) {
            a[i] = sc.nextInt();
            // 二分查找优化时间复杂度 logn
            // 查找最后一个小于 a[i] 的值
            int idx = bsearch(q, len, a[i]);
            if(idx == len) {
                len++;
                q[len] = a[i];
            }
            else{
                if(q[idx + 1] > a[i]) q[idx + 1] = a[i];
            }
        }
        System.out.println(len);
        
    }
    public static int bsearch(int[] q, int n, int x){
        // 找最后一个小于 x 的位置
        // 如果都比 x 大的话返回 0
        // 从 1 到 n 开始二分
        int low = 1, high = n;
        while(low <= high){
            int mid = (low + high) / 2;
            if(q[mid] < x){
                if(mid == n || q[mid + 1] >= x) return mid;
                else low = mid + 1;
            }
            else high = mid - 1;
        }
        return 0;
    }
}
```
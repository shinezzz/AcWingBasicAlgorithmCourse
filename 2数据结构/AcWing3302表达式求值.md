# AcWing 算法基础课 -- 数据结构

## AcWing 3302表达式求值

`难度：简单`

### 题目描述

给定一个表达式，其中运算符仅包含 +,-,*,/（加 减 乘 整除），可能包含括号，请你求出表达式的最终值。

注意：

- 数据保证给定的表达式合法。
- 题目保证符号 - 只作为减号出现，不会作为负号出现，例如，`-1+2,(2+2)*(-(1+1)+2)` 之类表达式均不会出现。
- 题目保证表达式中所有数字均为正整数。
- 题目保证表达式在中间计算过程以及结果中，均不超过 2^31−1。
- 题目中的整除是指向 0 取整，也就是说对于大于 0 的结果向下取整，例如 5/3=1，对于小于 0 的结果向上取整，例如 5/(1−4)=−1。
- C++和Java中的整除默认是向零取整；Python中的整除//默认向下取整，因此Python的eval()函数中的整除也是向下取整，在本题中不能直接使用。

**输入格式**

共一行，为给定表达式。

**输出格式**

共一行，为表达式的结果。

**数据范围**

表达式的长度不超过 10^5。

```r
输入样例：

(2+2)*(1+1)

输出样例：

8
```

### Solution

```java
import java.util.*;

class Main{
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        String s = sc.nextLine();
        int n = s.length();
        Deque<Integer> num = new LinkedList<>();
        Deque<Character> op = new LinkedList<>();
        Map<Character, Integer> pr = new HashMap<>();
        pr.put('+', 1);
        pr.put('-', 1);
        pr.put('*', 2);
        pr.put('/', 2);
        for(int i = 0; i < n; i++) {
            char c = s.charAt(i);
            if(c == ' ') continue;
            else if(Character.isDigit(c)) {
                int j = i, x = 0;
                while(j < n && Character.isDigit(s.charAt(j))) {
                    x = x * 10 + (s.charAt(j) - '0');
                    j++;
                }
                num.push(x);
                i = j - 1;
            }
            else if(c == '(') op.push(c);
            else if(c == ')') {
                while(op.peek() != '(') cal(num, op);
                op.pop();
            }
            else {
                while(!op.isEmpty() && op.peek() != '(' && pr.get(op.peek()) >= pr.get(c)) cal(num, op);
                op.push(c);
            }
        }
        while(!op.isEmpty()) cal(num, op);
        System.out.println(num.pop());
    }
    public static void cal(Deque<Integer> num, Deque<Character> op) {
        int b = num.pop();
        int a = num.pop();
        char c = op.pop();
        int x = 0;
        if (c == '+') x = a + b;
        else if (c == '-') x = a - b;
        else if (c == '*') x = a * b;
        else x = a / b;
        num.push(x);
    }
}
```
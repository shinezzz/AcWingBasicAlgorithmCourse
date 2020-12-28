# Java API

[TOC]

## java.lang

### Class Integer

1. 最大最小值 : `MAX_VALUE, MIN_VALUE`;
2. 十进制字符串转化为 int 整数 : `Integer.parseInt(String s)`;
3. 不同进制字符串转化为 int 整数 : `Integer.parseInt(String s, int radix)`;
4. 十进制字符串转化为 Integer 整数 : `Integer.valueOf(String s)`;
5. 不同进制字符串转化为 Integer 整数 : `Integer.valueOf(String s, int radix)`;

### Class String

1. 字符串转字符数组：`s.toCharArray()`;
2. 字符串长度： `s.length()`;
3. 数组转字符串 : `String.valueOf(char[] data)`;
4. 返回子字符串 : `s.substring(int beginIndex, int endIndex)`，左闭右开区间;`substring(int beginIndex)`
5. 字符串去除首尾空格 : `s.trim()`;
6. 使用特定切割符来分割字符串成一个字符串数组 : `s.split(String regex)`;
7. 使用特定切割符来分割字符串成一个字符串数组 : `s.split(String regex, int limit)`;
8. 判断字符串内容是否相同 : `equals(Object anObject)`;
9. 判断字符串和`StringBuilder`与`StringBuffer`是否相同 : `contentEquals(CharSequence cs);contentEquals(StringBuffer sb)`;
 

### Class StringBuilder

1. java.lang.StringBuilder
2. Constructor : `StringBuilder(); StringBuilder(String str)`;
3. 添加一个元素,参数 boolean, char, char[], double, float, int , long, String : `append(boolean b)`;
4. 返回相应下标的字符 :  `charAt(int index)`;
5. 转化为字符串 : `toString()`;
6. 替换 : `s.replace()`;TODO时间复杂度
7. 翻转字符串 : `s.reverse()`;
8. 合并生成字符串 : `String.join(CharSequence delimiter, Iterable<? extends CharSequence> elements)`;


## java.util.

### Class Arrays

1. 排序 : `Arrays.sort(array)`;
2. 数组转化为列表 : `Arrays.asList()`
3. 复制数组 : `Arrays.copyOf(T[] original, int newLength)`
4. 数组排序，指定范围 : `Arrays.sort(Object[] a, int fromIndex, int toIndex)`
5. 将数组g的 (1,n) 的元素用Pair的第二个元素升序排序 : `Arrays.sort(T[] a, int fromIndex, int toIndex, Comparator<? super T> c)`；例子如`Arrays.sort(g, 1, n + 1, (Pair p1, Pair p2) -> p1.b - p2.b);`左闭右开区间
6. 二维数组先根据第一个元素排序，再根据第二个元素排序 ：
   ```java
    Arrays.sort(cbs, (o1, o2) -> {
        if(o1[0] != o2[0]) return o1[0] - o2[0];
        else if(o1[1] != o2[1]) return o1[1] - o2[1];
        else return o1[2] - o2[2];
    });
    ```
7. 数组排序，重写比较器的写法：
    ```java
    Arrays.sort(newEdges, new Comparator<int[]>(){
        @Override
        public int compare(int[] o1, int[] o2){
            return o1[2] - o2[2];
        }
    });
    ```

### Interface Collection<E>


1. All Known Subinterfaces:

```java
BeanContext, BeanContextServices, BlockingDeque<E>, BlockingQueue<E>, Deque<E>, List<E>, NavigableSet<E>, Queue<E>, Set<E>, SortedSet<E>, TransferQueue<E>
```

2. All Known Implementing Classes:
```java
AbstractCollection, AbstractList, AbstractQueue, AbstractSequentialList, AbstractSet, ArrayBlockingQueue, ArrayDeque, ArrayList, AttributeList, BeanContextServicesSupport, BeanContextSupport, ConcurrentHashMap.KeySetView, ConcurrentLinkedDeque, ConcurrentLinkedQueue, ConcurrentSkipListSet, CopyOnWriteArrayList, CopyOnWriteArraySet, DelayQueue, EnumSet, HashSet, JobStateReasons, LinkedBlockingDeque, LinkedBlockingQueue, LinkedHashSet, LinkedList, LinkedTransferQueue, PriorityBlockingQueue, PriorityQueue, RoleList, RoleUnresolvedList, Stack, SynchronousQueue, TreeSet, Vector 
```

3. 例子：Deque 转为 List，因为LinkedList有`LinkedList(Collection<? extends E> c)`的构造方法。

```java
List<> list = new LinkedList(Deque);
```

### Interface Deque

1. Summary of Deque methods

||First Element |(Head) |Last Element| (Tail)|
|---|---|---|---|---|
||Throws exception|Special value|Throws exception|Special value|
|Insert|addFirst(e)|offerFirst(e)|addLast(e)|offerLast(e)|
|Remove|removeFirst()|pollFirst()|removeLast()|pollLast()|
|Examine|getFirst()|peekFirst()|getLast()|peekLast()|

2. Queue (FIFO)Comparison of Queue and Deque methods

Queue 队尾进元素，队首出元素

|Queue Method|Equivalent Deque Method|
|---|---|
|add(e)|addLast(e)|
|offer(e)|offerLast(e)|
|remove()|removeFirst()|
|poll()|pollFirst()|
|element()|getFirst()|
|peek()|peekFirst()|

3. Stack (LIFO) Comparison of Stack and Deque methods

**Stack 队首进元素，队首出元素**。

|Stack Method|Equivalent Deque Method|
|---|---|
|push(e)|addFirst(e)|
|pop()|removeFirst()|
|peek()|peekFirst()|

4. 返回大小 : `dq.size()`;

### Interface List

1. LinkedList实现的构造函数 : `LinkedList();LinkedList(Collection<? extends E> c)`;
2. 队尾添加元素 : `list.add(element)`;
3. 获取下标元素 : `list.get(int index)`;
4. 列表元素个数 : `list.size()`;
5. 列表转数组 : `list.toArray()`;//转化为int的比较繁琐
6. 列表是否为空 : `list.isEmpty()`;
7. 列表是否包含相应元素 : `list.contains(Object o)`;

### Interface Map

1. 得到键值，不存在就给默认值 : `map.getOrDefault(key, defaultValue)`;
2. 得到键值 : `map.get(key)`;
3. 是否包含key : `map.containsKey(Object key)`;
4. 返回map的值的集合 : `map.values()`; 可以用 LinkedList 的构造函数来转化为列表

### Regex.Class Pattern

### Class PriorityQueue<E>


> Implementation note: this implementation provides O(log(n)) time for the enqueuing and dequeuing methods (offer, poll, remove() and add); linear time for the remove(Object) and contains(Object) methods; and constant time for the retrieval methods (peek, element, and size). 


1. PriorityQueue : Creates a PriorityQueue with the default initial capacity (11) that orders its elements according to their natural ordering. 自然顺序，默认小根堆。如果要构造大根堆要重写比较器`Queue<Integer> pq = new PriorityQueue<>((v1, v2) -> v2 - v1)`。
2. 查看堆顶元素 : `pq.peek()`;
3. 添加元素 : `pq.add()`;

### Class Stack

不推荐 Stack 类来声明栈。因为 Stack 继承 Vector，Vector 是一个动态数组，可以在任意位置添加或者删除元素。因此 Stack 也有这个能力，这就破坏了封装成一个 Stack 的意义。一般用 Deque 来声明一个栈。

```java
Deque<Integer> stack = new ArrayDeque<Integer>();
```

---
---
```
C++ STL简介
vector, 变长数组，倍增的思想
    size()  返回元素个数
    empty()  返回是否为空
    clear()  清空
    front()/back()
    push_back()/pop_back()
    begin()/end()
    []
    支持比较运算，按字典序

pair<int, int>
    first, 第一个元素
    second, 第二个元素
    支持比较运算，以first为第一关键字，以second为第二关键字（字典序）

string，字符串
    size()/length()  返回字符串长度
    empty()
    clear()
    substr(起始下标，(子串长度))  返回子串
    c_str()  返回字符串所在字符数组的起始地址

queue, 队列
    size()
    empty()
    push()  向队尾插入一个元素
    front()  返回队头元素
    back()  返回队尾元素
    pop()  弹出队头元素

priority_queue, 优先队列，默认是大根堆
    size()
    empty()
    push()  插入一个元素
    top()  返回堆顶元素
    pop()  弹出堆顶元素
    定义成小根堆的方式：priority_queue<int, vector<int>, greater<int>> q;

stack, 栈
    size()
    empty()
    push()  向栈顶插入一个元素
    top()  返回栈顶元素
    pop()  弹出栈顶元素

deque, 双端队列
    size()
    empty()
    clear()
    front()/back()
    push_back()/pop_back()
    push_front()/pop_front()
    begin()/end()
    []

set, map, multiset, multimap, 基于平衡二叉树（红黑树），动态维护有序序列
    size()
    empty()
    clear()
    begin()/end()
    ++, -- 返回前驱和后继，时间复杂度 O(logn)

    set/multiset
        insert()  插入一个数
        find()  查找一个数
        count()  返回某一个数的个数
        erase()
            (1) 输入是一个数x，删除所有x   O(k + logn)
            (2) 输入一个迭代器，删除这个迭代器
        lower_bound()/upper_bound()
            lower_bound(x)  返回大于等于x的最小的数的迭代器
            upper_bound(x)  返回大于x的最小的数的迭代器
    map/multimap
        insert()  插入的数是一个pair
        erase()  输入的参数是pair或者迭代器
        find()
        []  注意multimap不支持此操作。 时间复杂度是 O(logn)
        lower_bound()/upper_bound()

unordered_set, unordered_map, unordered_multiset, unordered_multimap, 哈希表
    和上面类似，增删改查的时间复杂度是 O(1)
    不支持 lower_bound()/upper_bound()， 迭代器的++，--

bitset, 圧位
    bitset<10000> s;
    ~, &, |, ^
    >>, <<
    ==, !=
    []

    count()  返回有多少个1

    any()  判断是否至少有一个1
    none()  判断是否全为0

    set()  把所有位置成1
    set(k, v)  将第k位变成v
    reset()  把所有位变成0
    flip()  等价于~
    flip(k) 把第k位取反


作者：yxc
链接：https://www.acwing.com/blog/content/404/
来源：AcWing
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。
```
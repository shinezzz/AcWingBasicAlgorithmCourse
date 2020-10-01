# Java API Knowledge
[toc]
## Java 声明、定义、赋值、初始化、变量、引用、创建的区别

**变量**：由基本数据类型定义的变量称为普通变量，由类、数字、接口类型定义的变量称为引用型变量

**声明**：`int x;`声明不需要分配存储空间，只作用于编译器；

**定义**: `int x =0;`声明变量并进行初始化的过程称为定义，定义的方式包括声明、引用、创建、初始化；与声明的区别在于是否分配存储空间；

**初始化**: 从定义变量时的赋值或引用的过程称为初始化，也就是第一次赋值或者引用

**赋值**: 普通变量赋值可以不断更新栈中存储的数据，而对象引用用的是同一块堆内存

**引用**: 变量名 = 对象，这个等于的过程就是引用，也称为变量名指向一个对象；注意创建的变量名储存在栈中，而引用是指向堆内存，栈中存的是堆内存的首地址，因此，普通类型变量只在栈区占用一块内存，而引用类型变量要在栈区和堆区各占一块内存；

**创建**: 对于引用型变量，在内存中new（开辟）空间的过程称为创建，开辟的内存空间为堆内存

```java
int a; // 声明了一个类型为int，变量名为a的普通变量；
int a=1; // 定义了一个类型为int，变量名为a，初始化值为1的普通变量；
a=2; // 给已经声明了的变量a赋值为2；
String s; // 声明了一个类型为String 类，变量名为s的引用型变量
String s=null; // 定义了一个类型为String 类，变量名为s的引用型变量，初始化值为空；
String s=“123”; // "123"存储在String 常量池中，s指向存储"123"的地址（常量池：常量池在编译期间就将一部分数据存放于该区域，包含以final修饰的基本数据类型的常量值、String字符串）
String s=new String（“123”); // 定义了一个类型为String 类，变量名为s的引用型变量，创建一个String对象初始化值为"123"
```

## static 和 final 讲解

**可修饰部分**：

1. static：成员变量、方法、代码块（静态代码块）、内部类（静态内部类）
2. final： 类、成员变量、方法、局部变量
3. final在一个对象类唯一，static final在多个对象中都唯一；

**static**：

1. static的主要作用是：方便在没有创建对象的情况下来进行调用（方法/变量）。
2. static 修饰变量
   1. 无论一个类生成了多少个对象，所有这个对象共用唯一一份静态的成员变量；一个对象对该静态成员变量进行了修改，其他对象的该静态成员变量的值也会随之发生变化。如果一个成员变量是static的，那么我们可以通过类名.成员变量名的方式来使用它(推荐使用这种方式)。
   2. 没有被static修饰的变量，叫实例变量。对于实例变量，每创建一个实例，就会为实例变量分配一次内存，实例变量可以在内存中有多个拷贝，互不影响（灵活）。
3. static 修饰方法
   1. **static方法可以直接通过类名调用，任何的实例也都可以调用，static方法只能访问static的变量和方法**，因此static方法中不能用this和super关键字，不能直接访问所属类的实例变量和实例方法(就是不带static的成员变量和成员成员方法)，只能访问所属类的静态成员变量和成员方法。因为static方法独立于任何实例，因此static方法必须被实现，而不能是抽象的abstract。
   2. static的数据或方法，属于整个类的而不是属于某个对象的，是不会和类的任何对象实例联系到一起。所以子类和父类之间可以存在同名的static方法名。
   3. 静态方法只能继承，不能重写(Override)。
4. static 修饰类
   1. 一般的类是没有static的，只有内部类可以加上static来表示嵌套类。
5. static 和 final一起用来修饰成员变量和成员方法，可简单理解为“全局常量”
   1. 对于变量，表示一旦给值就不可修改，并且通过类名可以访问。
   2. 对于方法，表示不可覆盖，并且可以通过类名直接访问。
   3.  对于被static和final修饰过的实例常量，实例本身不能再改变了，但对于一些容器类型（比如，ArrayList、HashMap）的实例变量，不可以改变容器变量本身，但可以修改容器中存放的对象，这一点在编程中用到很多。
    ```java
    private static final String strStaticFinalVar = "aaa";  
    private static String strStaticVar = null;  
    private final String strFinalVar= null;  
    private static final int intStaticFinalVar = 0;  
    private static final Integer integerStaticFinalVar = new Integer(8);  
    private static final ArrayList<String> alStaticFinalVar = new ArrayList<String>();  
    
    //strStaticFinalVar="bbb";//错误，final表示终态,不可以改变变量本身.  
    strStaticVar = "bbb";     //正确，static表示类变量,值可以改变.  
    //strFinalVar="呵呵呵呵";      //错误, final表示终态，在定义的时候就要初值（哪怕给个null），一旦给定后就不可再更改。  
    //intStaticFinalVar=2;         //错误, final表示终态，在定义的时候就要初值（哪怕给个null），一旦给定后就不可再更改。  
    //integerStaticFinalVar=new Integer(8);        //错误, final表示终态，在定义的时候就要初值（哪怕给个null），一旦给定后就不可再更改。  
    alStaticFinalVar.add("aaa");   //正确，容器变量本身没有变化，但存放内容发生了变化。这个规则是非常常用的，有很多用途。  
    alStaticFinalVar.add("bbb");   //正确，容器变量本身没有变化，但存放内容发生了变化。这个规则是非常常用的，有很多用途。  
    ```
6. static 静态代码块
   1. static关键字还有一个比较关键的作用就是 用来形成静态代码块以优化程序性能。static块可以置于类中的任何地方，类中可以有多个static块。在类初次被加载的时候，会按照static块的顺序来执行每个static块，并且只会执行一次。
   2. 静态块要放在声明的变量下面。
   3. 如果继承体系既有构造方法，又有静态代码块，那么首先执行最顶层的类的静态代码块，一直执行到最底层类的静态代码块，然后再去执行最顶层类的构造方法，一直执行到最底层的构造方法，注意：**静态代码块只会执行一次**。
    ```java
    public class Main {
        public static void main(String[] args) {
            new R();
            new R();
        }
    }
    class P{
        //static静态代码块
        static {
            System.out.println("P static block");
        }
        public P(){
            System.out.println("P constructor");
        }
    }
    class Q extends P{
        static {
            System.out.println("Q static block");
        }
        public Q(){
            System.out.println("Q constructor");
        }
    }
    class R extends Q{
        static {
            System.out.println("R static block");
        }
        public R(){
            System.out.println("R constructor");
        }
    }
    ```
   4. 那就是当我们初始化static修饰的成员时，可以将他们统一放在一个以static开始，用花括号包裹起来的块状语句中：
7. 静态导包：不同于非static导入，采用static导入包后，在不与当前类的方法名冲突的情况下，无需使用“类名.方法名”的方法去调用类方法了，直接可以采用"方法名"去调用类方法，就好像是该类自己的方法一样使用即可。

**final**：

1. final修饰类：final类不能被继承，没有子类，final类中的方法默认是final的。
2. final修饰方法： 当一个方法被final所修饰的时，表示该方法是一个终态方法，即不能被重写(Override)。但可以被继承。
3. 类中所有的private方法都被隐含是final的。由于无法取用private方法，则也无法重载之。
4. final修饰变量：
   1. 基础类型 用fianl修饰后就变成了一个常量，不可以重新赋值。
   2. 包装类型 用final修饰后该变量指向的地址不变，但是该地址的的变量完全可以改变。
5. 对于final类型成员变量
6. final修饰方法参数
## Scanner和BufferedReader的区别和用法

Scanner 和 BufferedReader 同样能实现将键盘输入的数据送入程序

**BufferedReader**：

1. BufferedReader 对象只将回车看作输入结束，得到的字符串
2. BufferedReader 是字符输入流中读取文本，缓冲各个字符，从而提供字符、数组和行的高效读取！速度要比Scanner快！而且也可以设置缓冲区的大小，或者可使用默认的大小。大多数情况下，默认值就足够大了。
3. BufferedReader类位于java.io包中,所以要使用这个类,就要引入java.io这个包 
4. `import java.io.BufferedReader.readLine()`方法会返回用户在按下Enter键之前的所有字符输入,不包括最后按下的Enter返回字符.使用BufferedReader对象的readLine()方法必须处理java.io.IOException异常(Exception).使用BufferedReader来取得输入,理解起来要复杂得多.但是使用这个方法是固定的,每次使用前先如法炮制就可以了 

**Scanner**：
1. Scanner对象把回车,空格,tab键都看作输入结束，直接用sc.next()得到的是字符串形式 
2. 在创建Scanner类的对象时,需要用System.in作为它的参数,也可以将Scanner看作是System.in对象的支持者,System.in取得用户输入的内容后,交给Scanner来作一些处理
    ```java
    Scanner类中提供了多个方法:
    next():取得一个字符串;
    nextInt():将取得的字符串转换成int类型的整数;
    nextFloat():将取得的字符串转换成float型;
    nextBoolean():将取得的字符串转换成boolean型; 
    ```
3. Scanner类位于java.util包中,要加上import java.util.Scanner; 用Scanner获得用户的输入非常的方便,但是Scanner取得输入的依据是空格符,包括空格键,Tab键和Enter键.当按下这其中的任一键时,Scanner就会返回下一个输入.当你输入的内容中间包括空格时,显然,使用Scanner就不能完整的获得你输入的字符串.这时候我们可以考虑使用BufferedReader类取得输入.其实在Java SE 1.4及以前的版本中,尚没有提供Scanner方法,我们获得输入时也是使用BufferReader的.

## ArrayList 和 LinkedList

- ArrayList是基于索引的数据接口，它的底层是数组。它可以以O(1)时间复杂度对元素进行随机访问。
- LinkedList是以元素列表的形式存储它的数据，每一个元素都和它的前一个和后一个元素链接在一起，在这种情况下，查找某个元素的时间复杂度是O(n)。
- 相对于ArrayList，LinkedList的插入，添加，删除操作速度更快，因为当元素被添加到集合任意位置的时候，不需要像数组那样重新计算大小或者是更新索引。
- LinkedList比ArrayList更占内存，因为LinkedList为每一个节点存储了两个引用，一个指向前一个元素，一个指向下一个元素。
- ArrayList的实现用的是数组，LinkedList是基于链表，**ArrayList适合查找**，**LinkedList适合增删**。

## Stack 和 Deque

一个更加完整，一致的，后进先出的栈相关的操作，应该由 Deque 接口提供。并且，也推荐使用 Deque 这种数据结构（比如 ArrayDeque）来实现。

```java
Deque<Integer> stack = new ArrayDeque<Integer>();
```

1. Java 中的 Stack 类到底怎么了？
   
Java 中的 Stack 类，最大的问题是，继承了 Vector 这个类。Vector 就是一个动态数组。继承使得子类继承了父类的所有公有方法。而 Vector 作为动态数组，是有能力在数组中的任何位置添加或者删除元素的。因此，Stack 继承了 Vector，Stack 也有这样的能力。这就破坏了栈这种数据结构的封装。

2. 为什么使用接口？

接口在 OOP 设计中，也是非常重要的概念。并且，在近些年，变得越来越重要。甚至发展出了“面向接口的编程”这一思想（Interface-based programming）。

在 Java 语言中，Queue 就是一个接口。我们想实现一个队列，可以这么写：

```java
Queue<Integer> q1 = new LinkedList<>();
Queue<Integer> q2 = new ArrayDeque<>();
```

q1 和 q2 的底层具体实现不同，一个是 LinkedList，一个是 ArrayDeque。但是，从用户的角度看，q1 和 q2 是一致的：都是一个队列，只能执行队列规定的方法。

底层开发人员可以随意维护自己的 LinkedList 类或者 ArrayDeque 类，只要他们满足 Queue 接口规定的规范；**接口的设计相当于做了访问限制。**

3. LinkedList 还是 ArrayQueue 来实现 Deque

Java 官方推荐的创建栈的方式，使用了 Deque 接口。并且，在底层实现上，使用了 ArrayDeque，也就是基于动态数组的实现。为什么？

动态数组是可以进行扩容操作的。在触发扩容的时候，时间复杂度是 O(n) 的，但整体平均时间复杂度（Amortized Time）是 O(1)。

动态数组是可以进行扩容操作的。在触发扩容的时候，时间复杂度是 O(n) 的，但整体平均时间复杂度（Amortized Time）是 O(1)。

虽然如此，可是实际上，当数据量达到一定程度的时候，链表的性能是远远低于动态数组的。

这是因为，对于链表来说，每添加一个元素，都需要重新创建一个 Node 类的对象，也就是都需要进行一次 new 的内存操作。而对内存的操作，是非常慢的。

因此，甚至有人建议：在实践中，尤其是面对大规模数据的时候，不应该使用链表！

4. Vector 

实际上，Vector 这个类不仅仅是简单的一个动态数组而已，而更进一步，保证了线程安全。

因为要保证线程安全，所以 Vector 实际上效率也并不高。

Java 官方的 Vector 文档中明确指出了：如果你的应用场景不需要线程安全的特性，那么对于动态数组，应该使用 ArrayList。

## map 和 set

## java箭头函数，lambda表达式

## 常用数据结构的时间复杂度

|Data Structure|新增|查询/Find|删除/Delete|GetByIndex|
|---|---|---|---|---|
|数组  Array (T[]) |	O(n) |	O(n) 	|O(n) |	O(1)
|链表 Linked list (LinkedList<T>) |	O(1)| 	O(n) |	O(n) |	O(n)
Resizable array list (List<T>) |	O(1) 	|O(n) |	O(n) |	O(1)
|Stack (Stack<T>) |	O(1) |	- |	O(1) |	-|
|Queue (Queue<T>) 	|O(1) 	|- |	O(1) |	-|
|Hash table (Dictionary<K,T>) |	O(1) |	O(1) |	O(1) |	-|
|Tree-based dictionary(SortedDictionary<K,T>) |	O(log n) |	O(log n) |	O(log n)| 	-|
|Hash table based set (HashSet<T>) |	O(1) |	O(1) |	O(1) |	-|
|Tree based set (SortedSet<T>) |	O(log n) |	O(log n) 	|O(log n) |	-|

## Java 运算符优先级

下表中具有最高优先级的运算符在的表的最上面，最低优先级的在表的底部。

|类别|操作符|关联性|
|:---:|:---:|---|
|后缀|() [] . (点操作符)|左到右|
|一元|++ -- ！ ~|从右到左|
|乘性|*  /  ％|左到右|
|加性|+ -|左到右|
|移位|>> >>> <<|左到右|
|关系|> >= <> <=|左到右|
|相等|== !=|左到右|
|按位与|＆|左到右|
|按位异或|^|左到右|
|按位或|\||左到右|
|逻辑与|&&|左到右|
|逻辑或|\| \||左到右|
|条件|？：|从右到左|
|赋值|= += -= *= /= ％= >>= <<= ＆= ^= |从右到左|
|逗号|，|左到右|

## 由数据范围反推算法复杂度以及算法内容

一般ACM或者笔试题的时间限制是1秒或2秒。
在这种情况下，C++代码中的操作次数控制在 107107 为最佳。

下面给出在不同数据范围下，代码的时间复杂度和算法该如何选择：

1. $n≤30$, 指数级别, dfs+剪枝，状态压缩dp
2. $n≤100 => O(n3)$，floyd，dp
3. $n≤1000 => O(n2)，O(n2logn)$，dp，二分，朴素版Dijkstra、朴素版Prim、Bellman-Ford
4. $n≤10000 => O(n∗\sqrt{n})$，块状链表、分块、莫队
5. $n≤100000 => O(nlogn)$ => 各种sort，线段树、树状数组、set/map、heap、dijkstra+heap、6. prim+heap、spfa、求凸包、求半平面交、二分
6. $n≤1000000 => O(n), 以及常数较小的 O(nlogn) 算法 => hash、双指针扫描、并查集，kmp、AC自动机，常数比较小的 O(nlogn)的做法：sort、树状数组、heap、dijkstra、spfa
7. $n≤10000000 => O(n)$，双指针扫描、kmp、AC自动机、线性筛素数
8. $n≤10^9 => O(\sqrt{n})$，判断质数
9. $n≤10^18 => O(logn)$，最大公约数，快速幂
10. $n≤10^1000 => O((logn)^2)$，高精度加减乘除
11. $n≤10^100000 => O(logn×loglogn)$，高精度加减、FFT/NTT

作者：yxc
链接：https://www.acwing.com/blog/content/32/
来源：AcWing
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。
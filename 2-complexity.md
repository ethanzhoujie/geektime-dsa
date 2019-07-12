# 复杂度分析

#### 事后统计法

即用测试数据计算算法占用的时间内存等的方法。

1. 测试结果依赖测试环境
2. 测试结果依赖数据规模

#### 时间复杂度/空间复杂度

即不需要具体的测试数据来测试，就可以粗略的估算出算法的执行效率的方法。

##### 大O复杂度表示法

代码执行时间随**数据增长规模**的变化趋势

##### 时间复杂度

* **只关注执行次数最多的一段代码**

```java
int cal(int n) {
    int sum = ；
    int i = 1;
    for (; i <= n; ++i) {   // 这行代码被执行了 n 次，在这段程序中执行次数最多
        sum = sum + i;      // 这行代码被执行了 n 次，在这段程序中执行次数最多
    }
    return sum;
}
```

所以这段代码的时间复杂度就是 O\(n\)

* **加法法则：总复杂度等于量级最大的那段代码的复杂度**

如果 T1\(n\)=O\(f\(n\)\)，T2\(n\)=O\(g\(n\)\)；那么 T\(n\)=T1\(n\)+T2\(n\)=max\(O\(f\(n\), O\(g\(n\)\)\) =O\(max\(f\(n\), g\(n\)\)\)=O\(max\(f\(n\), g\(n\)\)\)

```java
int cal(int n) {

   //这段代码执行了 100 次，所以是一个常量规模，跟 n 的规模无关，即使执行了 10000000 次，对增长趋势并没有影响
   int sum_1 = 0;
   int p = 1;
   for (; p < 100; ++p) {
     sum_1 = sum_1 + p;
   }

   // O(n)
   int sum_2 = 0;
   int q = 1;
   for (; q < n; ++q) {
     sum_2 = sum_2 + q;
   }

   // O(n^2)
   int sum_3 = 0;
   int i = 1;
   int j = 1;
   for (; i <= n; ++i) {
     j = 1; 
     for (; j <= n; ++j) {
       sum_3 = sum_3 +  i * j;
     }
   }

   return sum_1 + sum_2 + sum_3;
 }
```

所以这段代码的时间复杂度就是 O\(n^2\)

* **乘法法则：嵌套代码的复杂度等于嵌套内外代码复杂度的乘积**

如果 T1=O\(f\(n\)\)， T2=O\(g\(n\)\)；那么T\(n\)=T1\(n\)\*T2\(n\)=O\(f\(n\)\)\*O\(g\(n\)\)=O\(f\(n\)\*g\(n\)\).

```java
int cal(int n) {
   int ret = 0; 
   int i = 1;
   // O(n)
   for (; i < n; ++i) {
     ret = ret + f(i);
   } 
} 

int f(int n) {
  int sum = 0;
  int i = 1;
  // O(n)
  for (; i < n; ++i) {
    sum = sum + i;
  } 
  return sum;
}
```

cal\(\) 的时间复杂度为 O\(n^2\)

##### 几种常见时间复杂度实例分析

![](./assets/complexitypic.png)

非多项式量级：O\(2^n\), O\(n!\)

多项式量级：其余均为多项式量级

* **O\(1\)**

```java
 int i = 8;
 int j = 6;
 int sum = i + j;
```

O\(1\) 不是只有一行代码，是指执行时间不随着 n 的增大而增长。

一般情况下，只要算法中不存在循环语句，递归语句，即使有成千上万行的代码，其时间复杂度也是 O\(1\)。

* **O\(logn\), O\(nlogn\)**

```java
 i=1;
 while (i <= n)  { // 第2行和第3行代码是循环次数最多的
   i = i * 2;      // 只要计算出第三行代码的时间复杂度就可以了
 }
```

![logn](./assets/logn.jpg)

2^x = n ---&gt; x = log2\(n\) —&gt; O\(log2\(n\)\)

根据对数换底公式：log2\(n\) \* log10\(2\) = log10\(n\) = logn

**所以在采用大 O 标记复杂度的时候可以忽略系数，即 O\(Cf\(n\)\) = O\(f\(n\)\)**

**因此在对数阶时间复杂度的表示方法里，可以忽略对数的底，统一表示为O\(logn\)**

* **O\(m+n\), O\(m\*n\)**

```java
int cal(int m, int n) {
  int sum_1 = 0;
  int i = 1;
  for (; i < m; ++i) {
    sum_1 = sum_1 + i;
  }

  int sum_2 = 0;
  int j = 1;
  for (; j < n; ++j) {
    sum_2 = sum_2 + j;
  }

  return sum_1 + sum_2;
}
```

代码的复杂度由两个数据的估摸来决定

![complexity-graph](./assets/complexity-graph.jpg)

##### 几种常见时间复杂度计算方法

- **最好情况时间复杂度**（best case time complexity）
- **最坏情况时间复杂度**（worst case time complexity）
- **平均情况时间复杂度**（average case time complexity）

```java
// n 表示数组 array 的长度
int find(int[] array, int n, int x) {
  int i = 0;
  int pos = -1;
  for (; i < n; ++i) {
    if (array[i] == x) {
       pos = i;
       break;
    }
  }
  return pos;
}
```

对于上段代码，有 n+1 中情况，即在 position = 0, 1, 2, … , n-1 位置找到 target x，和在 array 中未找到 target x，共 n+1 中情况。

(1+2+3+ … + n + n) / (n+1) = n(n+3) / 2(n+1)

已上的计算过程是没有考虑每种情况发生的概率的。

我们假设 target x 在数组中和不在数组中的概率是相等的，都是 1/2。所以

1 * 1/2n + 2 * 1/2n + 3 * 1/2n + … + n * 1/2n + n * 1/2 = (3n + 1) / 4

这个值就是就是概率中的**加权平均值**，也叫做**期望值**。所以**平均时间复杂度**的全称应该叫**加权平均时间复杂度**或者**期望时间复杂度**。

- **均摊时间复杂度**（amortized time complexity）

均摊时间复杂度就是一种特殊的平均情况时间复杂度

对一组数据结构进行一组连续操作中，大部分情况下时间复杂度都很低，只有个别情况下时间复杂度比较高，而且这些操作之间还有连贯的时序关系，这个时候，我们就可以将这一组操作放在一块分析，看是否能将那次较高时间复杂度操作的耗时，平摊到时间复杂度较低的操作上。



##### 空间复杂度分析

空间复杂度全称为渐进式空间复杂度\(asymptotic space complexity\)，表示算法的存储空间与数据规模之间的增长关系。


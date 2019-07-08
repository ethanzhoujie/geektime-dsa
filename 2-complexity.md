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

非多项式量级：O(2^n), O(n!)

多项式量级：其余均为多项式量级

- **O(1)**

```java
 int i = 8;
 int j = 6;
 int sum = i + j;
```

O(1) 不是只有一行代码，是指执行时间不随着 n 的增大而增长。

一般情况下，只要算法中不存在循环语句，递归语句，即使有成千上万行的代码，其时间复杂度也是 O(1)。

- **O(logn), O(nlogn)**

```java
 i=1;
 while (i <= n)  { // 第2行和第3行代码是循环次数最多的
   i = i * 2;      // 只要计算出第三行代码的时间复杂度就可以了
 }
```

![logn](./assets/logn.jpg)

2^x = n ---> x = log2(n) —> O(log2(n))

根据对数换底公式：log2(n) * log10(2) = log10(n) = logn

**所以在采用大 O 标记复杂度的时候可以忽略系数，即 O(Cf(n)) = O(f(n))**

**因此在对数阶时间复杂度的表示方法里，可以忽略对数的底，统一表示为O(logn)**

- **O(m+n), O(m*n)**

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

##### 空间复杂度分析

空间复杂度全称为渐进式空间复杂度(asymtotic space complexity)，表示算法的存储空间与数据规模之间的增长关系。






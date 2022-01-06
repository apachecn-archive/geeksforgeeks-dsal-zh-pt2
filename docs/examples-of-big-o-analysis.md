# 大 O 分析示例

> 原文:[https://www.geeksforgeeks.org/examples-of-big-o-analysis/](https://www.geeksforgeeks.org/examples-of-big-o-analysis/)

**前提:** [算法分析|大 O 分析](https://www.geeksforgeeks.org/analysis-algorithms-big-o-analysis/)

在[上一篇文章](https://www.geeksforgeeks.org/analysis-algorithms-big-o-analysis/)中，讨论了使用**大 O** [渐近符号](https://www.geeksforgeeks.org/analysis-of-algorithms-set-3asymptotic-notations/)的算法分析。本文讨论了一些例子来说明**大 O** 时间复杂度符号，并学习如何计算任何程序的时间复杂度。

有不同的渐近表示法来度量算法的时间复杂度。这里，使用**“O”(大 O)** 符号来获得时间复杂度。时间复杂度估计运行一个[算法](https://www.geeksforgeeks.org/fundamentals-of-algorithms/)的时间。这是通过计算电梯运行次数计算出来的。以只取决于算法及其输入的方式知道执行时间的原因始终是一种好的做法。这可以通过选择算法重复执行的基本运算来实现，并且将时间复杂度 **T(N)** 定义为算法在给定长度数组 **N** 的情况下执行的这种运算的数量。

**<u>例 1</u> :**

**<u>具有基本运算的循环的时间复杂度</u> :** 假设这些运算需要单位时间来执行。这个单位时间可以用 ***O(1)*** 表示。如果循环运行 **N 次**没有任何比较。下图也是同样的情况:

## C++

```
// C++ program to illustrate time
// complexity for single for-loop
#include <bits/stdc++.h>
using namespace std;

// Driver Code
int main()
{
    int a = 0, b = 0;
    int N = 4, M = 4;

    // This loop runs for N time
    for (int i = 0; i < N; i++) {
        a = a + 10;
    }
    // This loop runs for M time
    for (int i = 0; i < M; i++) {
        b = b + 40;
    }

    cout << a << ' ' << b;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to illustrate time
// complexity for single for-loop
class GFG
{

  // Driver Code
  public static void main(String[] args)
  {
    int a = 0, b = 0;
    int N = 4, M = 4;

    // This loop runs for N time
    for (int i = 0; i < N; i++)
    {
      a = a + 10;
    }

    // This loop runs for M time
    for (int i = 0; i < M; i++)
    {
      b = b + 40;
    }
    System.out.print(a + " " + b);
  }
}

// This code is contributed by rutvik_56
```

## 蟒蛇 3

```
# Python program to illustrate time
# complexity for single for-loop
a = 0
b = 0
N = 4
M = 4

# This loop runs for N time
for i in range(N):
    a = a + 10

# This loop runs for M time
for i in range(M):
    b = b + 40

print(a,b)

# This code is contributed by Shubham Singh
```

## C#

```
// C# program to illustrate time
// complexity for single for-loop
using System;
class GFG
{

  // Driver Code
  public static void Main(string[] args)
  {
    int a = 0, b = 0;
    int N = 4, M = 4;

    // This loop runs for N time
    for (int i = 0; i < N; i++)
    {
      a = a + 10;
    }

    // This loop runs for M time
    for (int i = 0; i < M; i++)
    {
      b = b + 40;
    }
    Console.Write(a + " " + b);
  }
}

// This code is contributed by pratham76.
```

## java 描述语言

```
<script>
// Javascript program to illustrate time
// complexity for single for-loop

// Driver Code
let a = 0;
let b = 0;
let N = 4;
let M = 4;

// This loop runs for N time
for (let  i = 0; i < N; i++) {
    a = a + 10;
}

// This loop runs for M time
for (let i = 0; i < M; i++) {
    b = b + 40;
}

document.write(a +' ' + b);

// This code is contributed by Shubham Singh
</script>
```

**Output:** 

```
40 160
```

**说明:**这里的时间复杂度会是 ***O(N + M)*** 。循环一是运行 **N 次**的单个 [for-loop](https://www.geeksforgeeks.org/loops-in-c-and-cpp/) ，其内部计算需要 ***O(1)次*** 。同样，另一个循环通过将两个不同的循环相加得到的结果相加得到的结果为 **M 次**是***O(N+M+1)= O(N+M)***。

**<u>例 2</u> :**

在熟悉了基本运算和单循环之后。现在，为了找到嵌套循环的时间复杂度，假设两个循环具有不同的迭代次数。可以看到，如果**外**环跑一次，内就会跑 **M 次**，给我们一个系列为 **M + M + M + M + M……N 次**，这个可以写成 **N * M** 。下图也是同样的情况:

## C++

```
// C++ program to illustrate time
// complexity for nested loop
#include <bits/stdc++.h>
using namespace std;

// Driver Code
int main()
{
    int a = 0, b = 0;
    int N = 4, M = 5;

    // Nested loops
    for (int i = 0; i < N; i++) {
        for (int j = 0; j < M; j++) {
            a = a + j;

            // Print the current
            // value of a
            cout << a << ' ';
        }
        cout << endl;
    }
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to illustrate time
// complexity for nested loop
import java.io.*;

class GFG{

// Driver Code
public static void main (String[] args)
{
    int a = 0;
    int b = 0;
    int N = 4;
    int M = 5;

    // Nested loops
    for(int i = 0; i < N; i++)
    {
        for(int j = 0; j < M; j++)
        {
            a = a + j;

            // Print the current
            // value of a
            System.out.print(a + " ");
        }
        System.out.println();
    }
}
}

// This code is contributed by Shubham Singh
```

## 蟒蛇 3

```
# Python program to illustrate time
# complexity for nested loop

# Driver Code
a = 0
b = 0
N = 4
M = 5

# Nested loops
for i in range(N):
    for j in range(M):
        a = a + j

        # Prthe current
        # value of a
        print(a, end = " ")

    print()

# This code is contributed by Shubham Singh
```

**Output:** 

```
0 1 3 6 10 
10 11 13 16 20 
20 21 23 26 30 
30 31 33 36 40
```

**<u>例 3</u> :**

得到以上问题后。让我们有两个迭代器，其中外一个运行 **N/2 次，**我们知道一个循环的时间复杂度被认为是 ***O(log N)*** ，如果迭代器被除以/乘以一个常量 **K** ，那么时间复杂度被认为是***O(log<sub>K</sub>N)***。下面是同样的说明:

## C++

```
// C++ program to illustrate time
// complexity of the form O(log2 N)
#include <bits/stdc++.h>
using namespace std;

// Driver Code
int main()
{
    int N = 8, k = 0;

    // First loop run N/2 times
    for (int i = N / 2; i <= N; i++) {

        // Inner loop run log N
        // times for all i
        for (int j = 2; j <= N;
             j = j * 2) {

            // Print the value k
            cout << k << ' ';

            k = k + N / 2;
        }
    }

    return 0;
}
```

**Output:** 

```
0 4 8 12 16 20 24 28 32 36 40 44 48 52 56
```

**<u>例 4</u> :**

现在，让我们理解 while 循环，并尝试将迭代器更新为表达式。下图也是同样的情况:

## C++

```
// C++ program to illustrate time
// complexity while updating the
// iteration
#include <bits/stdc++.h>
using namespace std;

// Driver Code
int main()
{
    int N = 18;
    int i = N, a = 0;

    // Iterate until i is greater
    // than 0
    while (i > 0) {

        // Print the value of a
        cout << a << ' ';
        a = a + i;

        // Update i
        i = i / 2;
    }

    return 0;
}
```

**Output:** 

```
0 18 27 31 33
```

**说明:**上述代码的等式可以给出如下:

> => (N/2) <sup>K</sup> = 1(针对 K 次迭代)
> = > N = 2 <sup>k</sup> (两边取原木)
> = > k =原木(N)基 2。
> 因此，时间复杂度将为
> T(N) = O(log N)

**<u>例 5</u> :** 求时间复杂度的另一种方法是把它们转换成表达式，用下面的公式得到需要的结果。给出一个基于该算法的表达式，任务是求解并找出时间复杂度。这种方法更简单，因为它使用基本的数学计算来扩展给定的公式，以获得特定的解决方案。下面是两个理解方法的例子。

**步骤:**

*   寻找**(N–1)**迭代/步骤的解。
*   同样，为下一步进行计算。
*   一旦你熟悉了模式，就找到了 **K <sup>第</sup>T3】步的解决方案。**
*   求 **N** 次的解，求所得表达式的解。

下图也是同样的情况:

> 设表达式为:
> T(N)= 3 * T(N–1)。
> 
> T(N)= 3 *(3T(N-2))
> T(N)= 3 * 3 *(3T(N–3))
> 
> **为 k 次:**
> t(n)=(3^k–1)*(3t(n–k))
> 
> **为 n 次:**
> t(n)= 3^n–1(3t(n–n))
> t(n)= 3^n–1 * 3(t(0))
> t(n)= 3^n * 1
> t(n)= 3^n

第三种也是最简单的方法是使用[大师定理](https://www.geeksforgeeks.org/analysis-algorithm-set-4-master-method-solving-recurrences/)或者计算时间复杂度。使用**大师定理**寻找时间复杂度，请参考[这篇文章](https://www.geeksforgeeks.org/analysis-algorithm-set-4-master-method-solving-recurrences/)。
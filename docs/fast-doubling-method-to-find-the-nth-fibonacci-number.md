# 快速加倍法求第 n 个斐波那契数

> 原文:[https://www . geesforgeks . org/fast-double-method-to-find-n-Fibonacci-number/](https://www.geeksforgeeks.org/fast-doubling-method-to-find-the-nth-fibonacci-number/)

给定一个整数 **N** ，任务是找到第 N 个[斐波那契数](https://www.geeksforgeeks.org/program-for-nth-fibonacci-number/)。
**例:**

> **输入:** N = 3
> **输出:** 2
> **解释:**
> F(1) = 1，F(2)= 1
> F(3)= F(1)+F(2)= 2
> **输入:** N = 6
> **输出:** 8

**进场:**

*   [矩阵求幂](http://www.geeksforgeeks.org/matrix-exponentiation/)方法前面已经讨论过了。倍增法虽然本身不使用矩阵乘法，但可以看作是对矩阵求幂法求第 N 个斐波那契数的一种改进。

*   斐波那契递归序列由
    给出

```
F(n+1) = F(n) + F(n-1)
```

*   The Matrix Exponentiation method uses the following formula

    ![\[ \begin{bmatrix} 1 & 1 \\ 1 & 0 \end{bmatrix}^n = \begin{bmatrix} F_{n+1} & F_n \\ F_n & F_{n-1} \end{bmatrix} \]          ](img/e45a36426d5f4bfadde84a9cd087f011.png "Rendered by QuickLaTeX.com")

*   该方法涉及代价高昂的矩阵乘法，而且重复计算两次。
    另一方面，快速倍增法基于两个基本公式:

```
F(2n) = F(n)[2F(n+1) – F(n)]
F(2n + 1) = F(n)<sup>2 + F(n+1)2</sup>
```

*   以下是对上述结果的简短解释:

> **以:**
> F(n+1)= F(n)+F(n-1)&
> F(n)= F(n)
> 开头，可以用矩阵形式改写为:
> 
> ![\[ \begin{bmatrix} F(n+1) \\ F(n) \end{bmatrix} = \begin{bmatrix} 1 & 1 \\ 1 & 0 \end{bmatrix} \begin{bmatrix} F(n) \\ F(n-1) \end{bmatrix} \] \[\quad\enspace= \begin{bmatrix} 1 & 1 \\ 1 & 0 \end{bmatrix}^2 \begin{bmatrix} F(n-1) \\ F(n-2) \end{bmatrix} \] \quad\quad\quad\quad\quad\quad\quad\quad\quad\quad\quad\enspace\enspace\thinspace......\\ \[= \begin{bmatrix} 1 & 1 \\ 1 & 0 \end{bmatrix}^n \begin{bmatrix} F(1) \\ F(0) \end{bmatrix} \]          ](img/923a14ad9b60c96f587eac21b27efe0a.png "Rendered by QuickLaTeX.com")
> 
> 为了加倍，我们只需在公式中插入“2n”:
> 
> ![\[ \begin{bmatrix} F(2n+1) \\ F(2n) \end{bmatrix} = \begin{bmatrix} 1 & 1 \\ 1 & 0 \end{bmatrix}^{2n} \begin{bmatrix} F(1) \\ F(0) \end{bmatrix} \] \[\quad\enspace= \begin{bmatrix} 1 & 1 \\ 1 & 0 \end{bmatrix}^n \begin{bmatrix} 1 & 1 \\ 1 & 0 \end{bmatrix}^n \begin{bmatrix} F(1) \\ F(0) \end{bmatrix} \] \[\quad\enspace= \begin{bmatrix} F(n+1) & F(n) \\ F(n) & F(n-1) \end{bmatrix} \begin{bmatrix} F(n+1) & F(n) \\ F(n) & F(n-1) \end{bmatrix} \begin{bmatrix} F(1) \\ F(0) \end{bmatrix} \] \[\quad\enspace= \begin{bmatrix} F(n+1)^2 + F(n)^2 \\ F(n)F(n+1) + F(n)F(n-1) \end{bmatrix} \]          ](img/5ed983908e7294abdde7ff4ae19b9f58.png "Rendered by QuickLaTeX.com")
> 
> 代入 F(n-1) = F(n+1)- F(n)，经过简化，我们得到:
> 
> ![\[ \begin{bmatrix} F(2n+1) \\ F(2n) \end{bmatrix} = \begin{bmatrix} F(n+1)^2 + F(n)^2 \\ 2F(n+1)F(n) - F(n)^2 \end{bmatrix} \]          ](img/e022a7014ee71aded58c791b86e5deb2.png "Rendered by QuickLaTeX.com")

以下是上述方法的实现:

## C++

```
// C++ program to find the Nth Fibonacci
// number using Fast Doubling Method
#include <bits/stdc++.h>
using namespace std;

int a, b, c, d;
#define MOD 1000000007

// Function calculate the N-th fibanacci
// number using fast doubling method
void FastDoubling(int n, int res[])
{
    // Base Condition
    if (n == 0) {
        res[0] = 0;
        res[1] = 1;
        return;
    }
    FastDoubling((n / 2), res);

    // Here a = F(n)
    a = res[0];

    // Here b = F(n+1)
    b = res[1];

    c = 2 * b - a;

    if (c < 0)
        c += MOD;

    // As F(2n) = F(n)[2F(n+1) – F(n)]
    // Here c  = F(2n)
    c = (a * c) % MOD;

    // As F(2n + 1) = F(n)^2 + F(n+1)^2
    // Here d = F(2n + 1)
    d = (a * a + b * b) % MOD;

    // Check if N is odd
    // or even
    if (n % 2 == 0) {
        res[0] = c;
        res[1] = d;
    }
    else {
        res[0] = d;
        res[1] = c + d;
    }
}

// Driver code
int main()
{
    int N = 6;
    int res[2] = { 0 };

    FastDoubling(N, res);

    cout << res[0] << "\n";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the Nth Fibonacci
// number using Fast Doubling Method
class GFG{

// Function calculate the N-th fibanacci
// number using fast doubling method
static void FastDoubling(int n, int []res)
{
    int a, b, c, d;
    int MOD = 1000000007;

    // Base Condition
    if (n == 0)
    {
        res[0] = 0;
        res[1] = 1;
        return;
    }
    FastDoubling((n / 2), res);

    // Here a = F(n)
    a = res[0];

    // Here b = F(n+1)
    b = res[1];

    c = 2 * b - a;

    if (c < 0)
        c += MOD;

    // As F(2n) = F(n)[2F(n+1) – F(n)]
    // Here c = F(2n)
    c = (a * c) % MOD;

    // As F(2n + 1) = F(n)^2 + F(n+1)^2
    // Here d = F(2n + 1)
    d = (a * a + b * b) % MOD;

    // Check if N is odd
    // or even
    if (n % 2 == 0)
    {
        res[0] = c;
        res[1] = d;
    }
    else
    {
        res[0] = d;
        res[1] = c + d;
    }
}

// Driver code
public static void main(String []args)
{
    int N = 6;
    int res[] = new int[2];

    FastDoubling(N, res);

    System.out.print(res[0]);
}
}

// This code is contributed by rock_cool
```

## 蟒蛇 3

```
# Python3 program to find the Nth Fibonacci
# number using Fast Doubling Method
MOD = 1000000007

# Function calculate the N-th fibanacci
# number using fast doubling method
def FastDoubling(n, res):

    # Base Condition
    if (n == 0):
        res[0] = 0
        res[1] = 1
        return

    FastDoubling((n // 2), res)

    # Here a = F(n)
    a = res[0]

    # Here b = F(n+1)
    b = res[1]

    c = 2 * b - a

    if (c < 0):
        c += MOD

    # As F(2n) = F(n)[2F(n+1) – F(n)]
    # Here c = F(2n)
    c = (a * c) % MOD

    # As F(2n + 1) = F(n)^2 + F(n+1)^2
    # Here d = F(2n + 1)
    d = (a * a + b * b) % MOD

    # Check if N is odd
    # or even
    if (n % 2 == 0):
        res[0] = c
        res[1] = d
    else :
        res[0] = d
        res[1] = c + d

# Driver code
N = 6
res = [0] * 2

FastDoubling(N, res)

print(res[0])

# This code is contributed by divyamohan123
```

## C#

```
// C# program to find the Nth Fibonacci
// number using Fast Doubling Method
using System;
class GFG{

// Function calculate the N-th fibanacci
// number using fast doubling method
static void FastDoubling(int n, int []res)
{
    int a, b, c, d;
    int MOD = 1000000007;

    // Base Condition
    if (n == 0)
    {
        res[0] = 0;
        res[1] = 1;
        return;
    }
    FastDoubling((n / 2), res);

    // Here a = F(n)
    a = res[0];

    // Here b = F(n+1)
    b = res[1];

    c = 2 * b - a;

    if (c < 0)
        c += MOD;

    // As F(2n) = F(n)[2F(n+1) – F(n)]
    // Here c = F(2n)
    c = (a * c) % MOD;

    // As F(2n + 1) = F(n)^2 + F(n+1)^2
    // Here d = F(2n + 1)
    d = (a * a + b * b) % MOD;

    // Check if N is odd
    // or even
    if (n % 2 == 0)
    {
        res[0] = c;
        res[1] = d;
    }
    else
    {
        res[0] = d;
        res[1] = c + d;
    }
}

// Driver code
public static void Main()
{
    int N = 6;
    int []res = new int[2];

    FastDoubling(N, res);

    Console.Write(res[0]);
}
}

// This code is contributed by Code_Mech
```

## java 描述语言

```
<script>

    // Javascript program to find the Nth Fibonacci
      // number using Fast Doubling Method

    let a, b, c, d;
    let MOD = 1000000007;

    // Function calculate the N-th fibanacci
    // number using fast doubling method
    function FastDoubling(n, res)
    {
        // Base Condition
        if (n == 0) {
            res[0] = 0;
            res[1] = 1;
            return;
        }
        FastDoubling(parseInt(n / 2, 10), res);

        // Here a = F(n)
        a = res[0];

        // Here b = F(n+1)
        b = res[1];

        c = 2 * b - a;

        if (c < 0)
            c += MOD;

        // As F(2n) = F(n)[2F(n+1) – F(n)]
        // Here c  = F(2n)
        c = (a * c) % MOD;

        // As F(2n + 1) = F(n)^2 + F(n+1)^2
        // Here d = F(2n + 1)
        d = (a * a + b * b) % MOD;

        // Check if N is odd
        // or even
        if (n % 2 == 0) {
            res[0] = c;
            res[1] = d;
        }
        else {
            res[0] = d;
            res[1] = c + d;
        }
    }

    let N = 6;
    let res = new Array(2);
    res.fill(0);

    FastDoubling(N, res);

    document.write(res[0]);

</script>
```

**Output**

```
8
```

**时间复杂度:**重复平方将时间从线性减少到对数。因此，在时间算法不变的情况下，时间复杂度为 **O(对数 n)** 。
**辅助空间:** O(n)。

**迭代版本**

我们可以实现上述方法的迭代版本，通过用两个元素初始化数组**F**=【F(0)，F(1)】=【0，1】并迭代构造 F(n)，在每一步我们将把 **f** 变换为**【F(2i)，F(2i+1)】**或**【F(2i+1)，F(2i+2)】**，其中 **i** 对应于 **i** 的当前值

**进场:**

*   用两个元素 **f** = [0，1]创建数组，表示[F(0)，F(1)]。
*   为了找到 F(n)，从左到右迭代 **n** 的二进制表示，让从左到右的 k <sup>第</sup>位为 b <sub>k</sub> 。
*   对 **n** 中的所有位重复应用以下步骤。
*   使用 b <sub>k</sub> 我们将决定是将**F =【F(I)，F(I+1)】**转换为**【F(2i)，F(2i+1)】**还是**【F(2i+1)，F(2i+2)】**。

```
if b<sub>k == 0:</sub>
 f = [F(2i), F(2i+1)] = [F(i){2F(i+1)-F(i)}, F(i+1)<sup>2+F(i)2]</sup>
if b<sub>k == 1:</sub>
 f = [F(2i+1), F(2i+2)] = [F(i+1)<sup>2+F(i)2, F(i+1){2F(i)+F(i+1)}]</sup>

where,
F(i) and F(i+1) are current values stored in f.
```

*   返回**f【0】**。

```
Example:
for n = 13 = (1101)<sub>2</sub>
b =          1               1               0               1
[F(0), F(1)] -> [F(1), F(2)] -> [F(3), F(4)] -> [F(6), F(7)] -> [F(13), F(14)]
[0, 1]       -> [1, 1]       -> [2, 3]       -> [8, 13]      -> [233, 377]
```

下面是上述方法的实现:

## C++

```
// C++ program to find the Nth Fibonacci
// number using Fast Doubling Method iteratively

#include <bitset>
#include <iostream>
#include <string>

using namespace std;

// helper function to get binary string
string decimal_to_bin(int n)
{
    // use bitset to get binary string
    string bin = bitset<sizeof(int) * 8>(n).to_string();
    auto loc = bin.find('1');
    // remove leading zeros
    if (loc != string::npos)
        return bin.substr(loc);
    return "0";
}

// computes fib(n) iteratively using fast doubling method
long long fastfib(int n)
{
    string bin_of_n
        = decimal_to_bin(n); // binary string of n

    long long f[] = { 0, 1 }; // [F(i), F(i+1)] => i=0

    for (auto b : bin_of_n) {
        long long f2i1
            = f[1] * f[1] + f[0] * f[0]; // F(2i+1)
        long long f2i = f[0] * (2 * f[1] - f[0]); // F(2i)

        if (b == '0') {
            f[0] = f2i; // F(2i)
            f[1] = f2i1; // F(2i+1)
        }
        else {
            f[0] = f2i1; // F(2i+1)
            f[1] = f2i1 + f2i; // F(2i+2)
        }
    }

    return f[0];
}

int main()
{
    int n = 13;
    long long fib = fastfib(n);
    cout << "F(" << n << ") = " << fib << "\n";
}
```

## 蟒蛇 3

```
# Python3 program to find the Nth Fibonacci
# number using Fast Doubling Method iteratively

def fastfib(n):
    """computes fib(n) iteratively using fast doubling method"""
    bin_of_n = bin(n)[2:]  # binary string of n
    f = [0, 1]  # [F(i), F(i+1)] => i=0

    for b in bin_of_n:
        f2i1 = f[1]**2 + f[0]**2  # F(2i+1)
        f2i = f[0]*(2*f[1]-f[0])  # F(2i)

        if b == '0':
            f[0], f[1] = f2i, f2i1  # [F(2i), F(2i+1)]
        else:
            f[0], f[1] = f2i1, f2i1+f2i  # [F(2i+1), F(2i+2)]

    return f[0]

n = 13
fib = fastfib(n)
print(f'F({n}) =', fib)
```

**Output**

```
F(13) = 233
```

**时间复杂度**:我们在迭代长度为 log(n)的 n 的二进制串，做常数时间算术运算，所以时间复杂度为 **O(log n)** 。

**辅助空间**:我们在 f 中存储两个元素，n 的二进制字符串长度为 log(n)，所以空间复杂度为 **O(log n)** 。
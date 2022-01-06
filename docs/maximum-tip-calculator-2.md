# 最大小费计算器

> 原文:[https://www.geeksforgeeks.org/maximum-tip-calculator-2/](https://www.geeksforgeeks.org/maximum-tip-calculator-2/)

**Rahul** 和 **Ankit** 是皇家餐厅仅有的两位服务员。今天餐厅收到 **N** 订单。当由不同的服务员处理时，小费的金额可能会有所不同，如果拉胡尔拿着**和**的订单，他会得到**艾**卢比的小费，如果安基特拿着这个订单，小费会是**比**卢比。
为了最大化总小费价值，他们决定在自己之间分配订单。一个订单只能由一个人处理。此外，由于时间限制，拉胡尔不能接受超过 **X** 的订单，安基特不能接受超过 **Y** 的订单。保证 **X + Y** 大于等于 **N** ，意味着所有订单都可以由 Rahul 或者 Ankit 处理。处理完所有订单后，找出**最大可能的小费总额**。

**示例:**

> **输入:** A[] = {1，2，3，4，5}，B[] = {5，4，3，2，1}，X = 3，Y = 3
> **输出:** 21
> 第 1、2、3 单由服务员 Y 取，
> 第 4、5 单由服务员 X 取
> 
> **输入:** A[] = {2，2，2}，B[] = {3，3，3}，X = 3，Y = 3
> T3】输出: 9

**递归解:**我们可以用递归的方式来计算最大订单金额，这样
的总小费将是最大的。该解决方案将包含 4 种情况:

1.  **i == n:** 当达到这个值时，意味着所有订单都被接受。所以返回 0 并后退。
2.  **X ≤ 0:** 当服务员 **X** 不能再接单时。
3.  **Y ≤ 0:** 当服务员 **Y** 不能再接单时。
4.  **max(Orders(X)，Orders(Y)):** 我们需要返回 **X** 和 **Y** 同时下单时的最大小费。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach

#include <bits/stdc++.h>
using namespace std;
int n;

// Recursive function to calculate sum of
// maximum tip order taken by X and Y
int solve(int i, int X, int Y,
          int a[], int b[], int n)
{

    // When all orders have been taken
    if (i == n)
        return 0;

    // When X cannot take more orders
    if (X <= 0)
        return b[i] + solve(i + 1, X,
                            Y - 1, a, b, n);

    // When Y cannot take more orders
    if (Y <= 0)
        return a[i] + solve(i + 1, X - 1,
                            Y, a, b, n);

    // When both can take order
    // calculate maximum out of two
    else
        return max(a[i] + solve(i + 1, X - 1,
                                Y, a, b, n),
                   b[i] + solve(i + 1, X,
                                Y - 1, a, b, n));
}

// Driver code
int main()
{
    int a[] = { 1, 2, 3, 4, 5 };
    int b[] = { 5, 4, 3, 2, 1 };
    int n = sizeof(a) / sizeof(a[0]);
    int x = 3, y = 3;

    cout << solve(0, x, y, a, b, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation for the above approach
import java.io.*;

class GFG
{
    static int n;

    // Recursive function to calculate sum of
    // maximum tip order taken by X and Y
    static int solve(int i, int X, int Y, int a[], int b[],
                     int n)
    {

        // When all orders have been taken
        if (i == n)
            return 0;

        // When X cannot take more orders
        if (X <= 0)
            return b[i] + solve(i + 1, X, Y - 1, a, b, n);

        // When Y cannot take more orders
        if (Y <= 0)
            return a[i] + solve(i + 1, X - 1, Y, a, b, n);

        // When both can take order
        // calculate maximum out of two
        else
            return Math.max(
                a[i] + solve(i + 1, X - 1, Y, a, b, n),
                b[i] + solve(i + 1, X, Y - 1, a, b, n));
    }

    // Driver code
    public static void main(String[] args)
    {
        int a[] = { 1, 2, 3, 4, 5 };
        int b[] = { 5, 4, 3, 2, 1 };
        int n = a.length;
        int x = 3, y = 3;

        System.out.println(solve(0, x, y, a, b, n));
    }
}

// This code is contributed by Potta Lokesh
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Recursive function to calculate sum of
# maximum tip order taken by X and Y
def solve(i, X, Y,
          a, b, n) :

    # When all orders have been taken
    if (i == n):
        return 0

    # When X cannot take more orders
    if (X <= 0):
        return (b[i] + solve(i + 1, X,
                            Y - 1, a, b, n))

    # When Y cannot take more orders
    if (Y <= 0):
        return (a[i] + solve(i + 1, X - 1,
                            Y, a, b, n))

    # When both can take order
    # calculate maximum out of two
    else:
        return max(a[i] + solve(i + 1, X - 1,
                                Y, a, b, n),
                   b[i] + solve(i + 1, X,
                                Y - 1, a, b, n))

# Driver code
a = [ 1, 2, 3, 4, 5 ]
b = [ 5, 4, 3, 2, 1 ]

n = len(a)

x = 3
y = 3

print(solve(0, x, y, a, b, n))

# This code is contributed by splevel62.
```

## C#

```
// C# program for the above approach
using System;

class GFG{

static int n;

// Recursive function to calculate sum of
// maximum tip order taken by X and Y
static int solve(int i, int X, int Y,
                 int[] a, int[] b, int n)
{

    // When all orders have been taken
    if (i == n)
        return 0;

    // When X cannot take more orders
    if (X <= 0)
        return b[i] + solve(i + 1, X, Y - 1,
                            a, b, n);

    // When Y cannot take more orders
    if (Y <= 0)
        return a[i] + solve(i + 1, X - 1, Y,
                            a, b, n);

    // When both can take order
    // calculate maximum out of two
    else
        return Math.Max(
            a[i] + solve(i + 1, X - 1, Y, a, b, n),
            b[i] + solve(i + 1, X, Y - 1, a, b, n));
}

// Driver Code
public static void Main(String[] args)
{
    int[] a = { 1, 2, 3, 4, 5 };
    int[] b = { 5, 4, 3, 2, 1 };
    // int n = a.Length;
    int x = 3, y = 3;

    Console.Write(solve(0, x, y, a, b, n));
}
}

// This code is contributed by sanjoy_62
```

## java 描述语言

```
<script>

// JavaScript implementation of the approach

let n;

// Recursive function to calculate sum of
// maximum tip order taken by X and Y
function solve(i, X, Y, a, b, n) {
  // When all orders have been taken
  if (i == n) return 0;

  // When X cannot take more orders
  if (X <= 0) return b[i] + solve(i + 1, X, Y - 1, a, b, n);

  // When Y cannot take more orders
  if (Y <= 0) return a[i] + solve(i + 1, X - 1, Y, a, b, n);
  // When both can take order
  // calculate maximum out of two
  else
    return Math.max(
      a[i] + solve(i + 1, X - 1, Y, a, b, n),
      b[i] + solve(i + 1, X, Y - 1, a, b, n)
    );
}

// Driver code

let a = [1, 2, 3, 4, 5];
let b = [5, 4, 3, 2, 1];
n = a.length;
let x = 3,
  y = 3;

document.write(solve(0, x, y, a, b, n));

</script>
```

**Output:** 

```
21
```

**时间复杂度:** O(2 <sup>n</sup>

**基于 DP 的方法:**先前方法的[最优子结构](https://www.geeksforgeeks.org/optimal-substructure-property-in-dynamic-programming-dp-2/)包含重复，这可以通过将先前计算的尖端存储在阵列中来避免。这将把时间复杂度降低到 0(n)。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Global Variables
int N, X, Y;

vector<int> A_right_sum, B_right_sum;
vector<unordered_map<int,
                     unordered_map<int, int> > >
    mem;
vector<unordered_map<int,
                     unordered_map<int, bool> > >
    vis;

// Function to check if visited before
bool get_vis_val(int i, int x, int y)
{
    if (i == N)
        return true;
    return vis[i][x][y];
}

// Function to return the tip value
int get_mem_val(int i, int x, int y)
{
    if (i == N)
        return 0;
    return mem[i][x][y];
}

// Function to calculate the maximum tip possible
void find_ans(int i, int x, int y,
              vector<int> A, vector<int> B)
{

    // If already visited
    if (get_vis_val(i, x, y))
        return;

    vis[i][x][y] = true;

    // If X cannot take more orders
    if (x == 0) {
        mem[i][x][y] = B_right_sum[i];
    }

    // If Y cannot take more orders
    else if (y == 0) {
        mem[i][x][y] = A_right_sum[i];
    }

    // If both can take orders then
    // calculate the maximum of two
    else {
        find_ans(i + 1, x - 1, y, A, B);
        find_ans(i + 1, x, y - 1, A, B);
        mem[i][x][y]
            = max(get_mem_val(i + 1, x - 1, y)
                      + A[i],
                  get_mem_val(i + 1, x, y - 1)
                      + B[i]);
    }
}

// Driver code
int main()
{

    int a[] = { 1, 2, 3, 4, 5 };
    int b[] = { 5, 4, 3, 2, 1 };
    N = sizeof(a) / sizeof(a[0]);
    X = 3;
    Y = 3;

    // Vector containing the tips of waiter X
    vector<int> A(a, a + N);

    // Vector containing the tips of waiter Y
    vector<int> B(b, b + N);

    // Memory allocation and clearing
    // of previous caches
    mem.clear();
    mem.resize(N + 1);
    vis.clear();
    vis.resize(N + 1);

    A_right_sum.resize(N);
    B_right_sum.resize(N);

    A_right_sum[N - 1] = A[N - 1];
    B_right_sum[N - 1] = B[N - 1];

    // Precalculation of sums
    // of tip at each ith order
    for (int i = N - 2; i >= 0; i--) {
        A_right_sum[i]
            = A_right_sum[i + 1] + A[i];
        B_right_sum[i]
            = B_right_sum[i + 1] + B[i];
    }

    // Bottom up dp based solution
    find_ans(0, X, Y, A, B);

    // Final ans stored in mem[0][X][Y]
    cout << get_mem_val(0, X, Y) << endl;

    return 0;
}
```

**Output:** 

```
21
```

**时间复杂度:**O(N)
T3】空间复杂度: O(N <sup>2</sup> )
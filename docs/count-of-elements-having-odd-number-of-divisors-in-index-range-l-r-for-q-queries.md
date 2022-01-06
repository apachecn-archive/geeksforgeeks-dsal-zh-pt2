# Q 查询的索引范围[L，R]中具有奇数除数的元素计数

> 原文:[https://www . geeksforgeeks . org/index-range-l-r-for-q-query/](https://www.geeksforgeeks.org/count-of-elements-having-odd-number-of-divisors-in-index-range-l-r-for-q-queries/)具有奇数除数的元素计数

给定一个正整数的[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】**和查询数量 **Q** ，每个查询包含两个数字 **L** 和 **R** 。任务是从索引 **L 到 R** 计算数组中具有奇数除数的元素数量。

**示例:**

> **输入:** arr[] = [2，4，5，6，9]，Q = 3，Query[][] = { {0，2}，{1，3}，{1，4} }
> **输出:**1 1 2
> T6】解释:
> 第一次查询:在 2 4 5 中只有 4 有奇数个除数。
> 第二次查询:在 4 5 6 中，只有 4 有奇数个除数。
> 第三次查询:在 4 5 6 9 中，只有 4，9 有奇数个除数。
> 
> **输入:** arr[] = [1，16，5，4，9]，Q = 2，Query[][] = { {1，3}，{0，2} }
> **输出:** 2 1

**天真方法:**天真方法是对每个查询迭代从 **L 到 R** 的数组，并计算具有奇数除数的范围**【L，R】**中的元素。如果是，则计算该查询的元素。

***时间复杂度:**O(Q * N * sqrt(N))*
***辅助空间:** O(1)*

**有效途径:**我们可以观察到除数只有在完美平方的情况下才是奇数。因此，最好的解决方案是检查给定的[数字是否是在**【L，R】**范围内的完美平方](https://www.geeksforgeeks.org/check-if-given-number-is-perfect-square-in-cpp/)。以下是步骤:

1.  用值 **0** 初始化大小为 **N** 的数组 **dp[]** 。
2.  遍历给定的数组 **arr[]** ，如果数组中的任何元素是一个完美的正方形，则更新 **dp[]** 中该索引处的值为 **1** 。
3.  为了有效地计算每个查询的答案，我们将预先计算答案。
4.  我们将对数组 **dp[]** 进行[前缀求和](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/)，对于范围【L，R】内的每个查询，答案将由下式给出:

```
OddDivisorCount(L, R) = DP[R] - DP[L-1]
```

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function count the number of elements
// having odd number of divisors
void OddDivisorsCount(
    int n, int q, int a[],
    vector<pair<int, int> > Query)
{
    // Initialise dp[] array
    int DP[n] = { 0 };

    // Precomputation
    for (int i = 0; i < n; i++) {
        int x = sqrt(a[i]);

        if (x * x == a[i])
            DP[i] = 1;
    }

    // Find the Prefix Sum
    for (int i = 1; i < n; i++) {
        DP[i] = DP[i - 1] + DP[i];
    }

    int l, r;

    // Iterate for each query
    for (int i = 0; i < q; i++) {
        l = Query[i].first;
        r = Query[i].second;

        // Find the answer for each query
        if (l == 0) {
            cout << DP[r] << endl;
        }
        else {
            cout << DP[r] - DP[l - 1]
                 << endl;
        }
    }
}

// Driver Code
int main()
{
    int N = 5;
    int Q = 3;

    // Given array arr[]
    int arr[] = { 2, 4, 5, 6, 9 };

    // Given Query
    vector<pair<int, int> > Query
        Query
        = { { 0, 2 }, { 1, 3 }, { 1, 4 } };

    // Function Call
    OddDivisorsCount(N, Q, arr, Query);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

static class pair
{
    int first, second;
    public pair(int first, int second)
    {
        this.first = first;
        this.second = second;
    }
}

// Function count the number of elements
// having odd number of divisors
static void OddDivisorsCount(int n, int q,
                             int a[],
                             pair []Query)
{

    // Initialise dp[] array
    int DP[] = new int[n];

    // Precomputation
    for(int i = 0; i < n; i++)
    {
       int x = (int)Math.sqrt(a[i]);

       if (x * x == a[i])
           DP[i] = 1;
    }

    // Find the Prefix Sum
    for(int i = 1; i < n; i++)
    {
       DP[i] = DP[i - 1] + DP[i];
    }

    int l, r;

    // Iterate for each query
    for(int i = 0; i < q; i++)
    {
       l = Query[i].first;
       r = Query[i].second;

       // Find the answer for each query
       if (l == 0)
       {
           System.out.print(DP[r] + "\n");
       }
       else
       {
           System.out.print(DP[r] -
                            DP[l - 1] + "\n");
       }
    }
}

// Driver Code
public static void main(String[] args)
{
    int N = 5;
    int Q = 3;

    // Given array arr[]
    int arr[] = { 2, 4, 5, 6, 9 };

    // Given Query
    pair []Query = { new pair(0, 2),
                     new pair(1, 3),
                     new pair(1, 4) };

    // Function Call
    OddDivisorsCount(N, Q, arr, Query);
}
}

// This code is contributed by amal kumar choubey
```

## 蟒蛇 3

```
# Python3 program for the above approach
import math

# Function count the number of elements
# having odd number of divisors
def OddDivisorsCount(n, q, a, Query):

    # Initialise dp[] array
    DP = [0 for i in range(n)]

    # Precomputation
    for i in range(n):
        x = int(math.sqrt(a[i]));

        if (x * x == a[i]):
            DP[i] = 1;

    # Find the Prefix Sum
    for i in range(1, n):
        DP[i] = DP[i - 1] + DP[i];

    l = 0
    r = 0

    # Iterate for each query
    for i in range(q):
        l = Query[i][0];
        r = Query[i][1];

        # Find the answer for each query
        if (l == 0):
            print(DP[r])
        else:
            print(DP[r] - DP[l - 1])

# Driver code
if __name__=="__main__":

    N = 5;
    Q = 3;

    # Given array arr[]
    arr = [ 2, 4, 5, 6, 9 ]

    # Given Query
    Query = [ [ 0, 2 ],
              [ 1, 3 ],
              [ 1, 4 ] ]

    # Function call
    OddDivisorsCount(N, Q, arr, Query);

# This code is contributed by rutvik_56
```

## C#

```
// C# program for the above approach
using System;

class GFG{
class pair
{
    public int first, second;
    public pair(int first, int second)
    {
        this.first = first;
        this.second = second;
    }
}

// Function count the number of elements
// having odd number of divisors
static void OddDivisorsCount(int n, int q,
                             int []a,
                             pair []Query)
{

    // Initialise []dp array
    int []DP = new int[n];

    // Precomputation
    for(int i = 0; i < n; i++)
    {
       int x = (int)Math.Sqrt(a[i]);
       if (x * x == a[i])
           DP[i] = 1;
    }

    // Find the Prefix Sum
    for(int i = 1; i < n; i++)
    {
       DP[i] = DP[i - 1] + DP[i];
    }

    int l, r;

    // Iterate for each query
    for(int i = 0; i < q; i++)
    {
       l = Query[i].first;
       r = Query[i].second;

       // Find the answer for each query
       if (l == 0)
       {
           Console.Write(DP[r] + "\n");
       }
       else
       {
           Console.Write(DP[r] -
                         DP[l - 1] + "\n");
       }
    }
}

// Driver Code
public static void Main(String[] args)
{
    int N = 5;
    int Q = 3;

    // Given array []arr
    int []arr = { 2, 4, 5, 6, 9 };

    // Given Query
    pair []Query = { new pair(0, 2),
                     new pair(1, 3),
                     new pair(1, 4) };

    // Function Call
    OddDivisorsCount(N, Q, arr, Query);
}
}

// This code is contributed by gauravrajput1
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function count the number of elements
// having odd number of divisors
function OddDivisorsCount(
    n, q, a,Query)
{

    // Initialise dp[] array
    var DP = new Array(n).fill(0);

    // Precomputation
    for (var i = 0; i < n; i++) {
        var x = Math.sqrt(a[i]);

        if (x * x == a[i])
            DP[i] = 1;
    }

    // Find the Prefix Sum
    for (var i = 1; i < n; i++) {
        DP[i] = DP[i - 1] + DP[i];
    }

    var l, r;

    // Iterate for each query
    for (var i = 0; i < q; i++) {
        l = Query[i][0];
        r = Query[i][1];

        // Find the answer for each query
        if (l == 0) {
            document.write( DP[r] + "<br>");
        }
        else {
            document.write( DP[r] - DP[l - 1]+ "<br>");
        }
    }
}

// Driver Code
var N = 5;
var Q = 3;

// Given array arr[]
var arr = [2, 4, 5, 6, 9];

// Given Query
var Query
    = [[0, 2 ], [1, 3 ], [1, 4 ]];

// Function Call
OddDivisorsCount(N, Q, arr, Query);

// This code is contributed by noob2000.
</script>
```

**Output:** 

```
1
1
2
```

***时间复杂度:***

*   *预计算:O(N)*
*   *对于每个查询:O(1)*

***辅助空间:**O(1)*T4】
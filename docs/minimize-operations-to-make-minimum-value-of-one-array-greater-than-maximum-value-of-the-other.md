# 最小化运算，使一个数组的最小值大于另一个数组的最大值

> 原文:[https://www . geesforgeks . org/最小化操作使一个数组的最小值大于另一个数组的最大值/](https://www.geeksforgeeks.org/minimize-operations-to-make-minimum-value-of-one-array-greater-than-maximum-value-of-the-other/)

给定由 **N** 和 **M** 整数组成的两个[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**A【】**和**B【】**，任务是找到使数组的最小元素**A【】**至少成为数组的最大元素**B【】**所需的最小操作数，从而在每个操作中，任何数组元素**A【】**都可以增加 **1** 或任何

**示例:**

> **输入:** A[] = {2，3}，B[] = {3，5}
> **输出:** 3
> **解释:**
> 执行如下操作:
> 
> 1.  将 A[1]的值增加 1 会修改数组 A[] = {3，3}。
> 2.  将 B[2]的值减 1 会修改数组 B[] = {3，4}。
> 3.  将 B[2]的值减 1 会修改数组 B[] = {3，3}。
> 
> 经过以上运算，数组 A[]的最小元素为 3，大于等于数组 B[]的最大元素为 3。因此，操作总数为 3。
> 
> **输入:** A[] = {1，2，3}，B[]= { 4 }
> T3】输出: 4

**进场:**使用 [**贪婪进场**](https://www.geeksforgeeks.org/greedy-algorithms/) 可以解决问题。按照以下步骤解决给定的问题:

*   [按照递增顺序](https://www.geeksforgeeks.org/c-program-to-sort-an-array-in-ascending-order/)对数组 **A[]** 进行排序。
*   [按降序排列数组**B[]**](https://www.geeksforgeeks.org/stable-sort-descending-order/)。
*   遍历两个数组**同时 A【I】<B【I】**，以使数组**A【】**和**B【】**的所有元素，直到索引 **i** 相等，比如说 **x** ，那么操作总数由下式给出:

> = >**(B[0]+B[1]+…+B[I])–I * x+(A[0]+A[1]+…+A[I])+I * x**
> =>**(B[0]–A[0])+(B[1]–A[1])+…+(B[I]–A[I])**。

*   遍历两个数组，直到 **A[i]** 的值小于 **B[i]** ，并且**(B[I]–A[I])**的值到达变量，比如 **ans** 。
*   完成上述步骤后，打印**和**的值作为所需的最小操作次数。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;
#define ll long long

// Comparator function
bool cmp(ll a, ll b) { return a > b; }

// Function to find the minimum number
// of operation required to satisfy the
// given conditions
int FindMinMoves(vector<ll> A, vector<ll> B)
{
    int n, m;
    n = A.size();
    m = B.size();

    // sort the array A and B in the
    // ascending and descending order
    sort(A.begin(), A.end());
    sort(B.begin(), B.end(), cmp);

    ll ans = 0;

    // Iterate over both the arrays
    for (int i = 0; i < min(m, n)
                    && A[i] < B[i];
         ++i) {

        // Add the difference to the
        // variable answer
        ans += (B[i] - A[i]);
    }

    // Return the resultant operations
    return ans;
}

// Driver Code
int main()
{
    vector<ll> A = { 2, 3 };
    vector<ll> B = { 3, 5 };
    cout << FindMinMoves(A, B);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.Arrays;

class GFG{

// Comparator function
public static boolean cmp(int a, int b)
{
    return a > b;
}

// Function to find the minimum number
// of operation required to satisfy the
// given conditions
public static int FindMinMoves(int[] A, int[] B)
{
    int n, m;
    n = A.length;
    m = B.length;

    // Sort the array A and B in the
    // ascending and descending order
    Arrays.sort(A);
    Arrays.sort(B);

    int ans = 0;

    // Iterate over both the arrays
    for(int i = 0;
            i < Math.min(m, n) && A[i] < B[i]; ++i)
    {

        // Add the difference to the
        // variable answer
        ans += (B[i] - A[i]);
    }

    // Return the resultant operations
    return ans;
}

// Driver Code
public static void main(String args[])
{
    int[] A = { 2, 3 };
    int[] B = { 3, 5 };

    System.out.println(FindMinMoves(A, B));
}
}

// This code is contributed by _saurabh_jaiswal
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the minimum number
# of operation required to satisfy the
# given conditions
def FindMinMoves(A, B):

    n = len(A)
    m = len(B)

    # sort the array A and B in the
    # ascending and descending order
    A.sort()
    B.sort(reverse = True)
    ans = 0

    # Iterate over both the arrays
    i = 0

    for i in range(min(m, n) and A[i] < B[i]):

        # Add the difference to the
        # variable answer
        ans += (B[i] - A[i])

    # Return the resultant operations
    return ans

# Driver Code
A = [ 2, 3 ]
B = [ 3, 5 ]

print(FindMinMoves(A, B))

# This code is contributed by gfgking
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Comparator function
public static bool cmp(int a, int b)
{
    return a > b;
}

// Function to find the minimum number
// of operation required to satisfy the
// given conditions
public static int FindMinMoves(int[] A, int[] B)
{
    int n, m;
    n = A.Length;
    m = B.Length;

    // Sort the array A and B in the
    // ascending and descending order
    Array.Sort(A);
    Array.Sort(B);

    int ans = 0;

    // Iterate over both the arrays
    for(int i = 0;
            i < Math.Min(m, n) && A[i] < B[i]; ++i)
    {

        // Add the difference to the
        // variable answer
        ans += (B[i] - A[i]);
    }

    // Return the resultant operations
    return ans;
}

// Driver Code
public static void Main()
{
    int[] A = { 2, 3 };
    int[] B = { 3, 5 };

    Console.Write(FindMinMoves(A, B));
}
}

// This code is contributed by target_2.
```

## java 描述语言

```
<script>

       // JavaScript program for the above approach

       // Function to find the minimum number
       // of operation required to satisfy the
       // given conditions
       function FindMinMoves(A, B)
       {
           let n, m;
           n = A.length;
           m = B.length;

           // sort the array A and B in the
           // ascending and descending order
           A.sort(function (a, b) { return a - b; });
           B.sort(function (a, b) { return b - a; });

           let ans = 0;

           // Iterate over both the arrays
           for (let i = 0; i < Math.min(m, n)
               && A[i] < B[i];
               ++i) {

               // Add the difference to the
               // variable answer
               ans += (B[i] - A[i]);
           }

           // Return the resultant operations
           return ans;
       }

       // Driver Code
       let A = [2, 3];
       let B = [3, 5];
       document.write(FindMinMoves(A, B));

   // This code is contributed by Potta Lokesh
   </script>
```

**Output:** 

```
3
```

**时间复杂度:** O(K*log K)，其中 K 的值为 max(N，M)。
***辅助空间:** O(1)*
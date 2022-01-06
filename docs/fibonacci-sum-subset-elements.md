# 包含所有元素的子集的斐波那契和< = k

> 原文:[https://www . geesforgeks . org/Fibonacci-sum-subset-elements/](https://www.geeksforgeeks.org/fibonacci-sum-subset-elements/)

给定一个由 n 个元素组成的数组，任务是求数组子集的斐波那契和，其中子集的每个元素<= k. 
精确地说，求**F(A<sub>i1</sub>)+F(A<sub>I2</sub>)+F(A<sub>i3</sub>)+…+F(A<sub>IX</sub>)**，其中(A <sub>i1</sub> ，A <sub>i2</sub> ，…， A <sub>ix</sub> ) < = K 和 1 < = (i <sub>1</sub> ，i <sub>2</sub> ，…，i <sub>x</sub> ) < = n .这里， **F(i)** 是 **i <sup>第</sup>个斐波那契数**
例:

```
Input : arr = {1, 2, 3, 4, 2, 7}
        Query 1 : K = 2
        Query 2 : K = 6
Output : 3
         8
```

**说明:**
在**查询 1** 中，子集 **{1，2，2}** 就是这样一个子集，在这种情况下，子集内的所有元素都是< = k，即< = 2。子集的斐波那契和= F(1)+F(2)+F(2)= 1+1+1 =**3**
在**查询 2** 中，子集 **{1，2，3，4，2}** 是这样一个子集，其中子集内的所有元素都是< = k，即本例中的< = 6。子集的斐波那契和= F(1)+F(2)+F(3)+F(4)+F(2)= 1+1+2+3+1 =**8**
使用两种不同的查询技术来解决这个问题，即:
1)在线查询，
2)离线查询
在这两种方法中，唯一常见的步骤是生成第 n 个<sup>斐波那契数。使用[和](https://www.geeksforgeeks.org/program-for-nth-fibonacci-number/)生成第 n 个<sup>斐波那契数的有效技术。
这种生成斐波那契数的方法在两种查询技术中都很常见。现在，看看如何使用这两种技术生成的斐波那契数。
**方法 1(在线查询):**
在这种技术中，在查询到达时进行处理。首先，按升序对数组进行排序。获得特定 k 的查询后，在这个排序的数组上使用二分搜索法来查找最后一个索引，其中数组的值是& < = k。让我们称这个位置为 x。
现在，由于数组是排序的，</sup></sup> 

```
For all i <= x, a[i] <= x
i.e
a[i] <= a[x] for all i ∈ [1, x]
```

所以，重点关注的子集是 A <sub>1</sub> ，A <sub>2</sub> ，A <sub>3</sub> ，…。排序后的数组 A 中的 A <sub>x</sub> ，斐波那契和为:**F(A<sub>1</sub>)+F(A<sub>2</sub>)+F(A<sub>3</sub>)+…+F(A<sub>x</sub>)**
使用[前缀和数组](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/)高效求子集 A <sub>1</sub> ，A <sub>2【的和 A <sub>x</sub> 。
如果 prefixbsum[I]存储斐波那契和直到排序数组 A 的第 I<sup>个索引，那么，数组子集从 1 到 x 的斐波那契和，就是 prefixbsum[x]
这样，**子集[1…x]= prefixbsum[x]**，prefixbsum[x]可以计算如下:
**prefixbsum[x]= prefixbsum**</sup></sub> 

## C++

```
// C++ program to find fibonacci sum of
// subarray where all elements <= k
#include <bits/stdc++.h>

using namespace std;

// Helper function that multiplies 2 matrices
// F and M of size 2*2, and puts the multiplication
// result back to F[][]
void multiply(int F[2][2], int M[2][2])
{
    int x = F[0][0] * M[0][0] + F[0][1] * M[1][0];
    int y = F[0][0] * M[0][1] + F[0][1] * M[1][1];
    int z = F[1][0] * M[0][0] + F[1][1] * M[1][0];
    int w = F[1][0] * M[0][1] + F[1][1] * M[1][1];

    F[0][0] = x;
    F[0][1] = y;
    F[1][0] = z;
    F[1][1] = w;
}

/* Helper function that calculates F[][]
   raise to the power n and puts the
   result in F[][]  */
void power(int F[2][2], int n)
{
    int i;
    int M[2][2] = { { 1, 1 }, { 1, 0 } };

    // n - 1 times multiply the
    // matrix to {{1, 0}, {0, 1}}
    for (i = 2; i <= n; i++)
        multiply(F, M);
}

// Returns the nth fibonacci number
int fib(int n)
{
    int F[2][2] = { { 1, 1 }, { 1, 0 } };
    if (n == 0)
        return 0;
    power(F, n - 1);

    return F[0][0];
}

int findLessThanK(int arr[], int n, int k)
{
    // find first index which is > k
    // using lower_bound
    return (lower_bound(arr, arr + n, k + 1)
                        - arr);
}

// Function to build Prefix Fibonacci Sum
int* buildPrefixFibonacciSum(int arr[], int n)
{
    // Allocate memory to prefix
    // fibonacci sum array
    int* prefixFibSum = new int[n];

    // Traverse the array from 0 to n - 1,
    // when at the ith index then we calculate
    // the a[i]th fibonacci number and calculate
    // the fibonacci sum till the ith index as
    // the sum of fibonacci sum till index i - 1
    // and the a[i]th fibonacci number
    for (int i = 0; i < n; i++)
    {
        int currFibNumber = fib(arr[i]);
        if (i == 0) {
            prefixFibSum[i] = currFibNumber;
        }
        else {
            prefixFibSum[i] = prefixFibSum[i - 1]
                              + currFibNumber;
        }
    }
    return prefixFibSum;
}

// Return the answer for each query
int processQuery(int arr[], int prefixFibSum[],
                 int n, int k)
{

    // index stores the index till where
    // the array elements are less than k
    int lessThanIndex = findLessThanK(arr, n, k);

    if (lessThanIndex == 0)
        return 0;
    return prefixFibSum[lessThanIndex - 1];
}

// Driver Code
int main()
{
    int arr[] = { 1, 2, 3, 4, 2, 7 };
    int n = sizeof(arr) / sizeof(arr[0]);

    // sort the array arr
    sort(arr, arr + n);

    // Build the prefix fibonacci sum array
    int* prefixFibSum =
         buildPrefixFibonacciSum(arr, n);

    // query array stores q queries
    int query[] = { 2, 6 };
    int q = sizeof(query) / sizeof(query[0]);

    for (int i = 0; i < q; i++) {
        int k = query[i];
        int ans =
            processQuery(arr, prefixFibSum, n, k);

        cout << "Query  " << i + 1 << " : "
             << ans << endl;
    }
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find fibonacci sum of
// subarray where all elements <= k
import java.util.*;

class GFG
{

    // Helper function that multiplies 2 matrices
    // F and M of size 2*2, and puts the multiplication
    // result back to F[][]
    static void multiply(int[][] F, int[][] M)
    {
        int x = F[0][0] * M[0][0] + F[0][1] * M[1][0];
        int y = F[0][0] * M[0][1] + F[0][1] * M[1][1];
        int z = F[1][0] * M[0][0] + F[1][1] * M[1][0];
        int w = F[1][0] * M[0][1] + F[1][1] * M[1][1];

        F[0][0] = x;
        F[0][1] = y;
        F[1][0] = z;
        F[1][1] = w;
    }

    /*
    * Helper function that calculates F[][]
    raise to the power n and puts the
    * result in F[][]
    */
    static void power(int[][] F, int n)
    {
        int i;
        int[][] M = { { 1, 1 }, { 1, 0 } };

        // n - 1 times multiply the
        // matrix to {{1, 0}, {0, 1}}
        for (i = 2; i <= n; i++)
            multiply(F, M);
    }

    // Returns the nth fibonacci number
    static int fib(int n)
    {
        int[][] F = { { 1, 1 }, { 1, 0 } };
        if (n == 0)
            return 0;
        power(F, n - 1);

        return F[0][0];
    }

    static int findLessThanK(int arr[], int n, int k)
    {
        // find first index which is > k
        // using lower_bound
        return (lower_bound(arr, 0, n, k + 1));
    }

    static int lower_bound(int[] a, int low,
                       int high, int element)
    {
        while (low < high)
        {
            int middle = low + (high - low) / 2;
            if (element > a[middle])
                low = middle + 1;
            else
                high = middle;
        }
        return low;
    }

    // Function to build Prefix Fibonacci Sum
    static int[] buildPrefixFibonacciSum(int arr[], int n)
    {
        // Allocate memory to prefix
        // fibonacci sum array
        int[] prefixFibSum = new int[n];

        // Traverse the array from 0 to n - 1,
        // when at the ith index then we calculate
        // the a[i]th fibonacci number and calculate
        // the fibonacci sum till the ith index as
        // the sum of fibonacci sum till index i - 1
        // and the a[i]th fibonacci number
        for (int i = 0; i < n; i++)
        {
            int currFibNumber = fib(arr[i]);
            if (i == 0)
            {
                prefixFibSum[i] = currFibNumber;
            }
            else
            {
                prefixFibSum[i] = prefixFibSum[i - 1] +
                                        currFibNumber;
            }
        }
        return prefixFibSum;
    }

    // Return the answer for each query
    static int processQuery(int arr[], int prefixFibSum[],
                                            int n, int k)
    {

        // index stores the index till where
        // the array elements are less than k
        int lessThanIndex = findLessThanK(arr, n, k);

        if (lessThanIndex == 0)
            return 0;
        return prefixFibSum[lessThanIndex - 1];
    }

    // Driver Code
    public static void main(String[] args)
    {
        int arr[] = { 1, 2, 3, 4, 2, 7 };
        int n = arr.length;

        // sort the array arr
        Arrays.sort(arr);

        // Build the prefix fibonacci sum array
        int[] prefixFibSum = buildPrefixFibonacciSum(arr, n);

        // query array stores q queries
        int query[] = { 2, 6 };
        int q = query.length;

        for (int i = 0; i < q; i++)
        {
            int k = query[i];
            int ans = processQuery(arr, prefixFibSum, n, k);

            System.out.print("Query " + (i + 1) + " : " + ans + "\n");
        }
    }
}

// This code is contributed by Rajput-Ji
```

## C#

```
// C# program to find fibonacci sum of
// subarray where all elements <= k
using System;

class GFG
{

    // Helper function that multiplies 2 matrices
    // F and M of size 2*2, and puts the multiplication
    // result back to F[,]
    static void multiply(int[,] F, int[,] M)
    {
        int x = F[0, 0] * M[0, 0] + F[0, 1] * M[1, 0];
        int y = F[0, 0] * M[0, 1] + F[0, 1] * M[1, 1];
        int z = F[1, 0] * M[0, 0] + F[1, 1] * M[1, 0];
        int w = F[1, 0] * M[0, 1] + F[1, 1] * M[1, 1];

        F[0, 0] = x;
        F[0, 1] = y;
        F[1, 0] = z;
        F[1, 1] = w;
    }

    /*
    * Helper function that calculates F[,]
    raise to the power n and puts the
    * result in F[,]
    */
    static void power(int[,] F, int n)
    {
        int i;
        int[,] M = { { 1, 1 }, { 1, 0 } };

        // n - 1 times multiply the
        // matrix to {{1, 0}, {0, 1}}
        for (i = 2; i <= n; i++)
            multiply(F, M);
    }

    // Returns the nth fibonacci number
    static int fib(int n)
    {
        int[,] F = {{ 1, 1 }, { 1, 0 }};
        if (n == 0)
            return 0;
        power(F, n - 1);

        return F[0, 0];
    }

    static int findLessThanK(int []arr, int n, int k)
    {
        // find first index which is > k
        // using lower_bound
        return (lower_bound(arr, 0, n, k + 1));
    }

    static int lower_bound(int[] a, int low,
                    int high, int element)
    {
        while (low < high)
        {
            int middle = low + (high - low) / 2;
            if (element > a[middle])
                low = middle + 1;
            else
                high = middle;
        }
        return low;
    }

    // Function to build Prefix Fibonacci Sum
    static int[] buildPrefixFibonacciSum(int []arr, int n)
    {
        // Allocate memory to prefix
        // fibonacci sum array
        int[] prefixFibSum = new int[n];

        // Traverse the array from 0 to n - 1,
        // when at the ith index then we calculate
        // the a[i]th fibonacci number and calculate
        // the fibonacci sum till the ith index as
        // the sum of fibonacci sum till index i - 1
        // and the a[i]th fibonacci number
        for (int i = 0; i < n; i++)
        {
            int currFibNumber = fib(arr[i]);
            if (i == 0)
            {
                prefixFibSum[i] = currFibNumber;
            }
            else
            {
                prefixFibSum[i] = prefixFibSum[i - 1] +
                                        currFibNumber;
            }
        }
        return prefixFibSum;
    }

    // Return the answer for each query
    static int processQuery(int []arr, int []prefixFibSum,
                                            int n, int k)
    {

        // index stores the index till where
        // the array elements are less than k
        int lessThanIndex = findLessThanK(arr, n, k);

        if (lessThanIndex == 0)
            return 0;
        return prefixFibSum[lessThanIndex - 1];
    }

    // Driver Code
    public static void Main(String[] args)
    {
        int []arr = { 1, 2, 3, 4, 2, 7 };
        int n = arr.Length;

        // sort the array arr
        Array.Sort(arr);

        // Build the prefix fibonacci sum array
        int[] prefixFibSum = buildPrefixFibonacciSum(arr, n);

        // query array stores q queries
        int []query = {2, 6};
        int q = query.Length;

        for (int i = 0; i < q; i++)
        {
            int k = query[i];
            int ans = processQuery(arr, prefixFibSum, n, k);

            Console.Write("Query " + (i + 1) + " : " + ans + "\n");
        }
    }
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>
// Javascript program to find fibonacci sum of
// subarray where all elements <= k

// Helper function that multiplies 2 matrices
// F and M of size 2*2, and puts the multiplication
// result back to F[,]
function multiply(F, M) {
    let x = F[0][0] * M[0][0] + F[0][1] * M[1][0];
    let y = F[0][0] * M[0][1] + F[0][1] * M[1][1];
    let z = F[1][0] * M[0][0] + F[1][1] * M[1][0];
    let w = F[1][0] * M[0][1] + F[1][1] * M[1][1];

    F[0][0] = x;
    F[0][1] = y;
    F[1][0] = z;
    F[1][1] = w;
}

/*
* Helper function that calculates F[,]
raise to the power n and puts the
* result in F[,]
*/
function power(F, n) {
    let i;
    let M = [[1, 1], [1, 0]];

    // n - 1 times multiply the
    // matrix to {{1, 0}, {0, 1}}
    for (i = 2; i <= n; i++)
        multiply(F, M);
}

// Returns the nth fibonacci number
function fib(n) {
    let F = [[1, 1], [1, 0]];
    if (n == 0)
        return 0;
    power(F, n - 1);

    return F[0][0];
}

function findLessThanK(arr, n, k) {
    // find first index which is > k
    // using lower_bound
    return (lower_bound(arr, 0, n, k + 1));
}

function lower_bound(a, low, high, element) {
    while (low < high) {
        let middle = Math.floor(low + (high - low) / 2);
        if (element > a[middle])
            low = middle + 1;
        else
            high = middle;
    }
    return low;
}

// Function to build Prefix Fibonacci Sum
function buildPrefixFibonacciSum(arr, n) {
    // Allocate memory to prefix
    // fibonacci sum array
    let prefixFibSum = new Array(n);

    // Traverse the array from 0 to n - 1,
    // when at the ith index then we calculate
    // the a[i]th fibonacci number and calculate
    // the fibonacci sum till the ith index as
    // the sum of fibonacci sum till index i - 1
    // and the a[i]th fibonacci number
    for (let i = 0; i < n; i++) {
        let currFibNumber = fib(arr[i]);
        if (i == 0) {
            prefixFibSum[i] = currFibNumber;
        }
        else {
            prefixFibSum[i] = prefixFibSum[i - 1] +
                currFibNumber;
        }
    }
    return prefixFibSum;
}

// Return the answer for each query
function processQuery(arr, prefixFibSum, n, k) {

    // index stores the index till where
    // the array elements are less than k
    let lessThanIndex = findLessThanK(arr, n, k);

    if (lessThanIndex == 0)
        return 0;
    return prefixFibSum[lessThanIndex - 1];
}

// Driver Code

let arr = [1, 2, 3, 4, 2, 7];
let n = arr.length;

// sort the array arr
arr.sort((a, b) => a - b);

// Build the prefix fibonacci sum array
let prefixFibSum = buildPrefixFibonacciSum(arr, n);

// query array stores q queries
let query = [2, 6];
let q = query.length;

for (let i = 0; i < q; i++) {
    let k = query[i];
    let ans = processQuery(arr, prefixFibSum, n, k);

    document.write("Query " + (i + 1) + " : " + ans + "<br>");
}

// This code is contributed by gfgking

</script>
```

## 蟒蛇 3

```
# Python3 program to find fibonacci sum of
# subarray where all elements <= k

from bisect import bisect

# Helper function that multiplies 2 matrices
# F and M of size 2*2, and puts the multiplication
# result back to F
def multiply(F, M):
    x = F[0][0] * M[0][0] + F[0][1] * M[1][0]
    y = F[0][0] * M[0][1] + F[0][1] * M[1][1]
    z = F[1][0] * M[0][0] + F[1][1] * M[1][0]
    w = F[1][0] * M[0][1] + F[1][1] * M[1][1]

    F[0][0] = x
    F[0][1] = y
    F[1][0] = z
    F[1][1] = w

# Helper function that calculates F
# raise to the power n and puts the
# result in F
def power(F, n):
    M = [[1, 1], [1, 0]]

    # n - 1 times multiply the
    # matrix to [[1, 0], [0, 1]]
    for i in range(1, n):
        multiply(F, M)

# Returns the nth fibonacci number
def fib(n):
    F = [[1, 1], [1, 0]]
    if (n == 0):
        return 0
    power(F, n - 1)

    return F[0][0]

def findLessThanK(arr, n, k):
    # find first index which is > k
    # using bisect
    return (bisect(arr, k))

#  Function to build Prefix Fibonacci Sum
def buildPrefixFibonacciSum(arr, n):
    # Allocate memory to prefix
    # fibonacci sum array
    prefixFibSum = [0]*n

    # Traverse the array from 0 to n - 1,
    # when at the ith index then we calculate
    # the a[i]th fibonacci number and calculate
    # the fibonacci sum till the ith index as
    # the sum of fibonacci sum till index i - 1
    # and the a[i]th fibonacci number
    for i in range(n):
        currFibNumber = fib(arr[i])
        if (i == 0):
            prefixFibSum[i] = currFibNumber
        else:
            prefixFibSum[i] = prefixFibSum[i - 1] + currFibNumber
    return prefixFibSum

# Return the answer for each query

def processQuery(arr, prefixFibSum, n, k):

    # index stores the index till where
    # the array elements are less than k
    lessThanIndex = findLessThanK(arr, n, k)

    if (lessThanIndex == 0):
        return 0
    return prefixFibSum[lessThanIndex - 1]

# Driver Code
if __name__ == '__main__':
    arr = [1, 2, 3, 4, 2, 7]
    n = len(arr)

    # sort the array arr
    arr.sort()

    # Build the prefix fibonacci sum array
    prefixFibSum = buildPrefixFibonacciSum(arr, n)

    # query array stores q queries
    query = [2, 6]
    q = len(query)

    for i in range(q):
        k = query[i]
        ans = processQuery(arr, prefixFibSum, n, k)

        print("Query  {} : {}".format(i+1, ans))

# This code is contributed by Amartya Ghosh
```

**Output:** 

```
Query  1 : 3
Query  2 : 8
```
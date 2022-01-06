# 每个数组元素的[1，arr[i]]范围内的非同素对的计数

> 原文:[https://www . geeksforgeeks . org/每数组元素 1 个 arri 范围内的非同素对的计数/](https://www.geeksforgeeks.org/count-of-non-co-prime-pairs-from-the-range-1-arri-for-every-array-element/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** ，数组中每个 **i <sup>第</sup>** 个元素的任务是从范围**【1，arr[I]】**中找出非共素[对的数量。](https://www.geeksforgeeks.org/check-two-numbers-co-prime-not/)

**示例:**

> **输入:** N = 2，arr[] = {3，4}
> **输出:**2 4
> T6】说明:
> 
> 1.  范围[1，3]中的所有非同素对都是(2，2)和(3，3)。
> 2.  范围[1，4]中的所有非同素对都是(2，2)，(2，4)，(3，3)和(4，4)。
> 
> **输入:** N = 3，arr[] = {5，10，20 }
> T3】输出: 5 23 82

**天真法:**解决问题最简单的方法是迭代每一个**I<sup>th</sup>T5】数组元素，然后从范围**【1，arr【I】**中生成每一个可能的对，对于每一对，检查其是否为非同素，即该对的 [**gcd**](https://www.geeksforgeeks.org/basic-and-extended-euclidean-algorithms/) 是否大于 **1** 。**

按照以下步骤解决此问题:

*   [使用变量迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，N–1】**，说出 **i、**并执行以下步骤:
    *   将变量**最后一个**初始化为**arr【I】**和**计数**为 **0** ，分别存储当前范围的最后一个值和共质数对。
    *   使用变量 **x** 和 **y** 迭代范围**【1，arr[I]】**中的每一对，并执行以下 **:**
        *   如果 **GCD(x，y)** 大于 **1** ，则增量**按 **1** 计数**。
    *   最后打印**数**作为答案。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Recursive function to
// return gcd of two numbers
int gcd(int a, int b)
{
    if (b == 0)
        return a;

    return gcd(b, a % b);
}

// Function to count the number of
// non co-prime pairs for each query
void countPairs(int* arr, int N)
{

    // Traverse the array arr[]
    for (int i = 0; i < N; i++) {

        // Stores the count of
        // non co-prime pairs
        int count = 0;

        // Iterate over the range [1, x]
        for (int x = 1; x <= arr[i]; x++) {

            // Iterate over the range [x, y]
            for (int y = x; y <= arr[i]; y++) {

                // If gcd of current pair
                // is greater than 1
                if (gcd(x, y) > 1)
                    count++;
            }
        }
        cout << count << " ";
    }
}

// Driver Code
int main()
{
    // Given Input
    int arr[] = { 5, 10, 20 };
    int N = 3;

    // Function Call
    countPairs(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Recursive function to
// return gcd of two numbers
static int gcd(int a, int b)
{
    if (b == 0)
        return a;

    return gcd(b, a % b);
}

// Function to count the number of
// non co-prime pairs for each query
static void countPairs(int[] arr, int N)
{

    // Traverse the array arr[]
    for(int i = 0; i < N; i++)
    {

        // Stores the count of
        // non co-prime pairs
        int count = 0;

        // Iterate over the range [1, x]
        for(int x = 1; x <= arr[i]; x++)
        {

            // Iterate over the range [x, y]
            for(int y = x; y <= arr[i]; y++)
            {

                // If gcd of current pair
                // is greater than 1
                if (gcd(x, y) > 1)
                    count++;
            }
        }
        System.out.print(count + " ");
    }
}

// Driver Code
public static void main(String[] args)
{

    // Given Input
    int arr[] = { 5, 10, 20 };
    int N = 3;

    // Function Call
    countPairs(arr, N);
}
}

// This code is contributed by subhammahato348
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Recursive program to
# return gcd of two numbers
def gcd(a, b):

    if b == 0:
        return a

    return gcd(b, a % b)

# Function to count the number of
# non co-prime pairs for each query
def countPairs(arr, N):

    # Traverse the array arr[]
    for i in range(0, N):

        # Stores the count of
        # non co-prime pairs
        count = 0

        # Iterate over the range [1,x]
        for x in range(1, arr[i] + 1):

            # Iterate over the range [x,y]
            for y in range(x, arr[i] + 1):

                # If gcd of current pair
                # is greater than 1
                if gcd(x, y) > 1:
                    count += 1

        print(count, end = " ")

# Driver code
if __name__ == '__main__':

    # Given Input
    arr = [ 5, 10, 20 ]
    N = len(arr)

    # Function Call
    countPairs(arr, N)

# This code is contributed by MuskanKalra1
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Recursive function to
// return gcd of two numbers
static int gcd(int a, int b)
{
    if (b == 0)
        return a;

    return gcd(b, a % b);
}

// Function to count the number of
// non co-prime pairs for each query
static void countPairs(int[] arr, int N)
{

    // Traverse the array arr[]
    for(int i = 0; i < N; i++)
    {

        // Stores the count of
        // non co-prime pairs
        int count = 0;

        // Iterate over the range [1, x]
        for(int x = 1; x <= arr[i]; x++)
        {

            // Iterate over the range [x, y]
            for(int y = x; y <= arr[i]; y++)
            {

                // If gcd of current pair
                // is greater than 1
                if (gcd(x, y) > 1)
                    count++;
            }
        }
        Console.Write(count + " ");
    }
}

// Driver Code
public static void Main(String[] args)
{

    // Given Input
    int []arr = { 5, 10, 20 };
    int N = 3;

    // Function Call
    countPairs(arr, N);
}
}

// This code is contributed by shivanisinghss2110
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Recursive function to
// return gcd of two numbers
function gcd(a, b)
{
    if (b == 0)
        return a;

    return gcd(b, a % b);
}

// Function to count the number of
// non co-prime pairs for each query
function countPairs(arr, N)
{

    // Traverse the array arr[]
    for(var i = 0; i < N; i++)
    {

        // Stores the count of
        // non co-prime pairs
        var count = 0;

        // Iterate over the range [1, x]
        for(var x = 1; x <= arr[i]; x++)
        {

            // Iterate over the range [x, y]
            for(var y = x; y <= arr[i]; y++)
            {

                // If gcd of current pair
                // is greater than 1
                if (gcd(x, y) > 1)
                    count++;
            }
        }
        document.write(count + " ");
    }
}

// Driver Code

// Given Input
var arr = [ 5, 10, 20 ];
var N = 3;

// Function Call
countPairs(arr, N);

// This code is contributed by shivanisinghss2110

</script>
```

**Output**

```
5 23 82 
```

***时间复杂度:** O(N*M <sup>2</sup> *log(M))，其中 M 为阵的最大元素。*
***辅助空间:** O(1)*

**高效方法:**上述方法可以通过使用[欧拉全能函数](https://www.geeksforgeeks.org/eulers-totient-function-for-all-numbers-smaller-than-or-equal-to-n/)、[前缀和数组](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/)进行优化。按照以下步骤解决问题:

*   初始化两个数组，将**φ[]**和 **ans[]** 表示为 **0** ，其中数组的 **i <sup>th</sup>** 元素表示与 **i** 互素的整数的计数和从范围**【1，arr[i]】形成的非互素对的计数。**
*   [使用变量迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【1，MAX】**，说出 **i、**并将 **i** 分配给**φ[I]。**
*   [使用变量迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【2，MAX】**，说出 **i，**并执行以下步骤:
    *   如果**φ[I]= I，**则使用变量 **j** 迭代范围**【I，MAX】**，并执行以下步骤:
        *   从**φ【j】**开始递减**φ【j】/I**，然后以 **i** 递增 **j** 。
*   [使用变量迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【1，MAX】**，说出 **i，**并执行以下步骤:
    *   更新**年[i]** 至**年[I–1]+(I–phi[I])。**
*   最后，完成以上步骤后，[打印阵列](https://www.geeksforgeeks.org/c-program-to-print-an-array-using-recursion/)**ans【】**。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;
const int MAX = 1005;

// Auxiliary function to pre-compute
// the answer for each array
void preCalculate(vector<int>& phi,
                  vector<int>& ans)
{
    phi[0] = 0;
    phi[1] = 1;

    // Iterate over the range [1, MAX]
    for (int i = 2; i <= MAX; i++)
        phi[i] = i;

    // Iterate over the range [1, MAX]
    for (int i = 2; i <= MAX; i++) {

        // If the number is prime
        if (phi[i] == i) {

            for (int j = i; j <= MAX; j += i)

                // Subtract the number of
                // pairs which has i as one
                // of their factors
                phi[j] -= (phi[j] / i);
        }
    }

    // Iterate over the range [1, MAX]
    for (int i = 1; i <= MAX; i++)
        ans[i] = ans[i - 1] + (i - phi[i]);
}

// Function to count the number of
// non co-prime pairs for each query
void countPairs(int* arr, int N)
{
    // The i-th element stores
    // the count of element that
    // are co-prime with i
    vector<int> phi(1e5, 0);

    // Stores the resulting array
    vector<int> ans(1e5, 0);

    // Function Call
    preCalculate(phi, ans);

    // Traverse the array arr[]
    for (int i = 0; i < N; ++i) {
        cout << ans[arr[i]] << " ";
    }
}

// Driver Code
int main()
{
    // Given Input
    int arr[] = { 5, 10, 20 };
    int N = 3;

    // Function Call
    countPairs(arr, N);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
class GFG {

static int MAX = 1005;

// Auxiliary function to pre-compute
// the answer for each array
static void preCalculate(int[] phi,
                  int[] ans)
{
    phi[0] = 0;
    phi[1] = 1;

    // Iterate over the range [1, MAX]
    for (int i = 2; i <= MAX; i++)
        phi[i] = i;

    // Iterate over the range [1, MAX]
    for (int i = 2; i <= MAX; i++) {

        // If the number is prime
        if (phi[i] == i) {

            for (int j = i; j <= MAX; j += i)

                // Subtract the number of
                // pairs which has i as one
                // of their factors
                phi[j] -= (phi[j] / i);
        }
    }

    // Iterate over the range [1, MAX]
    for (int i = 1; i <= MAX; i++)
        ans[i] = ans[i - 1] + (i - phi[i]);
}

// Function to count the number of
// non co-prime pairs for each query
static void countPairs(int[] arr, int N)
{
    // The i-th element stores
    // the count of element that
    // are co-prime with i
    int[] phi = new int[100000];
    Arrays.fill(phi, 0);

    // Stores the resulting array
    int[] ans = new int[100000];
    Arrays.fill(ans, 0);

    // Function Call
    preCalculate(phi, ans);

    // Traverse the array arr[]
    for (int i = 0; i < N; ++i) {
        System.out.print(ans[arr[i]] + " ");
    }
}

// Driver Code
public static void main(String[] args)
{
     // Given Input
    int arr[] = { 5, 10, 20 };
    int N = 3;

    // Function Call
    countPairs(arr, N);
}
}

// This code is contributed by code_hunt.
```

## 蟒蛇 3

```
MAX = 1005;

def preCalculate(phi,ans):
    phi[0] = 0
    phi[1] = 1

    # Iterate over the range [1, MAX]
    for i in range(2, MAX+1):
        phi[i] = i

    # Iterate over the range [1, MAX]
    for i in range(2, MAX+1):
        if (phi[i] == i):
            for j in range(i, MAX+1, i):

                # Subtract the number of
                # pairs which has i as one
                # of their factors
                phi[j] -= (phi[j] // i);

    # Iterate over the range [1, MAX]
    for i in range(1, MAX+1):
        ans[i] = ans[i - 1] + (i - phi[i]);

# Function to count the number of
# non co-prime pairs for each query
def countPairs(arr, N):

    # The i-th element stores
    # the count of element that
    # are co-prime with i
    phi = [0 for i in range(100001)]

    # Stores the resulting array
    ans = [0 for i in range(100001)]

    # Function Call
    preCalculate(phi, ans);

    # Traverse the array arr[]
    for i in range(N):
        print(ans[arr[i]],end=' ');

# Given Input
arr= [5, 10, 20]
N = 3;

# Function Call
countPairs(arr, N);

# This code is contributed by rutvik_56.
```

## C#

```
// C# program for the above approach
using System;
class GFG{

static int MAX = 1005;

// Auxiliary function to pre-compute
// the answer for each array
static void preCalculate(int[] phi,
                  int[] ans)
{
    phi[0] = 0;
    phi[1] = 1;

    // Iterate over the range [1, MAX]
    for (int i = 2; i <= MAX; i++)
        phi[i] = i;

    // Iterate over the range [1, MAX]
    for (int i = 2; i <= MAX; i++) {

        // If the number is prime
        if (phi[i] == i) {

            for (int j = i; j <= MAX; j += i)

                // Subtract the number of
                // pairs which has i as one
                // of their factors
                phi[j] -= (phi[j] / i);
        }
    }

    // Iterate over the range [1, MAX]
    for (int i = 1; i <= MAX; i++)
        ans[i] = ans[i - 1] + (i - phi[i]);
}

// Function to count the number of
// non co-prime pairs for each query
static void countPairs(int[] arr, int N)
{
    // The i-th element stores
    // the count of element that
    // are co-prime with i
    int[] phi = new int[100000];
    Array.Clear(phi, 0, 100000);

    // Stores the resulting array
    int[] ans = new int[100000];
    Array.Clear(ans, 0, 100000);

    // Function Call
    preCalculate(phi, ans);

    // Traverse the array arr[]
    for (int i = 0; i < N; ++i) {
        Console.Write(ans[arr[i]] + " ");
    }
}

// Driver Code
public static void Main()
{
    // Given Input
    int[] arr = { 5, 10, 20 };
    int N = 3;

    // Function Call
    countPairs(arr, N);
}
}

// This code is contributed by sanjoy_62.
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

const MAX = 1005;

// Auxiliary function to pre-compute
// the answer for each array
function preCalculate(phi, ans) {
  phi[0] = 0;
  phi[1] = 1;

  // Iterate over the range [1, MAX]
  for (let i = 2; i <= MAX; i++) phi[i] = i;

  // Iterate over the range [1, MAX]
  for (let i = 2; i <= MAX; i++) {
    // If the number is prime
    if (phi[i] == i) {
      for (let j = i; j <= MAX; j += i)
        // Subtract the number of
        // pairs which has i as one
        // of their factors
        phi[j] -= Math.floor(phi[j] / i);
    }
  }

  // Iterate over the range [1, MAX]
  for (let i = 1; i <= MAX; i++)
  ans[i] = ans[i - 1] + (i - phi[i]);
}

// Function to count the number of
// non co-prime pairs for each query
function countPairs(arr, N) {
  // The i-th element stores
  // the count of element that
  // are co-prime with i
  let phi = new Array(1e5).fill(0);

  // Stores the resulting array
  let ans = new Array(1e5).fill(0);

  // Function Call
  preCalculate(phi, ans);

  // Traverse the array arr[]
  for (let i = 0; i < N; ++i) {
    document.write(ans[arr[i]] + " ");
  }
}

// Driver Code

// Given Input
let arr = [5, 10, 20];
let N = 3;

// Function Call
countPairs(arr, N);

</script>
```

**Output**

```
5 23 82 
```

***时间复杂度:** O(N+ M*log(N))，其中 M 是数组的最大元素。*
***辅助空间:** O(M+N)*
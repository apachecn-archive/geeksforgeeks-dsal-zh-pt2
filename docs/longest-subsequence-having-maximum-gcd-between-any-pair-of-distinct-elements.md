# 任何一对不同元素之间具有最大 GCD 的最长子序列

> 原文:[https://www . geeksforgeeks . org/任意对不同元素之间的最长子序列具有最大 gcd/](https://www.geeksforgeeks.org/longest-subsequence-having-maximum-gcd-between-any-pair-of-distinct-elements/)

给定一个由 **N** 个正整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**，任务是从给定数组中找到[子序列](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)的最大长度，使得子序列中任意两个不同整数的 [GCD](https://www.geeksforgeeks.org/basic-and-extended-euclidean-algorithms/) 为**最大值**。

**示例:**

> **输入:** arr[] = {5，14，15，20，1}
> **输出:** 3
> **解释:**任意一对不同整数最大 GCD 的子序列为{5，15，20}。
> 上述序列中任意一对不同元素之间的 GCD 为 5，是数组中最大的 GCD。
> 
> **输入:** arr[] = {1，2，8，5，6}
> **输出:** 3
> **解释:** <任意一对不同整数最大 GCD 的子序列为{2，8，6}。
> 上述序列中任意两个不同数字之间的 GCD 为 2，是数组中最大的 GCD。

**朴素方法:**最简单的方法是使用[递归](https://www.geeksforgeeks.org/recursion/)和[递归生成给定数组的所有可能子序列](https://www.geeksforgeeks.org/generating-all-possible-subsequences-using-recursion/)，并在这些子序列中找到最大长度。以下是步骤:

*   使用厄拉多塞的[筛的思想，创建一个函数来查找数组中具有**最大 GCD** (比如**最大 GCD** )的对。](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)
*   创建另一个函数来计算子序列数组的最大长度，其中任意两个不同元素之间的 GCD 最大:
    *   创建一个辅助数组 **arr1[]** ，按照排序顺序存储[数组元素。](https://www.geeksforgeeks.org/c-program-to-sort-an-array-in-ascending-order/)
    *   将两个变量初始化为**【0，0】**，递归生成所有子序列，并将具有 GCD 的子序列的最大长度返回为 **maxGCD** 。
*   完成上述步骤后，打印上述递归调用返回的最大长度。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include<bits/stdc++.h>
using namespace std;

// Function to find GCD of pair with
// maximum GCD
int findMaxGCD(int arr[], int N)
{

    // Stores maximum element of arr[]
    int high = 0;

    // Find the maximum element
    for(int i = 0; i < N; i++)
    {
        high = max(high, arr[i]);
    }

    // Maintain a count array
    int count[high + 1] = {0};

    // Store the frequency of arr[]
    for(int i = 0; i < N; i++)
    {
        count[arr[i]] += 1;
    }

    // Stores the multiples of a number
    int counter = 0;

    // Iterate over the  range [MAX, 1]
    for(int i = high; i > 0; i--)
    {
        int j = i;

        // Iterate from current potential
        // GCD till it is less than MAX
        while (j <= high)
        {

            // A multiple found
            if (count[j] > 0)
                counter += count[j];

            // Increment potential GCD by
            // itself io check i, 2i, 3i...
            j += i;

            // If 2 multiples found max
            // GCD found
            if (counter == 2)
                return i;
        }
        counter = 0;
    }
}

// Function to find longest subsequence
// such that GCD of any two distinct
// integers is maximum
int maxlen(int i, int j, int arr[],
           int arr1[], int N, int maxgcd)
{
    int a = 1;

    // Base Cases
    if (i >= N or j >= N)
        return 0;

    // Compare current GCD to the
    // maximum GCD
    if (__gcd(arr[i], arr1[j]) == maxgcd &&
              arr[i] != arr1[j])
    {

        // If true increment and
        // move the pointer
        a = max(a, 1 + maxlen(i, j + 1,
                              arr, arr1,
                              N, maxgcd));
        return a;
    }

    // Return max of either subsequences
    return max(maxlen(i + 1, j, arr,
                      arr1, N, maxgcd),
               maxlen(i, j + 1, arr,
                      arr1, N, maxgcd));
}

// Driver Code
int main()
{
    int arr[] = { 1, 2, 8, 5, 6 };
    int arr1[] = { 1, 2, 8, 5, 6 };

    // Sorted array
    int n = sizeof(arr) / sizeof(arr[0]);

    sort(arr, arr + n);
    sort(arr1, arr1 + n);

    // Function call to calculate GCD of
    // pair with maximum GCD
    int maxgcd = findMaxGCD(arr, n);

    // Print the result
    cout << maxlen(0, 0, arr,
                   arr1, n, maxgcd) + 1;
}

// This code is contributed by ipg2016107
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the
// above approach
import java.util.*;

class GFG{

// Recursive function to
// return gcd of a and b 
static int __gcd(int a,
                 int b) 
{ 
  return b == 0 ?
         a :__gcd(b, a % b);    
}

// Function to find GCD of
// pair with maximum GCD
static int findMaxGCD(int arr[],
                      int N)
{   
  // Stores maximum element
  // of arr[]
  int high = 0;

  // Find the maximum element
  for(int i = 0; i < N; i++)
  {
    high = Math.max(high,
                    arr[i]);
  }

  // Maintain a count array
  int []count = new int[high + 1];

  // Store the frequency of arr[]
  for(int i = 0; i < N; i++)
  {
    count[arr[i]] += 1;
  }

  // Stores the multiples of
  // a number
  int counter = 0;

  // Iterate over the  range
  // [MAX, 1]
  for(int i = high; i > 0; i--)
  {
    int j = i;

    // Iterate from current potential
    // GCD till it is less than MAX
    while (j <= high)
    {
      // A multiple found
      if (count[j] > 0)
        counter += count[j];

      // Increment potential GCD by
      // itself io check i, 2i, 3i...
      j += i;

      // If 2 multiples found max
      // GCD found
      if (counter == 2)
        return i;
    }
    counter = 0;
  }
  return 0;
}

// Function to find longest
// subsequence such that GCD
// of any two distinct integers
// is maximum
static int maxlen(int i, int j,
                  int arr[],
                  int arr1[],
                  int N, int maxgcd)
{
  int a = 1;

  // Base Cases
  if (i >= N || j >= N)
    return 0;

  // Compare current GCD to
  // the maximum GCD
  if (__gcd(arr[i], arr1[j]) == maxgcd &&
      arr[i] != arr1[j])
  {
    // If true increment and
    // move the pointer
    a = Math.max(a, 1 + maxlen(i, j + 1,
                               arr, arr1,
                               N, maxgcd));
    return a;
  }

  // Return max of either subsequences
  return Math.max(maxlen(i + 1, j, arr,
                         arr1, N, maxgcd),
                  maxlen(i, j + 1, arr,
                         arr1, N, maxgcd));
}

// Driver Code
public static void main(String[] args)
{
  int arr[] = {1, 2, 8, 5, 6};
  int arr1[] = {1, 2, 8, 5, 6};

  // Sorted array
  int n = arr.length;

  Arrays.sort(arr);

  // Function call to calculate GCD of
  // pair with maximum GCD
  int maxgcd = findMaxGCD(arr, n);

  // Print the result
  System.out.print(maxlen(0, 0, arr,
                          arr1, n, maxgcd));
}
}

// This code is contributed by gauravrajput1
```

## 蟒蛇 3

```
# Python3 program for the above approach
import math

# Function to find GCD of pair with
# maximum GCD
def findMaxGCD(arr, N):

    # Stores maximum element of arr[]
    high = 0

    # Find the maximum element
    for i in range(0, N):
        high = max(high, arr[i])

    # Maintain a count array
    count = [0] * (high + 1)

    # Store the frequency of arr[]
    for i in range(0, N):
        count[arr[i]] += 1

    # Stores the multiples of a number
    counter = 0

    # Iterate over the  range [MAX, 1]
    for i in range(high, 0, -1):
        j = i

        # Iterate from current potential
        # GCD till it is less than MAX
        while (j <= high):

            # A multiple found
            if (count[j] > 0):
                counter += count[j]

            # Increment potential GCD by
            # itself io check i, 2i, 3i...
            j += i

            # If 2 multiples found max
            # GCD found
            if (counter == 2):
                return i

        counter = 0

# Function to find longest subsequence
# such that GCD of any two distinct
# integers is maximum
def maxlen(i, j):
    a = 0

    # Base Cases
    if i >= N or j >= N:
        return 0

    # Compare current GCD to the
    # maximum GCD
    if math.gcd(arr[i], arr1[j]) == maxgcd and arr[i] != arr1[j]:

        # If true increment and
        # move the pointer
        a = max(a, 1 + maxlen(i, j + 1))
        return a

    # Return max of either subsequences
    return max(maxlen(i + 1, j), maxlen(i, j + 1))

# Drivers Code
arr = [1, 2, 8, 5, 6]

# Sorted array
arr1 = sorted(arr)

# Length of the array
N = len(arr)

# Function call to calculate GCD of
# pair with maximum GCD
maxgcd = findMaxGCD(arr, N)

# Print the result
print(maxlen(0, 0))
```

## C#

```
// C# program for the
// above approach
using System;

class GFG{

// Recursive function to
// return gcd of a and b 
static int __gcd(int a, int b) 
{
  return b == 0 ?
         a :__gcd(b, a % b);    
}

// Function to find GCD of
// pair with maximum GCD
static int findMaxGCD(int []arr,
                      int N)
{   

  // Stores maximum element
  // of []arr
  int high = 0;

  // Find the maximum element
  for(int i = 0; i < N; i++)
  {
    high = Math.Max(high,
                    arr[i]);
  }

  // Maintain a count array
  int []count = new int[high + 1];

  // Store the frequency of []arr
  for(int i = 0; i < N; i++)
  {
    count[arr[i]] += 1;
  }

  // Stores the multiples of
  // a number
  int counter = 0;

  // Iterate over the  range
  // [MAX, 1]
  for(int i = high; i > 0; i--)
  {
    int j = i;

    // Iterate from current potential
    // GCD till it is less than MAX
    while (j <= high)
    {

      // A multiple found
      if (count[j] > 0)
        counter += count[j];

      // Increment potential GCD by
      // itself io check i, 2i, 3i...
      j += i;

      // If 2 multiples found max
      // GCD found
      if (counter == 2)
        return i;
    }
    counter = 0;
  }
  return 0;
}

// Function to find longest
// subsequence such that GCD
// of any two distinct integers
// is maximum
static int maxlen(int i, int j,
                  int []arr,
                  int []arr1,
                  int N, int maxgcd)
{
  int a = 1;

  // Base Cases
  if (i >= N || j >= N)
    return 0;

  // Compare current GCD to
  // the maximum GCD
  if (__gcd(arr[i], arr1[j]) == maxgcd &&
                      arr[i] != arr1[j])
  {

    // If true increment and
    // move the pointer
    a = Math.Max(a, 1 + maxlen(i, j + 1,
                               arr, arr1,
                               N, maxgcd));
    return a;
  }

  // Return max of either subsequences
  return Math.Max(maxlen(i + 1, j, arr,
                         arr1, N, maxgcd),
                  maxlen(i, j + 1, arr,
                         arr1, N, maxgcd));
}

// Driver Code
public static void Main(String[] args)
{
  int []arr = { 1, 2, 8, 5, 6 };
  int []arr1 = { 1, 2, 8, 5, 6 };

  // Sorted array
  int n = arr.Length;

  Array.Sort(arr);

  // Function call to calculate GCD of
  // pair with maximum GCD
  int maxgcd = findMaxGCD(arr, n);

  // Print the result
  Console.Write(maxlen(0, 0, arr,
                       arr1, n, maxgcd));
}
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>
// javascript program for the
// above approach

    // Recursive function to
    // return gcd of a and b
    function __gcd(a , b) {
        return b == 0 ? a : __gcd(b, a % b);
    }

    // Function to find GCD of
    // pair with maximum GCD
    function findMaxGCD(arr, N)
    {

        // Stores maximum element
        // of arr
        var high = 0;

        // Find the maximum element
        for (i = 0; i < N; i++)
        {
            high = Math.max(high, arr[i]);
        }

        // Maintain a count array
        var count = Array(high + 1).fill(0);

        // Store the frequency of arr
        for (i = 0; i < N; i++)
        {
            count[arr[i]] += 1;
        }

        // Stores the multiples of
        // a number
        var counter = 0;

        // Iterate over the range
        // [MAX, 1]
        for (i = high; i > 0; i--)
        {
            var j = i;

            // Iterate from current potential
            // GCD till it is less than MAX
            while (j <= high)
            {

                // A multiple found
                if (count[j] > 0)
                    counter += count[j];

                // Increment potential GCD by
                // itself io check i, 2i, 3i...
                j += i;

                // If 2 multiples found max
                // GCD found
                if (counter == 2)
                    return i;
            }
            counter = 0;
        }
        return 0;
    }

    // Function to find longest
    // subsequence such that GCD
    // of any two distinct integers
    // is maximum
    function maxlen(i , j , arr , arr1 , N , maxgcd)
    {
        var a = 1;

        // Base Cases
        if (i >= N || j >= N)
            return 0;

        // Compare current GCD to
        // the maximum GCD
        if (__gcd(arr[i], arr1[j]) == maxgcd && arr[i] != arr1[j])
        {

            // If true increment and
            // move the pointer
            a = Math.max(a, 1 + maxlen(i, j + 1, arr, arr1, N, maxgcd));
            return a;
        }

        // Return max of either subsequences
        return Math.max(maxlen(i + 1, j, arr, arr1, N, maxgcd), maxlen(i, j + 1, arr, arr1, N, maxgcd));
    }

    // Driver Code

        var arr = [ 1, 2, 8, 5, 6 ];
        var arr1 = [ 1, 2, 8, 5, 6 ];

        // Sorted array
        var n = arr.length;

        arr.sort();

        // Function call to calculate GCD of
        // pair with maximum GCD
        var maxgcd = findMaxGCD(arr, n);

        // Print the result
        document.write(maxlen(0, 0, arr, arr1, n, maxgcd));

// This code is contributed by gauravrajput1.
</script>
```

**Output:** 

```
3
```

***时间复杂度:**O(2<sup>N</sup>)*
***辅助空间:** O(N)*

**高效途径:**对上述途径进行优化，思路是使用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)，因为上述解中有很多[重叠子问题](https://www.geeksforgeeks.org/overlapping-subproblems-property-in-dynamic-programming-dp-1/)，一次次解决。因此，可以通过使用[记忆或制表](https://www.geeksforgeeks.org/tabulation-vs-memoization/)来避免相同子问题的重新计算。使用[字典](https://www.geeksforgeeks.org/python-dictionary/)记住两个索引之间的子序列的最大长度，并在下一次递归调用中使用这些值。以下是步骤:

1.  执行所有上述步骤。
2.  使用[字典](https://www.geeksforgeeks.org/python-dictionary/) **dp** 来存储两个索引之间的子序列的最大长度。
3.  进行递归调用时，只需检查表 **dp[][]** 中的值是否是先前计算的。如果发现是**真**那么使用这个值。否则，调用其他索引范围的函数。
4.  打印经过上述步骤计算的子序列的最大长度。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include<bits/stdc++.h>
using namespace std;

map<pair<int, int>, int>dp;
int maxgcd;
vector<int>arr, arr1;
int N;

// Function to find GCD of pair with
// maximum GCD
int findMaxGCD(vector<int>arr, int  N)
{

    // Stores maximum element of arr[]
    int high = 0;

    // Find the maximum element
    for(int i = 0; i < N; i++)
        high = max(high, arr[i]);

    // Maintain a count array
    int count[high + 1] = {0};

    // Store the frequency of arr[]
    for(int i = 0; i < N; i++)
        count[arr[i]] += 1;

    // Stores the multiples of a number
    int counter = 0;

    // Iterate over the  range [MAX, 1]
    for(int i = high; i > 0; i--)
    {
        int j = i;

        // Iterate from current potential
        // GCD till it is less than MAX
        while (j <= high)
        {

            // A multiple found
            if (count[j] > 0)
                counter += count[j];

            // Increment potential GCD by
            // itself io check i, 2i, 3i...
            j += i;

            // If 2 multiples found max
            // GCD found
            if (counter == 2)
                return i;
        }
        counter = 0;
    }
    return 1;
}

// Function to find longest subsequence
// such that GCD of any two distinct
// integers is maximum
int maxlen(int i, int j)
{
    int  a = 0;

    // Create the key
    // Base Case
    if (i >= N or j >= N)
        return 0;

    // Check if the current state is
    // already calculated
    if (dp[{i, j}])
        return dp[{i, j}];

    // Compare current GCD to the
    // maximum GCD
    if (__gcd(arr[i], arr1[j]) ==
        maxgcd && arr[i] != arr1[j])
    {

        // If true increment and
        // move the pointer
        dp[{i, j}] = 1 + maxlen(i, j + 1);
        return dp[{i, j}];
    }

    // Return max of either subsequences
    return (max(maxlen(i + 1, j),
                maxlen(i, j + 1)));
}

// Driver Code
int main()
{
    arr = { 1, 2, 8, 5, 6 };
    arr1 = arr;

    // Sorted array
    sort(arr1.begin(), arr1.end());

    // Length of the array
    N = arr.size();

    // Function Call
    maxgcd = findMaxGCD(arr, N);

    // Print the result
    cout << (maxlen(0, 0));
}

// This code is contributed by Stream_Cipher
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
import java.awt.Point;
public class Main
{
  static HashMap<Point, Integer> dp = new HashMap<>();
  static int maxgcd, N;
  static Vector<Integer> arr;
  static Vector<Integer> arr1;

  static int __gcd(int a, int b)
  {
    if (b == 0)
      return a;

    return __gcd(b, a % b);
  }

  // Function to find GCD of pair with
  // maximum GCD
  static int findMaxGCD(Vector<Integer> arr, int N)
  {

    // Stores maximum element of arr[]
    int high = 0;

    // Find the maximum element
    for(int i = 0; i < N; i++)
      high = Math.max(high, arr.get(i));

    // Maintain a count array
    int[] count = new int[high + 1];

    // Store the frequency of arr[]
    for(int i = 0; i < N; i++)
      count[arr.get(i)] += 1;

    // Stores the multiples of a number
    int counter = 0;

    // Iterate over the  range [MAX, 1]
    for(int i = high; i > 0; i--)
    {
      int j = i;

      // Iterate from current potential
      // GCD till it is less than MAX
      while (j <= high)
      {

        // A multiple found
        if (count[j] > 0)
          counter += count[j];

        // Increment potential GCD by
        // itself io check i, 2i, 3i...
        j += i;

        // If 2 multiples found max
        // GCD found
        if (counter == 2)
          return i;
      }
      counter = 0;
    }
    return 1;
  }

  // Function to find longest subsequence
  // such that GCD of any two distinct
  // integers is maximum
  static int maxlen(int i, int j)
  {

    // Create the key
    // Base Case
    if (i >= N || j >= N)
      return 0;

    // Check if the current state is
    // already calculated
    if (dp.containsKey(new Point(i, j)))
      return dp.get(new Point(i, j));

    // Compare current GCD to the
    // maximum GCD
    if (__gcd(arr.get(i), arr1.get(j)) ==
        maxgcd && arr.get(i) != arr1.get(j))
    {

      // If true increment and
      // move the pointer
      dp.put(new Point(i, j), 1 + maxlen(i, j + 1));
      return dp.get(new Point(i, j));
    }

    // Return max of either subsequences
    return (Math.max(maxlen(i + 1, j), maxlen(i, j + 1)));
  }

  public static void main(String[] args) {
    arr = new Vector<Integer>();
    arr.add(1);
    arr.add(2);
    arr.add(8);
    arr.add(5);
    arr.add(6);
    arr1 = arr;

    // Sorted array
    Collections.sort(arr1);

    // Length of the array
    N = arr.size();

    // Function Call
    maxgcd = findMaxGCD(arr, N);

    // Print the result
    System.out.println(maxlen(0, 0) + 1);
  }
}

// This code is contributed by divyeshrabadiya07.
```

## 蟒蛇 3

```
# Python3 program for the above approach
import math

# Function to find GCD of pair with
# maximum GCD
def findMaxGCD(arr, N):

    # Stores maximum element of arr[]
    high = 0

    # Find the maximum element
    for i in range(0, N):
        high = max(high, arr[i])

    # Maintain a count array
    count = [0] * (high + 1)

    # Store the frequency of arr[]
    for i in range(0, N):
        count[arr[i]] += 1

    # Stores the multiples of a number
    counter = 0

    # Iterate over the  range [MAX, 1]
    for i in range(high, 0, -1):
        j = i

        # Iterate from current potential
        # GCD till it is less than MAX
        while (j <= high):

            # A multiple found
            if (count[j] > 0):
                counter += count[j]

            # Increment potential GCD by
            # itself io check i, 2i, 3i...
            j += i

            # If 2 multiples found max
            # GCD found
            if (counter == 2):
                return i

        counter = 0

# Function to find longest subsequence
# such that GCD of any two distinct
# integers is maximum
def maxlen(i, j):

    a = 0

    # Create the key
    key = (i, j)

    # Base Case
    if i >= N or j >= N:
        return 0

    # Check if the current state is
    # already calculated
    if key in dp:
        return dp[key]

    # Compare current GCD to the
    # maximum GCD
    if math.gcd(arr[i], arr1[j]) == maxgcd and arr[i] != arr1[j]:

        # If true increment and
        # move the pointer
        dp[key] = 1 + maxlen(i, j + 1)

        return dp[key]

    # Return max of either subsequences
    return max(maxlen(i + 1, j), maxlen(i, j + 1))

# Drivers code
arr = [1, 2, 8, 5, 6]

# Empty dictionary
dp = dict()

# Sorted array
arr1 = sorted(arr)

# Length of the array
N = len(arr)

# Function Call
maxgcd = findMaxGCD(arr, N)

# Print the result
print(maxlen(0, 0))
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

static Dictionary<Tuple<int,
                        int>, int> dp = new Dictionary<Tuple<int,
                                                             int>, int>();
static int maxgcd, N;
static List<int> arr;
static List<int> arr1;

static int __gcd(int a, int b)
{
    if (b == 0)
        return a;

    return __gcd(b, a % b);
}

// Function to find GCD of pair with
// maximum GCD
static int findMaxGCD(List<int> arr, int N)
{

    // Stores maximum element of arr[]
    int high = 0;

    // Find the maximum element
    for(int i = 0; i < N; i++)
        high = Math.Max(high, arr[i]);

    // Maintain a count array
    int[] count = new int[high + 1];

    // Store the frequency of arr[]
    for(int i = 0; i < N; i++)
        count[arr[i]] += 1;

    // Stores the multiples of a number
    int counter = 0;

    // Iterate over the  range [MAX, 1]
    for(int i = high; i > 0; i--)
    {
        int j = i;

        // Iterate from current potential
        // GCD till it is less than MAX
        while (j <= high)
        {

            // A multiple found
            if (count[j] > 0)
                counter += count[j];

            // Increment potential GCD by
            // itself io check i, 2i, 3i...
            j += i;

            // If 2 multiples found max
            // GCD found
            if (counter == 2)
                return i;
        }
        counter = 0;
    }
    return 1;
}

// Function to find longest subsequence
// such that GCD of any two distinct
// integers is maximum
static int maxlen(int i, int j)
{

    // Create the key
    // Base Case
    if (i >= N || j >= N)
        return 0;

    // Check if the current state is
    // already calculated
    if (dp.ContainsKey(new Tuple<int, int>(i, j)))
        return dp[new Tuple<int, int>(i, j)];

    // Compare current GCD to the
    // maximum GCD
    if (__gcd(arr[i], arr1[j]) ==
             maxgcd && arr[i] != arr1[j])
    {

        // If true increment and
        // move the pointer
        dp[new Tuple<int, int>(i, j)] = 1 + maxlen(
                                     i, j + 1);
        return dp[new Tuple<int, int>(i, j)];
    }

    // Return max of either subsequences
    return (Math.Max(maxlen(i + 1, j),
                  maxlen(i, j + 1)));
}

// Driver code
static void Main()
{
    arr = new List<int>(new int[]{ 1, 2, 8, 5, 6 });
    arr1 = arr;

    // Sorted array
    arr1.Sort();

    // Length of the array
    N = arr.Count;

    // Function Call
    maxgcd = findMaxGCD(arr, N);

    // Print the result
    Console.Write(maxlen(0, 0) + 1);
}
}

// This code is contributed by divyesh072019
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

var dp = new Map();
var maxgcd;
var arr = [], arr1 = [];
var N;

// Function to find GCD of pair with
// maximum GCD
function findMaxGCD(arr, N)
{

    // Stores maximum element of arr[]
    var high = 0;

    // Find the maximum element
    for(var i = 0; i < N; i++)
        high = Math.max(high, arr[i]);

    // Maintain a count array
    var count = Array(high+1).fill(0);

    // Store the frequency of arr[]
    for(var i = 0; i < N; i++)
        count[arr[i]] += 1;

    // Stores the multiples of a number
    var counter = 0;

    // Iterate over the  range [MAX, 1]
    for(var i = high; i > 0; i--)
    {
        var j = i;

        // Iterate from current potential
        // GCD till it is less than MAX
        while (j <= high)
        {

            // A multiple found
            if (count[j] > 0)
                counter += count[j];

            // Increment potential GCD by
            // itself io check i, 2i, 3i...
            j += i;

            // If 2 multiples found max
            // GCD found
            if (counter == 2)
                return i;
        }
        counter = 0;
    }
    return 1;
}

function __gcd(a, b)
{
    if (b == 0)
        return a;

    return __gcd(b, a % b);
}

// Function to find longest subsequence
// such that GCD of any two distinct
// integers is maximum
function maxlen(i, j)
{
    var a = 0;

    // Create the key
    // Base Case
    if (i >= N ||  j >= N)
        return 0;

    // Check if the current state is
    // already calculated
    if (dp.has([i, j].toString()))
        return dp.get([i, j].toString());

    // Compare current GCD to the
    // maximum GCD
    if (__gcd(arr[i], arr1[j]) ==
        maxgcd && arr[i] != arr1[j])
    {

        // If true increment and
        // move the pointer
        dp.set([i, j].toString(), 1 + maxlen(i, j + 1));
        return dp.get([i, j].toString());
    }

    // Return max of either subsequences
    return (Math.max(maxlen(i + 1, j),
                maxlen(i, j + 1)));
}

// Driver Code
arr = [1, 2, 8, 5, 6];
arr1 = JSON.parse(JSON.stringify(arr));

// Sorted array
arr1.sort((a,b)=>a-b);

// Length of the array
N = arr.length;

// Function Call
maxgcd = findMaxGCD(arr, N);

// Print the result
document.write(maxlen(0, 0));

</script>
```

**Output:** 

```
3
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(N)*
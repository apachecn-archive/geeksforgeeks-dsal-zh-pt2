# 最大化前 N 个自然数和给定数组的排列的相同索引元素的按位“与”和

> 原文:[https://www . geesforgeks . org/最大化第一个 n 个自然数和给定数组的按位和同索引元素的和/](https://www.geeksforgeeks.org/maximize-sum-of-bitwise-and-of-same-indexed-elements-of-a-permutation-of-first-n-natural-numbers-and-a-given-array/)

给定一个由 **N** 正整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，任务是找出第一个 **N** 自然数和数组 **arr[]** 的[排列的相同索引元素的](https://www.geeksforgeeks.org/find-permutation-of-first-n-natural-numbers-that-satisfies-the-given-condition/)[位与](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)的最大和。

**示例:**

> **输入:** arr[] = {4，2，3，6}
> **输出:** 5
> **解释:**考虑排列{1，0，3，2}。上述排列与给定数组的按位 AND 之和= 1&4+0&2+3&3+2&6 = 0+0+3+2 = 5，在所有排列中最大。
> 
> **输入:** arr[] = {3，4，1，0，5}
> **输出:** 8

**方法:**解决给定问题的思路是[生成第一个 **N 个**自然数](https://www.geeksforgeeks.org/heaps-algorithm-for-generating-permutations/)的所有排列，并用数组**arr【】**计算生成排列的[位与](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)之和。检查每个排列后，打印得到的**位与**之和的最大值。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to calculate sum of
// Bitwise AND of same indexed
// elements of the arrays p[] and arr[]
int calcScore(vector<int> p, int arr[], int N)
{

    // Stores the resultant sum
    int ans = 0;

    // Traverse the array
    for (int i = 0; i < N; i++) {

        // Update sum of Bitwise AND
        ans += (p[i] & arr[i]);
    }

    // Return the value obtained
    return ans;
}

// Function to generate all permutations
// and calculate the maximum sum of Bitwise
// AND of same indexed elements present in
// any permutation and an array arr[]
int getMaxUtil(vector<int> p, int arr[], int ans,
               bool chosen[], int N)
{

    // If the size of the array is N
    if (p.size() == N) {

        // Calculate cost of permutation
        ans = max(ans, calcScore(p, arr, N));

        return ans;
    }

    // Generate all permutations
    for (int i = 0; i < N; i++) {

        if (chosen[i]) {
            continue;
        }

        // Update chosen[i]
        chosen[i] = true;

        // Update the permutation p[]
        p.push_back(i);

        // Generate remaining permutations
        ans = getMaxUtil(p, arr, ans, chosen, N);

        chosen[i] = false;

        p.pop_back();
    }

    // Return the resultant sum
    return ans;
}

// Function to find the maximum sum of Bitwise
// AND of same indexed elements in a permutation
// of first N natural numbers and arr[]
void getMax(int arr[], int N)
{

    // Stores the resultant maximum sum
    int ans = 0;

    bool chosen[N];
    for (int i = 0; i < N; i++)
        chosen[i] = false;

    // Stores the generated permutation P
    vector<int> p;

    // Function call to store result
    int res = getMaxUtil(p, arr, ans, chosen, N);

    // Print the result
    cout << res;
}

// Driven Program
int main()
{
    int arr[] = { 4, 2, 3, 6 };
    int N = sizeof(arr) / sizeof(arr[0]);

    // Function call
    getMax(arr, N);

    return 0;
}

// This code is contributed by Kingash.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.lang.*;
import java.util.*;

class GFG {

  // Function to calculate sum of
  // Bitwise AND of same indexed
  // elements of the arrays p[] and arr[]
  static int calcScore(ArrayList<Integer> p, int arr[])
  {

    // Stores the resultant sum
    int ans = 0;

    // Traverse the array
    for (int i = 0; i < arr.length; i++) {

      // Update sum of Bitwise AND
      ans += (p.get(i) & arr[i]);
    }

    // Return the value obtained
    return ans;
  }

  // Function to generate all permutations
  // and calculate the maximum sum of Bitwise
  // AND of same indexed elements present in
  // any permutation and an array arr[]
  static int getMaxUtil(ArrayList<Integer> p, int arr[],
                        int ans, boolean chosen[], int N)
  {

    // If the size of the array is N
    if (p.size() == N) {

      // Calculate cost of permutation
      ans = Math.max(ans, calcScore(p, arr));

      return ans;
    }

    // Generate all permutations
    for (int i = 0; i < N; i++) {

      if (chosen[i]) {
        continue;
      }

      // Update chosen[i]
      chosen[i] = true;

      // Update the permutation p[]
      p.add(i);

      // Generate remaining permutations
      ans = getMaxUtil(p, arr, ans, chosen, N);

      chosen[i] = false;

      p.remove(p.size() - 1);
    }

    // Return the resultant sum
    return ans;
  }

  // Function to find the maximum sum of Bitwise
  // AND of same indexed elements in a permutation
  // of first N natural numbers and arr[]
  static void getMax(int arr[], int N)
  {

    // Stores the resultant maximum sum
    int ans = 0;

    boolean chosen[] = new boolean[N];

    // Stores the generated permutation P
    ArrayList<Integer> p = new ArrayList<>();

    // Function call to store result
    int res = getMaxUtil(p, arr, ans, chosen, N);

    // Print the result
    System.out.println(res);
  }

  // Driver Code
  public static void main(String[] args)
  {

    int arr[] = { 4, 2, 3, 6 };
    int N = arr.length;

    // Function Call
    getMax(arr, N);
  }
}

// This code is contributed by Kingash.
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to calculate sum of
# Bitwise AND of same indexed
# elements of the arrays p[] and arr[]
def calcScore(p, arr):

    # Stores the resultant sum
    ans = 0

    # Traverse the array
    for i in range(len(arr)):

        # Update sum of Bitwise AND
        ans += (p[i] & arr[i])

    # Return the value obtained
    return ans

# Function to generate all permutations
# and calculate the maximum sum of Bitwise
# AND of same indexed elements present in
# any permutation and an array arr[]
def getMaxUtil(p, arr, ans, chosen, N):

    # If the size of the array is N
    if len(p) == N:

        # Calculate cost of permutation
        ans = max(ans, calcScore(p, arr))

        return ans

    # Generate all permutations
    for i in range(N):

        if chosen[i]:
            continue

        # Update chosen[i]
        chosen[i] = True

        # Update the permutation p[]
        p.append(i)

        # Generate remaining permutations
        ans = getMaxUtil(p, arr, ans, chosen, N)

        chosen[i] = False

        p.pop()

    # Return the resultant sum
    return ans

# Function to find the maximum sum of Bitwise
# AND of same indexed elements in a permutation
# of first N natural numbers and arr[]
def getMax(arr, N):

    # Stores the resultant maximum sum
    ans = 0

    chosen = [False for i in range(N)]

    # Stores the generated permutation P
    p = []

    # Function call to store result
    res = getMaxUtil(p, arr, ans, chosen, N)

    # Print the result
    print(res)

# Driver Code
if __name__ == '__main__':

    # Given array
    arr = [4, 2, 3, 6]
    N = len(arr)

    # Function Call
    getMax(arr, N)
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to calculate sum of
// Bitwise AND of same indexed
// elements of the arrays p[] and arr[]
static int calcScore(List<int> p, int[] arr)
{

    // Stores the resultant sum
    int ans = 0;

    // Traverse the array
    for(int i = 0; i < arr.Length; i++)
    {

        // Update sum of Bitwise AND
        ans += (p[i] & arr[i]);
    }

    // Return the value obtained
    return ans;
}

// Function to generate all permutations
// and calculate the maximum sum of Bitwise
// AND of same indexed elements present in
// any permutation and an array arr[]
static int getMaxUtil(List<int> p, int[] arr,
                           int ans, bool[] chosen,
                           int N)
{

    // If the size of the array is N
    if (p.Count == N)
    {

        // Calculate cost of permutation
        ans = Math.Max(ans, calcScore(p, arr));

        return ans;
    }

    // Generate all permutations
    for(int i = 0; i < N; i++)
    {
        if (chosen[i])
        {
            continue;
        }

        // Update chosen[i]
        chosen[i] = true;

        // Update the permutation p[]
        p.Add(i);

        // Generate remaining permutations
        ans = getMaxUtil(p, arr, ans, chosen, N);

        chosen[i] = false;

        p.Remove(p.Count - 1);
    }

    // Return the resultant sum
    return ans;
}

// Function to find the maximum sum of Bitwise
// AND of same indexed elements in a permutation
// of first N natural numbers and arr[]
static void getMax(int[] arr, int N)
{

    // Stores the resultant maximum sum
    int ans = 0;

    bool[] chosen = new bool[N];

    // Stores the generated permutation P
    List<int> p = new List<int>();

    // Function call to store result
    int res = getMaxUtil(p, arr, ans, chosen, N);

    // Print the result
    Console.Write(res);
}

// Driver Code
public static void Main()
{
    int[] arr = { 4, 2, 3, 6 };
    int N = arr.Length;

    // Function Call
    getMax(arr, N);
}
}

// This code is contributed by sanjoy_62
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to calculate sum of
// Bitwise AND of same indexed
// elements of the arrays p[] and arr[]
function calcScore(p, arr, N)
{

    // Stores the resultant sum
    var ans = 0;

    // Traverse the array
    for (var i = 0; i < N; i++) {

        // Update sum of Bitwise AND
        ans += (p[i] & arr[i]);
    }

    // Return the value obtained
    return ans;
}

// Function to generate all permutations
// and calculate the maximum sum of Bitwise
// AND of same indexed elements present in
// any permutation and an array arr[]
function getMaxUtil(p, arr, ans, chosen, N)
{

    // If the size of the array is N
    if (p.length == N) {

        // Calculate cost of permutation
        ans = Math.max(ans, calcScore(p, arr, N));

        return ans;
    }

    // Generate all permutations
    for (var i = 0; i < N; i++) {

        if (chosen[i]) {
            continue;
        }

        // Update chosen[i]
        chosen[i] = true;

        // Update the permutation p[]
        p.push(i);

        // Generate remaining permutations
        ans = getMaxUtil(p, arr, ans, chosen, N);

        chosen[i] = false;

        p.pop();
    }

    // Return the resultant sum
    return ans;
}

// Function to find the maximum sum of Bitwise
// AND of same indexed elements in a permutation
// of first N natural numbers and arr[]
function getMax(arr, N)
{

    // Stores the resultant maximum sum
    var ans = 0;

    var chosen = Array(N).fill(false);

    // Stores the generated permutation P
    var p = [];

    // Function call to store result
    var res = getMaxUtil(p, arr, ans, chosen, N);

    // Print the result
    document.write( res);
}

// Driven Program
var arr = [ 4, 2, 3, 6 ];
var N = arr.length;
// Function call
getMax(arr, N);

</script>
```

**Output:** 

```
5
```

***时间复杂度:** O(N*N！)*
***辅助空间:** O(N)*
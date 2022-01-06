# 仅去除一个元素形成的最长斐波那契子阵列的长度

> 原文:[https://www . geeksforgeeks . org/最长斐波那契子数组长度-仅移除一个元素形成/](https://www.geeksforgeeks.org/length-of-longest-fibonacci-subarray-formed-by-removing-only-one-element/)

给定一个包含整数的数组 **A** ，任务是找出通过从数组中只移除一个元素而形成的最长斐波那契子数组的长度。
**例:**

> **输入:** arr[] = { 2，8，5，7，3，5，7 }
> **输出:** 5
> **解释:**
> 如果我们去掉索引 3 处的数字 7，那么剩下的数组包含一个长度为 5 的斐波那契子数组{ 2，8，5，3，5}，这是最大值。
> **输入:** arr[] = { 2，3，6，1 }
> **输出:** 3
> **解释:**
> 如果我们去掉索引 2 处的数字 6，那么剩下的数组包含一个长度为 3 的斐波那契子数组{ 2，3，1 }，这是最大值。

**方法:**上述问题可以通过计算每个指数之前和之后的连续斐波那契数来解决。

1.  现在再次遍历数组，找到一个前后斐波那契数最大的索引。
2.  为了检查[斐波那契数](https://www.geeksforgeeks.org/program-for-nth-fibonacci-number/)，我们将构建一个包含数组中所有小于或等于最大值的斐波那契数的[哈希表](https://www.geeksforgeeks.org/hashing-set-1-introduction/)，以在 O(1)时间内测试一个数。

**以下是上述方法的实施:**

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ program to find length of the longest
// subarray with all fibonacci numbers

#include <bits/stdc++.h>
using namespace std;
#define N 100000

// Function to create hash table
// to check for Fibonacci numbers
void createHash(set<int>& hash,
                int maxElement)
{

    // Insert first two fibnonacci numbers
    int prev = 0, curr = 1;

    hash.insert(prev);
    hash.insert(curr);

    while (curr <= maxElement) {

        // Summation of last two numbers
        int temp = curr + prev;

        hash.insert(temp);

        // Update the variable each time
        prev = curr;
        curr = temp;
    }
}

// Function to find the
// longest fibonacci subarray
int longestFibSubarray(
    int arr[], int n)
{

    // Find maximum value in the array
    int max_val
        = *max_element(arr, arr + n);

    // Creating a set
    // containing Fibonacci numbers
    set<int> hash;

    createHash(hash, max_val);

    int left[n], right[n];
    int fibcount = 0, res = -1;

    // Left array is used to count number of
    // continuous fibonacci numbers starting
    // from left of current element
    for (int i = 0; i < n; i++) {

        left[i] = fibcount;

        // Check if current element
        // is a fibonacci number
        if (hash.find(arr[i])
            != hash.end()) {
            fibcount++;
        }

        else
            fibcount = 0;
    }

    // Right array is used to count number of
    // continuous fibonacci numbers starting
    // from right of current element
    fibcount = 0;

    for (int i = n - 1; i >= 0; i--) {

        right[i] = fibcount;

        // Check if current element
        // is a fibonacci number
        if (hash.find(arr[i])
            != hash.end()) {
            fibcount++;
        }
        else
            fibcount = 0;
    }

    for (int i = 0; i < n; i++)
        res = max(
            res,
            left[i] + right[i]);

    return res;
}

// Driver code
int main()
{

    int arr[] = { 2, 8, 5, 7, 3, 5, 7 };
    int n = sizeof(arr) / sizeof(arr[0]);

    cout << longestFibSubarray(arr, n)
         << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find length of the longest
// subarray with all fibonacci numbers
import java.util.*;

class GFG{
static final int N = 100000;

// Function to create hash table
// to check for Fibonacci numbers
static void createHash(HashSet<Integer> hash,
                int maxElement)
{

    // Insert first two fibnonacci numbers
    int prev = 0, curr = 1;

    hash.add(prev);
    hash.add(curr);

    while (curr <= maxElement) {

        // Summation of last two numbers
        int temp = curr + prev;

        hash.add(temp);

        // Update the variable each time
        prev = curr;
        curr = temp;
    }
}

// Function to find the
// longest fibonacci subarray
static int longestFibSubarray(
    int arr[], int n)
{

    // Find maximum value in the array
    int max_val = Arrays.stream(arr).max().getAsInt();

    // Creating a set
    // containing Fibonacci numbers
    HashSet<Integer> hash = new HashSet<Integer>();

    createHash(hash, max_val);

    int []left = new int[n];
    int []right = new int[n];
    int fibcount = 0, res = -1;

    // Left array is used to count number of
    // continuous fibonacci numbers starting
    // from left of current element
    for (int i = 0; i < n; i++) {

        left[i] = fibcount;

        // Check if current element
        // is a fibonacci number
        if (hash.contains(arr[i])) {
            fibcount++;
        }

        else
            fibcount = 0;
    }

    // Right array is used to count number of
    // continuous fibonacci numbers starting
    // from right of current element
    fibcount = 0;

    for (int i = n - 1; i >= 0; i--) {

        right[i] = fibcount;

        // Check if current element
        // is a fibonacci number
        if (hash.contains(arr[i])) {
            fibcount++;
        }
        else
            fibcount = 0;
    }

    for (int i = 0; i < n; i++)
        res = Math.max(
            res,
            left[i] + right[i]);

    return res;
}

// Driver code
public static void main(String[] args)
{

    int arr[] = { 2, 8, 5, 7, 3, 5, 7 };
    int n = arr.length;

    System.out.print(longestFibSubarray(arr, n)
         +"\n");

}
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 program to find length of the longest
# subarray with all fibonacci numbers

N = 100000

# Function to create hash table
# to check for Fibonacci numbers
def createHash(hash, maxElement) :

    # Insert first two fibnonacci numbers
    prev = 0
    curr = 1

    hash.add(prev)
    hash.add(curr)

    while (curr <= maxElement) :

        # Summation of last two numbers
        temp = curr + prev

        hash.add(temp)

        # Update the variable each time
        prev = curr
        curr = temp

# Function to find the
# longest fibonacci subarray 
def longestFibSubarray(arr, n) :

    # Find maximum value in the array
    max_val = max(arr)

    # Creating a set
    # containing Fibonacci numbers
    hash = {int}

    createHash(hash, max_val)

    left = [ 0 for i in range(n)]

    right = [ 0 for i in range(n)]

    fibcount = 0
    res = -1

    # Left array is used to count number of
    # continuous fibonacci numbers starting
    # from left of current element
    for i in range(n) :

        left[i] = fibcount

        # Check if current element
        # is a fibonacci number
        if (arr[i] in hash) :
            fibcount += 1
        else:
            fibcount = 0

    # Right array is used to count number of
    # continuous fibonacci numbers starting
    # from right of current element
    fibcount = 0

    for i in range(n-1,-1,-1) :

        right[i] = fibcount

        # Check if current element
        # is a fibonacci number
        if (arr[i] in hash) :
            fibcount += 1
        else:
            fibcount = 0

    for i in range(0,n) :
        res = max(res, left[i] + right[i])

    return res

# Driver code
arr = [ 2, 8, 5, 7, 3, 5, 7 ]
n = len(arr)
print(longestFibSubarray(arr, n))

# This code is contributed by Sanjit_Prasad
```

## C#

```
// C# program to find length of the longest
// subarray with all fibonacci numbers
using System;
using System.Linq;
using System.Collections.Generic;

class GFG{
static readonly int N = 100000;

// Function to create hash table
// to check for Fibonacci numbers
static void createHash(HashSet<int> hash,
                int maxElement)
{

    // Insert first two fibnonacci numbers
    int prev = 0, curr = 1;

    hash.Add(prev);
    hash.Add(curr);

    while (curr <= maxElement) {

        // Summation of last two numbers
        int temp = curr + prev;

        hash.Add(temp);

        // Update the variable each time
        prev = curr;
        curr = temp;
    }
}

// Function to find the
// longest fibonacci subarray
static int longestFibSubarray(
    int []arr, int n)
{

    // Find maximum value in the array
    int max_val = arr.Max();

    // Creating a set
    // containing Fibonacci numbers
    HashSet<int> hash = new HashSet<int>();

    createHash(hash, max_val);

    int []left = new int[n];
    int []right = new int[n];
    int fibcount = 0, res = -1;

    // Left array is used to count number of
    // continuous fibonacci numbers starting
    // from left of current element
    for (int i = 0; i < n; i++) {

        left[i] = fibcount;

        // Check if current element
        // is a fibonacci number
        if (hash.Contains(arr[i])) {
            fibcount++;
        }

        else
            fibcount = 0;
    }

    // Right array is used to count number of
    // continuous fibonacci numbers starting
    // from right of current element
    fibcount = 0;

    for (int i = n - 1; i >= 0; i--) {

        right[i] = fibcount;

        // Check if current element
        // is a fibonacci number
        if (hash.Contains(arr[i])) {
            fibcount++;
        }
        else
            fibcount = 0;
    }

    for (int i = 0; i < n; i++)
        res = Math.Max(
            res,
            left[i] + right[i]);

    return res;
}

// Driver code
public static void Main(String[] args)
{

    int []arr = { 2, 8, 5, 7, 3, 5, 7 };
    int n = arr.Length;

    Console.Write(longestFibSubarray(arr, n)
         +"\n"); 
}
}

// This code is contributed by sapnasingh4991
```

## java 描述语言

```
<script>

// Javascript program to find length of the longest
// subarray with all fibonacci numbers

let N = 100000;

// Function to create hash table
// to check for Fibonacci numbers
function createHash( hash, maxElement)
{

    // Insert first two fibnonacci numbers
    let prev = 0, curr = 1;

    hash.add(prev);
    hash.add(curr);

    while (curr <= maxElement) {

        // Summation of last two numbers
        let temp = curr + prev;

        hash.add(temp);

        // Update the variable each time
        prev = curr;
        curr = temp;
    }
}

// Function to find the
// longest fibonacci subarray
function longestFibSubarray(arr, n)
{

    // Find maximum value in the array
    let max_val = Math.max(...arr);

    // Creating a set
    // containing Fibonacci numbers
    let hash = new Set();

    createHash(hash, max_val);

    let left = Array.from({length: n}, (_, i) => 0);
    let right = Array.from({length: n}, (_, i) => 0);
    let fibcount = 0, res = -1;

    // Left array is used to count number of
    // continuous fibonacci numbers starting
    // from left of current element
    for (let i = 0; i < n; i++) {

        left[i] = fibcount;

        // Check if current element
        // is a fibonacci number
        if (hash.has(arr[i])) {
            fibcount++;
        }

        else
            fibcount = 0;
    }

    // Right array is used to count number of
    // continuous fibonacci numbers starting
    // from right of current element
    fibcount = 0;

    for (let i = n - 1; i >= 0; i--) {

        right[i] = fibcount;

        // Check if current element
        // is a fibonacci number
        if (hash.has(arr[i])) {
            fibcount++;
        }
        else
            fibcount = 0;
    }

    for (let i = 0; i < n; i++)
        res = Math.max(
            res,
            left[i] + right[i]);

    return res;
}

// Driver code

      let arr = [ 2, 8, 5, 7, 3, 5, 7 ];
    let n = arr.length;

    document.write(longestFibSubarray(arr, n)
         +"<br/>");

 // This code is contributed by sanjoy_62.
</script>
```

**Output:** 

```
5
```
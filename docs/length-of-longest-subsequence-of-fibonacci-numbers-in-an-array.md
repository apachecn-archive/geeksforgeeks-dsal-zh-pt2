# 数组中斐波那契数最长子序列的长度

> 原文:[https://www . geesforgeks . org/Fibonacci 数组中最长子序列的长度/](https://www.geeksforgeeks.org/length-of-longest-subsequence-of-fibonacci-numbers-in-an-array/)

给定一个包含非负整数的数组 **arr** ，任务是打印这个数组中[斐波那契数](https://www.geeksforgeeks.org/program-for-nth-fibonacci-number/)的最长子序列的长度。
**例:**

> **输入:** arr[] = { 3，4，11，2，9，21 }
> **输出:** 3
> 这里，子序列是{ 3，2，21 }，因此答案是 3。
> **输入:** arr[] = { 6，4，10，13，9，25 }
> **输出:** 1
> 这里，子序列是{1}，因此答案是 1。

**进场:**

*   构建包含所有[斐波那契数](https://www.geeksforgeeks.org/program-for-nth-fibonacci-number/)的[哈希表](https://www.geeksforgeeks.org/hashing-set-1-introduction/)，该哈希表将用于在 0(1)时间内测试一个数。
*   现在，我们将遍历给定的数组。
*   我们将包括在遍历最长子序列时遇到的所有斐波那契数，因此每次遇到斐波那契数时，答案都会增加 1。
*   一旦遇到了整个初始数组，我们就有了只包含斐波那契数的最长子序列的长度。

以下是上述方法的实现:

## C++

```
// C++ program to find the length
// of longest subsequence of
// Fibonacci Numbers in an Array

#include <bits/stdc++.h>
using namespace std;
#define N 100005

// Function to create hash table
// to check Fibonacci numbers
void createHash(set<int>& hash,
                int maxElement)
{
    int prev = 0, curr = 1;
    hash.insert(prev);
    hash.insert(curr);

    while (curr <= maxElement) {
        int temp = curr + prev;
        hash.insert(temp);
        prev = curr;
        curr = temp;
    }
}

// Function to find the longest
// subsequence containing
// all Fibonacci numbers
int longestFibonacciSubsequence(
    int arr[], int n)
{
    set<int> hash;
    createHash(
        hash,
        *max_element(arr, arr + n));

    int answer = 0;

    for (int i = 0; i < n; i++) {
        if (hash.find(arr[i])
            != hash.end()) {
            answer++;
        }
    }

    return answer;
}

// Driver code
int main()
{
    int arr[] = { 3, 4, 11, 2, 9, 21 };
    int n = sizeof(arr) / sizeof(arr[0]);

    // Function call
    cout << longestFibonacciSubsequence(arr, n)
         << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the length
// of longest subsequence of
// Fibonacci Numbers in an Array
import java.util.*;

class GFG{
static final int N = 100005;

// Function to create hash table
// to check Fibonacci numbers
static void createHash(HashSet<Integer> hash,
                int maxElement)
{
    int prev = 0, curr = 1;
    hash.add(prev);
    hash.add(curr);

    while (curr <= maxElement) {
        int temp = curr + prev;
        hash.add(temp);
        prev = curr;
        curr = temp;
    }
}

// Function to find the longest
// subsequence containing
// all Fibonacci numbers
static int longestFibonacciSubsequence(
    int arr[], int n)
{
    HashSet<Integer> hash = new HashSet<Integer>();
    createHash(
        hash,Arrays.stream(arr).max().getAsInt());

    int answer = 0;

    for (int i = 0; i < n; i++) {
        if (hash.contains(arr[i])) {
            answer++;
        }
    }

    return answer;
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 3, 4, 11, 2, 9, 21 };
    int n = arr.length;

    // Function call
    System.out.print(longestFibonacciSubsequence(arr, n)
         +"\n");

}
}

// This code contributed by Princi Singh
```

## 蟒蛇 3

```
# Python 3 program to find the length
# of longest subsequence of
# Fibonacci Numbers in an Array

N = 100005

# Function to create hash table
# to check Fibonacci numbers
def createHash(hash,maxElement):
    prev = 0
    curr = 1
    hash.add(prev)
    hash.add(curr)

    while (curr <= maxElement):
        temp = curr + prev
        hash.add(temp)
        prev = curr
        curr = temp

# Function to find the longest
# subsequence containing
# all Fibonacci numbers
def longestFibonacciSubsequence(arr, n):
    hash = set()
    createHash(hash,max(arr))

    answer = 0

    for i in range(n):
        if (arr[i] in hash):
            answer += 1

    return answer

# Driver code
if __name__ == '__main__':
    arr = [3, 4, 11, 2, 9, 21]
    n = len(arr)

    # Function call
    print(longestFibonacciSubsequence(arr, n))

# This code is contributed by Surendra_Gangwar
```

## C#

```
// C# program to find the length
// of longest subsequence of
// Fibonacci Numbers in an Array
using System;
using System.Linq;
using System.Collections.Generic;

class GFG{
static readonly int N = 100005;

// Function to create hash table
// to check Fibonacci numbers
static void createHash(HashSet<int> hash,
                int maxElement)
{
    int prev = 0, curr = 1;
    hash.Add(prev);
    hash.Add(curr);

    while (curr <= maxElement) {
        int temp = curr + prev;
        hash.Add(temp);
        prev = curr;
        curr = temp;
    }
}

// Function to find the longest
// subsequence containing
// all Fibonacci numbers
static int longestFibonacciSubsequence(
    int []arr, int n)
{
    HashSet<int> hash = new HashSet<int>();
    createHash(hash,arr.Max());

    int answer = 0;

    for (int i = 0; i < n; i++) {
        if (hash.Contains(arr[i])) {
            answer++;
        }
    }

    return answer;
}

// Driver code
public static void Main(String[] args)
{
    int []arr = { 3, 4, 11, 2, 9, 21 };
    int n = arr.Length;

    // Function call
    Console.Write(longestFibonacciSubsequence(arr, n)
         +"\n");
}
}

// This code is contributed by sapnasingh4991
```

## java 描述语言

```
<script>

// Javascript program to find the length
// of longest subsequence of
// Fibonacci Numbers in an Array

let N = 100005;

// Function to create hash table
// to check Fibonacci numbers
function createHash(hash, maxElement)
{
    let prev = 0, curr = 1;
    hash.add(prev);
    hash.add(curr);

    while (curr <= maxElement) {
        let temp = curr + prev;
        hash.add(temp);
        prev = curr;
        curr = temp;
    }
}

// Function to find the longest
// subsequence containing
// all Fibonacci numbers
function longestFibonacciSubsequence(arr, n)
{
    let hash = new Set();
    createHash(hash, Math.max(...arr));

    let answer = 0;

    for (let i = 0; i < n; i++) {
        if (hash.has(arr[i])) {
            answer++;
        }
    }

    return answer;
}

// Driver code   
      let arr = [ 3, 4, 11, 2, 9, 21 ];
    let n = arr.length;

    // Function call
    document.write(longestFibonacciSubsequence(arr, n)
         +"\n");

  // This code is contributed by sanjoy_62.
</script>
```

**Output:** 

```
3
```
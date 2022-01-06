# 在 N 个整数的数组中找到一个非空子集，使得子集的元素之和可以被 N 整除

> 原文:[https://www . geesforgeks . org/find-a-n 整数数组中的非空子集-这样子集的元素和就可以被 n 整除/](https://www.geeksforgeeks.org/find-a-non-empty-subset-in-an-array-of-n-integers-such-that-sum-of-elements-of-subset-is-divisible-by-n/)

给定一个由 N 个整数组成的数组，任务是找到一个非空子集，使得该子集的元素之和可被 N 整除。输出任何这样的子集及其大小和原始数组中元素的索引(基于 1 的索引)，如果它存在的话。
**先决条件:** [鸽子洞原理](https://www.geeksforgeeks.org/discrete-mathematics-the-pigeonhole-principle/)
**示例:**

```
Input: arr[] = { 2, 3, 7, 1, 9 }
Output: 2
        1 2
The required subset is { 2, 3 } whose indices are 1 and 2.

Input: arr[] = {2, 11, 4}
Output: 2
        2 3 
```

一种简单的方法是使用给定数组的[幂集](https://www.geeksforgeeks.org/power-set/)生成所有可能的子集，计算它们各自的和，并检查和是否可被 N 整除。
**时间复杂度:** O(2 <sup>N</sup> * N)，O(2 <sup>N</sup> )用于生成所有子集，O(N)用于计算每个子集的和。
**有效方法:**考虑前缀和，我们得到:

> prefixSum<sub>0</sub>= arr<sub>0</sub>
> prefixSum<sub>1</sub>= arr<sub>0</sub>+arr<sub>1</sub>T11】prefixSum<sub>2</sub>= arr<sub>0</sub>+arr<sub>1</sub>+arr<sub>2</sub>T20】……
> prefixSum<sub>N</sub>= arr<sub>0 <sub>L</sub>+arr<sub>L+1</sub>+…+arr<sub>R</sub>(L≤R)等于 prefixSum<sub>R</sub>–
> prefixSum<sub>L-1</sub>。 如果任意连续子段的和可被 N 整除，则
> 表示取 prefixSum<sub>R</sub>–prefixSum<sub>L-1</sub>
> 的模 N 后的余数为零，即
> (prefixSum<sub>R</sub>–prefixSum<sub>L-1</sub>)% N = 0；
> 拆分模，
> 前缀<sub>R</sub>% N–前缀 <sub>L-1</sub> % N = 0
> 前缀 <sub>R</sub> % N =前缀 <sub>L-1</sub> % N</sub>

因为 N (0，1，2 … N-2，N-1)有(N)个前缀和 N 个可能的残基。因此，根据鸽子洞原理，总是存在一个相邻的亚段，其前缀末端相等。如果在任何情况下，前缀 <sub>L</sub> ，那么前 L 个索引将给出子集。
以下是上述办法的实施情况:

## C++

```
// CPP Program to find Non empty
// subset such that its elements' sum
// is divisible by N
#include <bits/stdc++.h>
using namespace std;

// Function to print the subset index and size
void findNonEmptySubset(int arr[], int N)
{

    // Hash Map to store the indices of residue upon
    // taking modulo N of prefixSum
    unordered_map<int, int> mp;

    int sum = 0;
    for (int i = 0; i < N; i++) {
        // Calculating the residue of prefixSum
        sum = (sum + arr[i]) % N;

        // If the pre[i]%n==0
        if (sum == 0) {
            // print size
            cout << i + 1 << endl;

            // Print the first i indices
            for (int j = 0; j <= i; j++)
                cout << j + 1 << " ";
            return;
        }

        // If this sum was seen earlier, then
        // the contiguous subsegment has been found
        if (mp.find(sum) != mp.end()) {
            // Print the size of subset
            cout << (i - mp[sum]) << endl;

            // Print the indices of contiguous subset
            for (int j = mp[sum] + 1; j <= i; j++)
                cout << j + 1 << " ";

            return;
        }
        else
            mp[sum] = i;
    }
}

// Driver Code
int main()
{
    int arr[] = { 2, 3, 7, 1, 9 };
    int N = sizeof(arr) / sizeof(arr[0]);

    findNonEmptySubset(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to find Non
// empty subset such that
// its elements' sum is
// divisible by N
import java.io.*;
import java.util.HashMap;
import java.util.Map.Entry;
import java.util.Map;
import java.lang.*;

class GFG
{

// Function to print the
// subset index and size
static void findNonEmptySubset(int arr[],
                               int N)
{

    // Hash Map to store the
    // indices of residue upon
    // taking modulo N of prefixSum
    HashMap<Integer, Integer> mp =
                new HashMap<Integer, Integer>();

    int sum = 0;
    for (int i = 0; i < N; i++)
    {
        // Calculating the
        // residue of prefixSum
        sum = (sum + arr[i]) % N;

        // If the pre[i]%n==0
        if (sum == 0)
        {
            // print size
            System.out.print(i + 1 + "\n");

            // Print the first i indices
            for (int j = 0; j <= i; j++)
                System.out.print(j + 1 + " ");
            return;
        }

        // If this sum was seen
        // earlier, then the
        // contiguous subsegment
        // has been found
        if (mp.containsKey(sum) == true)
        {
            // Print the size of subset
            System.out.println((i -
                              mp.get(sum)));

            // Print the indices of
            // contiguous subset
            for (int j = mp.get(sum) + 1;
                     j <= i; j++)
                System.out.print(j + 1 + " ");

            return;
        }
        else
            mp.put(sum,i);
    }
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 2, 3, 7, 1, 9 };
    int N = arr.length;

    findNonEmptySubset(arr, N);
}
}
```

## 蟒蛇 3

```
# Python3 Program to find Non
# empty subset such that its
# elements' sum is divisible
# by N

# Function to print the subset
# index and size
def findNonEmptySubset(arr, N):

    # Hash Map to store the indices
    # of residue upon taking modulo
    # N of prefixSum
    mp = {}

    Sum = 0
    for i in range(N):
        # Calculating the residue of
        # prefixSum
        Sum = (Sum + arr[i]) % N

        # If the pre[i]%n==0
        if (Sum == 0) :
            # print size
            print(i + 1)

            # Print the first i indices
            for j in range(i + 1):
                print(j + 1, end = " ")
            return

        # If this sum was seen earlier,
        # then the contiguous subsegment
        # has been found
        if Sum in mp :

            # Print the size of subset
            print((i - mp[Sum]))

            # Print the indices of contiguous
            # subset
            for j in range(mp[Sum] + 1,
                           i + 1):
                print(j + 1, end = " ")

            return
        else:
            mp[Sum] = i

# Driver code
arr = [2, 3, 7, 1, 9]
N = len(arr)
findNonEmptySubset(arr, N)

# This code is contributed by divyeshrabadiya07
```

## C#

```
// C# Program to find Non
// empty subset such that
// its elements' sum is
// divisible by N

using System;
using System.Collections ;

class GFG
{    
    // Function to print the
    // subset index and size
    static void findNonEmptySubset(int []arr, int N)
    {

        // Hash Map to store the
        // indices of residue upon
        // taking modulo N of prefixSum
        Hashtable mp = new Hashtable();

        int sum = 0;
        for (int i = 0; i < N; i++)
        {
            // Calculating the
            // residue of prefixSum
            sum = (sum + arr[i]) % N;

            // If the pre[i]%n==0
            if (sum == 0)
            {
                // print size
                Console.Write(i + 1 + "\n");

                // Print the first i indices
                for (int j = 0; j <= i; j++)
                    Console.Write(j + 1 + " ");
                return;
            }

            // If this sum was seen
            // earlier, then the
            // contiguous subsegment
            // has been found
            if (mp.ContainsKey(sum) == true)
            {
                // Print the size of subset
                    Console.WriteLine(i - Convert.ToInt32(mp[sum]));

                // Print the indices of
                // contiguous subset
                for (int j = Convert.ToInt32(mp[sum]) + 1;
                        j <= i; j++)
                        Console.Write(j + 1 + " ");

                return;
            }
            else
                mp.Add(sum,i);
        }
    }

    // Driver Code
    public static void Main()
    {
        int []arr = { 2, 3, 7, 1, 9 };
        int N = arr.Length;

        findNonEmptySubset(arr, N);
    }
    // This code is contributed by Ryuga
}
```

**Output:** 

```
2
1 2
```

**时间复杂度:** O(N)，其中 N 是数组的大小。
**辅助空间:** O(N)
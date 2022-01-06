# 数组中一组字谜的最大值和最小值之差

> 原文:[https://www . geeksforgeeks . org/数组最大和最小字谜之差/](https://www.geeksforgeeks.org/difference-between-maximum-and-minimum-of-a-set-of-anagrams-from-an-array/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】**，任务是找出数字为彼此的[字谜](https://www.geeksforgeeks.org/check-whether-two-strings-are-anagram-of-each-other/)的整数，并打印它们的最大值和最小值之差。如果这些数字都不构成字谜，则打印 **-1** 。

**注意:**最多一组数组元素可以是彼此的字谜。该数组至少包含两个数字，并且给定数组中的所有数字都具有相同的长度。

**示例:**

> ***输入:** arr[] = {121，312，234，211，112，102}*
> ***输出:** 99*
> ***说明:**在给定数组中，集合{121，211，112}是彼此的字谜。*
> *集合中最大值为 211。*
> *集合中的最小值为 112。*
> *因此，差= 211–112 = 99。*
> 
> ***输入:** arr[] = {345，441，604，189，113}*
> ***输出:** -1*

**方法:**想法是使用[哈希](https://www.geeksforgeeks.org/hashing-data-structure/)通过为每个字谜号码生成唯一的哈希值来确定字谜。按照以下步骤解决问题:

*   将质数用于散列目的，通过用前 10 个质数初始化数组**质数【10】**，将前 10 个质数分配给数字 0-9。

> 质数[10] = {2，3，5，7，11，13，17，19，23，29}
> 质数[0] = 2 即数字 0 对应的质数为“2”
> 质数[1] = 3 即数字 1 对应的质数为“3”
> 质数[2] = 5 即数字 2 对应的质数为“5”以此类推…

*   然后，通过乘以 **arr[i]** 每个数字对应的素数，找到每个数组元素 **arr[i]** 的哈希值。这样，对于不是字谜的数字，哈希值会有所不同。
*   使用**哈希函数(N)** 为每个数组元素**arr【I】**找到哈希值 **h** 。
*   将数组元素存储在[映射](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)中，键作为它们的哈希值 **h** 。
*   [遍历地图](https://www.geeksforgeeks.org/traversing-a-map-or-unordered_map-in-cpp-stl/)找到一个大小大于 1 的向量，找到它的最大和最小元素。如果不存在这样的向量，则打印-1。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Utility function to find the hash value
// for each element of the given array
int hashFunction(int N)
{
    // Initialize an array with
    // first 10 prime numbers
    int prime[10] = { 2, 3, 5, 7, 11,
                      13, 17, 19, 23, 29 };

    int value = 1, r;

    // Iterate over digits of N
    while (N != 0) {
        r = N % 10;

        // Update Hash Value
        value = value * prime[r];

        // Update N
        N = N / 10;
    }
    return value;
}

// Function to find the set of anagrams in the array
// and print the difference between the maximum and
// minimum of these numbers
void findDiff(int arr[], int n)
{

    // Map to store the hash value
    // and the array elements having that hash value
    map<int, vector<int> > m;

    int h, min, max;
    for (int i = 0; i < n; i++) {

        // Find the hash value for each arr[i]
        // by calling hash function
        h = hashFunction(arr[i]);

        m[h].push_back(arr[i]);
    }

    // Iterate over the map
    for (auto i = 0; i != m.size(); i++) {

        // If size of vector at m[i] greater than 1
        // then it must contain the anagrams
        if (m[i].size() > 1) {

            // Find the minimum and maximum
            // element of this anagrams vector
            min = *min_element(
                m[i].begin(), m[i].end());
            max = *max_element(
                m[i].begin(), m[i].end());

            // Display the difference
            cout << max - min;
            break;
        }

        // If the end of Map is reached,
        // then no anagrams are present
        else if (i == m.size() - 1)
            cout << -1;
    }
}

// Driver Code
int main()
{
    // Given array
    int arr[] = { 121, 312, 234,
                  211, 112, 102 };

    // Size of the array
    int N = sizeof(arr)
            / sizeof(arr[0]);

    findDiff(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Utility function to find the hash value
// for each element of the given array
static int hashFunction(int N)
{

    // Initialize an array with
    // first 10 prime numbers
    int[] prime = { 2, 3, 5, 7, 11, 13,
                    17, 19, 23, 29 };

    int value = 1, r;

    // Iterate over digits of N
    while (N != 0)
    {
        r = N % 10;

        // Update Hash Value
        value = value * prime[r];

        // Update N
        N = N / 10;
    }
    return value;
}

// Function to find the set of anagrams in the array
// and print the difference between the maximum and
// minimum of these numbers
static void findDiff(int[] arr, int n)
{

    // Map to store the hash value
    // and the array elements having that hash value
    HashMap<Integer, Vector<Integer>> m = new HashMap<>();

    int h, min, max;
    for(int i = 0; i < n; i++)
    {

        // Find the hash value for each arr[i]
        // by calling hash function
        h = hashFunction(arr[i]);

        if (!m.containsKey(h))
        {
            m.put(h, new Vector<Integer>());
        }

        m.get(h).add(arr[i]);
    }

    for(Map.Entry<Integer, Vector<Integer>> i : m.entrySet())
    {

        // If size of vector at m[i] greater than 1
        // then it must contain the anagrams
        if (i.getValue().size() > 1)
        {

            // Find the minimum and maximum
            // element of this anagrams vector
            min = Integer.MAX_VALUE;
            max = -(Integer.MAX_VALUE);

            for (int j = 0; j < i.getValue().size(); j++)
            {
                if (m.get(i.getKey()).get(j) < min)
                {
                    min = m.get(i.getKey()).get(j);
                }

                if (m.get(i.getKey()).get(j) > max)
                {
                    max = m.get(i.getKey()).get(j);
                }
            }

            // Display the difference
            System.out.print(max - min);
            break;
        }

        // If the end of Map is reached,
        // then no anagrams are present
        else if (m.get(i.getKey()) == m.values().toArray()[m.size() - 1])
            System.out.print(-1);
    }
}

// Driver code
public static void main(String[] args)
{
    // Given array
    int[] arr = { 121, 312, 234,
                 211, 112, 102 };

    // Size of the array
    int N = arr.length;

    findDiff(arr, N);
}
}

// This code is contributed by divyeshrabadiya07
```

## 蟒蛇 3

```
# Python3 program for the above approach
import math
from collections import defaultdict

# Utility function to find the hash value
# for each element of the given array
def hashFunction(N) :

    # Initialize an array with
    # first 10 prime numbers
    prime = [ 2, 3, 5, 7, 11,
                      13, 17, 19, 23, 29 ]
    value = 1

    # Iterate over digits of N
    while (N != 0) :
        r = N % 10

        # Update Hash Value
        value = value * prime[r]

        # Update N
        N = N // 10
    return value

# Function to find the set of anagrams in the array
# and print the difference between the maximum and
# minimum of these numbers
def findDiff(arr, n):

    # Map to store the hash value
    # and the array elements having that hash value
    m = defaultdict(lambda : [])
    for i in range(n):

        # Find the hash value for each arr[i]
        # by calling hash function
        h = hashFunction(arr[i])
        m[h].append(arr[i])

    # Iterate over the map
    i = 0
    while(i != len(m)) :

        # If size of vector at m[i] greater than 1
        # then it must contain the anagrams
        if (len(m[i]) > 1) :

            # Find the minimum and maximum
            # element of this anagrams vector
            minn = min(m[i])
            maxx = max(m[i])

            # Display the difference
            print(maxx - minn)
            break

        # If the end of Map is reached,
        # then no anagrams are present
        elif (i == (len(m) - 1)) :
            print(-1)   
        i += 1

# Driver Code

# Given array
arr = [ 121, 312, 234,
                211, 112, 102 ]

# Size of the array
N = len(arr)
findDiff(arr, N)

# This code is contributed by sanjoy_62.
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;
using System.Linq;
class GFG {

  // Utility function to find the hash value
  // for each element of the given array
  static int hashFunction(int N)
  {
    // Initialize an array with
    // first 10 prime numbers
    int[] prime = { 2, 3, 5, 7, 11, 13, 17, 19, 23, 29 };

    int value = 1, r;

    // Iterate over digits of N
    while (N != 0) {
      r = N % 10;

      // Update Hash Value
      value = value * prime[r];

      // Update N
      N = N / 10;
    }
    return value;
  }

  // Function to find the set of anagrams in the array
  // and print the difference between the maximum and
  // minimum of these numbers
  static void findDiff(int[] arr, int n)
  {

    // Map to store the hash value
    // and the array elements having that hash value
    Dictionary<int, List<int>> m = new Dictionary<int, List<int>>();

    int h, min, max;
    for (int i = 0; i < n; i++) {

      // Find the hash value for each arr[i]
      // by calling hash function
      h = hashFunction(arr[i]);

      if(!m.ContainsKey(h))
      {
        m[h] = new List<int>();
      }

      m[h].Add(arr[i]);
    }

    // Iterate over the map
    foreach(KeyValuePair<int, List<int>> i in m)
    {
      // If size of vector at m[i] greater than 1
      // then it must contain the anagrams
      if (i.Value.Count > 1) {

        // Find the minimum and maximum
        // element of this anagrams vector
        min = Int32.MaxValue;
        max = Int32.MinValue;
        for(int j = 0; j < i.Value.Count; j++)
        {
          if(m[i.Key][j] < min)
          {
            min = m[i.Key][j];
          }

          if(m[i.Key][j] > max)
          {
            max = m[i.Key][j];
          }
        }

        // Display the difference
        Console.Write(max - min);
        break;
      }

      // If the end of Map is reached,
      // then no anagrams are present
      else if (m[i.Key].Equals( m.Last().Value ))
        Console.Write(-1);
    }
  }

  // Driver code
  static void Main()
  {
    // Given array
    int[] arr = { 121, 312, 234,
                 211, 112, 102 };

    // Size of the array
    int N = arr.Length;

    findDiff(arr, N);
  }
}

// This code is contributed by divyesh072019.
```

## java 描述语言

```
<script>
    // Javascript program for the above approach

    // Utility function to find the hash value
    // for each element of the given array
    function hashFunction(N)
    {

        // Initialize an array with
        // first 10 prime numbers
        let prime = [ 2, 3, 5, 7, 11, 13, 17, 19, 23, 29 ];

        let value = 1, r;

        // Iterate over digits of N
        while (N != 0)
        {
            r = N % 10;

            // Update Hash Value
            value = value * prime[r];

            // Update N
            N = parseInt(N / 10, 10);
        }
        return value;
    }

    // Function to find the set of anagrams in the array
    // and print the difference between the maximum and
    // minimum of these numbers
    function findDiff(arr, n)
    {

      // Map to store the hash value
      // and the array elements having that hash value
      let m = new Map();

      let h, min, max;
      for (let i = 0; i < n; i++) {

        // Find the hash value for each arr[i]
        // by calling hash function
        h = hashFunction(arr[i]);

        if(!m.has(h))
        {
          m.set(h, []);
        }

        (m.get(h)).push(arr[i]);
      }

      // Iterate over the map
      m.forEach((values,keys)=>{
        // If size of vector at m[i] greater than 1
        // then it must contain the anagrams
        if (values.length > 1) {

          // Find the minimum and maximum
          // element of this anagrams vector
          min = Number.MAX_VALUE;
          max = Number.MIN_VALUE;
          for(let j = 0; j < values.length; j++)
          {
            if((m.get(keys))[j] < min)
            {
              min = m.get(keys)[j];
            }

            if(m.get(keys)[j] > max)
            {
              max = m.get(keys)[j];
            }
          }

          // Display the difference
          document.write(max - min);
        }
      })
    }

    // Given array
    let arr = [ 121, 312, 234, 211, 112, 102 ];

    // Size of the array
    let N = arr.length;

    findDiff(arr, N);

// This code is contributed by suresh07.
</script>
```

**Output:** 

```
99
```

***时间复杂度** : O(N*logN)*
***辅助空间:** O(N)*
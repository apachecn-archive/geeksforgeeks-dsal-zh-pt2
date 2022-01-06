# 对数组中的对进行计数，使它们与其索引之间的差值相等

> 原文:[https://www . geeksforgeeks . org/对数组中的对进行计数，以使它们与它们的索引之间的差异相等/](https://www.geeksforgeeks.org/count-the-pairs-in-an-array-such-that-the-difference-between-them-and-their-indices-is-equal/)

给定一个大小为 **N** 的数组 **arr[]** ，任务是计算对的数量 **(arr[i]，arr[j])** ，使得**arr[j]–arr[I]= j–I**。
**举例:**

> **输入:** arr[] = {5，2，7}
> **输出:** 1
> 唯一有效的对是(arr[0]，arr[2])为 7–5 = 2–0 = 2。
> **输入:** arr[] = {1，2，3，4}
> **输出:** 6

**方法:**一对 **(arr[i]，arr[j])** 据说有效如果**(arr[j]–arr[I])=(j–I)**，也可以写成**(arr[j]–j)=(arr[I]–I)**这是元素与其索引的区别。现在，任务是将数组分成多个组，使得每个组都有与其索引相等的元素差，然后对于每个组，如果它有 **N** 个元素，可能的对的计数将是**(N *(N–1))/2**。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the count
// of all valid pairs
int countPairs(int arr[], int n)
{

    // To store the frequencies
    // of (arr[i] - i)
    unordered_map<int, int> map;
    for (int i = 0; i < n; i++)
        map[arr[i] - i]++;

    // To store the required count
    int res = 0;
    for (auto x : map) {
        int cnt = x.second;

        // If cnt is the number of elements
        // whose difference with their index
        // is same then ((cnt * (cnt - 1)) / 2)
        // such pairs are possible
        res += ((cnt * (cnt - 1)) / 2);
    }

    return res;
}

// Driver code
int main()
{
    int arr[] = { 1, 5, 6, 7, 9 };
    int n = sizeof(arr) / sizeof(arr[0]);

    cout << countPairs(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.HashMap;

class GFG
{

    // Function to return the count
    // of all valid pairs
    static int countPairs(int arr[], int n)
    {

        // To store the frequencies
        // of (arr[i] - i)
        HashMap<Integer,
                Integer> map = new HashMap<Integer,
                                           Integer>();
        for (int i = 0; i < n; i++)
            map.put(arr[i] - i, 0);

        for (int i = 0; i < n; i++)
            map.put(arr[i] - i, map.get(arr[i] - i) + 1);

        // To store the required count
        int res = 0;
        for (int x : map.values())
        {
            int cnt = x;

            // If cnt is the number of elements
            // whose difference with their index
            // is same then ((cnt * (cnt - 1)) / 2)
            // such pairs are possible
            res += ((cnt * (cnt - 1)) / 2);
        }

        return res;
    }

    // Driver code
    public static void main (String[] args)
    {
        int arr[] = { 1, 5, 6, 7, 9 };
        int n = arr.length;

        System.out.println(countPairs(arr, n));
    }
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the count
# of all valid pairs
def countPairs(arr, n):

    # To store the frequencies
    # of (arr[i] - i)
    map = dict()
    for i in range(n):
        map[arr[i] - i] = map.get(arr[i] - i, 0) + 1

    # To store the required count
    res = 0
    for x in map:
        cnt = map[x]

        # If cnt is the number of elements
        # whose difference with their index
        # is same then ((cnt * (cnt - 1)) / 2)
        # such pairs are possible
        res += ((cnt * (cnt - 1)) // 2)

    return res

# Driver code
arr = [1, 5, 6, 7, 9]
n = len(arr)

print(countPairs(arr, n))

# This code is contributed by Mohit Kumar
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;
class GFG
{

    // Function to return the count
    // of all valid pairs
    static int countPairs(int []arr, int n)
    {

        // To store the frequencies
        // of (arr[i] - i)
        Dictionary<int,
                   int> map = new Dictionary<int,
                                             int>();
        for (int i = 0; i < n; i++)
            map[arr[i] - i] = 0;

        for (int i = 0; i < n; i++)
            map[arr[i] - i]++;

        // To store the required count
        int res = 0;
        foreach(KeyValuePair<int, int> x in map)
        {
            int cnt = x.Value;

            // If cnt is the number of elements
            // whose difference with their index
            // is same then ((cnt * (cnt - 1)) / 2)
            // such pairs are possible
            res += ((cnt * (cnt - 1)) / 2);
        }
        return res;
    }

    // Driver code
    public static void Main (String []args)
    {
        int []arr = { 1, 5, 6, 7, 9 };
        int n = arr.Length;

        Console.WriteLine(countPairs(arr, n));
    }
}

// This code is contributed by Arnab Kundu
```

## java 描述语言

```
<script>
      // JavaScript implementation of the approach
      // Function to return the count
      // of all valid pairs
      function countPairs(arr, n) {
        // To store the frequencies
        // of (arr[i] - i)
        var map = {};
        for (var i = 0; i < n; i++) map[arr[i] - i] = 0;

        for (var i = 0; i < n; i++) map[arr[i] - i]++;

        // To store the required count
        var res = 0;
        for (const [key, value] of Object.entries(map)) {
          var cnt = value;

          // If cnt is the number of elements
          // whose difference with their index
          // is same then ((cnt * (cnt - 1)) / 2)
          // such pairs are possible
          res += (cnt * (cnt - 1)) / 2;
        }
        return res;
      }

      // Driver code
      var arr = [1, 5, 6, 7, 9];
      var n = arr.length;

      document.write(countPairs(arr, n));
    </script>
```

**Output:** 

```
3
```
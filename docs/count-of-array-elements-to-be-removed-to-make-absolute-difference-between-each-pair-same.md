# 要移除的数组元素的计数，以使每对元素之间的绝对差异相同

> 原文:[https://www . geeksforgeeks . org/要移除的数组元素计数每对之间的绝对差异相同/](https://www.geeksforgeeks.org/count-of-array-elements-to-be-removed-to-make-absolute-difference-between-each-pair-same/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**，任务是找到必须移除的最小数组元素数，使得每个元素对之间的绝对差值相等。

**示例:**

> **输入:** arr[] = {1，2}
> **输出:** 0
> **说明:**只有一对绝对差的整数| arr[1]—arr[2]| = | 1-2 | = 1。所以不需要从给定的数组中删除任何整数。
> 
> **输入:** arr[] = {2，5，1，2，2}
> **输出:** 2
> **说明:**删除 1 和 5 后，数组 A 变为[2，2，2]，每对整数的绝对差为 0。

**方法:**给定的问题可以通过[计算数组元素的频率](https://www.geeksforgeeks.org/counting-frequencies-of-array-elements/)来解决，并根据以下观察结果打印结果:

*   如果所有阵元中的[最大频率为 **1** ，则必须移除所有**(N–2)阵元**。](https://www.geeksforgeeks.org/frequent-element-array/)
*   否则，必须移除的数组元素的最大数量为**(N–最大频率)**，使得所有数组元素相同，并且任意两对元素之间的差异相同。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

void countToMakeDiffEqual(int arr[], int n)
{
    // Stores the element having maximum
    // frequency in the array
    int ma = 0;

    unordered_map<int, int> m;

    for (int i = 0; i < n; i++) {

        m[arr[i]]++;

        // Find the most occurring element
        ma = max(ma, m[arr[i]]);
    }

    // If only one pair exists then the
    // absolute difference between them
    // will be same
    if (n <= 2)
        cout << 0 << endl;

    else if (ma == 1) {
        cout << n - 2 << endl;
    }

    // Elements to remove is equal to the
    // total frequency minus frequency
    // of most frequent element
    else
        cout << n - ma << endl;
}

// Driver Code
int main()
{
    int arr[] = { 2, 5, 1, 2, 2 };
    int N = sizeof(arr) / sizeof(arr[0]);

    countToMakeDiffEqual(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.HashMap;

class GFG {

    public static void countToMakeDiffEqual(int arr[], int n)
    {

        // Stores the element having maximum
        // frequency in the array
        int ma = 0;

        HashMap<Integer, Integer> m = new HashMap<Integer, Integer>();

        for (int i = 0; i < n; i++) {

            // m[arr[i]]++;
            if (m.containsKey(arr[i])) {
                m.put(arr[i], m.get(arr[i]) + 1);
            } else {
                m.put(arr[i], 1);
            }

            // Find the most occurring element
            ma = Math.max(ma, m.get(arr[i]));
        }

        // If only one pair exists then the
        // absolute difference between them
        // will be same
        if (n <= 2)
            System.out.println(0);

        else if (ma == 1) {
            System.out.println(n - 2);
        }

        // Elements to remove is equal to the
        // total frequency minus frequency
        // of most frequent element
        else
            System.out.println(n - ma);
    }

    // Driver Code
    public static void main(String args[]) {
        int arr[] = { 2, 5, 1, 2, 2 };
        int N = arr.length;

        countToMakeDiffEqual(arr, N);
    }
}

// This code is contributed by gfgking.
```

## 蟒蛇 3

```
# Python 3 program for the above approach
from collections import defaultdict

def countToMakeDiffEqual(arr, n):

    # Stores the element having maximum
    # frequency in the array
    ma = 0

    m = defaultdict(int)

    for i in range(n):

        m[arr[i]] += 1

        # Find the most occurring element
        ma = max(ma, m[arr[i]])

    # If only one pair exists then the
    # absolute difference between them
    # will be same
    if (n <= 2):
        print(0)

    elif (ma == 1):
        print(n - 2)

    # Elements to remove is equal to the
    # total frequency minus frequency
    # of most frequent element
    else:
        print(n - ma)

# Driver Code
if __name__ == "__main__":

    arr = [2, 5, 1, 2, 2]
    N = len(arr)

    countToMakeDiffEqual(arr, N)

    # This code is contributed by ukasp.
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

static void countToMakeDiffEqual(int []arr, int n)
{
    // Stores the element having maximum
    // frequency in the array
    int ma = 0;

    Dictionary<int, int> m = new Dictionary<int,int>();

    for (int i = 0; i < n; i++) {
        if(m.ContainsKey(arr[i]))
          m[arr[i]]++;
        else
         m.Add(arr[i],1);

        // Find the most occurring element
        ma = Math.Max(ma, m[arr[i]]);
    }

    // If only one pair exists then the
    // absolute difference between them
    // will be same
    if (n <= 2)
        Console.WriteLine(0);

    else if (ma == 1) {
        Console.WriteLine(n - 2);
    }

    // Elements to remove is equal to the
    // total frequency minus frequency
    // of most frequent element
    else
        Console.WriteLine(n - ma);
}

// Driver Code
public static void Main()
{
    int []arr = { 2, 5, 1, 2, 2 };
    int N = arr.Length;

    countToMakeDiffEqual(arr, N);
}
}

// This code is contributed by ipg2016107.
```

## java 描述语言

```
<script>
      // JavaScript Program to implement
      // the above approach
      function countToMakeDiffEqual(arr, n)
      {

          // Stores the element having maximum
          // frequency in the array
          let ma = 0;

          let m = new Map();

          for (let i = 0; i < n; i++) {
              if (m.has(arr[i])) {
                  m.set(arr[i], m.get(arr[i]) + 1);
              }
              else {
                  m.set(arr[i], 1);
              }

              // Find the most occurring element
              ma = Math.max(ma, m.get(arr[i]));
          }

          // If only one pair exists then the
          // absolute difference between them
          // will be same
          if (n <= 2) {
              document.write(0 + '<br>');
          }
          else if (ma == 1) {
              document.write(n - 2 + '<br>');
          }

          // Elements to remove is equal to the
          // total frequency minus frequency
          // of most frequent element
          else {
              document.write(n - ma + '<br>');
          }
      }

      // Driver Code
      let arr = [2, 5, 1, 2, 2];
      let N = arr.length;

      countToMakeDiffEqual(arr, N);

   // This code is contributed by Potta Lokesh
  </script>
```

**Output:** 

```
2
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)
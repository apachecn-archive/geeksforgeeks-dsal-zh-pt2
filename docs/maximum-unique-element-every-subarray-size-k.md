# 大小为 K 的每个子阵列中的最大唯一元素

> 原文:[https://www . geesforgeks . org/maximum-unique-element-ever-subarray-size-k/](https://www.geeksforgeeks.org/maximum-unique-element-every-subarray-size-k/)

给定一个数组和一个整数 K，我们需要找到长度为 K 的每个段的最大值，该段中没有重复。

**示例:**

```
Input : a[] = {1, 2, 2, 3, 3}, 
          K = 3.
Output : 1 3 2
For segment (1, 2, 2), Maximum = 1.
For segment (2, 2, 3), Maximum = 3.
For segment (2, 3, 3), Maximum = 2\. 

Input : a[] = {3, 3, 3, 4, 4, 2},
          K = 4.
Output : 4 Nothing 3 
```

一个**简单的解决方案**是运行两个循环。对于每个子阵列，找到所有不同的元素并打印最大数量的唯一元素。

一个有效的解决方案是使用[滑动窗口技术](https://www.geeksforgeeks.org/window-sliding-technique/)。我们每个窗口都有两个结构。
1)哈希表，用于存储当前窗口中所有元素的计数。
2)一个自平衡 BST(使用 C++ STL 中的[集](https://www.geeksforgeeks.org/set-in-cpp-stl/)和 Java 中的 [TreeSet 实现)](https://www.geeksforgeeks.org/treeset-class-java-examples/)。想法是快速找到最大元素并更新最大元素。
我们处理前 K-1 个元素，并将它们的计数存储在哈希表中。我们还存储独特的元素插图。现在，我们一个接一个地处理每个窗口的最后一个元素。如果当前元素是唯一的，我们将其添加到集合中。我们也增加了它的数量。处理完最后一个元素后，我们打印集合中的最大值。在开始下一个迭代之前，我们移除上一个窗口的第一个元素。

## C++

```
// C++ code to calculate maximum unique
// element of every segment of array
#include <bits/stdc++.h>
using namespace std;

void find_max(int A[], int N, int K)
{
    // Storing counts of first K-1 elements
    // Also storing distinct elements.
    map<int, int> Count;
    for (int i = 0; i < K - 1; i++)
        Count[A[i]]++;
    set<int> Myset;
    for (auto x : Count)
        if (x.second == 1)
            Myset.insert(x.first);

    // Before every iteration of this loop,
    // we maintain that K-1 elements of current
    // window are processed.
    for (int i = K - 1; i < N; i++) {

        // Process K-th element of current window
        Count[A[i]]++;
        if (Count[A[i]] == 1)
            Myset.insert(A[i]);
        else
            Myset.erase(A[i]);

        // If there are no distinct
        // elements in current window
        if (Myset.size() == 0)
            printf("Nothing\n");

        // Set is ordered and last element
        // of set gives us maximum element.
        else
            printf("%d\n", *Myset.rbegin());

        // Remove first element of current
        // window before next iteration.
        int x = A[i - K + 1];
        Count[x]--;
        if (Count[x] == 1)
            Myset.insert(x);
        if (Count[x] == 0)
            Myset.erase(x);
    }
}

// Driver code
int main()
{
    int a[] = { 1, 2, 2, 3, 3 };
    int n = sizeof(a) / sizeof(a[0]);
    int k = 3;
    find_max(a, n, k);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to calculate maximum unique
// element of every segment of array
import java.io.*;
import java.util.*;
class GFG {

    static void find_max(int[] A, int N, int K)
    {
        // Storing counts of first K-1 elements
        // Also storing distinct elements.
        HashMap<Integer, Integer> Count = new HashMap<>();
        for (int i = 0; i < K - 1; i++)
            if (Count.containsKey(A[i]))
                Count.put(A[i], 1 + Count.get(A[i]));
            else
                Count.put(A[i], 1);

        TreeSet<Integer> Myset = new TreeSet<Integer>();
        for (Map.Entry x : Count.entrySet()) {
            if (Integer.parseInt(String.valueOf(x.getValue())) == 1)
                Myset.add(Integer.parseInt(String.valueOf(x.getKey())));
        }

        // Before every iteration of this loop,
        // we maintain that K-1 elements of current
        // window are processed.
        for (int i = K - 1; i < N; i++) {

            // Process K-th element of current window
            if (Count.containsKey(A[i]))
                Count.put(A[i], 1 + Count.get(A[i]));
            else
                Count.put(A[i], 1);

            if (Integer.parseInt(String.valueOf(Count.get(A[i]))) == 1)
                Myset.add(A[i]);
            else
                Myset.remove(A[i]);

            // If there are no distinct
            // elements in current window
            if (Myset.size() == 0)
                System.out.println("Nothing");

            // Set is ordered and last element
            // of set gives us maximum element.
            else
                System.out.println(Myset.last());

            // Remove first element of current
            // window before next iteration.
            int x = A[i - K + 1];
            Count.put(x, Count.get(x) - 1);

            if (Integer.parseInt(String.valueOf(Count.get(x))) == 1)
                Myset.add(x);
            if (Integer.parseInt(String.valueOf(Count.get(x))) == 0)
                Myset.remove(x);
        }
    }

    // Driver code
    public static void main(String args[])
    {
        int[] a = { 1, 2, 2, 3, 3 };
        int n = a.length;
        int k = 3;
        find_max(a, n, k);
    }
}

// This code is contributed by rachana soma
```

## 蟒蛇 3

```
# Python3 code to calculate maximum unique
# element of every segment of array
def find_max(A, N, K):

    # Storing counts of first K-1 elements
    # Also storing distinct elements.
    Count = dict()
    for i in range(K - 1):
        Count[A[i]] = Count.get(A[i], 0) + 1

    Myset = dict()
    for x in Count:
        if (Count[x] == 1):
            Myset[x] = 1

    # Before every iteration of this loop,
    # we maintain that K-1 elements of current
    # window are processed.
    for i in range(K - 1, N):

        # Process K-th element of current window
        Count[A[i]] = Count.get(A[i], 0) + 1

        if (Count[A[i]] == 1):
            Myset[A[i]] = 1
        else:
            del Myset[A[i]]

        # If there are no distinct
        # elements in current window
        if (len(Myset) == 0):
            print("Nothing")

        # Set is ordered and last element
        # of set gives us maximum element.
        else:
            maxm = -10**9
            for i in Myset:
                maxm = max(i, maxm)
            print(maxm)

        # Remove first element of current
        # window before next iteration.
        x = A[i - K + 1]
        if x in Count.keys():
            Count[x] -= 1
            if (Count[x] == 1):
                Myset[x] = 1
            if (Count[x] == 0):
                del Myset[x]

# Driver code
a = [1, 2, 2, 3, 3 ]
n = len(a)
k = 3
find_max(a, n, k)

# This code is contributed
# by mohit kumar
```

## C#

```
using System;
using System.Collections.Generic;

public class GFG
{
  static void find_max(int[] A, int N, int K)
  {

    // Storing counts of first K-1 elements
    // Also storing distinct elements.
    Dictionary<int, int> count = new Dictionary<int, int>(); 
    for (int i = 0; i < K - 1; i++)
    {
      if(count.ContainsKey(A[i]))
      {
        count[A[i]]++;
      }
      else
      {
        count.Add(A[i], 1);
      }
    }
    HashSet<int> Myset = new HashSet<int>();
    foreach(KeyValuePair<int, int> x in count)
    {
      if(x.Value == 1)
      {
        Myset.Add(x.Key);
      }
    }

    // Before every iteration of this loop,
    // we maintain that K-1 elements of current
    // window are processed.
    for (int i = K - 1; i < N; i++)
    {

      // Process K-th element of current window
      if (count.ContainsKey(A[i]))
      {
        count[A[i]]++;
      }
      else
      {
        count.Add(A[i], 1);
      }
      if(count[A[i]] == 1)
      {
        Myset.Add(A[i]);
      }
      else
      {
        Myset.Remove(A[i]);
      }

      // If there are no distinct
      // elements in current window
      if (Myset.Count == 0)
        Console.Write("Nothing\n");

      // Set is ordered and last element
      // of set gives us maximum element.
      else
      {
        List<int> myset = new List<int>(Myset);
        Console.WriteLine(myset[myset.Count - 1]);
      }

      // Remove first element of current
      // window before next iteration.
      int x = A[i - K + 1];
      count[x]--;
      if(count[x] == 1)
      {
        Myset.Add(x);
      }
      if(count[x] == 0)
      {
        Myset.Remove(x);
      }
    }

  }

  // Driver code
  static public void Main ()
  {
    int[] a = { 1, 2, 2, 3, 3 };
    int n=a.Length;
    int k = 3;
    find_max(a, n, k);
  }
}

// This code is contributed by rag2127
```

## java 描述语言

```
<script>
    // Javascript code to calculate maximum unique
    // element of every segment of array

    function find_max(A,N,K)
    {
        // Storing counts of first K-1 elements
        // Also storing distinct elements.
        let Count = new Map();
        for (let i = 0; i < K - 1; i++)
            if (Count.has(A[i]))
                Count.set(A[i], 1 + Count.get(A[i]));
            else
                Count.set(A[i], 1);

        let Myset = new Set();
        for (let [key, value] of Count.entries()) {
            if (value==1)
                Myset.add(key);
        }

        // Before every iteration of this loop,
        // we maintain that K-1 elements of current
        // window are processed.
        for (let i = K - 1; i < N; i++) {

            // Process K-th element of current window
            if (Count.has(A[i]))
                Count.set(A[i], 1 + Count.get(A[i]));
            else
                Count.set(A[i], 1);

            if ((Count.get(A[i])) == 1)
                Myset.add(A[i]);
            else
                Myset.delete(A[i]);

            // If there are no distinct
            // elements in current window
            if (Myset.size == 0)
                document.write("Nothing<br>");

            // Set is ordered and last element
            // of set gives us maximum element.
            else
                document.write(Array.from(Myset)[Myset.size-1]+"<br>");

            // Remove first element of current
            // window before next iteration.
            let x = A[i - K + 1];
            Count.set(x, Count.get(x) - 1);

            if (Count.get(x) == 1)
                Myset.add(x);
            if (Count.get(x) == 0)
                Myset.delete(x);
        }
    }

    // Driver code
    let a=[1, 2, 2, 3, 3];
    let n = a.length;
    let k = 3;
    find_max(a, n, k);

// This code is contributed by unknown2108
</script>
```

**输出:**

```
1
3
2
```

**时间复杂度:** O(N Log K)
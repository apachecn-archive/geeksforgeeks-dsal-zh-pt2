# 在未排序的数组中找到 k 个最接近的数字

> 原文:[https://www . geesforgeks . org/find-k-最接近数字的未排序数组/](https://www.geeksforgeeks.org/find-k-closest-numbers-in-an-unsorted-array/)

给定一个未排序的数组和两个数字 x 和 k，找到与 x 最接近的 k 个值。
**示例:**

```
Input : arr[] = {10, 2, 14, 4, 7, 6}, x = 5, k = 3 
Output : 4 6 7
Three closest values of x are 4, 6 and 7.

Input : arr[] = {-10, -50, 20, 17, 80}, x = 20, k = 2
Output : 17, 20
```

一个**简单的解决方案**就是对数组进行排序。然后将所讨论的方法应用于排序数组中的 [k 个最接近的值。
**时间复杂度:** O(n Log n)
A **更好的解决方案**是使用**堆数据结构**
1)与前 k 个元素进行最大差异堆。
2)对于从第(k+1)个元素开始的每个元素，执行以下操作。
…..a)找出当前元素与 x 的差异。
…..b)如果差异大于堆的根，忽略当前元素。
…..c)否则在移除根之后将当前元素插入堆。
3)最后堆中有 k 个最接近的元素。](https://www.geeksforgeeks.org/find-k-closest-elements-given-value/) 

## C++

```
// C++ program to find k closest elements
#include <bits/stdc++.h>
using namespace std;

void printKclosest(int arr[], int n, int x,
                   int k)
{
    // Make a max heap of difference with
    // first k elements.
    priority_queue<pair<int, int> > pq;
    for (int i = 0; i < k; i++)
        pq.push({ abs(arr[i] - x), i });

    // Now process remaining elements.
    for (int i = k; i < n; i++) {

        int diff = abs(arr[i] - x);

        // If difference with current
        // element is more than root,
        // then ignore it.
        if (diff > pq.top().first)
            continue;

        // Else remove root and insert
        pq.pop();
        pq.push({ diff, i });
    }

    // Print contents of heap.
    while (pq.empty() == false) {
        cout << arr[pq.top().second] << " ";
        pq.pop();
    }
}

// Driver program to test above functions
int main()
{
    int arr[] = { -10, -50, 20, 17, 80 };
    int x = 20, k = 2;
    int n = sizeof(arr) / sizeof(arr[0]);
    printKclosest(arr, n, x, k);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
//Java program to find k closest elements
import java.util.Comparator;
import java.util.PriorityQueue;

class Pair
{
    Integer key;
    Integer value;

    public Pair(Integer key, Integer value)
    {
        this.key = key;
        this.value = value;
    }
    public Integer getKey()
    {
        return key;
    }
    public void setKey(Integer key)
    {
        this.key = key;
    }
    public Integer getValue()
    {
        return value;
    }
    public void setValue(Integer value)
    {
        this.value = value;
    }
}

class GFG{

public static void printKclosest(int[] arr, int n,
                                 int x, int k)
{

    // Make a max heap.
    PriorityQueue<Pair> pq = new PriorityQueue<>(
                             new Comparator<Pair>()
    {
        public int compare(Pair p1, Pair p2)
        {
            return p2.getValue().compareTo(
                   p1.getValue());
        }
    });

    // Build heap of difference with
    // first k elements
    for(int i = 0; i < k; i++)
    {
        pq.offer(new Pair(arr[i],
                 Math.abs(arr[i] - x)));
    }

    // Now process remaining elements.
    for(int i = k; i < n; i++)
    {
        int diff = Math.abs(arr[i] - x);

        // If difference with current
        // element is more than root,
        // then ignore it.
        if(diff > pq.peek().getValue()) continue;

        // Else remove root and insert
        pq.poll();
        pq.offer(new Pair(arr[i], diff));
    }

    // Print contents of heap.
    while(!pq.isEmpty())
    {
        System.out.print(pq.poll().getKey() + " ");
    }
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { -10, -50, 20, 17, 80 };
    int x = 20, k = 2;
    int n = arr.length;

    printKclosest(arr, n, x, k);
}
}

// This code is contributed by Ashok Borra
```

## 蟒蛇 3

```
# Python3 program to find k closest elements
import math
import sys
from queue import PriorityQueue
def printKclosest(arr,n,x,k):

    # Make a max heap of difference with
    # first k elements.
    pq = PriorityQueue()
    for i in range(k):
        pq.put((-abs(arr[i]-x),i))

    # Now process remaining elements
    for i in range(k,n):
        diff = abs(arr[i]-x)
        p,pi = pq.get()
        curr = -p

        # If difference with current
        # element is more than root,
        # then put it back.
        if diff>curr:
            pq.put((-curr,pi))
            continue
        else:

            # Else remove root and insert
            pq.put((-diff,i))

    # Print contents of heap.
    while(not pq.empty()):
        p,q = pq.get()
        print("{} ".format(arr[q]),end = "")

# Driver program to test above functions
if __name__=='__main__':
    arr = [-10,-50,20,17,80]
    x,k = 20,2
    n = len(arr)
    printKclosest(arr, n, x, k)

# This code is contributed by Vikash Kumar 37
```

## C#

```
// C# program to find k closest elements
using System;
using System.Collections.Generic;
class GFG {

  static void printKclosest(int[] arr, int n, int x, int k)
  {
    // Make a max heap of difference with
    // first k elements.
    List<Tuple<int, int>> pq = new List<Tuple<int, int>>();
    for (int i = 0; i < k; i++)
    {
      pq.Add(new Tuple<int,int>(Math.Abs(arr[i] - x), i));
    }

    pq.Sort();
    pq.Reverse();

    // Now process remaining elements.
    for (int i = k; i < n; i++)
    {

      int diff = Math.Abs(arr[i] - x);

      // If difference with current
      // element is more than root,
      // then ignore it.
      if (diff > pq[0].Item1)
        continue;

      // Else remove root and insert
      pq.RemoveAt(0);
      pq.Add(new Tuple<int,int>(diff, i));
      pq.Sort();
      pq.Reverse();
    }

    // Print contents of heap.
    while (pq.Count > 0)
    {
      Console.Write(arr[pq[0].Item2] + " ");
      pq.RemoveAt(0);
    }
  }

  // Driver code
  static void Main()
  {
    int[] arr = { -10, -50, 20, 17, 80 };
    int x = 20, k = 2;
    int n = arr.Length;
    printKclosest(arr, n, x, k);
  }
}

// This code is contributed by divyesh072019.
```

**Output:** 

```
17 20
```

**时间复杂度:** O(n Log k)
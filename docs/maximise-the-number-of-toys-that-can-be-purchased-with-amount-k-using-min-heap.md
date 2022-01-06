# 使用最小堆

最大化可购买的玩具数量

> 原文:[https://www . geeksforgeeks . org/最大化可以用最小堆购买的玩具数量/](https://www.geeksforgeeks.org/maximise-the-number-of-toys-that-can-be-purchased-with-amount-k-using-min-heap/)

给定一个数组 **arr[]** ，该数组由玩具成本和整数 **K** 组成，该整数描述了可用于购买玩具的金额。任务是用 **K** 的数量找到一个人能买的最大玩具数量。
**注:**一个人只能购买 1 个数量的特定玩具。

**例:**

> **输入:** arr[] = {1，12，5，111，200，1000，10，9，12，15}，K = 50
> **输出:** 6
> 可以购买数量为 1，5，9，10，12 和 12
> 的玩具，总计 49 个。
> 因此，玩具的最大数量为 6 个。
> 
> **输入:** arr[] = {1，12，5，111，200，1000，10}，K = 50
> **输出:** 4

**方法:**将给定数组的所有元素插入[优先级队列](https://www.geeksforgeeks.org/priority-queue-in-cpp-stl/)中，现在逐个从该优先级队列中移除元素，并将这些成本添加到初始化为 **0** 的变量 **sum** 中。继续移除元素，同时新添加的元素保持总和小于 **K** 。最终，移除的元素数将是所需的答案。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the count of
// maximum toys that can be bought
int maxToys(int arr[], int n, int k)
{

    // Create a priority_queue and push
    // all the array elements in it
    priority_queue<int, vector<int>, greater<int> > pq;
    for (int i = 0; i < n; i++) {
        pq.push(arr[i]);
    }

    // To store the count of maximum
    // toys that can be bought
    int count = 0;
    while (pq.top() <= k) {
        count++;
        k = k - pq.top();
        pq.pop();
    }
    return count;
}

// Driver code
int main()
{
    int arr[] = { 1, 12, 5, 111, 200, 1000, 10 };
    int n = sizeof(arr) / sizeof(arr[0]);
    int k = 50;

    cout << maxToys(arr, n, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.io.*;
import java.util.*;

class GFG{

// Function to return the count of
// maximum toys that can be bought    
public static int maxToys(int[] arr, int k)
{
    int n = arr.length;

    // Create a priority_queue and push
    // all the array elements in it
    PriorityQueue<Integer> pq = new PriorityQueue<Integer>();
    for(int i = 0; i < n; i++)
    {
        pq.offer(arr[i]);
    }

    // To store the count of maximum
    // toys that can be bought
    int count = 0;
    while (!pq.isEmpty() && pq.peek() <= k)
    {
        k = k - pq.poll();
        count++;
    }
    return count;
}

// Driver code
public static void main (String[] args)
{
    int[] arr = new int[]{ 1, 12, 5, 111,
                           200, 1000, 10 };
    int k = 50;                      

      System.out.println(maxToys(arr, k));     
}
}

// This code is contributed by ankit bajpai
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the count of
# maximum toys that can be bought
def maxToys(arr, n, k) :

    # Create a priority_queue and push
    # all the array elements in it
    pq = []
    for i in range(n) :
        pq.append(arr[i])
    pq.sort()

    # To store the count of maximum
    # toys that can be bought
    count = 0
    while (pq[0] <= k) :
        count += 1
        k = k - pq[0]
        pq.pop(0)
    return count

    # Driver code
arr = [ 1, 12, 5, 111, 200, 1000, 10 ]
n = len(arr)
k = 50
print(maxToys(arr, n, k))

# This code is contributed by divyesh072019
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;
class GFG
{

    // Function to return the count of
    // maximum toys that can be bought
    static int maxToys(int[] arr, int n, int k)
    {

        // Create a priority_queue and push
        // all the array elements in it
        List<int> pq = new List<int>();
        for (int i = 0; i < n; i++)
        {
            pq.Add(arr[i]);
        }

        pq.Sort();

        // To store the count of maximum
        // toys that can be bought
        int count = 0;
        while (pq[0] <= k)
        {
            count++;
            k = k - pq[0];
            pq.RemoveAt(0);
        }
        return count;
    }

  // Driver code
  static void Main()
  {
    int[] arr = { 1, 12, 5, 111, 200, 1000, 10 };
    int n = arr.Length;
    int k = 50;
    Console.WriteLine(maxToys(arr, n, k));
  }
}

// This code is contributed by divyeshrabadiya07.
```

## java 描述语言

```
<script>

    // Javascript implementation of the approach

    // Function to return the count of
    // maximum toys that can be bought
    function maxToys(arr, n, k)
    {

        // Create a priority_queue and push
        // all the array elements in it
        let pq = [];
        for (let i = 0; i < n; i++)
        {
            pq.push(arr[i]);
        }

        pq.sort(function(a, b){return a - b});

        // To store the count of maximum
        // toys that can be bought
        let count = 0;
        while (pq[0] <= k)
        {
            count++;
            k = k - pq[0];
            pq.shift();
        }
        return count;
    }

    let arr = [ 1, 12, 5, 111, 200, 1000, 10 ];
    let n = arr.length;
    let k = 50;
    document.write(maxToys(arr, n, k));

</script>
```

**Output:** 

```
4
```

**时间复杂度:**O(N * logN)
T3】辅助空间: O(N)
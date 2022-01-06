# 每次访问后最大值递减时阵列的最大值

> 原文:[https://www . geeksforgeeks . org/每次访问后最大值递减时从数组中删除最大值/](https://www.geeksforgeeks.org/maximums-from-array-when-the-maximum-decrements-after-every-access/)

给定一个整数 *K* 和一个整数数组 *arr* ，任务是从数组中找到最大元素，每次检索后，该数字将递减 *1* 。精确地重复这些步骤 *K* 次，并打印最后检索到的所有值的总和。

**示例:**

> **输入:** K = 3，arr[] = {2，3，5，4 }
> T3】输出: 13
> 对于 K = 1，电流最大值为 5 (Sum = 5 和 arr[] = {2，3，4，4})
> 对于 K = 2，电流最大值为 4 (Sum = 5 + 4 = 9 和 arr[] = {2，3，3，4})
> 对于 K = 3，电流最大值为 4 (Sum = 9 + 4 = 13 和 arr[]= { 0
> 
> **输入:** K = 4，arr[] = {1，2，4 }
> T3】输出: 11

**方法:**主要思想是使用一个最大[堆](https://www.geeksforgeeks.org/binary-heap/)，在任何时刻它的根都有最大的元素。

*   创建数组所有元素的最大堆。
*   获取堆的根元素，并将其添加到总和中。
*   弹出根元素并按 *1* 递减，然后再次将其插入堆中。
*   精确重复以上两个步骤 *K* 次。
*   最后打印总和。

下面是上述方法的实现:

## C++

```
// C++ implementation of above approach
#include <bits/stdc++.h>
using namespace std;
#define ll long long

ll getSum(int arr[], int K, int n)
{
    ll sum = 0;
    priority_queue<ll> maxHeap;
    for (ll i = 0; i < n; i++) {

        // put all array elements
        // in a max heap
        maxHeap.push(arr[i]);
    }

    while (K--) {

        // Get the current maximum element
        ll currentMax = maxHeap.top();

        // Add it to the sum
        sum += currentMax;

        // Remove the current max from the heap
        maxHeap.pop();

        // Add the current max back to the
        // heap after decrementing it by 1
        maxHeap.push(currentMax - 1);
    }
    return sum;
}

// driver code
int main()
{
    int arr[] = { 2, 3, 5, 4 }, K = 3;
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << getSum(arr, K, n) << endl;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of above approach
import java.util.*;
class Solution
{

static int getSum(int arr[], int K, int n)
{
    int sum = 0;
    PriorityQueue<Integer> maxHeap =
                          new PriorityQueue<Integer>(n,Collections.reverseOrder());
    for (int i = 0; i < n; i++) {

        // put aint array elements
        // in a max heap
        maxHeap.add(arr[i]);
    }

    while (K-->0) {

        // Get the current maximum element
        int currentMax = (int)maxHeap.peek();

        // Add it to the sum
        sum += currentMax;

        // Remove the current max from the heap
        maxHeap.remove();

        // Add the current max back to the
        // heap after decrementing it by 1
        maxHeap.add(currentMax - 1);
    }
    return sum;
}

// driver code
public static void main(String args[])
{
    int arr[] = { 2, 3, 5, 4 }, K = 3;
    int n =arr.length;
    System.out.println(getSum(arr, K, n));
}
}
//contributed by Arnab Kundu
```

## 蟒蛇 3

```
# Python3 implementation of above approach
def getSum(arr, K, n) :
    Sum = 0
    maxHeap = []
    for i in range(n) :

        # put all array elements
        # in a max heap
        maxHeap.append(arr[i])

    maxHeap.sort()
    maxHeap.reverse()

    while (K > 0) :

        # Get the current maximum element
        currentMax = maxHeap[0]

        # Add it to the sum
        Sum += currentMax

        # Remove the current max from the heap
        maxHeap.pop(0)

        # Add the current max back to the
        # heap after decrementing it by 1
        maxHeap.append(currentMax - 1)
        maxHeap.sort()
        maxHeap.reverse()
        K -= 1

    return Sum

arr = [ 2, 3, 5, 4 ]
K = 3;
n = len(arr)
print(getSum(arr, K, n))

#. This code is contributed by divyeshrabadiya07.
```

## C#

```
// C# implementation of above approach
using System;
using System.Collections.Generic;
class GFG {

    static int getSum(int[] arr, int K, int n)
    {
        int sum = 0;
        List<int> maxHeap = new List<int>();
        for (int i = 0; i < n; i++) {

            // put all array elements
            // in a max heap
            maxHeap.Add(arr[i]);
        }

        maxHeap.Sort();
        maxHeap.Reverse();

        while (K-- > 0) {

            // Get the current maximum element
            int currentMax = maxHeap[0];

            // Add it to the sum
            sum += currentMax;

            // Remove the current max from the heap
            maxHeap.RemoveAt(0);

            // Add the current max back to the
            // heap after decrementing it by 1
            maxHeap.Add(currentMax - 1);
            maxHeap.Sort();
            maxHeap.Reverse();
        }
        return sum;
    } 

  // Driver code
  static void Main()
  {
    int[] arr = { 2, 3, 5, 4 };
    int K = 3;
    int n = arr.Length;
    Console.Write(getSum(arr, K, n));
  }
}

// This code is contributed by divyesh072019.
```

## java 描述语言

```
<script>
    // Javascript implementation of above approach

    function getSum(arr, K, n)
    {
        let sum = 0;
        let maxHeap = [];
        for (let i = 0; i < n; i++) {

            // put all array elements
            // in a max heap
            maxHeap.push(arr[i]);
        }

        maxHeap.sort(function(a, b){return a - b});
        maxHeap.reverse();

        while (K-- > 0) {

            // Get the current maximum element
            let currentMax = maxHeap[0];

            // Add it to the sum
            sum += currentMax;

            // Remove the current max from the heap
            maxHeap.shift();

            // Add the current max back to the
            // heap after decrementing it by 1
            maxHeap.push(currentMax - 1);
            maxHeap.sort(function(a, b){return a - b});
            maxHeap.reverse();
        }
        return sum;
    }

    // Driver code
    let arr = [ 2, 3, 5, 4 ];
    let K = 3;
    let n = arr.length;
    document.write(getSum(arr, K, n));

    // This code is contributed by suresh07.
</script>
```

**Output:** 

```
13
```
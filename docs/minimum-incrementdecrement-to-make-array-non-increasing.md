# 使数组不增加的最小增量/减量

> 原文:[https://www . geesforgeks . org/minimum-increment 减量-to-make-array-non-递增/](https://www.geeksforgeeks.org/minimum-incrementdecrement-to-make-array-non-increasing/)

给定一个数组 a，你的任务是把它转换成一个不递增的形式，这样我们就可以在尽可能少的变化中把数组值递增或递减 1。

**示例:**

```
Input : a[] = {3, 1, 2, 1}
Output : 1
Explanation :
We can convert the array into 3 1 1 1 by
changing 3rd element of array i.e. 2 
into its previous integer 1 in one step
hence only one step is required.

Input : a[] = {3, 1, 5, 1}
Output : 4
We need to decrease 5 to 1 to make array sorted
in non-increasing order.

Input : a[] = {1, 5, 5, 5}
Output : 4
We need to increase 1 to 5.
```

**蛮力方法:**我们考虑每个元素的两种可能性，并找到两种可能性的最小值。

**有效方法:**计算最终数组元素和当前数组元素之间的绝对差之和。因此，答案将是第 I 个元素和在此之前出现的最小元素之差的总和。为此，我们可以维护一个最小堆来查找在此之前遇到的最小元素。在最小优先级队列中，我们将把元素和新元素与之前的最小值进行比较。如果找到新的最小值，我们将更新它，这样做是因为每个下一个要来的元素应该比目前找到的最小元素小。在这里，我们计算差，这样我们就可以得到我们必须改变当前数字的多少，以便它等于或小于之前遇到的数字。最后，所有这些差异的总和将是我们的答案，因为这将给出我们必须改变元素的最终值。

下面是上述方法的实现:

## C++

```
// CPP code to count the change required to
// convert the array into non-increasing array
#include <bits/stdc++.h>
using namespace std;

int DecreasingArray(int a[], int n)
{
    int sum = 0, dif = 0;

    // min heap
    priority_queue<int, vector<int>, greater<int> > pq;

    // Here in the loop we will
    // check that whether the upcoming
    // element of array is less than top
    // of priority queue. If yes then we
    // calculate the difference. After
    // that we will remove that element
    // and push the current element in
    // queue. And the sum is incremented
    // by the value of difference
    for (int i = 0; i < n; i++) {
        if (!pq.empty() && pq.top() < a[i]) {
            dif = a[i] - pq.top();
            sum += dif;
            pq.pop();
        }
        pq.push(a[i]);
    }

    return sum;
}

// Driver Code
int main()
{
    int a[] = { 3, 1, 2, 1 };
    int n = sizeof(a) / sizeof(a[0]);

    cout << DecreasingArray(a, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to count the change required to
// convert the array into non-increasing array
import java.util.PriorityQueue;

class GFG
{
    public static int DecreasingArray(int a[], int n)
    {
        int sum = 0, dif = 0;

        PriorityQueue<Integer> pq = new PriorityQueue<>();

        // Here in the loop we will
        // check that whether the upcoming
        // element of array is less than top
        // of priority queue. If yes then we
        // calculate the difference. After
        // that we will remove that element
        // and push the current element in
        // queue. And the sum is incremented
        // by the value of difference
        for (int i = 0; i < n; i++)
        {
            if (!pq.isEmpty() && pq.element() < a[i])
            {
                dif = a[i] - pq.element();
                sum += dif;
                pq.remove();
            }
            pq.add(a[i]);
        }

    return sum;
    }

    // Driver Code
    public static void main(String[] args)
    {

        int[] a = {3, 1, 2, 1};

        int n = a.length;

        System.out.println(DecreasingArray(a, n));
    }
}

// This Code is contributed by sanjeev2552
```

## 蟒蛇 3

```
# Python3 code to count the change required to
# convert the array into non-increasing array
from queue import PriorityQueue

def DecreasingArray(a, n):

    ss, dif = (0,0)

    # min heap
    pq = PriorityQueue()

    # Here in the loop we will
    # check that whether the upcoming
    # element of array is less than top
    # of priority queue. If yes then we
    # calculate the difference. After
    # that we will remove that element
    # and push the current element in
    # queue. And the sum is incremented
    # by the value of difference
    for i in range(n):
        tmp = 0

        if not pq.empty():
            tmp = pq.get()
            pq.put(tmp)

        if not pq.empty() and tmp < a[i]:
            dif = a[i] - tmp
            ss += dif
            pq.get()

        pq.put(a[i])

    return ss

# Driver code   
if __name__=="__main__":

    a = [ 3, 1, 2, 1 ]
    n = len(a)

    print(DecreasingArray(a, n))

# This code is contributed by rutvik_56
```

## C#

```
// C# code to count the change required to
// convert the array into non-increasing array
using System;
using System.Collections.Generic;
class GFG
{
    static int DecreasingArray(int[] a, int n)
    {
        int sum = 0, dif = 0;

        // min heap
        List<int> pq = new List<int>();

        // Here in the loop we will
        // check that whether the upcoming
        // element of array is less than top
        // of priority queue. If yes then we
        // calculate the difference. After
        // that we will remove that element
        // and push the current element in
        // queue. And the sum is incremented
        // by the value of difference
        for (int i = 0; i < n; i++)
        {
            if (pq.Count > 0 && pq[0] < a[i])
            {
                dif = a[i] - pq[0];
                sum += dif;
                pq.RemoveAt(0);
            }
            pq.Add(a[i]);
            pq.Sort();
        }

        return sum;
    }  

  // Driver code
  static void Main()
  {
    int[] a = { 3, 1, 2, 1 };
    int n = a.Length;

    Console.Write(DecreasingArray(a, n));
  }
}

// This code is contributed by divyeshrabadiya07.
```

## java 描述语言

```
<script>

// Javascript code to count the change required to
// convert the array into non-increasing array
function DecreasingArray(a, n)
{
    var sum = 0, dif = 0;

    // min heap
    var pq = [];

    // Here in the loop we will
    // check that whether the upcoming
    // element of array is less than top
    // of priority queue. If yes then we
    // calculate the difference. After
    // that we will remove that element
    // and push the current element in
    // queue. And the sum is incremented
    // by the value of difference
    for (var i = 0; i < n; i++)
    {
        if (pq.length != 0 && pq[pq.length - 1] < a[i]) {
            dif = a[i] - pq[pq.length - 1];
            sum += dif;
            pq.pop();
        }
        pq.push(a[i]);
        pq.sort((a, b)=>b - a);
    }

    return sum;
}

// Driver Code
var a = [3, 1, 2, 1];
var n = a.length;
document.write(DecreasingArray(a, n));

// This code is contributed by rrrtnx.
</script>
```

**Output:** 

```
1
```

**时间复杂度:O(n log(n))**
**空间复杂度:** **O(n)**
另见:[转换为变化最小的严格递增阵。](https://www.geeksforgeeks.org/convert-strictly-increasing-array-minimum-changes/)
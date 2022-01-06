# 通过最多执行 K 次增量运算

最大化等元素子阵列的长度

> 原文:[https://www . geeksforgeeks . org/通过执行最多 k 个增量操作来最大化等元素子数组的长度/](https://www.geeksforgeeks.org/maximize-length-of-subarray-of-equal-elements-by-performing-at-most-k-increment-operations/)

给定一个由 **N** 整数和一个整数 **K** 组成的数组**A【】**，任务是在对数组元素执行最多 **K** 增量 1 后，最大化具有**相等**元素的子数组的长度。

**注意:**同一个数组元素可以多次递增。

**示例:**

> **输入:** A[] = {2，4，8，5，9，6}，K = 6
> **输出:** 3
> **说明:**
> 斯巴瑞【8，5，9】可以修改为【9，9，9】。
> 所需增量总数为 5，小于 K(= 6)。
> 
> **输入:** A[] = {2，2，4}，K = 10
> T3】输出: 3

天真方法:解决这个问题最简单的方法是生成所有可能的子阵列，对于每个子阵列，检查它的所有元素是否可以以最多 K 个增量相等。打印获得的此类子阵列的最大长度。

***时间复杂度:**O(N<sup>3</sup>)*
***辅助空间:** O(1)*

**方法:**上述方法可以使用[滑动窗口技术](https://www.geeksforgeeks.org/window-sliding-technique/)进行优化。按照以下步骤解决问题:

*   记录窗口的**最大**元素。
*   特定窗口所需的总运算量通过以下等式获得:

> 操作计数=(到目前为止计算的窗口长度+ 1) *(窗口的最大元素)-窗口的总和

*   现在，检查上述计算值是否超过 **K** 。如果是，那么向右滑动窗口的开始指针，否则增加到目前为止计算的窗口长度。
*   重复以上步骤，获得满足要求条件的最长窗口。

下面是上述方法的实现:

## C++14

```
// C++14 program for above approach
#include <bits/stdc++.h>
using namespace std;
#define newl "\n"

// Function to find the maximum length
// of subarray of equal elements after
// performing at most K increments
int maxSubarray(int a[], int k, int n)
{

    // Stores the size
    // of required subarray
    int answer = 0;

    // Starting point of a window
    int start = 0;

    // Stores the sum of window
    long int s = 0;

    deque<int> dq;

    // Iterate over array
    for(int i = 0; i < n; i++)
    {

        // Current element
        int x = a[i];

        // Remove index of minimum elements
        // from deque which are less than
        // the current element
        while (!dq.empty() &&
               a[dq.front()] <= x)
            dq.pop_front();

        // Insert current index in deque
        dq.push_back(i);

        // Update current window sum
        s += x;

        // Calculate required operation to
        // make current window elements equal
        long int cost = (long int)a[dq.front()] *
                        (answer + 1) - s;

        // If cost is less than k
        if (cost <= (long int)k)
            answer++;

        // Shift window start pointer towards
        // right and update current window sum
        else
        {
            if (dq.front() == start)
                dq.pop_front();

            s -= a[start++];
        }
    }

    // Return answer
    return answer;
}

// Driver Code
int main()
{
    int a[] = { 2, 2, 4 };
    int k = 10;

    // Length of array
    int n = sizeof(a) / sizeof(a[0]);

    cout << (maxSubarray(a, k, n));

    return 0;
}

// This code is contributed by jojo9911
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program for above approach
import java.util.*;

class GFG {

    // Function to find the maximum length
    // of subarray of equal elements after
    // performing at most K increments
    static int maxSubarray(int[] a, int k)
    {
        // Length of array
        int n = a.length;

        // Stores the size
        // of required subarray
        int answer = 0;

        // Starting point of a window
        int start = 0;

        // Stores the sum of window
        long s = 0;

        Deque<Integer> dq = new LinkedList<>();

        // Iterate over array
        for (int i = 0; i < n; i++) {

            // Current element
            int x = a[i];

            // Remove index of minimum elements
            // from deque which are less than
            // the current element
            while (!dq.isEmpty() && a[dq.peek()] <= x)
                dq.poll();

            // Insert current index in deque
            dq.add(i);

            // Update current window sum
            s += x;

            // Calculate required operation to
            // make current window elements equal
            long cost
                = (long)a[dq.peekFirst()] * (answer + 1)
                  - s;

            // If cost is less than k
            if (cost <= (long)k)
                answer++;

            // Shift window start pointer towards
            // right and update current window sum
            else {
                if (dq.peekFirst() == start)
                    dq.pollFirst();
                s -= a[start++];
            }
        }

        // Return answer
        return answer;
    }

    // Driver Code
    public static void main(String[] args)
    {

        int[] a = { 2, 2, 4 };
        int k = 10;

        // Function call
        System.out.println(maxSubarray(a, k));
    }
}
```

## 蟒蛇 3

```
# Python3 program for above approach
from collections import deque

# Function to find the maximum length
# of subarray of equal elements after
# performing at most K increments
def maxSubarray(a, k):

    # Length of array
    n = len(a)

    # Stores the size
    # of required subarray
    answer = 0

    # Starting po of a window
    start = 0

    # Stores the sum of window
    s = 0

    dq = deque()

    # Iterate over array
    for i in range(n):

        # Current element
        x = a[i]

        # Remove index of minimum elements
        # from deque which are less than
        # the current element
        while (len(dq) > 0 and a[dq[-1]] <= x):
            dq.popleft()

        # Insert current index in deque
        dq.append(i)

        # Update current window sum
        s += x

        # Calculate required operation to
        # make current window elements equal
        cost = a[dq[0]] * (answer + 1) - s

        # If cost is less than k
        if (cost <= k):
            answer += 1

        # Shift window start pointer towards
        # right and update current window sum
        else:
            if (dq[0] == start):
                dq.popleft()

            s -= a[start]
            start += 1

    # Return answer
    return answer

# Driver Code
if __name__ == '__main__':

    a = [ 2, 2, 4 ]
    k = 10

    # Function call
    print(maxSubarray(a, k))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# Program for
// the above approach
using System;
using System.Collections.Generic;
class GFG{

// Function to find the maximum length
// of subarray of equal elements after
// performing at most K increments
static int maxSubarray(int[] a, int k)
{
  // Length of array
  int n = a.Length;

  // Stores the size
  // of required subarray
  int answer = 0;

  // Starting point of a window
  int start = 0;

  // Stores the sum of window
  long s = 0;

  Queue<int> dq = new Queue<int>();

  // Iterate over array
  for (int i = 0; i < n; i++)
  {
    // Current element
    int x = a[i];

    // Remove index of minimum
    // elements from deque
    // which are less than
    // the current element
    while (dq.Count!=0 &&
           a[dq.Peek()] <= x)
      dq.Dequeue();

    // Insert current
    // index in deque
    dq.Enqueue(i);

    // Update current window sum
    s += x;

    // Calculate required operation to
    // make current window elements equal
    long cost = (long)a[dq.Peek()] *
                (answer + 1) - s;

    // If cost is less than k
    if (cost <= (long)k)
      answer++;

    // Shift window start pointer towards
    // right and update current window sum
    else
    {
      if (dq.Peek() == start)
        dq.Dequeue();
      s -= a[start++];
    }
  }

  // Return answer
  return answer;
}

// Driver Code
public static void Main(String[] args)
{
  int[] a = {2, 2, 4};
  int k = 10;

  // Function call
  Console.WriteLine(maxSubarray(a, k));
}
}

// This code is contributed by gauravrajput1
```

## java 描述语言

```
<script>

// Javascript program for above approach

// Function to find the maximum length
// of subarray of equal elements after
// performing at most K increments
function maxSubarray(a, k, n)
{

    // Stores the size
    // of required subarray
    var answer = 0;

    // Starting point of a window
    var start = 0;

    // Stores the sum of window
    var s = 0;

    var dq = [];

    // Iterate over array
    for(var i = 0; i < n; i++)
    {

        // Current element
        var x = a[i];

        // Remove index of minimum elements
        // from deque which are less than
        // the current element
        while (dq.length!=0 &&
               a[dq[0]] <= x)
            dq.shift();

        // Insert current index in deque
        dq.push(i);

        // Update current window sum
        s += x;

        // Calculate required operation to
        // make current window elements equal
        var cost = a[dq[0]] *
                        (answer + 1) - s;

        // If cost is less than k
        if (cost <= k)
            answer++;

        // Shift window start pointer towards
        // right and update current window sum
        else
        {
            if (dq[0] == start)
                dq.shift();

            s -= a[start++];
        }
    }

    // Return answer
    return answer;
}

// Driver Code
var a = [2, 2, 4];
var k = 10;

// Length of array
var n = a.length;

document.write(maxSubarray(a, k, n));

</script>
```

**Output:** 

```
3
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)
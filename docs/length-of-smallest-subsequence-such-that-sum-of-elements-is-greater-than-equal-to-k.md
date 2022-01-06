# 最小子序列的长度，使得元素之和大于或等于 K

> 原文:[https://www . geeksforgeeks . org/最小子序列长度-元素和大于等于 k/](https://www.geeksforgeeks.org/length-of-smallest-subsequence-such-that-sum-of-elements-is-greater-than-equal-to-k/)

给定一个大小为 N 且数量为 K 的数组 **arr[]** ，任务是找到最小子序列的长度，使得子序列的和大于或等于数量 K。
**示例:**

> **输入:** arr[] = {2，3，1，5，6，3，7，9，14，10，2，5}，K = 35
> **输出:** 4
> 总和大于或等于给定总和 K 的最小子序列为{7，9，14，10}
> **输入:** arr[] = {1，2，2，3，4，5，4，7，6，5，12}，K

**进场:**

*   这个问题可以借助[优先级队列](https://www.geeksforgeeks.org/priority-queue-set-1-introduction/)解决
*   遍历输入数组，并将每个数组元素插入优先级队列。
*   初始化保存从优先级队列中挑选的元素和变量之和的变量，以将从优先级队列中挑选的元素计数设置为 0
*   将元素从优先级队列中弹出，直到优先级队列不为空
    1.  将元素添加到**和**中
    2.  增加计数，因为该元素被挑选以贡献总和
    3.  检查**之和**是否大于给定数值 **K** ，如果是，则停止检查并输出计数。

下面是上述方法的实现。

## C++

```
// C++ implementation to find length of smallest
// subsequence such that sum of elements
// is greater than equal to given number K

#include <bits/stdc++.h>
using namespace std;

// Function to find the smallest
// subsequence such that sum of elements
// is greater than equal to given number K
int lengthOfSmallestSubsequence(int K, vector<int> v)
{
    // Initialize priority queue
    priority_queue<int> pq;

    // Loop to insert all elements into
    // the priority queue
    for (int i = 0; i < v.size(); i++) {
        pq.push(v[i]);
    }
    int sum = 0, count = 0;

    // Loop to find the smallest
    // subsequence such that sum of elements
    // is greater than equal to given number K
    while (!pq.empty() && sum < K) {
        sum += pq.top();
        pq.pop();
        count++;
    }
    // If sum is less then K
    // then return -1 else return count.
    if (sum < K) {
        return -1;
    }
    return count;
}

// Driver code
int main()
{

    vector<int> v{ 2, 3, 1, 5,
                   6, 3, 7, 9,
                   14, 10, 2, 5 };
    int K = 35;

    cout << lengthOfSmallestSubsequence(K, v);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find length of smallest
// subsequence such that sum of elements
// is greater than equal to given number K
import java.util.*;

class GFG
{

// Function to find the smallest
// subsequence such that sum of elements
// is greater than equal to given number K
static int lengthOfSmallestSubsequence(int K, int []v)
{
    // Initialize priority queue
    Queue<Integer> pq =
            new PriorityQueue<Integer>(Collections.reverseOrder());

    // Loop to insert all elements into
    // the priority queue
    for (int i = 0; i < v.length; i++)
    {
        pq.add(v[i]);
    }
    int sum = 0, count = 0;

    // Loop to find the smallest
    // subsequence such that sum of elements
    // is greater than equal to given number K
    while (!pq.isEmpty() && sum < K)
    {
        sum += pq.peek();
        pq.remove();
        count++;
    }

    // If sum is less then K
    // then return -1 else return count.
    if (sum < K)
    {
        return -1;
    }
    return count;
}

// Driver code
public static void main(String[] args)
{
    int []v = { 2, 3, 1, 5,
                6, 3, 7, 9,
                14, 10, 2, 5 };
    int K = 35;
    System.out.print(lengthOfSmallestSubsequence(K, v));
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 implementation to find length of smallest
# subsequence such that sum of elements
# is greater than equal to given number K

# Function to find the smallest
# subsequence such that sum of elements
# is greater than equal to given number K
def lengthOfSmallestSubsequence(K, v):

    # Initialize priority queue
    pq = []

    # Loop to insert all elements into
    # the priority queue
    for i in v:
        pq.append(i)
    pq.sort()

    sum = 0
    count = 0

    # Loop to find the smallest
    # subsequence such that sum of elements
    # is greater than equal to given number K
    while (len(pq) > 0 and sum < K):
        sum += pq[-1]
        del pq[-1]
        count += 1

    # If sum is less then K
    # then return -1 else return count.
    if (sum < K):
        return -1
    return count

# Driver code
v = [2, 3, 1, 5,
    6, 3, 7, 9,
    14, 10, 2, 5]
K = 35

print(lengthOfSmallestSubsequence(K, v))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# implementation to find length of smallest
// subsequence such that sum of elements
// is greater than equal to given number K using System;
using System;
using System.Collections.Generic;
using System.Linq;
class GFG
{

  // Function to find the smallest
  // subsequence such that sum of elements
  // is greater than equal to given number K
  static int lengthOfSmallestSubsequence(int K, int []v)
  {

    // Initialize List
    List<int> pq = new List<int>();

    // Loop to insert all elements into
    // the List
    for (int i = 0; i < v.Length; i++) 
    {
      pq.Add(v[i]);
    }

    // Sort list in reverse order
    pq.Sort();
    pq.Reverse();
    int sum = 0;
    int count = 0;

    // Loop to find the smallest
    // subsequence such that sum of elements
    // is greater than equal to given number K
    while(pq.Count > 0 && sum < K)
    {
      sum += pq[0];
      pq.RemoveAt(0);
      count++;
    }

    // If sum is less then K
    // then return -1 else return count.
    if (sum < K)
    {
      return -1;
    }
    return count;
  }

  // Driver code
  static public void Main ()
  {
    int []v = { 2, 3, 1, 5,6, 3, 7, 9, 14, 10, 2, 5 };
    int K = 35;
    Console.WriteLine(lengthOfSmallestSubsequence(K, v));
  }
}

// This code is contributed by avanitrachhadiya2155
```

## java 描述语言

```
<script>

// JavaScript implementation to find length of smallest
// subsequence such that sum of elements
// is greater than equal to given number K using System;

// Function to find the smallest
// subsequence such that sum of elements
// is greater than equal to given number K
function lengthOfSmallestSubsequence(K, v) {

    // Initialize List
    let pq = new Array();

    // Loop to insert all elements into
    // the List
    for (let i = 0; i < v.length; i++) {
        pq.push(v[i]);
    }

    // Sort list in reverse order
    pq.sort((a, b) => b - a);

    let sum = 0;
    let count = 0;

    // Loop to find the smallest
    // subsequence such that sum of elements
    // is greater than equal to given number K
    while (pq.length > 0 && sum < K) {
        sum += pq[0];
        pq.splice(0, 1);
        count++;
    }

    // If sum is less then K
    // then return -1 else return count.
    if (sum < K) {
        return -1;
    }
    return count;
}

// Driver code
let v = [2, 3, 1, 5, 6, 3, 7, 9, 14, 10, 2, 5];
let K = 35;
document.write(lengthOfSmallestSubsequence(K, v));

// This code is contributed by gfgking

</script>
```

**Output:** 

```
4
```
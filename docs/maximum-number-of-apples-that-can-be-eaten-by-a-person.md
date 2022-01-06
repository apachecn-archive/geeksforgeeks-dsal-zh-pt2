# 一个人能吃的苹果最大数量

> 原文:[https://www . geeksforgeeks . org/最多可被一个人吃掉的苹果数量/](https://www.geeksforgeeks.org/maximum-number-of-apples-that-can-be-eaten-by-a-person/)

给定两个[数组](https://www.geeksforgeeks.org/array-data-structure/) **苹果【】**和**天数【】**分别代表一棵苹果树从 **i <sup>th</sup>** 日开始的苹果产量和这些苹果可食用的天数，任务是找到一个人一天最多能吃一个苹果的最大苹果数。

**示例**

> **输入:**苹果[] = { 1，2，3，5，2 }，天[] = { 3，2，1，4，2 }
> **输出:** 7
> **说明:**
> 1<sup>ST</sup>日，人在 1 <sup>st</sup> 日吃苹果树生产的苹果。
> 2<sup>日</sup>日，人在 2 <sup>日</sup>日吃苹果树生产的苹果。
> 第 3 <sup>日</sup>日，人在第 2 <sup>日</sup>吃苹果树生产的苹果。
> 4<sup>日</sup>至 7 <sup>日</sup>日，人在 4 <sup>日</sup>吃苹果树生产的苹果。
> 
> **输入:**苹果[] = { 3，0，0，0，0，2 }，天[] = { 3，0，0，0，0，2 }
> **输出:** 5

**做法:**想法是吃最接近保质期的苹果。按照以下步骤解决问题:

*   初始化一个[优先级队列](https://www.geeksforgeeks.org/priority-queue-in-cpp-stl/)来存储在**I<sup>th</sup>T5【日】生产的苹果数量以及这些苹果的过期日期。**
*   [遍历两个数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，在**I<sup>th</sup>T5【日】插入苹果的数量和苹果树生产的苹果的过期日期。**
*   检查 priority_queue 的[顶部元素的过期日期是否已过期。如果发现为真，则](https://www.geeksforgeeks.org/priority_queuetop-c-stl/)[从优先级队列](https://www.geeksforgeeks.org/priority_queuepush-priority_queuepop-c-stl/)中弹出元素。
*   否则，增加最大计数，减少[优先级队列](https://www.geeksforgeeks.org/priority-queue-in-cpp-stl/)中的苹果数。
*   最后，打印获得的最大计数。

以下是上述方法的实现:

## C++

```
// C++ program of the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the maximum number of apples
// a person can eat such that the person eat
// at most one apple in a day.
int cntMaxApples(vector<int> apples, vector<int> days)
{

    // Stores count of apples and number
    // of days those apples are edible
    typedef pair<int, int> P;

    // Store count of apples and number
    // of days those apples are edible
    priority_queue<P, vector

<p>, greater

<p> > pq;

    // Stores indices of the array
    int i = 0;

    // Stores count of days
    int n = apples.size();

    // Stores maximum count of
    // edible apples
    int total_apples = 0;

    // Traverse both the arrays
    while (i < n || !pq.empty()) {

        // If top element of the apple
        // is not already expired
        if (i < n && apples[i] != 0) {

            // Insert count of apples and
            // their expiration date
            pq.push({ i + days[i] - 1, apples[i] });
        }

        // Remove outdated apples
        while (!pq.empty() && pq.top().first < i) {
            pq.pop();
        }

        // Insert all the apples produces by
        // tree on current day
        if (!pq.empty()) {

            // Stores top element of pq
            auto curr = pq.top();

            // Remove top element of pq
            pq.pop();

            // If count of apples in curr
            // is greater than 0
            if (curr.second > 1) {

                // Insert count of apples and
                // their expiration date
                pq.push({ curr.first,
                          curr.second - 1 });
            }

            // Update total_apples
            ++total_apples;
        }

        // Update index
        ++i;
    }

    return total_apples;
}

// Driver Code
int main()
{
    vector<int> apples = { 1, 2, 3, 5, 2 };
    vector<int> days = { 3, 2, 1, 4, 2 };
    cout << cntMaxApples(apples, days);
    return 0;
}
```

## 蟒蛇 3

```
# Python3 program of the above approach

# Function to find the maximum number of apples
# a person can eat such that the person eat
# at most one apple in a day.
def cntMaxApples(apples, days) :

    # Store count of apples and number
    # of days those apples are edible
    pq = []

    # Stores indices of the array
    i = 0

    # Stores count of days
    n = len(apples)

    # Stores maximum count of
    # edible apples
    total_apples = 0

    # Traverse both the arrays
    while (i < n or len(pq) > 0) :

      # If top element of the apple
      # is not already expired
      if (i < n and apples[i] != 0) :

        # Insert count of apples and
        # their expiration date
        pq.append([i + days[i] - 1, apples[i]])
        pq.sort()

      # Remove outdated apples
      while (len(pq) > 0 and pq[0][0] < i) :
        pq.pop(0)

      # Insert all the apples produces by
      # tree on current day
      if (len(pq) > 0) :

        # Stores top element of pq
        curr = pq[0]

        # Remove top element of pq
        pq.pop(0)

        # If count of apples in curr
        # is greater than 0
        if (len(curr) > 1) :

          # Insert count of apples and
          # their expiration date
          pq.append([curr[0], curr[1] - 1])
          pq.sort()

        # Update total_apples
        total_apples += 1

      # Update index
      i += 1

    return total_apples

apples = [ 1, 2, 3, 5, 2 ]
days = [ 3, 2, 1, 4, 2 ]

print(cntMaxApples(apples, days))

# This code is contributed by divyesh072019
```

## C#

```
// C# program of the above approach
using System;
using System.Collections.Generic;
class GFG {

  // Function to find the maximum number of apples
  // a person can eat such that the person eat
  // at most one apple in a day.
  static int cntMaxApples(int[] apples, int[] days)
  {

    // Store count of apples and number
    // of days those apples are edible
    List<Tuple<int,int>> pq = new List<Tuple<int,int>>();

    // Stores indices of the array
    int i = 0;

    // Stores count of days
    int n = apples.Length;

    // Stores maximum count of
    // edible apples
    int total_apples = 0;

    // Traverse both the arrays
    while (i < n || pq.Count > 0) {

      // If top element of the apple
      // is not already expired
      if (i < n && apples[i] != 0) {

        // Insert count of apples and
        // their expiration date
        pq.Add(new Tuple<int,int>(i + days[i] - 1, apples[i]));
        pq.Sort();
      }

      // Remove outdated apples
      while (pq.Count > 0 && pq[0].Item1 < i) {
        pq.RemoveAt(0);
      }

      // Insert all the apples produces by
      // tree on current day
      if (pq.Count > 0) {

        // Stores top element of pq
        Tuple<int,int> curr = pq[0];

        // Remove top element of pq
        pq.RemoveAt(0);

        // If count of apples in curr
        // is greater than 0
        if (curr.Item2 > 1) {

          // Insert count of apples and
          // their expiration date
          pq.Add(new Tuple<int,int>(curr.Item1, curr.Item2 - 1));
          pq.Sort();
        }

        // Update total_apples
        ++total_apples;
      }

      // Update index
      ++i;
    }

    return total_apples;
  }   

  // Driver code
  static void Main() {
    int[] apples = { 1, 2, 3, 5, 2 };
    int[] days = { 3, 2, 1, 4, 2 };

    Console.Write(cntMaxApples(apples, days));
  }
}

// This code is contributed by divyeshrabadiya07.
```

**Output:** 

```
7
```

***时间复杂度:** O(NlogN)*
***辅助空间:** O(N)*
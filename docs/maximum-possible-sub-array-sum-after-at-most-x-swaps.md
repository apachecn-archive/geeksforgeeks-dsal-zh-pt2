# 最多 X 次交换后最大可能的子阵列总和

> 原文:[https://www . geesforgeks . org/最大可能子数组-最多 x 次交换后求和/](https://www.geeksforgeeks.org/maximum-possible-sub-array-sum-after-at-most-x-swaps/)

给定一个由 **N** 个整数和一个整数 **X** 组成的数组 **arr[]** ，任务是在最多应用 **X** 次交换后找到最大可能的子数组和。
**举例:**

> **输入:** arr[] = {5，-1，2，3，4，-2，5}，X = 2
> **输出:** 19
> 交换(arr[0]，arr[1])和(arr[5]，arr[6])。
> 现在，最大子阵和将为(5 + 2 + 3 + 4 + 5) = 19
> **输入:** arr[] = {-2，-3，-1，-10}，X = 10
> **输出:** -1

**方法:**对于每个可能的子阵列，将不属于该子阵列的元素视为已丢弃。现在，当剩下交换并且当前考虑的子阵列的和可以最大化时，即丢弃的元素中最大的元素可以与子阵列的最小元素交换，保持更新子阵列的和。当没有剩余的交换或子阵列总和不能进一步最大化时，更新到目前为止找到的当前最大子阵列总和，这将是最终所需的答案。
以下是上述办法的实施情况:

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the maximum
// sub-array sum after at most x swaps
int SubarraySum(int a[], int n, int x)
{
    // To store the required answer
    int ans = -10000;

    // For all possible intervals
    for (int i = 0; i < n; i++) {
        for (int j = i; j < n; j++) {

            // Keep current ans as zero
            int curans = 0;

            // To store the integers which are
            // not part of the sub-array
            // currently under consideration
            priority_queue<int, vector<int> > pq;

            // To store elements which are
            // part of the sub-array
            // currently under consideration
            priority_queue<int, vector<int>, greater<int> > pq2;

            // Create two sets
            for (int k = 0; k < n; k++) {
                if (k >= i && k <= j) {
                    curans += a[k];
                    pq2.push(a[k]);
                }
                else
                    pq.push(a[k]);
            }
            ans = max(ans, curans);

            // Swap at most X elements
            for (int k = 1; k <= x; k++) {
                if (pq.empty() || pq2.empty()
                    || pq2.top() >= pq.top())
                    break;

                // Remove the minimum of
                // the taken elements
                curans -= pq2.top();
                pq2.pop();

                // Add maximum of the
                // discarded elements
                curans += pq.top();
                pq.pop();

                // Update the answer
                ans = max(ans, curans);
            }
        }
    }

    // Return the maximized sub-array sum
    return ans;
}

// Driver code
int main()
{
    int a[] = { 5, -1, 2, 3, 4, -2, 5 }, x = 2;
    int n = sizeof(a) / sizeof(a[0]);

    cout << SubarraySum(a, n, x);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.io.*;
import java.util.*;
class GFG
{

  // Function to return the maximum
  // sub-array sum after at most x swaps
  static int SubarraySum(int[] a, int n, int x)
  {

    // To store the required answer
    int ans = -10000;

    // For all possible intervals
    for (int i = 0; i < n; i++)
    {
      for (int j = i; j < n; j++)
      {

        // Keep current ans as zero
        int curans = 0;

        // To store the integers which are
        // not part of the sub-array
        // currently under consideration
        ArrayList<Integer> pq = new ArrayList<Integer>();

        // To store elements which are
        // part of the sub-array
        // currently under consideration
        ArrayList<Integer> pq2 = new ArrayList<Integer>();

        // Create two sets
        for (int k = 0; k < n; k++) {
          if (k >= i && k <= j) {
            curans += a[k];
            pq2.add(a[k]);
          }
          else
            pq.add(a[k]);
        }

        Collections.sort(pq);
        Collections.reverse(pq);
        Collections.sort(pq2);

        ans = Math.max(ans, curans);

        // Swap at most X elements
        for (int k = 1; k <= x; k++) {
          if (pq.size() == 0 || pq2.size() == 0
              || pq2.get(0) >= pq.get(0))
            break;

          // Remove the minimum of
          // the taken elements
          curans -= pq2.get(0);
          pq2.remove(0);

          // Add maximum of the
          // discarded elements
          curans += pq.get(0);
          pq.remove(0);

          // Update the answer
          ans = Math.max(ans, curans);
        }
      }
    }

    // Return the maximized sub-array sum
    return ans;
  }

  // Driver code.
  public static void main (String[] args)
  {

    int[] a = { 5, -1, 2, 3, 4, -2, 5 };
    int x = 2;
    int n = a.length;

    System.out.println(SubarraySum(a, n, x));
  }
}

// This code is contributed by avanitrachhadiya2155
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the maximum
# sub-array sum after at most x swaps
def SubarraySum(a, n, x) :

    # To store the required answer
    ans = -10000

    # For all possible intervals
    for i in range(n) :

      for j in range(i, n) :

        # Keep current ans as zero
        curans = 0

        # To store the integers which are
        # not part of the sub-array
        # currently under consideration
        pq = []

        # To store elements which are
        # part of the sub-array
        # currently under consideration
        pq2 = []

        # Create two sets
        for k in range(n) :
          if (k >= i and k <= j) :
            curans += a[k]
            pq2.append(a[k])

          else :
            pq.append(a[k])

        pq.sort()
        pq.reverse()
        pq2.sort()

        ans = max(ans, curans)

        # Swap at most X elements
        for k in range(1, x + 1) :
          if (len(pq) == 0 or len(pq2) == 0 or pq2[0] >= pq[0]) :
            break

          # Remove the minimum of
          # the taken elements
          curans -= pq2[0]
          pq2.pop(0)

          # Add maximum of the
          # discarded elements
          curans += pq[0]
          pq.pop(0)

          # Update the answer
          ans = max(ans, curans)

    # Return the maximized sub-array sum
    return ans

    # Driver code
a = [ 5, -1, 2, 3, 4, -2, 5 ]
x = 2;
n = len(a)
print(SubarraySum(a, n, x))

# This ccode is contributed by divyesh072019.
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;
class GFG
{

  // Function to return the maximum
  // sub-array sum after at most x swaps
  static int SubarraySum(int[] a, int n, int x)
  {

    // To store the required answer
    int ans = -10000;

    // For all possible intervals
    for (int i = 0; i < n; i++)
    {
      for (int j = i; j < n; j++)
      {

        // Keep current ans as zero
        int curans = 0;

        // To store the integers which are
        // not part of the sub-array
        // currently under consideration
        List<int> pq = new List<int>();

        // To store elements which are
        // part of the sub-array
        // currently under consideration
        List<int> pq2 = new List<int>();

        // Create two sets
        for (int k = 0; k < n; k++) {
          if (k >= i && k <= j) {
            curans += a[k];
            pq2.Add(a[k]);
          }
          else
            pq.Add(a[k]);
        }

        pq.Sort();
        pq.Reverse();
        pq2.Sort();

        ans = Math.Max(ans, curans);

        // Swap at most X elements
        for (int k = 1; k <= x; k++) {
          if (pq.Count == 0 || pq2.Count == 0
              || pq2[0] >= pq[0])
            break;

          // Remove the minimum of
          // the taken elements
          curans -= pq2[0];
          pq2.RemoveAt(0);

          // Add maximum of the
          // discarded elements
          curans += pq[0];
          pq.RemoveAt(0);

          // Update the answer
          ans = Math.Max(ans, curans);
        }
      }
    }

    // Return the maximized sub-array sum
    return ans;
  }

  // Driver code.
  static void Main() {
    int[] a = { 5, -1, 2, 3, 4, -2, 5 };
    int x = 2;
    int n = a.Length;
    Console.WriteLine(SubarraySum(a, n, x));
  }
}

// This code is contributed by divyeshrabaiya07.
```

## java 描述语言

```
<script>
    // Javascript implementation of the approach

    // Function to return the maximum
    // sub-array sum after at most x swaps
    function SubarraySum(a, n, x)
    {

      // To store the required answer
      let ans = -10000;

      // For all possible intervals
      for (let i = 0; i < n; i++)
      {
        for (let j = i; j < n; j++)
        {

          // Keep current ans as zero
          let curans = 0;

          // To store the integers which are
          // not part of the sub-array
          // currently under consideration
          let pq = [];

          // To store elements which are
          // part of the sub-array
          // currently under consideration
          let pq2 = [];

          // Create two sets
          for (let k = 0; k < n; k++) {
            if (k >= i && k <= j) {
              curans += a[k];
              pq2.push(a[k]);
            }
            else
              pq.push(a[k]);
          }

          pq.sort();
          pq.reverse();
          pq2.sort();

          ans = Math.max(ans, curans);

          // Swap at most X elements
          for (let k = 1; k <= x; k++) {
            if (pq.length == 0 || pq2.length == 0
                || pq2[0] >= pq[0])
              break;

            // Remove the minimum of
            // the taken elements
            curans -= pq2[0];
            pq2.shift();

            // Add maximum of the
            // discarded elements
            curans += pq[0];
            pq.shift();

            // Update the answer
            ans = Math.max(ans, curans);
          }
        }
      }

      // Return the maximized sub-array sum
      return ans;
    }

    let a = [ 5, -1, 2, 3, 4, -2, 5 ];
    let x = 2;
    let n = a.length;
    document.write(SubarraySum(a, n, x));

        // This code is contributed by suresh07.
</script>
```

**Output:** 

```
19
```
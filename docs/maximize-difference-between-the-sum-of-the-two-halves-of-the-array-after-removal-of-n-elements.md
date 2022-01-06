# 去除 N 个元素后，最大化数组两半之和的差值

> 原文:[https://www . geeksforgeeks . org/n-elements 移除后数组两半之和的最大差值/](https://www.geeksforgeeks.org/maximize-difference-between-the-sum-of-the-two-halves-of-the-array-after-removal-of-n-elements/)

给定一个整数 **N** 和由 **3 * N** 个整数组成的数组**arr【】**，任务是在从数组中精确移除 **N** 个元素后，找出数组前半部分**与后半部分**之间的**最大差值**。

**示例:**

> **输入:** N = 2，arr[] = {3，1，4，1，5，9}
> **输出:** 1
> **解释:**
> 从数组中移除 arr[1]和 arr[5]会使差异最大化=(3+4)–(1+5)= 7–6 = 1。
> 
> **输入:** N = 1，arr[] = {1，2，3 }
> T3】输出: -1

**方法:**
按照下面给出的步骤解决问题

*   从头开始遍历数组，并不断更新数组开始处最大 **N** 个元素的和。
*   同样，从数组末尾开始，不断更新最小 **N** 个元素的和。
*   遍历这些总和，计算每个点的差异，并更新获得的最大差异。
*   打印获得的最大差值。

下面是上述方法的实现:

## C++

```
// C++ Program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to print the maximum difference
// possible between the two halves of the array
long long FindMaxDif(vector<long long> a, int m)
{
    int n = m / 3;

    vector<long long> l(m + 5), r(m + 5);

    // Stores n maximum values from the start
    multiset<long long> s;

    for (int i = 1; i <= m; i++) {

        // Insert first n elements
        if (i <= n) {

            // Update sum of largest n
            // elements from left
            l[i] = a[i - 1] + l[i - 1];
            s.insert(a[i - 1]);
        }

        // For the remaining elements
        else {
            l[i] = l[i - 1];

            // Obtain minimum value
            // in the set
            long long d = *s.begin();

            // Insert only if it is greater
            // than minimum value
            if (a[i - 1] > d) {

                // Update sum from left
                l[i] -= d;
                l[i] += a[i - 1];

                // Remove the minimum
                s.erase(s.find(d));

                // Insert the current element
                s.insert(a[i - 1]);
            }
        }
    }

    // Clear the set
    s.clear();

    // Store n minimum elements from the end
    for (int i = m; i >= 1; i--) {

        // Insert the last n elements
        if (i >= m - n + 1) {

            // Update sum of smallest n
            // elements from right
            r[i] = a[i - 1] + r[i + 1];
            s.insert(a[i - 1]);
        }

        // For the remaining elements
        else {

            r[i] = r[i + 1];

            // Obtain the minimum
            long long d = *s.rbegin();

            // Insert only if it is smaller
            // than maximum value
            if (a[i - 1] < d) {

                // Update sum from right
                r[i] -= d;
                r[i] += a[i - 1];

                // Remove the minimum
                s.erase(s.find(d));

                // Insert the new element
                s.insert(a[i - 1]);
            }
        }
    }

    long long ans = -9e18L;

    for (int i = n; i <= m - n; i++) {

        // Compare the difference and
        // store the maximum
        ans = max(ans, l[i] - r[i + 1]);
    }

    // Return the maximum
    // possible difference
    return ans;
}

// Driver Code
int main()
{

    vector<long long> vtr = { 3, 1, 4, 1, 5, 9 };
    int n = vtr.size();

    cout << FindMaxDif(vtr, n);

    return 0;
}
```

## 蟒蛇 3

```
# Python3 Program to implement
# the above approach

# Function to print the maximum difference
# possible between the two halves of the array
def FindMaxDif(a, m) :

    n = m // 3

    l = [0] * (m + 5)
    r = [0] * (m + 5)

    # Stores n maximum values from the start
    s = []

    for i in range(1, m + 1) :

        # Insert first n elements
        if (i <= n) :

            # Update sum of largest n
            # elements from left
            l[i] = a[i - 1] + l[i - 1]
            s.append(a[i - 1])

        # For the remaining elements
        else :
            l[i] = l[i - 1]

            # Obtain minimum value
            # in the set
            s.sort()
            d = s[0]

            # Insert only if it is greater
            # than minimum value
            if (a[i - 1] > d) :

                # Update sum from left
                l[i] -= d
                l[i] += a[i - 1]

                # Remove the minimum
                s.remove(d)

                # Insert the current element
                s.append(a[i - 1])

    # Clear the set
    s.clear()

    # Store n minimum elements from the end
    for i in range(m, 0, -1) :

        # Insert the last n elements
        if (i >= m - n + 1) :

            # Update sum of smallest n
            # elements from right
            r[i] = a[i - 1] + r[i + 1]
            s.append(a[i - 1])

        # For the remaining elements
        else :

            r[i] = r[i + 1]
            s.sort()

            # Obtain the minimum
            d = s[-1]

            # Insert only if it is smaller
            # than maximum value
            if (a[i - 1] < d) :

                # Update sum from right
                r[i] -= d
                r[i] += a[i - 1]

                # Remove the minimum
                s.remove(d)

                # Insert the new element
                s.append(a[i - 1])

    ans = -9e18

    for i in range(n, m - n + 1) :

        # Compare the difference and
        # store the maximum
        ans = max(ans, l[i] - r[i + 1])

    # Return the maximum
    # possible difference
    return ans

# Driver code 
vtr = [ 3, 1, 4, 1, 5, 9 ]
n = len(vtr)

print(FindMaxDif(vtr, n))

# This code is contributed by divyesh072019
```

## C#

```
// C# program to implement
// the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to print the maximum difference
// possible between the two halves of the array
static long FindMaxDif(List<long> a, int m)
{
    int n = m / 3;

    long[] l = new long[m + 5];
    long[] r = new long[m + 5];

    // Stores n maximum values from the start
    List<long> s = new List<long>();

    for(int i = 1; i <= m; i++)
    {

        // Insert first n elements
        if (i <= n)
        {

            // Update sum of largest n
            // elements from left
            l[i] = a[i - 1] + l[i - 1];
            s.Add(a[i - 1]);
        }

        // For the remaining elements
        else
        {
            l[i] = l[i - 1];

            s.Sort();

            // Obtain minimum value
            // in the set
            long d = s[0];

            // Insert only if it is greater
            // than minimum value
            if (a[i - 1] > d)
            {

                // Update sum from left
                l[i] -= d;
                l[i] += a[i - 1];

                // Remove the minimum
                s.Remove(d);

                // Insert the current element
                s.Add(a[i - 1]);
            }
        }
    }

    // Clear the set
    s.Clear();

    // Store n minimum elements from the end
    for(int i = m; i >= 1; i--)
    {

        // Insert the last n elements
        if (i >= m - n + 1)
        {

            // Update sum of smallest n
            // elements from right
            r[i] = a[i - 1] + r[i + 1];
            s.Add(a[i - 1]);
        }

        // For the remaining elements
        else
        {
            r[i] = r[i + 1];

            s.Sort();

            // Obtain the minimum
            long d = s[s.Count - 1];

            // Insert only if it is smaller
            // than maximum value
            if (a[i - 1] < d)
            {

                // Update sum from right
                r[i] -= d;
                r[i] += a[i - 1];

                // Remove the minimum
                s.Remove(d);

                // Insert the new element
                s.Add(a[i - 1]);
            }
        }
    }

    long ans = (long)(-9e18);

    for(int i = n; i <= m - n; i++)
    {

        // Compare the difference and
        // store the maximum
        ans = Math.Max(ans, l[i] - r[i + 1]);
    }

    // Return the maximum
    // possible difference
    return ans;
}

// Driver Code
static void Main()
{
    List<long> vtr = new List<long>(
        new long[]{ 3, 1, 4, 1, 5, 9 });
    int n = vtr.Count;

    Console.Write(FindMaxDif(vtr, n));
}
}

// This code is contributed by divyeshrabadiya07
```

**Output:** 

```
1
```

***时间复杂度:** O(NlogN)*
***辅助空间:** O(N)*
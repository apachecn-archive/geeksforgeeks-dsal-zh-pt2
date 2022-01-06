# 给定条件下使用递增子序列和子阵列的数组的最大得分

> 原文:[https://www . geesforgeks . org/给定条件下数组使用递增子序列和子数组的最大得分/](https://www.geeksforgeeks.org/maximum-score-of-array-using-increasing-subsequence-and-subarray-with-given-conditions/)

给定数组 **arr[]** 。任务是为**I =【1，N-2】**找到从**arr【】**可以达到的最大得分。评分条件如下。

1.  如果**arr[0…j]<arr[I]<arr[I+1…N-1]**，那么**得分= 2** 。
2.  如果**arr[I-1]<arr[I]<arr[I+1]**且先前条件不满足，则**得分= 1** 。
3.  如果这些条件都不成立，则**得分= 0** 。

**示例:**

> **输入:** arr[] = {1，2，3}
> **输出:** 2
> **说明:**arr[1]的分数等于 2，这是最大可能。
> 
> **输入:** arr[] = {2，4，6，4}
> **输出** : 1
> **说明:**对于 1 <范围内的每个指标 I = I<= 2:
> nums[1]的得分等于 1。
> nums[2]的分数等于 0。
> 因此 1 是最大可能得分。

**方法:**这个问题可以通过使用前缀 Max 和后缀 Min 来解决。按照以下步骤解决给定的问题。

*   元素分数为 **2** 时，应该大于左边的每个元素，小于右边的每个元素。
*   所以预先计算，为每个数组元素找到**前缀 max** 和**后缀 min** 。
*   现在在 **i** 检查每个数组 **arr[]** 元素:
    *   如果在 **i-1** 大于前缀 max，在 **i+1** 小于后缀 min，则得分为 **2** 。
    *   否则如果大于**arr【I-1】**小于**arr【I+1】**，得分为 **1** 。
    *   否则得分将为 **0** 。
*   总结所有的分数，并将其作为最终答案返回。

下面是上述方法的实现。

## C++

```
// C++ program for above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find maximum score
int maxScore(vector<int>& nums)
{

    // Size of array
    int n = nums.size(), i;
    int ans = 0;

    // Prefix max
    vector<int> pre(n, 0);

    // Suffix min
    vector<int> suf(n, 0);

    pre[0] = nums[0];

    for (i = 1; i < n; i++)
        pre[i] = max(pre[i - 1], nums[i]);

    suf[n - 1] = nums[n - 1];
    for (i = n - 2; i >= 0; i--)
        suf[i] = min(suf[i + 1], nums[i]);

    for (i = 1; i < n - 1; i++) {
        if (nums[i] > pre[i - 1]
            && nums[i] < suf[i + 1])
            ans += 2;
        else if (nums[i] > nums[i - 1]
                 && nums[i] < nums[i + 1])
            ans += 1;
    }

    return ans;
}

// Driver Code
int main()
{
    int N = 3;

    vector<int> arr = { 1, 2, 3 };

    // Function Call
    cout << maxScore(arr);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for above approach
import java.util.*;
public class GFG
{

    // Function to find maximum score
    static int maxScore(ArrayList<Integer> nums)
    {

        // Size of array
        int n = nums.size(), i = 0;

        int ans = 0;

        // Prefix max
        int[] pre = new int[n];

        // Suffix min
        int[] suf = new int[n];

        pre[0] = (int)nums.get(0);

        for (i = 1; i < n; i++)
            pre[i] = Math.max(pre[i - 1], (int)nums.get(i));

        suf[n - 1] = (int)nums.get(n - 1);
        for (i = n - 2; i >= 0; i--)
            suf[i] = Math.min(suf[i + 1], (int)nums.get(i));

        for (i = 1; i < n - 1; i++) {
            if ((int)nums.get(i) > pre[i - 1]
                && (int)nums.get(i) < suf[i + 1])
                ans += 2;
            else if ((int)nums.get(i) > (int)nums.get(i - 1)
                     && (int)nums.get(i) < (int)nums.get(i + 1))
                ans += 1;
        }

        return ans;
    }

    // Driver Code
    public static void main(String args[])
    {

        ArrayList<Integer> arr = new ArrayList<Integer>();

        arr.add(1);
        arr.add(2);
        arr.add(3);

        // Function Call
        System.out.println(maxScore(arr));
    }
}

// This code is contributed by Samim Hossain Mondal.
```

## 蟒蛇 3

```
# python program for above approach

# Function to find maximum score
def maxScore(nums):

    # Size of array
    n = len(nums)
    ans = 0

    # Prefix max
    pre = [0 for _ in range(n)]

    # Suffix min
    suf = [0 for _ in range(n)]

    pre[0] = nums[0]

    for i in range(1, n):
        pre[i] = max(pre[i - 1], nums[i])

    suf[n - 1] = nums[n - 1]
    for i in range(n-2, -1, -1):
        suf[i] = min(suf[i + 1], nums[i])

    for i in range(1, n-1):
        if (nums[i] > pre[i - 1] and nums[i] < suf[i + 1]):
            ans += 2
        elif (nums[i] > nums[i - 1] and nums[i] < nums[i + 1]):
            ans += 1

    return ans

# Driver Code
if __name__ == "__main__":
    N = 3
    arr = [1, 2, 3]

    # Function Call
    print(maxScore(arr))

# This code is contributed by rakeshsahni
```

## C#

```
// C# program for above approach
using System;
using System.Collections.Generic;
class GFG
{

    // Function to find maximum score
    static int maxScore(List<int> nums)
    {

        // Size of array
        int n = nums.Count, i = 0;

        int ans = 0;

        // Prefix max
        int[] pre = new int[n];

        // Suffix min
        int[] suf = new int[n];

        pre[0] = nums[0];

        for (i = 1; i < n; i++)
            pre[i] = Math.Max(pre[i - 1], nums[i]);

        suf[n - 1] = nums[n - 1];
        for (i = n - 2; i >= 0; i--)
            suf[i] = Math.Min(suf[i + 1], nums[i]);

        for (i = 1; i < n - 1; i++) {
            if (nums[i] > pre[i - 1]
                && nums[i] < suf[i + 1])
                ans += 2;
            else if (nums[i] > nums[i - 1]
                     && nums[i] < nums[i + 1])
                ans += 1;
        }

        return ans;
    }

    // Driver Code
    public static void Main()
    {

        List<int> arr = new List<int>() { 1, 2, 3 };

        // Function Call
        Console.WriteLine(maxScore(arr));
    }
}

// This code is contributed by ukasp.
```

## java 描述语言

```
<script>
      // JavaScript code for the above approach

      // Function to find maximum score
      function maxScore(nums) {

          // Size of array
          let n = nums.length, i;
          let ans = 0;

          // Prefix max
          let pre = new Array(n).fill(0)

          // Suffix min
          let suf = new Array(n).fill(0);

          pre[0] = nums[0];

          for (i = 1; i < n; i++)
              pre[i] = Math.max(pre[i - 1], nums[i]);

          suf[n - 1] = nums[n - 1];
          for (i = n - 2; i >= 0; i--)
              suf[i] = Math.min(suf[i + 1], nums[i]);

          for (i = 1; i < n - 1; i++) {
              if (nums[i] > pre[i - 1]
                  && nums[i] < suf[i + 1])
                  ans += 2;
              else if (nums[i] > nums[i - 1]
                  && nums[i] < nums[i + 1])
                  ans += 1;
          }

          return ans;
      }

      // Driver Code

      let N = 3;

      let arr = [1, 2, 3];

      // Function Call
      document.write(maxScore(arr));

// This code is contributed by Potta Lokesh
  </script>
```

**Output**

```
2
```

**时间复杂度:**O(N)
T3】辅助空间: O(N)
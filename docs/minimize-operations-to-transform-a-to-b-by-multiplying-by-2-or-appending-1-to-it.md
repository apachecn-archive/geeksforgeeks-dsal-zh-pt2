# 通过乘以 2 或附加 1 来最小化将 A 转换为 B 的操作

> 原文:[https://www . geeksforgeeks . org/最小化-运算-转换-a-b-乘-2-或-追加-1-it/](https://www.geeksforgeeks.org/minimize-operations-to-transform-a-to-b-by-multiplying-by-2-or-appending-1-to-it/)

给定两个数字 **A** 和 **B** ，任务是找到将 **A** 转换为 **B** 的以下操作的最小数量:

1.  将当前数字乘以 2(即将数字 **X** 替换为 **2X**
2.  将数字 1 追加到当前数字的右边(即把数字 **X** 替换为 **10X + 1** )。

如果无法将 **A** 转换为 **B** ，则打印-1。

**示例:**

> **输入:** A = 2，B = 162
> **输出:** 4
> **说明:**
> 操作 1:将 A 改为 2*A，所以 A=2*2=4
> 操作 2:将 A 改为 2*A，所以 A=2*4=8。
> 操作 3:将 A 改为 10*A+1，所以 A=10*8+1=81
> 操作 4:将 A 改为 2*A，所以 A=2*81=162
> 
> **输入:** A = 4，B = 42
> **输出:** -1

**方法:**这个问题可以通过递归生成所有可能的解，然后从中选择最小值来解决。现在，要解决这个问题，请遵循以下步骤:

1.  创建一个递归函数**微操作**，它将接受三个参数，即当前编号**(当前)**、目标编号 **(B)** 和一个映射 **(dp)** 来记录返回的结果。此函数将返回将当前数字转换为目标数字所需的最小操作数。
2.  最初通过 **A** 作为**曲线**、 **B** 和**次操作**中的空地图 **dp** 。
3.  现在在每个递归调用中:
    1.  检查 **cur** 是否大于 **B** ，如果大于则返回 INT_MAX，因为无法将当前号码转换为 **B** 。
    2.  检查 **cur** 是否等于 **B** ，如果是则返回 0。
    3.  还要检查这个函数调用的结果是否已经存储在 map **dp** 中。如果是，那就从那里还回来。
    4.  否则，对 **(cur* 2)** 和 **(cur*10+1)** 再次调用该函数，并在记忆后返回这两者的最小结果。
4.  现在，如果初始调用返回 INT_MAX，则打印-1，因为无法将 **A** 转换为 **B** 。否则，答案就是这个函数调用返回的整数。

下面是上述方法的实现:

## C++

```
// C++ code for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find
// the minimum number of operations
// needed to transform A to B
int minOperations(int cur, int B,
                  unordered_map<int, int>& dp)
{

    // If current number
    // is greater than target
    if (cur > B) {
        return INT_MAX;
    }

    // if current number
    // is equal to the target
    if (cur == B) {
        return 0;
    }

    // If the number of minimum
    // operations required to
    // change the current number
    // to the target number
    // is already memoised
    if (dp.count(cur)) {
        return dp[cur];
    }

    // Minimum number of operations
    // required if the current element
    // gets multiplied by 2
    int ans1 = minOperations(cur * 2, B, dp);

    // Minimum number of operations
    // required if the 1 is appended to
    // the right of the current element
    int ans2 = minOperations(cur * 10 + 1, B, dp);

    // If it is not possible
    // to reach the target value
    // from the current element
    if (min(ans1, ans2) == INT_MAX) {
        return dp[cur] = INT_MAX;
    }

    // Returning the minimum
    // number of operations
    return dp[cur] = min(ans1, ans2) + 1;
}

// Driver Code
int main()
{
    int A = 2, B = 162;
    unordered_map<int, int> dp;
    int ans = minOperations(A, B, dp);

    // If A cannot be transformed to B
    if (ans == INT_MAX) {
        cout << -1;
    }

    else {
        cout << ans;
    }
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code for the above approach
import java.util.HashMap;
class GFG {

  // Function to find
  // the minimum number of operations
  // needed to transform A to B
  static int minOperations(int cur, int B, HashMap<Integer, Integer> dp) {

    // If current number
    // is greater than target
    if (cur > B) {
      return Integer.MAX_VALUE;
    }

    // if current number
    // is equal to the target
    if (cur == B) {
      return 0;
    }

    // If the number of minimum
    // operations required to
    // change the current number
    // to the target number
    // is already memoised
    if (dp.containsKey(cur)) {
      return dp.get(cur);
    }

    // Minimum number of operations
    // required if the current element
    // gets multiplied by 2
    int ans1 = minOperations(cur * 2, B, dp);

    // Minimum number of operations
    // required if the 1 is appended to
    // the right of the current element
    int ans2 = minOperations(cur * 10 + 1, B, dp);

    // If it is not possible
    // to reach the target value
    // from the current element
    if (Math.min(ans1, ans2) == Integer.MAX_VALUE) {
      dp.put(cur, Integer.MAX_VALUE);
      return dp.get(cur);
    }

    // Returning the minimum
    // number of operations
    dp.put(cur, Math.min(ans1, ans2) + 1);
    return dp.get(cur);
  }

  // Driver Code
  public static void main(String args[])
  {
    int A = 2, B = 162;
    HashMap<Integer, Integer> dp = new HashMap<Integer, Integer>();
    int ans = minOperations(A, B, dp);

    // If A cannot be transformed to B
    if (ans == Integer.MAX_VALUE) {
      System.out.println(-1);
    }

    else {
      System.out.println(ans);
    }
  }
}

// This code is contributed by gfgking.
```

## 蟒蛇 3

```
# Python 3 code for the above approach
import sys
# Function to find
# the minimum number of operations
# needed to transform A to B

def minOperations(cur, B,
                  dp):

    # If current number
    # is greater than target
    if (cur > B):
        return sys.maxsize

    # if current number
    # is equal to the target
    if (cur == B):
        return 0

    # If the number of minimum
    # operations required to
    # change the current number
    # to the target number
    # is already memoised
    if (cur in dp):
        return dp[cur]

    # Minimum number of operations
    # required if the current element
    # gets multiplied by 2
    ans1 = minOperations(cur * 2, B, dp)

    # Minimum number of operations
    # required if the 1 is appended to
    # the right of the current element
    ans2 = minOperations(cur * 10 + 1, B, dp)

    # If it is not possible
    # to reach the target value
    # from the current element
    if (min(ans1, ans2) == sys.maxsize):
        dp[cur] = sys.maxsize
        return dp[cur]

    # Returning the minimum
    # number of operations
    dp[cur] = min(ans1, ans2) + 1
    return dp[cur]

# Driver Code
if __name__ == "__main__":

    A = 2
    B = 162
    dp = {}
    ans = minOperations(A, B, dp)

    # If A cannot be transformed to B
    if (ans == sys.maxsize):
        print(-1)
    else:
        print(ans)

        # This code is contributed by ukasp.
```

## C#

```
// C# code for the above approach
using System;
using System.Collections.Generic;
class GFG {

    // Function to find
    // the minimum number of operations
    // needed to transform A to B
    static int minOperations(int cur, int B,
                             Dictionary<int, int> dp)
    {

        // If current number
        // is greater than target
        if (cur > B) {
            return Int32.MaxValue;
        }

        // if current number
        // is equal to the target
        if (cur == B) {
            return 0;
        }

        // If the number of minimum
        // operations required to
        // change the current number
        // to the target number
        // is already memoised
        if (dp.ContainsKey(cur)) {
            return dp[cur];
        }

        // Minimum number of operations
        // required if the current element
        // gets multiplied by 2
        int ans1 = minOperations(cur * 2, B, dp);

        // Minimum number of operations
        // required if the 1 is appended to
        // the right of the current element
        int ans2 = minOperations(cur * 10 + 1, B, dp);

        // If it is not possible
        // to reach the target value
        // from the current element
        if (Math.Min(ans1, ans2) == Int32.MaxValue) {
            dp[cur] = Int32.MaxValue;
            return dp[cur];
        }

        // Returning the minimum
        // number of operations
        dp[cur] = Math.Min(ans1, ans2) + 1;
        return dp[cur];
    }

    // Driver Code
    public static void Main(string[] args)
    {
        int A = 2, B = 162;
        Dictionary<int, int> dp
            = new Dictionary<int, int>();
        int ans = minOperations(A, B, dp);

        // If A cannot be transformed to B
        if (ans == Int32.MaxValue) {
            Console.WriteLine(-1);
        }

        else {
            Console.WriteLine(ans);
        }
    }
}

// This code is contributed by gaurav01.
```

## java 描述语言

```
<script>
      // JavaScript code for the above approach

      // Function to find
      // the minimum number of operations
      // needed to transform A to B
      function minOperations(cur, B,
          dp) {

          // If current number
          // is greater than target
          if (cur > B) {
              return Number.MAX_VALUE;
          }

          // if current number
          // is equal to the target
          if (cur == B) {
              return 0;
          }

          // If the number of minimum
          // operations required to
          // change the current number
          // to the target number
          // is already memoised
          if (dp[cur] != 0) {
              return dp[cur];
          }

          // Minimum number of operations
          // required if the current element
          // gets multiplied by 2
          let ans1 = minOperations(cur * 2, B, dp);

          // Minimum number of operations
          // required if the 1 is appended to
          // the right of the current element
          let ans2 = minOperations(cur * 10 + 1, B, dp);

          // If it is not possible
          // to reach the target value
          // from the current element
          if (Math.min(ans1, ans2) == Number.MAX_VALUE) {
              return dp[cur] = Number.MAX_VALUE;
          }

          // Returning the minimum
          // number of operations
          return dp[cur] = Math.min(ans1, ans2) + 1;
      }

      // Driver Code
      let A = 2, B = 162;
      let dp = new Array(100000).fill(0);
      let ans = minOperations(A, B, dp);

      // If A cannot be transformed to B
      if (ans == Number.MAX_VALUE) {
          document.write(-1);
      }

      else {
          document.write(ans);
      }

// This code is contributed by Potta Lokesh
  </script>
```

**Output**

```
4
```

***时间复杂度:***O(log<sub>2</sub>B * log<sub>10</sub>B)
***辅助空间:*** O(max(log <sub>2</sub> B，log <sub>10</sub> B))
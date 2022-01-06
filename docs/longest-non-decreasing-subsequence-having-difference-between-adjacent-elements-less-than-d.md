# 相邻元素之差小于 D 的最长非递减子序列

> 原文:[https://www . geesforgeks . org/最长-非递减-子序列-相邻元素间有差异-小于-d/](https://www.geeksforgeeks.org/longest-non-decreasing-subsequence-having-difference-between-adjacent-elements-less-than-d/)

给定一个由 **N** 个整数和一个整数 **D** 组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，任务是[找到最长的非递减子序列](https://www.geeksforgeeks.org/longest-increasing-subsequence-dp-3/)的长度，使得每个相邻元素之间的差小于 **D** 。

**示例:**

> **输入:** arr[] = {1，3，2，4，5}，D = 2
> **输出:** 3
> **解释:**
> 考虑子序列为{3，4，5}，其最大长度= 3 满足给定标准。
> 
> **输入:** arr[] = {1，5，3，2，7}，D = 2
> T3】输出: 2

**方法:**给定的问题是[最长递增子序列](https://www.geeksforgeeks.org/longest-increasing-subsequence/)的变型，相邻数组元素之间的差的标准小于 **D** ，这个思想可以使用[动态编程](https://www.geeksforgeeks.org/dynamic-programming/)来实现。按照以下步骤解决给定的问题:

*   初始化一个 **dp** 数组，其中**DP【I】**将存储包含第 **i <sup>个</sup>** 元素后的非递减子序列的最大长度，使得每对相邻元素之间的差值小于 **D** 。
*   将数组 **dp[]** 的所有值初始化为 **1** 。
*   [在范围【T10，N】](https://www.geeksforgeeks.org/loops-in-c-and-cpp/)上迭代一个循环，在每次迭代中， **i** [使用变量 **j** 在范围**【0，I–1】**上遍历给定数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **arr【】和**如果**arr【j】**的值至少为**arr【I】**且它们之间的差值小于
*   **完成上述步骤后，打印数组 **dp[]** 的[最大值作为结果。](https://www.geeksforgeeks.org/c-program-find-largest-element-array/)**

**下面是上述方法的实现:**

## **C++**

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to return the length of the
// longest non-decreasing subsequence
// having the difference as D for every
// adjacent elements
int longestSubsequence(vector<int> arr,
                       int d)
{
    // Store the size of array
    int n = arr.size();

    // Stores the maximum length of the
    // subsequence after including the
    // ith element
    vector<int> dp(n, 1);

    for (int i = 0; i < n; i++) {
        for (int j = 0; j < i; j++) {

            // If it satisfies the
            // given condition
            if (arr[i] - d < arr[j]
                and arr[i] >= arr[j]) {

                // Update dp[i]
                dp[i] = max(dp[i], dp[j] + 1);
            }
        }
    }

    // Maximum value in the dp
    // table is the answer
    return *max_element(
        dp.begin(), dp.end());
}

// Driver Code
int main()
{
    vector<int> arr = { 1, 3, 2, 4, 5 };
    int D = 2;
    cout << longestSubsequence(arr, D);

    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java program for the above approach
import java.util.*;
public class GFG {

    // Function to return the length of the
    // longest non-decreasing subsequence
    // having the difference as D for every
    // adjacent elements
    static int longestSubsequence(int  []arr,
                           int d)
    {

        // Store the size of array
        int n = arr.length;

        // Stores the maximum length of the
        // subsequence after including the
        // ith element
        int []dp = new int[n];

        for(int i = 0; i < n ; i++)
            dp[i] = 1;

        for (int i = 0; i < n; i++) {
            for (int j = 0; j < i; j++) {

                // If it satisfies the
                // given condition
                if (arr[i] - d < arr[j] && arr[i] >= arr[j]) {

                    // Update dp[i]
                    dp[i] = Math.max(dp[i], dp[j] + 1);
                }
            }
        }

        // Maximum value in the dp
        // table is the answer
        Arrays.sort(dp);
        return dp[n - 1];
    }

    // Driver Code
    public static void main (String[] args) {
        int arr[] = { 1, 3, 2, 4, 5 };
        int D = 2;
        System.out.println(longestSubsequence(arr, D));
    }
}

// This code is contributed by AnkThon
```

## **蟒蛇 3**

```
# python program for the above approach

# Function to return the length of the
# longest non-decreasing subsequence
# having the difference as D for every
# adjacent elements
def longestSubsequence(arr, d):

    # Store the size of array
    n = len(arr)

    # Stores the maximum length of the
    # subsequence after including the
    # ith element
    dp = [1 for _ in range(n)]

    for i in range(0, n):
        for j in range(0, i):

            # If it satisfies the
            # given condition
            if (arr[i] - d < arr[j] and arr[i] >= arr[j]):

                # Update dp[i]
                dp[i] = max(dp[i], dp[j] + 1)

    # Maximum value in the dp
    # table is the answer
    return max(dp)

# Driver Code
if __name__ == "__main__":

    arr = [1, 3, 2, 4, 5]
    D = 2
    print(longestSubsequence(arr, D))

    # This code is contributed by rakeshsahni
```

## **C#**

```
// C# program for the above approach
using System;

public class GFG {

    // Function to return the length of the
    // longest non-decreasing subsequence
    // having the difference as D for every
    // adjacent elements
    static int longestSubsequence(int  []arr,
                           int d)
    {

        // Store the size of array
        int n = arr.Length;

        // Stores the maximum length of the
        // subsequence after including the
        // ith element
        int []dp = new int[n];

        for(int i = 0; i < n ; i++)
            dp[i] = 1;

        for (int i = 0; i < n; i++) {
            for (int j = 0; j < i; j++) {

                // If it satisfies the
                // given condition
                if (arr[i] - d < arr[j] && arr[i] >= arr[j]) {

                    // Update dp[i]
                    dp[i] = Math.Max(dp[i], dp[j] + 1);
                }
            }
        }

        // Maximum value in the dp
        // table is the answer
        Array.Sort(dp);
        return dp[n - 1];
    }

    // Driver Code
    public static void Main (string[] args) {
        int []arr = { 1, 3, 2, 4, 5 };
        int D = 2;
        Console.WriteLine(longestSubsequence(arr, D));
    }
}

// This code is contributed by AnkThon
```

## **java 描述语言**

```
<script>
// Javascript program for the above approach

// Function to return the length of the
// longest non-decreasing subsequence
// having the difference as D for every
// adjacent elements
function longestSubsequence(arr, d)
{

  // Store the size of array
  let n = arr.length;

  // Stores the maximum length of the
  // subsequence after including the
  // ith element
  let dp = new Array(n).fill(1);

  for (let i = 0; i < n; i++)
  {
    for (let j = 0; j < i; j++)
    {

      // If it satisfies the
      // given condition
      if (arr[i] - d < arr[j] && arr[i] >= arr[j])
      {

        // Update dp[i]
        dp[i] = Math.max(dp[i], dp[j] + 1);
      }
    }
  }

  // Maximum value in the dp
  // table is the answer
  return dp.sort((a, b) => b - a)[0];
}

// Driver Code
let arr = [1, 3, 2, 4, 5];
let D = 2;
document.write(longestSubsequence(arr, D));

// This code is contributed by gfgking.
</script>
```

****Output:** 

```
3
```** 

*****时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(N)***
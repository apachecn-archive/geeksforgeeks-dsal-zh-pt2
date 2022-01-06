# 最大化通过值 I 跳转索引选择的元素 arr[i]的总和

> 原文:[https://www . geeksforgeeks . org/最大化元素总和-arri-按跳跃选择-按值索引-i/](https://www.geeksforgeeks.org/maximize-the-sum-of-elements-arri-selected-by-jumping-index-by-value-i/)

给定一个[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**，任务是计算数组中元素的最大和，这样，如果选择了一个带有元素的**，那么**arr【I】**将被添加到和中，并且 **i 跳转**将从当前索引中向前获取。**

**示例**:

> **输入:** N = 5，arr[] = {7，3，1，2，3}
> **输出:** 7
> **解释:**
> 
> 1.  将第一个元素 7 作为我们的分数，然后我们向前移动 7 个索引，并退出数组，因此最终答案是 7。
> 2.  从第 2 个元素 3 开始并将其添加到分数中，然后向前移动 3 个索引并落在数组的最后一个索引上并将其添加到我们的分数中，因此最终分数将为 3+3=6。
> 3.  从第三个元素 1 开始，加到我们的分数上，然后向前移动 1 个指数，加 2 到我们的分数上，这样最终的分数是=1+2=3。
> 4.  从第 4 个元素 2 开始，并将其添加到分数中，当我们伸出数组时，向前移动 2 个索引，最终分数是 2。
> 5.  从第 5 个元素 3 开始，将其添加到我们的分数中，我们的最终分数将是 3。
> 
> 所以从所有的案例来看，最高分是 7 分。
> 
> **输入:** N = 2，arr[] = {3，1 }
> T3】输出: 3

**逼近**:使用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)可以解决任务。取一个 **dp** 容器，该容器将存储从该特定索引到数组末尾的最大得分，并在找出所有索引的最大得分后，打印其中的最大得分。
按照以下步骤解决问题:

*   创建一个与数组大小相同的 **Dp** 容器和 **ans** 变量。
*   现在将**DP【n-1】**指定为**arr【n-1】**，因为该指数的最大和是**a【n-1】**。
*   将循环从 n-2 向后迭代到 0。
*   对于每个索引，将 arr[i]添加到 dp 并检查
    *   如果 i+arr[i]小于数组的大小
        *   如果是，在 **dp[i]中添加 **dp[i+arr[i]]** 。**
*   迭代 dp 数组，找到 dp 的**最大值**，并将其存储在我们的 ans 变量中。
*   最后，打印 ans。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to to find the maximum
// score from the given array.
void findMaximumScore(int arr[], int n)
{
    // Initialize dp.
    int dp[n + 1] = { 0 };
    dp[n - 1] = arr[n - 1];

    // Store the max sum
    int ans = 0;

    // Iterating backwards from n-2 to 0.
    for (int i = n - 2; i >= 0; i--) {
        dp[i] = arr[i];
        int j = i + arr[i];
        if (j < n) {
            dp[i] += dp[j];
        }
    }

    // Finding the maximum
    // score present in the dp.
    for (int i = 0; i < n; i++) {
        ans = max(dp[i], ans);
    }
    cout << ans << endl;
}

// Driver Code
int main()
{
    int n = 5;
    int arr[] = { 7, 3, 1, 2, 3 };
    findMaximumScore(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
public class GFG {

    // Function to to find the maximum
    // score from the given array.
    static void findMaximumScore(int arr[], int n)
    {

        // Initialize dp.
        int dp[] = new int[n + 1];
        dp[n - 1] = arr[n - 1];

        // Store the max sum
        int ans = 0;

        // Iterating backwards from n-2 to 0.
        for (int i = n - 2; i >= 0; i--) {
            dp[i] = arr[i];
            int j = i + arr[i];
            if (j < n) {
                dp[i] += dp[j];
            }
        }

        // Finding the maximum
        // score present in the dp.
        for (int i = 0; i < n; i++) {
            ans = Math.max(dp[i], ans);
        }
        System.out.println(ans);
    }

    // Driver Code
    public static void main (String[] args)
    {
        int n = 5;
        int arr[] = { 7, 3, 1, 2, 3 };
        findMaximumScore(arr, n);
    }

}

// This code is contributed by AnkThon
```

## 蟒蛇 3

```
# Python Program to implement
# the above approach

# Function to to find the maximum
# score from the given array.
def findMaximumScore(arr, n):

    # Initialize dp.
    dp = [0] * (n + 1)
    dp[n - 1] = arr[n - 1]

    # Store the max sum
    ans = 0

    # Iterating backwards from n-2 to 0.
    for i in range(n-2, -1, -1):
        dp[i] = arr[i]
        j = i + arr[i]
        if (j < n):
            dp[i] += dp[j]

    # Finding the maximum
    # score present in the dp.
    for i in range(n):
        ans = max(dp[i], ans)

    print(ans)

# Driver Code
n = 5
arr = [7, 3, 1, 2, 3]
findMaximumScore(arr, n)

# This code is contributed by Saurabh Jaiswal
```

## C#

```
// C# program for the above approach

using System;

public class GFG {

    // Function to to find the maximum
    // score from the given array.
    static void findMaximumScore(int []arr, int n)
    {

        // Initialize dp.
        int []dp = new int[n + 1];
        dp[n - 1] = arr[n - 1];

        // Store the max sum
        int ans = 0;

        // Iterating backwards from n-2 to 0.
        for (int i = n - 2; i >= 0; i--) {
            dp[i] = arr[i];
            int j = i + arr[i];
            if (j < n) {
                dp[i] += dp[j];
            }
        }

        // Finding the maximum
        // score present in the dp.
        for (int i = 0; i < n; i++) {
            ans = Math.Max(dp[i], ans);
        }
        Console.WriteLine(ans);
    }

    // Driver Code
    public static void Main (string[] args)
    {
        int n = 5;
        int []arr = { 7, 3, 1, 2, 3 };
        findMaximumScore(arr, n);
    }

}

// This code is contributed by AnkThon
```

## java 描述语言

```
<script>
       // JavaScript Program to implement
       // the above approach

       // Function to to find the maximum
       // score from the given array.
       function findMaximumScore(arr, n)
       {

           // Initialize dp.
           let dp = new Array(n + 1).fill(0)
           dp[n - 1] = arr[n - 1];

           // Store the max sum
           let ans = 0;

           // Iterating backwards from n-2 to 0.
           for (let i = n - 2; i >= 0; i--) {
               dp[i] = arr[i];
               let j = i + arr[i];
               if (j < n) {
                   dp[i] += dp[j];
               }
           }

           // Finding the maximum
           // score present in the dp.
           for (let i = 0; i < n; i++) {
               ans = Math.max(dp[i], ans);
           }
           document.write(ans + '<br>');
       }

       // Driver Code
       let n = 5;
       let arr = [7, 3, 1, 2, 3];
       findMaximumScore(arr, n);

   // This code is contributed by Potta Lokesh
   </script>
```

**Output**

```
7
```

***时间复杂度** :* O(N)
***辅助空间*** : O(N)
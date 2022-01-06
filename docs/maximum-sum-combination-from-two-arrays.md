# 两个数组的最大和组合

> 原文:[https://www . geeksforgeeks . org/两个数组的最大和组合/](https://www.geeksforgeeks.org/maximum-sum-combination-from-two-arrays/)

给定两个阵列 **arr1[]** 和 **arr2[]** ，每个阵列大小为 **N** 。任务是从两个数组中选择一些元素，使得没有两个元素具有相同的索引，并且不能从单个数组中选择两个连续的数字。找出上面选择的数字的最大可能和。

**示例:**

> **输入:** arr1[] = {9，3，5，7，3}，arr2[] = {5，8，1，4，5}
> **输出:** 29
> 从第一个数组中选择第一、第三和第五个元素。
> 从第二个数组中选择第二个和第四个元素。
> 
> **输入:** arr1[] = {1，2，9}，arr2[] = {10，1，1}
> **输出:** 19
> 从第一个数组中选择最后一个元素，从第二个数组中选择第一个元素。

**进场:**
这个问题是基于[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)的。

*   如果最后一个元素取自位置 **(i-1，1)** ，则让 **dp(i，1)** 为新选择元素的最大和。
*   **dp(i，2)** 相同，但最后一个元素的位置为 **(i-1，2)**
*   **dp(i，3)** 相同，但我们没有从位置 **i-1** 获取任何元素

递归关系是:

> dp（i， 1）=max（dp （i – 1， 2） + scar（i， 1）， dp（i – 1， 3） + scar（i， 1）， scar（i， 1） ）;
> dp（i， 2）=max（dp（i – 1， 1） + scar（i， 2 ）， dp（i – 1， 3） + scar （i， 2）， scar（i， 2））;
> dp（i， 3）=max（dp（i- 1， 1）， dp（ i-1， 2） ）。

我们实际上不需要 **dp( i，3)** ，如果我们更新 **dp(i，1)** 为 **max(dp(i，1)，dp(i-1，1))** 和 **dp(i，2)** 为 **max(dp(i，2)，dp(i-1，2))** 。
因此， **dp(i，j)** 是如果最后一个元素取自位置 **(i-1，1** )或更少时所选元素的最大总和。与 **dp(i，2)** 相同。因此上述问题的答案是 **max(dp(n，1)，dp(n，2))** 。

下面是上述方法的实现:

## C++

```
// CPP program to maximum sum
// combination from two arrays
#include <bits/stdc++.h>
using namespace std;

// Function to maximum sum
// combination from two arrays
int Max_Sum(int arr1[], int arr2[], int n)
{
    // To store dp value
    int dp[n][2];

    // For loop to calculate the value of dp
    for (int i = 0; i < n; i++)
    {
        if(i==0)
        {
            dp[i][0] = arr1[i];
            dp[i][1] = arr2[i];
            continue;
        }

       dp[i][0] = max(dp[i - 1][0], dp[i - 1][1] + arr1[i]);
       dp[i][1] = max(dp[i - 1][1], dp[i - 1][0] + arr2[i]);
    }

    // Return the required answer
    return max(dp[n-1][0], dp[n-1][1]);
}

// Driver code
int main()
{
    int arr1[] = {9, 3, 5, 7, 3};
    int arr2[] = {5, 8, 1, 4, 5};

    int n = sizeof(arr1) / sizeof(arr1[0]);

    // Function call
    cout << Max_Sum(arr1, arr2, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to maximum sum
// combination from two arrays
class GFG
{

// Function to maximum sum
// combination from two arrays
static int Max_Sum(int arr1[],
                   int arr2[], int n)
{
    // To store dp value
    int [][]dp = new int[n][2];

    // For loop to calculate the value of dp
    for (int i = 0; i < n; i++)
    {
        if(i == 0)
        {
            dp[i][0] = arr1[i];
            dp[i][1] = arr2[i];
            continue;
        }

        dp[i][0] = Math.max(dp[i - 1][0],
                            dp[i - 1][1] + arr1[i]);
        dp[i][1] = Math.max(dp[i - 1][1],  
                            dp[i - 1][0] + arr2[i]);
    }

    // Return the required answer
    return Math.max(dp[n - 1][0],
                    dp[n - 1][1]);
}

// Driver code
public static void main(String[] args)
{
    int arr1[] = {9, 3, 5, 7, 3};
    int arr2[] = {5, 8, 1, 4, 5};

    int n = arr1.length;

    // Function call
    System.out.println(Max_Sum(arr1, arr2, n));
}
}

// This code is contributed
// by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 program to maximum sum
# combination from two arrays

# Function to maximum sum
# combination from two arrays
def Max_Sum(arr1, arr2, n):

    # To store dp value
    dp = [[0 for i in range(2)]
             for j in range(n)]

    # For loop to calculate the value of dp
    for i in range(n):
        if(i == 0):
            dp[i][0] = arr1[i]
            dp[i][1] = arr2[i]
            continue
        else:
            dp[i][0] = max(dp[i - 1][0],
                           dp[i - 1][1] + arr1[i])
            dp[i][1] = max(dp[i - 1][1],
                           dp[i - 1][0] + arr2[i])

    # Return the required answer
    return max(dp[n - 1][0],
               dp[n - 1][1])

# Driver code
if __name__ == '__main__':
    arr1 = [9, 3, 5, 7, 3]
    arr2 = [5, 8, 1, 4, 5]

    n = len(arr1)

    # Function call
    print(Max_Sum(arr1, arr2, n))

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# program to maximum sum
// combination from two arrays
using System;

class GFG
{

// Function to maximum sum
// combination from two arrays
static int Max_Sum(int []arr1,
                   int []arr2, int n)
{
    // To store dp value
    int [,]dp = new int[n, 2];

    // For loop to calculate the value of dp
    for (int i = 0; i < n; i++)
    {
        if(i == 0)
        {
            dp[i, 0] = arr1[i];
            dp[i, 1] = arr2[i];
            continue;
        }

        dp[i, 0] = Math.Max(dp[i - 1, 0],
                            dp[i - 1, 1] + arr1[i]);
        dp[i, 1] = Math.Max(dp[i - 1, 1],
                            dp[i - 1, 0] + arr2[i]);
    }

    // Return the required answer
    return Math.Max(dp[n - 1, 0],
                    dp[n - 1, 1]);
}

// Driver code
public static void Main()
{
    int []arr1 = {9, 3, 5, 7, 3};
    int []arr2 = {5, 8, 1, 4, 5};

    int n = arr1.Length;

    // Function call
    Console.WriteLine(Max_Sum(arr1, arr2, n));
}
}

// This code is contributed
// by anuj_67..
```

## java 描述语言

```
<script>
    // Javascript program to maximum sum combination from two arrays

    // Function to maximum sum
    // combination from two arrays
    function Max_Sum(arr1, arr2, n)
    {
        // To store dp value
        let dp = new Array(n);
        for (let i = 0; i < n; i++)
        {
            dp[i] = new Array(2);
            for (let j = 0; j < 2; j++)
            {
                dp[i][j] = 0;   
            }
        }

        // For loop to calculate the value of dp
        for (let i = 0; i < n; i++)
        {
            if(i == 0)
            {
                dp[i][0] = arr1[i];
                dp[i][1] = arr2[i];
                continue;
            }

            dp[i][0] = Math.max(dp[i - 1][0],
                                dp[i - 1][1] + arr1[i]);
            dp[i][1] = Math.max(dp[i - 1][1],  
                                dp[i - 1][0] + arr2[i]);
        }

        // Return the required answer
        return Math.max(dp[n - 1][0],
                        dp[n - 1][1]);
    }

    let arr1 = [9, 3, 5, 7, 3];
    let arr2 = [5, 8, 1, 4, 5];

    let n = arr1.length;

    // Function call
    document.write(Max_Sum(arr1, arr2, n));

</script>
```

**Output:** 

```
29
```

**时间复杂度:** O(N)
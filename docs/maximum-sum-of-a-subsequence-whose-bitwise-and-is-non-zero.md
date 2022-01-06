# 位与非零的子序列的最大和

> 原文:[https://www . geeksforgeeks . org/子序列的最大和，其位与为非零/](https://www.geeksforgeeks.org/maximum-sum-of-a-subsequence-whose-bitwise-and-is-non-zero/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，任务是从元素的[位与](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)不等于零的数组中找到任意子序列的[最大和。](https://www.geeksforgeeks.org/maximum-sum-subsequence-of-length-k/)

**示例:**

> **输入:** arr[] = {5，4，1，7，11}
> **输出:** 24
> **说明:**
> 和最大的子序列是整个数组。数组的按位“与”为 0。因此，不能考虑子序列。
> 下一个较大和的子序列是{5，1，7，11}。因为这个子序列的按位“与”是非零的，所以这个子序列的和(= 24)就是所需的答案。
> 
> **输入:** arr[] = {5，6，2 }
> T3】输出: 11

**天真方法:**解决给定问题的最简单方法是[生成给定数组的所有可能的子序列](https://www.geeksforgeeks.org/generating-all-possible-subsequences-using-recursion/)，并打印该子序列的最大和，该子序列的所有元素的[位“与”](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)都不为零。

***时间复杂度:**O(2<sup>N</sup>)*
***辅助空间:** O(1)*

**有效方法:**上述方法也可以通过观察以下事实进行优化，即只有那些在所有选择的数组元素中其位被设置的元素的和给出其位“与”为非零的子序列。因此，想法是最大化所有这些元素的总和。按照以下步骤解决问题:

*   初始化一个变量，比如说**和**，它存储子序列的最大和，子序列的值**按位“与”**为正。
*   [使用变量 **i** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，32】**，并执行以下步骤:
    *   初始化一个变量，比如说 **sum** ，它存储所有元素的总和，这些元素的 **i <sup>第</sup>位**被设置。
    *   [遍历给定数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)和[如果数组元素**的 **i <sup>第</sup>位**被设置为**](https://www.geeksforgeeks.org/check-whether-k-th-bit-set-not/)arr【I】，则将该值添加到变量 **sum** 中。
    *   将 **ans** 的值更新为 **ans** 和 **sum** 的最大值。
*   完成上述步骤后，打印**和**的值作为子序列的最大和。

以下是我们方法的实施情况:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the maximum sum of
// a subsequence whose Bitwise AND is non-zero
int maximumSum(int arr[], int N)
{
    // Stores the resultant maximum
    // sum of the subsequence
    int ans = 0;

    // Iterate over all the bits
    for (int bit = 0; bit < 32; bit++) {

        // Stores the sum of array
        // elements whose i-th bit is set
        int sum = 0;

        // Traverse the array elements
        for (int i = 0; i < N; i++) {

            // If the bit is set, then
            // add its value to the sum
            if (arr[i] & (1 << bit)) {
                sum += arr[i];
            }
        }

        // Update the resultant
        // maximum sum
        ans = max(ans, sum);
    }

    // Return the maximum sum
    return ans;
}

// Driver Code
int main()
{
    int arr[] = { 5, 4, 1, 7, 11 };
    int N = sizeof(arr) / sizeof(arr[0]);
    cout << maximumSum(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
public class GFG
{

 // Function to find the maximum sum of
 // a subsequence whose Bitwise AND is non-zero
 static int maximumSum(int arr[], int N)
 {

     // Stores the resultant maximum
     // sum of the subsequence
     int ans = 0;

     // Iterate over all the bits
     for (int bit = 0; bit < 32; bit++) {

         // Stores the sum of array
         // elements whose i-th bit is set
         int sum = 0;

         // Traverse the array elements
         for (int i = 0; i < N; i++) {

             // If the bit is set, then
             // add its value to the sum
             if ((arr[i] & (1 << bit)) == 1) {
                 sum += arr[i];
             }
         }

         // Update the resultant
         // maximum sum
         ans = Math.max(ans, sum);
     }

     // Return the maximum sum
     return ans;
 }

    // Driver code
    public static void main(String[] args)
    {   
        int arr[] = { 5, 4, 1, 7, 11 };
        int N = arr.length;
       System.out.println(maximumSum(arr, N));
    }
}

// This code is contributed by abhinavjain194
```

## 蟒蛇 3

```
# python3 program for the above approach

# Function to find the maximum sum of
# a subsequence whose Bitwise AND is non-zero
def maximumSum(arr, N):

    # Stores the resultant maximum
    # sum of the subsequence
    ans = 0

    # Iterate over all the bits
    for bit in range(32):

        # Stores the sum of array
        # elements whose i-th bit is set
        sum = 0

        # Traverse the array elements
        for i in range(N):

            # If the bit is set, then
            # add its value to the sum
            if (arr[i] & (1 << bit)):
                sum += arr[i]

        # Update the resultant
        # maximum sum
        ans = max(ans, sum)

    # Return the maximum sum
    return ans

# Driver Code
if __name__ == '__main__':
    arr = [5, 4, 1, 7, 11]
    N = len(arr)
    print(maximumSum(arr, N))

    # This code is contributed by bgangwar59.
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to find the maximum sum of
// a subsequence whose Bitwise AND is non-zero
static int maximumSum(int[] arr, int N)
{

    // Stores the resultant maximum
    // sum of the subsequence
    int ans = 0;

    // Iterate over all the bits
    for(int bit = 0; bit < 32; bit++)
    {

        // Stores the sum of array
        // elements whose i-th bit is set
        int sum = 0;

        // Traverse the array elements
        for(int i = 0; i < N; i++)
        {

            // If the bit is set, then
            // add its value to the sum
            if ((arr[i] & (1 << bit)) != 0)
            {
                sum += arr[i];
            }
        }

        // Update the resultant
        // maximum sum
        ans = Math.Max(ans, sum);
    }

    // Return the maximum sum
    return ans;
}

// Driver code
static public void Main()
{
    int[] arr = { 5, 4, 1, 7, 11 };
    int N = arr.Length;

    Console.Write(maximumSum(arr, N));
}
}

// This code is contributed by offbeat
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to find the maximum sum of
// a subsequence whose Bitwise AND is non-zero
function maximumSum(arr, N)
{
    // Stores the resultant maximum
    // sum of the subsequence
    let ans = 0;

    // Iterate over all the bits
    for (let bit = 0; bit < 32; bit++) {

        // Stores the sum of array
        // elements whose i-th bit is set
        let sum = 0;

        // Traverse the array elements
        for (let i = 0; i < N; i++) {

            // If the bit is set, then
            // add its value to the sum
            if (arr[i] & (1 << bit)) {
                sum += arr[i];
            }
        }

        // Update the resultant
        // maximum sum
        ans = Math.max(ans, sum);
    }

    // Return the maximum sum
    return ans;
}

// Driver Code
    let arr = [ 5, 4, 1, 7, 11 ];
    let N = arr.length;
    document.write(maximumSum(arr, N));

</script>
```

**Output:** 

```
24
```

***时间复杂度:** O(N*32)*
***辅助空间:** O(1)*
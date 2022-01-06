# 数组中位置 j 的计数，使得 arr[i]在索引范围[i，j]中最大，端点相同

> 原文:[https://www . geeksforgeeks . org/数组中的位置计数-j-arri-is-index-range-I-j-with-end-points-as-same/](https://www.geeksforgeeks.org/count-of-positions-j-in-array-such-that-arri-is-maximum-in-index-range-i-j-with-end-points-as-same/)

给定一个由 **N** 正整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**，任务是找出所有 **j** ，使得 **rr[j] = arr[i]** 以及**【min(j，I)，max(j，I)】**范围内的所有数字小于或等于 **arr[i]** ，其中 **1 ≤ i ≤ N** 。

**示例:**

> **输入:** arr[] = {4，7，7，9，7}，N = 5
> **输出:** 1 2 2 1 1
> **解释:**
> 对于 i = 1，j = 1 是唯一一个 arr[i] = arr[j]且中间没有任何元素的值大于 arr[1]的元素。
> 对于 i = 2，j = 2 和 3 是 arr[i] = arr[j]的元素，中间没有任何元素的值大于 arr[2]。
> 对于 i = 3，j = 2 和 3 是 arr[i] = arr[j]的元素，中间没有任何元素的值大于 arr[3]。
> 对于 i = 4，j = 4 是 arr[i] = arr[j]的唯一元素，中间没有任何元素的值大于 arr[4]。
> 对于 i = 5，j = 5 是唯一一个 arr[i] = arr[j]的元素，中间没有一个元素的值大于 arr[5]。
> 
> **输入:** arr[] = {1，2，1，2，4}，N = 5
> T3】输出: 1 2 1 2 1

**方法:**解决问题最简单的方法是使用两个[嵌套的 for 循环](https://www.geeksforgeeks.org/nested-loops-in-c-with-examples/)到[遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)并找到配对，使得 **arr[i] = arr[j]** 并且 **[i，j]** 范围内没有元素大于 **arr[i]** 。按照以下步骤解决问题:

*   初始化一个[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)，比如说**ans【】**存储范围内所有元素的答案**【0，N-1】**。
*   [使用变量 **i** 在范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【N-1，0】**中迭代，并执行以下步骤:
    *   [使用变量 **j** 在范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【I，0】**中迭代，并执行以下步骤:
        *   如果 **arr[j] = arr[i]** ，则将 **ans[i]** 的值增加 **1** 。
        *   如果 **arr[j] > arr[i]** ，则终止循环。
    *   [使用变量 **j** 在范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【I+1，N-1】**中迭代，并执行以下步骤:
        *   如果 **arr[j] = arr[i]** ，则将 **ans[i]** 的值增加 **1** 。
        *   如果 **arr[j] > arr[i]** ，则终止循环。
*   完成以上步骤后，[打印阵列](https://www.geeksforgeeks.org/how-to-print-an-array-in-java-without-using-loop/)**ans【】**作为答案。

下面是上述方法的实现

## C++

```
// C++ program for the above approach
#include <iostream>
using namespace std;

// Function to find j such that arr[j]=arr[i]
// and no element is greater than arr[i] in the
// range [j, i]
void findElements(int arr[], int N)
{

    // To Store answer
    int ans[N];

    // Initialize the value of ans[i] as 0
    for (int i = 0; i < N; i++) {
        ans[i] = 0;
    }

    // Traverse the array in reverse direction
    for (int i = N - 1; i >= 0; i--) {

        // Traverse in the range [i, 0]
        for (int j = i; j >= 0; j--) {
            if (arr[j] == arr[i]) {

                // Increment ans[i] if arr[j] =arr[i]
                ans[i]++;
            }
            else
                // Terminate the loop
                if (arr[j] > arr[i])
                break;
        }

        // Traverse in the range [i+1, N-1]
        for (int j = i + 1; j < N; j++) {
            // Increment ans[i] if arr[i] = arr[j]
            if (arr[j] == arr[i])
                ans[i]++;
            else if (arr[j] > arr[i]) {
                break;
            }
        }
    }

    for (int i = 0; i < N; i++) {
        cout << ans[i] << " ";
    }
}

// Driver Code
int main()
{
    // Given Input
    int arr[] = { 1, 2, 1, 2, 4 };
    int N = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    findElements(arr, N);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
public class GFG
{

    // Function to find j such that arr[j]=arr[i]
    // and no element is greater than arr[i] in the
    // range [j, i]
    static void findElements(int arr[], int N)
    {

        // To Store answer
        int ans[] = new int[N];

        // Initialize the value of ans[i] as 0
        for (int i = 0; i < N; i++) {
            ans[i] = 0;
        }

        // Traverse the array in reverse direction
        for (int i = N - 1; i >= 0; i--) {

            // Traverse in the range [i, 0]
            for (int j = i; j >= 0; j--) {
                if (arr[j] == arr[i]) {

                    // Increment ans[i] if arr[j] =arr[i]
                    ans[i]++;
                }
                else
                    // Terminate the loop
                    if (arr[j] > arr[i])
                    break;
            }

            // Traverse in the range [i+1, N-1]
            for (int j = i + 1; j < N; j++)
            {
                // Increment ans[i] if arr[i] = arr[j]
                if (arr[j] == arr[i])
                    ans[i]++;
                else if (arr[j] > arr[i]) {
                    break;
                }
            }
        }

        for (int i = 0; i < N; i++) {
            System.out.print(ans[i] + " ");
        }
    }

    // Driver code
    public static void main(String[] args)
    {
        // Given Input
        int arr[] = { 1, 2, 1, 2, 4 };
        int N = arr.length;

        // Function Call
        findElements(arr, N);
    }
}

// This code is contributed by abhinavjain194
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find j such that arr[j]=arr[i]
# and no element is greater than arr[i] in the
# range [j, i]
def findElements(arr, N):

    # Initialising a list to store ans
    # Initialize the value of ans[i] as 0
    ans = [0 for i in range(N)]

    # Traverse the array in reverse direction
    for i in range(N - 1, -1, -1):

        # Traverse in the range [i, 0]
        for j in range(i, -1, -1):
            if arr[j] == arr[i]:

                # Increment ans[i] if arr[j] = arr[i]
                ans[i] += 1

            else:

                # Terminate the loop
                if arr[j] > arr[i]:
                    break

        # Traverse in the range [i+1, N-1]
        for j in range(i+1, N):

            # Increment ans[i] if arr[j] = arr[i]
            if arr[j] == arr[i]:
                ans[i] += 1
            else:
                if arr[j] > arr[i]:
                    break

    # Print the ans
    for i in range(N):
        print(ans[i], end = " ")

    return

# Driver Code
if __name__ == '__main__':

    # Given Input
    arr = [ 1, 2, 1, 2, 4 ]
    N = len(arr)

    # Function call
    findElements(arr, N)

# This code is contributed by MuskanKalra1
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to find j such that arr[j]=arr[i]
// and no element is greater than arr[i] in the
// range [j, i]
static void findElements(int []arr, int N)
{

    // To Store answer
    int []ans = new int[N];

    // Initialize the value of ans[i] as 0
    for(int i = 0; i < N; i++)
    {
        ans[i] = 0;
    }

    // Traverse the array in reverse direction
    for(int i = N - 1; i >= 0; i--)
    {

        // Traverse in the range [i, 0]
        for(int j = i; j >= 0; j--)
        {
            if (arr[j] == arr[i])
            {

                // Increment ans[i] if arr[j] =arr[i]
                ans[i]++;
            }
            else

                // Terminate the loop
                if (arr[j] > arr[i])
                    break;
        }

        // Traverse in the range [i+1, N-1]
        for(int j = i + 1; j < N; j++)
        {

            // Increment ans[i] if arr[i] = arr[j]
            if (arr[j] == arr[i])
                ans[i]++;
            else if (arr[j] > arr[i])
            {
                break;
            }
        }
    }

    for(int i = 0; i < N; i++)
    {
        Console.Write(ans[i] + " ");
    }
}

// Driver Code
public static void Main()
{

    // Given Input
    int []arr = { 1, 2, 1, 2, 4 };
    int N = arr.Length;

    // Function Call
    findElements(arr, N);
}
}

// This code is contributed by SURENDRA_GANGWAR
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to find j such that arr[j]=arr[i]
// and no element is greater than arr[i] in the
// range [j, i]
function findElements(arr, N) {

    // To Store answer
    let ans = new Array(N);

    // Initialize the value of ans[i] as 0
    for (let i = 0; i < N; i++) {
        ans[i] = 0;
    }

    // Traverse the array in reverse direction
    for (let i = N - 1; i >= 0; i--) {

        // Traverse in the range [i, 0]
        for (let j = i; j >= 0; j--) {
            if (arr[j] == arr[i]) {

                // Increment ans[i] if arr[j] =arr[i]
                ans[i]++;
            }
            else
                // Terminate the loop
                if (arr[j] > arr[i])
                    break;
        }

        // Traverse in the range [i+1, N-1]
        for (let j = i + 1; j < N; j++) {
            // Increment ans[i] if arr[i] = arr[j]
            if (arr[j] == arr[i])
                ans[i]++;
            else if (arr[j] > arr[i]) {
                break;
            }
        }
    }

    for (let i = 0; i < N; i++) {
        document.write(ans[i] + " ");
    }
}

// Driver Code

// Given Input
let arr = [1, 2, 1, 2, 4];
let N = arr.length

// Function Call
findElements(arr, N);

</script>
```

**Output**

```
1 2 1 2 1 
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(N)*
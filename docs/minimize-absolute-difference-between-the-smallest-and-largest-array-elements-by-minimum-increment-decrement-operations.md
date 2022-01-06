# 通过最小增量递减操作

最小化最小和最大数组元素之间的绝对差异

> 原文:[https://www . geeksforgeeks . org/最小化最小和最大数组元素之间的绝对差异最小递增递减运算/](https://www.geeksforgeeks.org/minimize-absolute-difference-between-the-smallest-and-largest-array-elements-by-minimum-increment-decrement-operations/)

给定一个由正整数 **N** 组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，任务是最小化运算次数，以最小化数组中最小和最大元素之间的绝对差异。在每个操作中，从一个数组元素中减去 **1** ，并增加 **1** 到另一个数组元素。

**示例:**

> **输入:** arr[] = {1，6}
> **输出:** 2
> **解释:**
> 下面是执行的操作:
> **操作 1:** 从第 2 个元素中减去 1，并将 1 加到第 1 个元素将数组修改为{2，5}。
> **操作 2:** 从第二个元素中减去 1，并在第一个元素中加上 1，将数组修改为{3，4}。
> 上述运算后，最小和最大元素的绝对差为(4–3)= 1，最小，所需运算次数为 2。
> 
> **输入:** arr[] = {1，2，2，1，1}
> **输出:** 0

**方法:**给定的问题可以通过观察以下事实来解决:阵列元素的增量和减量由 **1** 成对执行，因此如果阵列元素的[和](https://www.geeksforgeeks.org/program-find-sum-elements-given-array/)可以被 **N** 整除，那么所有阵列元素可以被**和/N** 整除。否则，在执行给定操作后，一些元素将具有值**和/N** ，一些元素将具有值**(和/N + 1)** 。按照以下步骤解决给定的问题:

*   初始化一个辅助数组，比如 **final[]** ，它存储具有所需最小差异的结果数组。
*   [给定数组按递增顺序排序](https://www.geeksforgeeks.org/c-program-to-sort-an-array-in-ascending-order/)。
*   [遍历给定数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，如果当前索引 **i** 小于**总和%N** ，则将最终数组的当前元素更新为值**(总和/N + 1)** 。否则，将**最终【I】**更新为**(和/否)**。
*   [反阵**决赛[]**T3】。](https://www.geeksforgeeks.org/write-a-program-to-reverse-an-array-or-string/)
*   初始化一个变量，比如说 **ans = 0** ，它存储将 **arr[]** 转换为 **final[]** 的最小操作数。
*   同时遍历数组 **arr[]** 和 **final[]** ，并将 **arr[i]** 和 **final[i]** 之差的绝对值加到变量 **ans** 上。
*   完成上述步骤后，打印 **ans/2** 的值作为最小运算结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to minimize the operations
// for the difference between minimum
// and maximum element by incrementing
// decrementing array elements in pairs
void countMinimumSteps(int arr[], int N)
{
    // Stores the sum of the array
    int sum = 0;

    // Find the sum of array element
    for (int i = 0; i < N; i++) {
        sum += arr[i];
    }

    // Stores the resultant final array
    int finalArray[N];

    // Iterate over the range [0, N]
    for (int i = 0; i < N; ++i) {

        // Assign values to finalArray
        if (i < sum % N) {
            finalArray[i] = sum / N + 1;
        }
        else {
            finalArray[i] = sum / N;
        }
    }

    // Reverse the final array
    reverse(finalArray, finalArray + N);

    // Stores the minimum number of
    // operations required
    int ans = 0;

    // Update the value of ans
    for (int i = 0; i < N; ++i) {
        ans += abs(arr[i] - finalArray[i]);
    }

    // Print the result
    cout << ans / 2;
}

// Driver Code
int main()
{
    int arr[] = { 1, 6 };
    int N = sizeof(arr) / sizeof(arr[0]);
    countMinimumSteps(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG{

static void reverse(int a[], int n)
{
    int i, k, t;
    for(i = 0; i < n / 2; i++)
    {
        t = a[i];
        a[i] = a[n - i - 1];
        a[n - i - 1] = t;
    }
}

// Function to minimize the operations
// for the difference between minimum
// and maximum element by incrementing
// decrementing array elements in pairs
static void countMinimumSteps(int arr[], int N)
{

    // Stores the sum of the array
    int sum = 0;

    // Find the sum of array element
    for(int i = 0; i < N; i++)
    {
        sum += arr[i];
    }

    // Stores the resultant final array
    int finalArray[] = new int[N];

    // Iterate over the range [0, N]
    for(int i = 0; i < N; ++i)
    {

        // Assign values to finalArray
        if (i < sum % N)
        {
            finalArray[i] = sum / N + 1;
        }
        else
        {
            finalArray[i] = sum / N;
        }
    }

    // Reverse the final array
    reverse(finalArray, finalArray.length);

    // Stores the minimum number of
    // operations required
    int ans = 0;

    // Update the value of ans
    for(int i = 0; i < N; ++i)
    {
        ans += Math.abs(arr[i] - finalArray[i]);
    }

    // Print the result
    System.out.println(ans / 2);
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 1, 6 };
    int N = arr.length;

    countMinimumSteps(arr, N);
}
}

// This code is contributed by abhinavjain194
```

## 蟒蛇 3

```
# Python program for the above approach

# Function to minimize the operations
# for the difference between minimum
# and maximum element by incrementing
# decrementing array elements in pairs
def countMinimumSteps(arr, N):

    # Stores the sum of the array
    sum = 0;

    # Find the sum of array element
    for i in range(N):
        sum += arr[i];

    # Stores the resultant final array
    finalArray = [0] * N;

    # Iterate over the range [0, N]

    for i in range(0, N):
        #print(i)

        # Assign values to finalArray
        if (i < sum % N):
            finalArray[i] = (sum // N)+ 1;
        else:
            finalArray[i] = sum // N;

    # Reverse the final array
    finalArray = finalArray[::-1];

    # Stores the minimum number of
    # operations required
    ans = 0;

    # Update the value of ans
    for i in range(N):
        ans += abs(arr[i] - finalArray[i]);

    # Print the result
    print(ans // 2);

# Driver Code
arr = [1, 6];
N = len(arr);
countMinimumSteps(arr, N);

# This code is contributed by _saurabh_jaiswal.
```

## C#

```
// C# program for the above approach
using System;

class GFG{

static void reverse(int[] a, int n)
{
    int i, t;
    for(i = 0; i < n / 2; i++)
    {
        t = a[i];
        a[i] = a[n - i - 1];
        a[n - i - 1] = t;
    }
}

// Function to minimize the operations
// for the difference between minimum
// and maximum element by incrementing
// decrementing array elements in pairs
static void countMinimumSteps(int[] arr, int N)
{

    // Stores the sum of the array
    int sum = 0;

    // Find the sum of array element
    for(int i = 0; i < N; i++)
    {
        sum += arr[i];
    }

    // Stores the resultant final array
    int[] finalArray = new int[N];

    // Iterate over the range [0, N]
    for(int i = 0; i < N; ++i)
    {

        // Assign values to finalArray
        if (i < sum % N)
        {
            finalArray[i] = sum / N + 1;
        }
        else
        {
            finalArray[i] = sum / N;
        }
    }

    // Reverse the final array
    reverse(finalArray, finalArray.Length);

    // Stores the minimum number of
    // operations required
    int ans = 0;

    // Update the value of ans
    for(int i = 0; i < N; ++i)
    {
        ans += Math.Abs(arr[i] - finalArray[i]);
    }

    // Print the result
    Console.WriteLine(ans / 2);
}

// Driver Code
public static void Main(String[] args)
{
    int[] arr = { 1, 6 };
    int N = arr.Length;

    countMinimumSteps(arr, N);
}
}

// This code is contributed by target_2
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to minimize the operations
// for the difference between minimum
// and maximum element by incrementing
// decrementing array elements in pairs
function countMinimumSteps(arr, N)
{

    // Stores the sum of the array
    let sum = 0;

    // Find the sum of array element
    for (let i = 0; i < N; i++) {
        sum += arr[i];
    }

    // Stores the resultant final array
    let finalArray = new Array(N);

    // Iterate over the range [0, N]
    for (let i = 0; i < N; ++i) {

        // Assign values to finalArray
        if (i < sum % N) {
            finalArray[i] = Math.floor(sum / N + 1);
        }
        else {
            finalArray[i] = Math.floor(sum / N);
        }
    }

    // Reverse the final array
    finalArray.reverse();

    // Stores the minimum number of
    // operations required
    let ans = 0;

    // Update the value of ans
    for (let i = 0; i < N; ++i) {
        ans += Math.abs(arr[i] - finalArray[i]);
    }

    // Print the result
    document.write(Math.floor(ans / 2));
}

// Driver Code
let arr = [1, 6];
let N = arr.length
countMinimumSteps(arr, N);

// This code is contributed by _saurabh_jaiswal.
</script>
```

**Output:** 

```
2
```

***时间复杂度:** O(N*log N)*
***辅助空间:** O(N)*
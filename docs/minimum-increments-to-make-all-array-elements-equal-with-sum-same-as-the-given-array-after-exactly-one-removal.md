# 精确一次移除后，使所有数组元素相等且总和与给定数组相同的最小增量

> 原文:[https://www . geeksforgeeks . org/最小增量使所有数组元素与给定数组在完全一次移除后相等/](https://www.geeksforgeeks.org/minimum-increments-to-make-all-array-elements-equal-with-sum-same-as-the-given-array-after-exactly-one-removal/)

给定一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】**和一个整数 **K** ，任务是通过移除一个数组元素并递增所有其他数组元素的值来检查是否可以使所有数组元素相等，从而使数组元素的[总和](https://www.geeksforgeeks.org/program-find-sum-elements-given-array/)保持不变。如果发现是真的，则打印**“是”**。否则，打印**“否”**。

**示例:**

> **输入:** arr[] = { 2，2，2，3 }
> **输出**:是
> **解释:**
> 从数组中移除 arr[2](基于 0 的索引)并将所有其他元素递增 1 会将 arr[]修改为{ 3，3，3 }
> ，因为所有数组元素都是相等的。因此，要求的输出是“是”。
> 
> **输入:** arr[] = { 0，3，0 }，K = 3
> **输出:**:否
> 从数组中移除 arr[1](基于 0 的索引)，并将 arr[0]的值增加 1，将 arr[2]的值增加 2，将 arr[]修改为{ 1，2 }
> ，因为所有数组元素都不相等。因此，要求的输出是“否”。

**方法:**使用[贪婪手法](https://www.geeksforgeeks.org/greedy-algorithms/)可以解决问题。其思想是移除[最大的数组元素](https://www.geeksforgeeks.org/c-program-find-largest-element-array/)，并增加其他元素的值，使得总和保持不变。按照以下步骤解决问题:

*   初始化一个变量，比如**秒最大值**，来存储数组的第二大元素[。](https://www.geeksforgeeks.org/find-second-largest-element-array/)
*   初始化一个变量，比如 **totalSum** ，来存储数组元素的[和。](https://www.geeksforgeeks.org/program-find-sum-elements-given-array/)
*   [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)计算数组元素的和，找到第二大的数组元素。
*   如果**总计<(N–1)*秒最大**或**总计(N–1)！= 0** ，则打印**“否”**。
*   否则，打印**“是”**。

下面是上述方法的实现

## C++

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to check if an array of
// equal elements with sum equal to
// the given array can be obtained or not
bool CheckAllarrayEqual(int arr[], int N)
{
    // Base case
    if (N == 1) {
        return true;
    }

    // Stores sum of
    // array elements
    int totalSum = arr[0];

    // Stores second largest
    // array element
    int secMax = INT_MIN;

    // Stores the largest
    // array element
    int Max = arr[0];

    // Traverse the array
    for (int i = 1; i < N; i++) {

        if (arr[i] >= Max) {

            // Update secMax
            secMax = Max;

            // Update Max
            Max = arr[i];
        }
        else if (arr[i] > secMax) {

            // Update secMax
            secMax = arr[i];
        }

        // Update totalSum
        totalSum += arr[i];
    }

    // If totalSum is less than
    // secMax * (N - 1))
    if ((secMax * (N - 1)) > totalSum) {

        return false;
    }

    // If totalSum is not
    // divisible by (N - 1)
    if (totalSum % (N - 1)) {

        return false;
    }

    return true;
}

// Driver Code
int main()
{
    int arr[] = { 6, 2, 2, 2 };
    int N = sizeof(arr) / sizeof(arr[0]);

    if (CheckAllarrayEqual(arr, N)) {
        cout << "YES";
    }
    else {
        cout << "NO";
    }
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;

class GFG{

// Function to check if an array of
// equal elements with sum equal to
// the given array can be obtained or not
static boolean CheckAllarrayEqual(int[] arr,
                                  int N)
{

    // Base case
    if (N == 1)
    {
        return true;
    }

    // Stores sum of
    // array elements
    int totalSum = arr[0];

    // Stores second largest
    // array element
    int secMax = Integer.MIN_VALUE;

    // Stores the largest
    // array element
    int Max = arr[0];

    // Traverse the array
    for(int i = 1; i < N; i++)
    {
        if (arr[i] >= Max)
        {

            // Update secMax
            secMax = Max;

            // Update Max
            Max = arr[i];
        }
        else if (arr[i] > secMax)
        {

            // Update secMax
            secMax = arr[i];
        }

        // Update totalSum
        totalSum += arr[i];
    }

    // If totalSum is less than
    // secMax * (N - 1))
    if ((secMax * (N - 1)) > totalSum)
    {
        return false;
    }

    // If totalSum is not
    // divisible by (N - 1)
    if (totalSum % (N - 1) != 0)
    {
        return false;
    }

    return true;
}

// Driver Code
public static void main(String[] args)
{
    int[] arr = { 6, 2, 2, 2 };
    int N = arr.length;

    if (CheckAllarrayEqual(arr, N))
    {
        System.out.print("YES");
    }
    else
    {
        System.out.print("NO");
    }
}
}

// This code is contributed by susmitakundugoaldanga
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to check if an array of
# equal elements with sum equal to
# the given array can be obtained or not
def CheckAllarrayEqual(arr, N):

    # Base case
    if (N == 1):
        return True

    # Stores sum of
    # array elements
    totalSum = arr[0]

    # Stores second largest
    # array element
    secMax = -10**19

    # Stores the largest
    # array element
    Max = arr[0]

    # Traverse the array
    for i in range(1,N):

        if (arr[i] >= Max):

            # Update secMax
            secMax = Max

            # Update Max
            Max = arr[i]
        elif (arr[i] > secMax):

            # Update secMax
            secMax = arr[i]

        # Update totalSum
        totalSum += arr[i]

    # If totalSum is less than
    # secMax * (N - 1))
    if ((secMax * (N - 1)) > totalSum):

        return False

    # If totalSum is not
    # divisible by (N - 1)
    if (totalSum % (N - 1)):
        return False
    return True

# Driver Code
if __name__ == '__main__':
    arr=[6, 2, 2, 2]
    N = len(arr)

    if (CheckAllarrayEqual(arr, N)):
        print("YES")
    else:
        print("NO")

        # This code is contributed by mohit kumar 29
```

## C#

```
// C# program to implement
// the above approach 
using System;
class GFG
{

// Function to check if an array of
// equal elements with sum equal to
// the given array can be obtained or not
static bool CheckAllarrayEqual(int[] arr, int N)
{
    // Base case
    if (N == 1) {
        return true;
    }

    // Stores sum of
    // array elements
    int totalSum = arr[0];

    // Stores second largest
    // array element
    int secMax = Int32.MinValue;

    // Stores the largest
    // array element
    int Max = arr[0];

    // Traverse the array
    for (int i = 1; i < N; i++) {

        if (arr[i] >= Max) {

            // Update secMax
            secMax = Max;

            // Update Max
            Max = arr[i];
        }
        else if (arr[i] > secMax) {

            // Update secMax
            secMax = arr[i];
        }

        // Update totalSum
        totalSum += arr[i];
    }

    // If totalSum is less than
    // secMax * (N - 1))
    if ((secMax * (N - 1)) > totalSum) {

        return false;
    }

    // If totalSum is not
    // divisible by (N - 1)
    if (totalSum % (N - 1) != 0) {

        return false;
    }

    return true;
}

// Driver Code
public static void Main()
{
    int[] arr = { 6, 2, 2, 2 };
    int N = arr.Length;

    if (CheckAllarrayEqual(arr, N)) {
        Console.Write("YES");
    }
    else {
        Console.Write("NO");
    }
}
}

// This code is contributed by sanjoy_62
```

## java 描述语言

```
<script>

// JavaScript program to implement
// the above approach

// Function to check if an array of
// equal elements with sum equal to
// the given array can be obtained or not
function CheckAllarrayEqual(arr,N)
{

    // Base case
    if (N == 1)
    {
        return true;
    }

    // Stores sum of
    // array elements
    let totalSum = arr[0];

    // Stores second largest
    // array element
    let secMax = Number.MIN_VALUE;

    // Stores the largest
    // array element
    let Max = arr[0];

    // Traverse the array
    for(let i = 1; i < N; i++)
    {
        if (arr[i] >= Max)
        {

            // Update secMax
            secMax = Max;

            // Update Max
            Max = arr[i];
        }
        else if (arr[i] > secMax)
        {

            // Update secMax
            secMax = arr[i];
        }

        // Update totalSum
        totalSum += arr[i];
    }

    // If totalSum is less than
    // secMax * (N - 1))
    if ((secMax * (N - 1)) > totalSum)
    {
        return false;
    }

    // If totalSum is not
    // divisible by (N - 1)
    if (totalSum % (N - 1) != 0)
    {
        return false;
    }

    return true;
}

// Driver Code

    let arr = [ 6, 2, 2, 2 ];
    let N = arr.length;

    if (CheckAllarrayEqual(arr, N))
    {
        document.write("YES");
    }
    else
    {
        document.write("NO");
    }

// This code is contributed by sravan kumar Gottumukkala

</script>
```

**Output:** 

```
YES
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)
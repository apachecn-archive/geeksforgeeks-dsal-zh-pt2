# 形成算术级数(AP)的最长子阵列

> 原文:[https://www . geesforgeks . org/long-subarray-forming-an-算术级数-ap/](https://www.geeksforgeeks.org/longest-subarray-forming-an-arithmetic-progression-ap/)

给定一个大小为 **N** 的数组 **arr[]** ，任务是找出形成[等差数列](https://www.geeksforgeeks.org/arithmetic-progression/)的最长子数组的长度。
**示例:**

> **输入:** arr[] = {3，4，5}
> **输出:** 3
> **说明:**形成一个 AP 的最长子阵是{3，4，5}，共差 1。
> **输入:** {10，7，4，6，8，10，11}
> **输出:** 4
> **解释:**形成一个 AP 的最长可能的子阵是{4，6，8，10}，它们有共同的区别(= 2)。

**天真方法:**解决问题最简单的方法是[生成所有可能的子阵列](https://www.geeksforgeeks.org/generating-subarrays-using-recursion/)，对于每个子阵列，检查相邻元素之间的[差异是否始终保持不变。在所有满足条件的子阵列中，存储最长子阵列的长度并将其作为结果打印出来。
***时间复杂度:**O(N<sup>3</sup>)*
***辅助空间:** O(1)*](https://www.geeksforgeeks.org/python-calculate-difference-between-adjacent-elements-in-given-list/)

**高效方法:**要优化上述方法，这里的思路是观察每当当前相邻元素对之间的差异不等于前一对相邻元素之间的差异时，将前一个子阵列的长度与迄今为止获得的最大值进行比较，并启动新的子阵列并相应地重复。按照以下步骤解决问题:

1.  初始化变量 **res** 以存储形成一个 [AP](https://www.geeksforgeeks.org/progressions-ap-gp-hp/) 的最长子阵列的长度。
2.  迭代剩余的数组，并将当前的相邻差与前一个相邻差进行比较。
3.  迭代数组，对于每个元素，计算当前相邻元素对之间的差，并检查它是否等于前一对相邻元素。如果发现为真，通过将 **res** 增加 1 来继续正在进行的子阵列。
4.  否则，考虑一个新的子阵列。通过与前一个子阵列的长度进行比较，更新目前获得的最大长度，即 **res** 。
5.  最后，返回 **res** 作为所需答案。

以下是上述方法的实现:

## C++14

```
// C++ Program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to return the length
// of longest subarray forming an AP
int getMaxLength(int arr[], int N)
{
    //single number is also an AP
    //with common difference as 0
    if(N==1)
    return 1;

    // Minimum possible length of
    // required subarray is 2
    int res = 2;

    // Stores the length of the
    // current subarray
    int dist = 2;

    // Stores the common difference
    // of the current AP
    int curradj = (arr[1] - arr[0]);

    // Stores the common difference
    // of the previous AP
    int prevadj = (arr[1] - arr[0]);
    for (int i = 2; i < N; i++) {
        curradj = arr[i] - arr[i - 1];

        // If the common differences
        // are found to be equal
        if (curradj == prevadj) {

            // Continue the previous subarray
            dist++;
        }

        // Start a new subarray
        else {
            prevadj = curradj;

            // Update the length to
            // store maximum length
            res = max(res, dist);
            dist = 2;
        }
    }

    // Update the length to
    // store maximum length
    res = max(res, dist);

    // Return the length of
    // the longest subarray
    return res;
}

// Driver Code
int main()
{
    int arr[] = {10, 7, 4, 6, 8, 10, 11};
    int N = sizeof(arr) / sizeof(arr[0]);
    cout << getMaxLength(arr, N);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to implement
// the above approach
import java.util.*;
class GFG{

// Function to return the length
// of longest subarray forming an AP
static int getMaxLength(int arr[], int N)
{

    // Minimum possible length of
    // required subarray is 2
    int res = 2;

    // Stores the length of the
    // current subarray
    int dist = 2;

    // Stores the common difference
    // of the current AP
    int curradj = (arr[1] - arr[0]);

    // Stores the common difference
    // of the previous AP
    int prevadj = (arr[1] - arr[0]);
    for (int i = 2; i < N; i++)
    {
        curradj = arr[i] - arr[i - 1];

        // If the common differences
        // are found to be equal
        if (curradj == prevadj)
        {
            // Continue the previous subarray
            dist++;
        }

        // Start a new subarray
        else
        {
            prevadj = curradj;

            // Update the length to
            // store maximum length
            res = Math.max(res, dist);
            dist = 2;
        }
    }

    // Update the length to
    // store maximum length
    res = Math.max(res, dist);

    // Return the length of
    // the longest subarray
    return res;
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = {10, 7, 4,
                 6, 8, 10, 11};
    int N = arr.length;
    System.out.print(getMaxLength(arr, N));
}
}

// This code is contributed by shikhasingrajput
```

## 蟒蛇 3

```
# python3 Program to implement
# the above approach

# Function to return the length
# of longest subarray forming an AP
def getMaxLength(arr,  N):

    # Minimum possible length of
    # required subarray is 2
    res = 2

    # Stores the length of the
    # current subarray
    dist = 2

    # Stores the common difference
    # of the current AP
    curradj = (arr[1] - arr[0])

    # Stores the common difference
    # of the previous AP
    prevadj = (arr[1] - arr[0])
    for i in range(2, N):
        curradj = arr[i] - arr[i - 1]

        # If the common differences
        # are found to be equal
        if (curradj == prevadj):

            # Continue the previous subarray
            dist += 1

        # Start a new subarray
        else:
            prevadj = curradj

            # Update the length to
            # store maximum length
            res = max(res, dist)
            dist = 2

    # Update the length to
    # store maximum length
    res = max(res, dist)

    # Return the length of
    # the longest subarray
    return res

# Driver Code
if __name__ == "__main__":
    arr = [10, 7, 4, 6, 8, 10, 11]
    N = len(arr)
    print(getMaxLength(arr, N))

# This code is contributed by Chitranayal
```

## C#

```
// C# Program to implement
// the above approach
using System;

public class GFG{

// Function to return the length
// of longest subarray forming an AP
static int getMaxLength(int []arr,
                        int N)
{

    // Minimum possible length of
    // required subarray is 2
    int res = 2;

    // Stores the length of the
    // current subarray
    int dist = 2;

    // Stores the common difference
    // of the current AP
    int curradj = (arr[1] - arr[0]);

    // Stores the common difference
    // of the previous AP
    int prevadj = (arr[1] - arr[0]);

    for (int i = 2; i < N; i++)
    {
        curradj = arr[i] - arr[i - 1];

        // If the common differences
        // are found to be equal
        if (curradj == prevadj)
        {
            // Continue the previous subarray
            dist++;
        }

        // Start a new subarray
        else
        {
            prevadj = curradj;

            // Update the length to
            // store maximum length
            res = Math.Max(res, dist);
            dist = 2;
        }
    }

    // Update the length to
    // store maximum length
    res = Math.Max(res, dist);

    // Return the length of
    // the longest subarray
    return res;
}

// Driver Code
public static void Main(String[] args)
{
    int []arr = {10, 7, 4,
                 6, 8, 10, 11};
    int N = arr.Length;
    Console.Write(getMaxLength(arr, N));
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript Program to implement
// the above approach

// Function to return the length
// of longest subarray forming an AP
function getMaxLength(arr, N)
{

    // Minimum possible length of
    // required subarray is 2
    let res = 2;

    // Stores the length of the
    // current subarray
    let dist = 2;

    // Stores the common difference
    // of the current AP
    let curradj = (arr[1] - arr[0]);

    // Stores the common difference
    // of the previous AP
    let prevadj = (arr[1] - arr[0]);
    for (let i = 2; i < N; i++) {
        curradj = arr[i] - arr[i - 1];

        // If the common differences
        // are found to be equal
        if (curradj == prevadj) {

            // Continue the previous subarray
            dist++;
        }

        // Start a new subarray
        else {
            prevadj = curradj;

            // Update the length to
            // store maximum length
            res = Math.max(res, dist);
            dist = 2;
        }
    }

    // Update the length to
    // store maximum length
    res = Math.max(res, dist);

    // Return the length of
    // the longest subarray
    return res;
}

// Driver Code

    let arr= [ 10, 7, 4, 6, 8, 10, 11 ];
    let N = arr.length;
    document.write(getMaxLength(arr, N));

// This code is contributed by Mayank Tyagi

</script>
```

**Output:** 

```
4
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)
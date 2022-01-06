# 找到和在[(K+1)/2，K]

范围内的子序列

> 原文:[https://www . geesforgeks . org/find-a-subsequence-with-sum-in-range-k1-2-k/](https://www.geeksforgeeks.org/find-a-subsequence-with-sum-in-range-k1-2-k/)

给定一个由 **N** 个正整数和一个正整数 **K** 组成的[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】**，任务是找到一个[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】**的[子序列](https://www.geeksforgeeks.org/generating-all-possible-subsequences-using-recursion/)，其元素之和在 **[(K+1)/2，K]** 的范围内。如果有子序列，则打印[子序列](https://www.geeksforgeeks.org/generating-all-possible-subsequences-using-recursion/)的索引，否则打印 **-1** 。

**注意:**这个问题可能有多个答案，打印任意一个。

**示例:**

> **输入:** arr[ ] = {6，2，20，3，5，6}，K = 13
> **输出:** 0 1 3
> **解释:**
> 子序列{6，2，3}的元素之和是在[(K+1)/2，K]范围内的 11。
> 
> **输入:** arr[ ] = {20，24，33，100}，K = 2
> **输出:** -1

**进场:**这个问题可以通过[穿越](https://www.geeksforgeeks.org/iterating-arraylists-java/) [阵](https://www.geeksforgeeks.org/array-data-structure/)**arr【】**来解决。按照以下步骤解决此问题:

*   初始化一个[向量](https://www.geeksforgeeks.org/vector-in-cpp-stl/) **和**来存储结果子序列的索引， **totalSum** 来存储子序列的元素之和。
*   [使用变量 **i** 在范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，N-1】**中迭代，并执行以下步骤:
    *   如果**arr【I】>K**，继续遍历数组的元素。
    *   如果 **arr[i]** 在 **[(K+1)/2，K]** 范围内，则返回当前元素的索引作为答案并终止循环。
    *   如果 **arr[i] +totalSum** 小于 **K，**则将当前元素添加到 **totalSum** 中，并在[向量](https://www.geeksforgeeks.org/vector-in-cpp-stl/) **ans 中添加索引 **i** 。**
*   如果 **totalSum** 不在给定范围内，则打印 **-1、**否则打印[矢量](https://www.geeksforgeeks.org/vector-in-cpp-stl/) **ans。**

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find a subsequence of the
// given array whose sum of the elements
// is in range [K+1/2, K]
void isSumOfSubSeqInRange(int arr[], int n, int k)
{

    // Vector to store the subsequence indices
    vector<int> ans;

    // Variable to store the sum of subsequence
    int totalSum = 0;

    for (int i = 0; i < n; i++) {

        // If the current element is
        // greater than K then move
        // forward
        if (arr[i] > k) {
            continue;
        }

        // If the current element is in
        // the given range
        if (arr[i] >= (k + 1) / 2) {
            ans.clear();
            ans.push_back(i);
            totalSum = arr[i];
            break;
        }
        // If current element and totalSum
        // is less than K
        else if (arr[i] + totalSum <= k) {

            totalSum += arr[i];
            ans.push_back(i);
        }
    }

    // Checking if the totalSum is not
    // in the given range then print -1
    if (2 * totalSum < k) {
        cout << -1 << endl;
        return;
    }

    // Otherwise print the answer
    for (int x : ans) {
        cout << x << " ";
    }
    cout << endl;
}

// Driver Code
int main()
{

    // Given Input
    int arr[] = { 6, 2, 20, 3, 5, 6 };
    int N = 6;
    int K = 13;

    // Function Call
    isSumOfSubSeqInRange(arr, N, K);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.Vector;

public class GFG {

    // Function to find a subsequence of the
    // given array whose sum of the elements
    // is in range [K+1/2, K]
    static void isSumOfSubSeqInRange(int arr[], int n,
                                     int k)
    {

        // Vector to store the subsequence indices
        Vector<Integer> ans = new Vector<>();

        // Variable to store the sum of subsequence
        int totalSum = 0;

        for (int i = 0; i < n; i++) {

            // If the current element is
            // greater than K then move
            // forward
            if (arr[i] > k) {
                continue;
            }

            // If the current element is in
            // the given range
            if (arr[i] >= (k + 1) / 2) {
                ans.clear();
                ans.add(i);
                totalSum = arr[i];
                break;
            }
            // If current element and totalSum
            // is less than K
            else if (arr[i] + totalSum <= k) {

                totalSum += arr[i];
                ans.add(i);
            }
        }

        // Checking if the totalSum is not
        // in the given range then print -1
        if (2 * totalSum < k) {
            System.out.println(-1);
            return;
        }

        // Otherwise print the answer
        for (int x : ans) {
            System.out.print(x + " ");
        }
        System.out.println();
    }

    // Driver code
    public static void main(String[] args)
    {
        // Given Input
        int arr[] = { 6, 2, 20, 3, 5, 6 };
        int N = 6;
        int K = 13;

        // Function Call
        isSumOfSubSeqInRange(arr, N, K);
    }
}
// This code is contributed by abhinavjain194
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find a subsequence of the
# given array whose sum of the elements
# is in range [K+1/2, K]
def isSumOfSubSeqInRange(arr, n, k):

    # Vector to store the subsequence indices
    ans = []

    # Variable to store the sum of subsequence
    totalSum = 0

    for i in range(n):

        # If the current element is
        # greater than K then move
        # forward
        if (arr[i] > k):
            continue

        # If the current element is in
        # the given range
        if (arr[i] >= (k + 1) / 2):
            ans.clear()
            ans.append(i)
            totalSum = arr[i]
            break

        # If current element and totalSum
        # is less than K
        elif (arr[i] + totalSum <= k):
            totalSum += arr[i]
            ans.append(i)

    # Checking if the totalSum is not
    # in the given range then print -1
    if (2 * totalSum < k):
        print(-1)
        return

    # Otherwise print the answer
    for x in ans:
        print(x, end = " ")

# Driver Code
if __name__ == '__main__':

    # Given Input
    arr = [ 6, 2, 20, 3, 5, 6 ]
    N = 6
    K = 13

    # Function Call
    isSumOfSubSeqInRange(arr, N, K)

# This code is contributed by bgangwar59
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

public class GFG {

    // Function to find a subsequence of the
    // given array whose sum of the elements
    // is in range [K+1/2, K]
    static void isSumOfSubSeqInRange(int[] arr, int n,
                                     int k)
    {

        // Vector to store the subsequence indices
        List<int> ans = new List<int>();

        // Variable to store the sum of subsequence
        int totalSum = 0;

        for (int i = 0; i < n; i++) {

            // If the current element is
            // greater than K then move
            // forward
            if (arr[i] > k) {
                continue;
            }

            // If the current element is in
            // the given range
            if (arr[i] >= (k + 1) / 2) {
                ans.Clear();
                ans.Add(i);
                totalSum = arr[i];
                break;
            }

            // If current element and totalSum
            // is less than K
            else if (arr[i] + totalSum <= k) {

                totalSum += arr[i];
                ans.Add(i);
            }
        }

        // Checking if the totalSum is not
        // in the given range then print -1
        if (2 * totalSum < k) {
            Console.WriteLine(-1);
            return;
        }

        // Otherwise print the answer
        foreach(int x in ans)
        {
            Console.Write(x + " ");
        }
        Console.WriteLine();
    }

    // Driver code
    static public void Main ()
    {

        // Given Input
        int[] arr = { 6, 2, 20, 3, 5, 6 };
        int N = 6;
        int K = 13;

        // Function Call
        isSumOfSubSeqInRange(arr, N, K);
    }
}

// This Code is contributed by ShubhamSingh10
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to find a subsequence of the
// given array whose sum of the elements
// is in range [K+1/2, K]
function isSumOfSubSeqInRange(arr, n, k) {

    // Vector to store the subsequence indices
    let ans = [];

    // Variable to store the sum of subsequence
    let totalSum = 0;

    for (let i = 0; i < n; i++) {

        // If the current element is
        // greater than K then move
        // forward
        if (arr[i] > k) {
            continue;
        }

        // If the current element is in
        // the given range
        if (arr[i] >= (k + 1) / 2) {
            ans = [];
            ans.push(i);
            totalSum = arr[i];
            break;
        }

        // If current element and totalSum
        // is less than K
        else if (arr[i] + totalSum <= k) {

            totalSum += arr[i];
            ans.push(i);
        }
    }

    // Checking if the totalSum is not
    // in the given range then print -1
    if (2 * totalSum < k) {
        document.write(-1 + "<br>");
        return;
    }

    // Otherwise print the answer
    for (let x of ans) {
        document.write(x + " ");
    }
    document.write("<br>");
}

// Driver Code

// Given Input
let arr = [6, 2, 20, 3, 5, 6];
let N = 6;
let K = 13;

// Function Call
isSumOfSubSeqInRange(arr, N, K);

// This code is contributed by gfgking.
</script>
```

**Output**

```
0 1 3 
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)
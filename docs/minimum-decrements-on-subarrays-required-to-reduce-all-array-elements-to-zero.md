# 将所有阵列元素降至零所需的子阵列最小减量

> 原文:[https://www . geesforgeks . org/subarray 上的最小递减-需要将所有数组元素减少到零/](https://www.geeksforgeeks.org/minimum-decrements-on-subarrays-required-to-reduce-all-array-elements-to-zero/)

给定一个由非负整数 **N** 组成的数组 **arr[]** ，任务是找到需要减少 1 的最小子数组数，使得所有数组元素都等于 0。

**示例:**

> **输入:** arr[] = {1，2，3，2，1}
> **输出:** 3
> **解释:**
> 操作 1: {1，2，3，2，1} - > {0，1，2，1，0}
> 操作 2: {0，1，2，1，0} - > {0，1，0，0}
> 操作 3: {0，0，1，0，0 }--
> 
> **输入:** arr[] = {5，4，3，4，4}
> **输出:** 6
> **解释:**
> {5，4，3，4，4}，- > {4，3，2，3，3，3} - > {3，2，1，2，2，2} - > {2，1，0，1，1} - > {2，1，0，0} - >

**方法:**
这可以通过从索引 **0** 遍历给定数组，找到直到索引 **i** 的答案来实现，其中 **0 ≤ i < N** 。如果 **arr[i] ≥ arr[i+1]** ，那么 **(i + 1) <sup>第</sup>** 元素可以包含在 **i <sup>第</sup>** 元素的每个子阵列操作中，因此不需要额外的操作。如果 **arr[i] < arr[i + 1]** ，那么 **(i + 1) <sup>第</sup>** 元素可以包含在 **i <sup>第</sup>** 元素的每个子阵列操作中，并且在所有操作之后， **arr[i+1]** 变成 **arr[i+1]-arr[i]** 。因此，我们需要 **arr[i+1]-arr[i]** 的额外操作将其降为零。

按照以下步骤解决问题:

*   将第一个元素**arr【0】**添加到**答案**中，因为我们至少需要**arr【0】**来制作给定的数组 **0** 。
*   遍历索引**【1，N-1】**，对于每个元素，检查它是否大于前一个元素。如果发现是真的，将它们的差异添加到**答案**中。

下面是上述方法的实现:

## C++

```
// C++ Program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to count the minimum
// number of subarrays that are
// required to be decremented by 1
int min_operations(vector<int>& A)
{
    // Base Case
    if (A.size() == 0)
        return 0;

    // Initialize ans to first element
    int ans = A[0];

    for (int i = 1; i < A.size(); i++) {

        // For A[i] > A[i-1], operation
        // (A[i] - A[i - 1]) is required
        ans += max(A[i] - A[i - 1], 0);
    }

    // Return the answer
    return ans;
}

// Driver Code
int main()
{
    vector<int> A{ 1, 2, 3, 2, 1 };

    cout << min_operations(A) << "\n";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to implement
// the above approach
import java.io.*;

class GFG {

    // Function to count the minimum
    // number of subarrays that are
    // required to be decremented by 1
    static int min_operations(int A[], int n)
    {
        // Base Case
        if (n == 0)
            return 0;

        // Initializing ans to first element
        int ans = A[0];
        for (int i = 1; i < n; i++) {

            // For A[i] > A[i-1], operation
            // (A[i] - A[i - 1]) is required
            if (A[i] > A[i - 1]) {
                ans += A[i] - A[i - 1];
            }
        }

        // Return the count
        return ans;
    }

    // Driver Code
    public static void main(String[] args)
    {
        int n = 5;
        int A[] = { 1, 2, 3, 2, 1 };
        System.out.println(min_operations(A, n));
    }
}
```

## 计算机编程语言

```
# Python Program to implement
# the above approach

# Function to count the minimum
# number of subarrays that are
# required to be decremented by 1
def min_operations(A):

    # Base case
    if len(A) == 0:
        return 0

    # Initializing ans to first element
    ans = A[0]
    for i in range(1, len(A)):

        if A[i] > A[i-1]:
            ans += A[i]-A[i-1]

    return ans

# Driver Code
A = [1, 2, 3, 2, 1]
print(min_operations(A))
```

## C#

```
// C# program to implement
// the above approach
using System;

class GFG{

// Function to count the minimum
// number of subarrays that are
// required to be decremented by 1
static int min_operations(int[] A, int n)
{

    // Base Case
    if (n == 0)
        return 0;

    // Initializing ans to first element
    int ans = A[0];

    for(int i = 1; i < n; i++)
    {

        // For A[i] > A[i-1], operation
        // (A[i] - A[i - 1]) is required
        if (A[i] > A[i - 1])
        {
            ans += A[i] - A[i - 1];
        }
    }

    // Return the count
    return ans;
}

// Driver Code
public static void Main()
{
    int n = 5;
    int[] A = { 1, 2, 3, 2, 1 };

    Console.WriteLine(min_operations(A, n));
}
}

// This code is contributed by bolliranadheer
```

## java 描述语言

```
<script>

// Javascript program to implement
// the above approach

// Function to count the minimum
// number of subarrays that are
// required to be decremented by 1
function min_operations(A)
{

    // Base Case
    if (A.length == 0)
        return 0;

    // Initialize ans to first element
    let ans = A[0];

    for(let i = 1; i < A.length; i++)
    {

        // For A[i] > A[i-1], operation
        // (A[i] - A[i - 1]) is required
        ans += Math.max(A[i] - A[i - 1], 0);
    }

    // Return the answer
    return ans;
}

// Driver Code
let A = [ 1, 2, 3, 2, 1 ];
document.write(min_operations(A));

// This code is contributed by subhammahato348

</script>
```

**输出:**

```
3
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)
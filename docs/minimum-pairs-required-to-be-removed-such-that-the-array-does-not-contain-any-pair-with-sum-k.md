# 需要移除的最少对，使得数组不包含任何和为 K 的对

> 原文:[https://www . geeksforgeeks . org/最小对-需要移除-这样-数组不包含任何带 sum-k 的对/](https://www.geeksforgeeks.org/minimum-pairs-required-to-be-removed-such-that-the-array-does-not-contain-any-pair-with-sum-k/)

给定一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】**和一个整数 **K** ，任务是找到需要移除的最小对数，使得数组中不存在元素之和等于 **K** 的对。

**示例:**

> **输入:** arr[] = { 3，1，3，4，3 }，K = 6
> **输出:** 1
> **解释:**
> 移除对(arr[0]，arr[2])会将 arr[]修改为 arr[] = { 1，4，3 }
> 由于元素之和等于 K(=6)的 arr[]中不存在对，因此需要的输出为 1。
> 
> **输入:** arr = { 1，2，3，4 }，K = 5
> **输出:** 2
> **解释:**
> 移除对(arr[0]，arr[3])将 arr[]修改为 arr[] = { 2，3 }
> 移除对(arr[0，arr[1])将 arr[]修改为 arr[] = { }
> 由于元素之和等于 K(=5)的 arr[]中不存在对，因此所需输出为 2。

**方法:**使用[两点](https://www.geeksforgeeks.org/two-pointers-technique/)技术可以解决问题。按照以下步骤解决此问题:

*   [按升序排列数组](https://www.geeksforgeeks.org/c-program-to-sort-an-array-in-ascending-order/)。
*   初始化两个变量，比如**左= 0** 和**右= N–1**分别存储左右指针的索引。
*   初始化一个变量，比如 **cntPairs** ，以存储需要移除的最小配对数，这样数组中就不存在总和等于 **K** 的配对。
*   [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)并检查以下条件。
    *   如果**arr[左]+arr[右] == K** ，那么将 **cntPairs** 的值增加 **1** 并更新 **left += 1** 和 right -= 1。
    *   如果**arr[左]+arr[右] < K** ，那么更新 **left += 1** 。
    *   如果**arr[左]+arr[右] < K** ，那么更新 **right -= 1** 。
*   最后，打印 **cntPairs** 的值。

下面是上述方法的实现:

## C++14

```
// C++14 program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the maximum count of pairs
// required to be removed such that no pairs
// exist whose sum equal to K
int maxcntPairsSumKRemoved(vector<int> arr, int k)
{

    // Stores maximum count of pairs required
    // to be removed such that no pairs
    // exist whose sum equal to K
    int cntPairs = 0;

    // Base Case
    if (arr.size() <= 1)
        return cntPairs;

    // Sort the array
    sort(arr.begin(), arr.end());

    // Stores index of
    // left pointer
    int left = 0;

    // Stores index of
    // right pointer
    int right = arr.size() - 1;

    while (left < right)
    {

        // Stores sum of left
        // and right pointer
        int s = arr[left] + arr[right];

        // If s equal to k
        if (s == k)
        {

            // Update cntPairs
            cntPairs += 1;

            // Update left
            left += 1;

            // Update right
            right -= 1;
        }

        // If s > k
        else if (s > k)

            // Update right
            right -= 1;
        else

            // Update left
            left += 1;
    }

    // Return the cntPairs
    return cntPairs;
}

// Driver Code
int main()
{
    vector<int> arr = { 1, 2, 3, 4 };
    int K = 5;

    // Function call
    cout << (maxcntPairsSumKRemoved(arr, K));

    return 0;
}

// This code is contributed by mohit kumar 29
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach 
import java.util.*;

class GFG{

// Function to find the maximum count of pairs
// required to be removed such that no pairs
// exist whose sum equal to K
static int maxcntPairsSumKRemoved(int[] arr, int k)
{

    // Stores maximum count of pairs required
    // to be removed such that no pairs
    // exist whose sum equal to K
    int cntPairs = 0;

    // Base Case
    if (arr.length <= 1)
        return cntPairs;

    // Sort the array
    Arrays.sort(arr);

    // Stores index of
    // left pointer
    int left = 0;

    // Stores index of
    // right pointer
    int right = arr.length - 1;

    while (left < right)
    {

        // Stores sum of left
        // and right pointer
        int s = arr[left] + arr[right];

        // If s equal to k
        if (s == k)
        {

            // Update cntPairs
            cntPairs += 1;

            // Update left
            left += 1;

            // Update right
            right -= 1;
        }

        // If s > k
        else if (s > k)

            // Update right
            right -= 1;
        else

            // Update left
            left += 1;
    }

    // Return the cntPairs
    return cntPairs;
}  

// Driver Code   
public static void main (String[] args)   
{   
    int[] arr = { 1, 2, 3, 4 };
    int K = 5;

    // Function call
    System.out.println (maxcntPairsSumKRemoved(arr, K));  
}
}
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to find the maximum count of pairs
# required to be removed such that no pairs
# exist whose sum equal to K
def maxcntPairsSumKRemoved(arr, k):

    # Stores maximum count of pairs required
    # to be removed such that no pairs
    # exist whose sum equal to K
    cntPairs = 0

    # Base Case
    if not arr or len(arr) == 1:
        return cntPairs

    # Sort the array   
    arr.sort()

    # Stores index of
    # left pointer
    left = 0

    # Stores index of
    # right pointer
    right = len(arr) - 1

    while left < right:

        # Stores sum of left
        # and right pointer
        s = arr[left] + arr[right]

        # If s equal to k
        if s == k:

            # Update cntPairs
            cntPairs += 1

            # Update left
            left += 1

            # Update right
            right-= 1

        # If s > k
        elif s > k:

            # Update right
            right-= 1
        else:

            # Update left
            left+= 1

    # Return the cntPairs
    return cntPairs

# Driver Code
if __name__ == "__main__":
    arr =[1, 2, 3, 4]
    K = 5

    # Function call
    print(maxcntPairsSumKRemoved(arr, K))
```

## C#

```
// C# program for the above approach 
using System;
class GFG{

// Function to find the maximum count of pairs
// required to be removed such that no pairs
// exist whose sum equal to K
static int maxcntPairsSumKRemoved(int[] arr, int k)
{

    // Stores maximum count of pairs required
    // to be removed such that no pairs
    // exist whose sum equal to K
    int cntPairs = 0;

    // Base Case
    if (arr.Length <= 1)
        return cntPairs;

    // Sort the array
    Array.Sort(arr);

    // Stores index of
    // left pointer
    int left = 0;

    // Stores index of
    // right pointer
    int right = arr.Length - 1;

    while (left < right)
    {

        // Stores sum of left
        // and right pointer
        int s = arr[left] + arr[right];

        // If s equal to k
        if (s == k)
        {

            // Update cntPairs
            cntPairs += 1;

            // Update left
            left += 1;

            // Update right
            right -= 1;
        }

        // If s > k
        else if (s > k)

            // Update right
            right -= 1;
        else

            // Update left
            left += 1;
    }

    // Return the cntPairs
    return cntPairs;
}  

// Driver Code   
public static void Main(String[] args)   
{   
    int[] arr = { 1, 2, 3, 4 };
    int K = 5;

    // Function call
    Console.WriteLine (maxcntPairsSumKRemoved(arr, K));  
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
//Javascript program to implement
// the above approach

// Function to find the maximum count of pairs
// required to be removed such that no pairs
// exist whose sum equal to K
function maxcntPairsSumKRemoved( arr, k)
{

    // Stores maximum count of pairs required
    // to be removed such that no pairs
    // exist whose sum equal to K
    var cntPairs = 0;

    // Base Case
    if (arr.length <= 1)
        return cntPairs;

    // Sort the array
    arr.sort();

    // Stores index of
    // left pointer
    var left = 0;

    // Stores index of
    // right pointer
    var right = arr.length - 1;

    while (left < right)
    {

        // Stores sum of left
        // and right pointer
        var s = arr[left] + arr[right];

        // If s equal to k
        if (s == k)
        {

            // Update cntPairs
            cntPairs += 1;

            // Update left
            left += 1;

            // Update right
            right -= 1;
        }

        // If s > k
        else if (s > k)

            // Update right
            right -= 1;
        else

            // Update left
            left += 1;
    }

    // Return the cntPairs
    return cntPairs;
}

var arr = [ 1,2,3,4];
var K = 5;

// Function call
document.write(maxcntPairsSumKRemoved(arr, K));

//This code is contributed by SoumikMondal
</script>
```

**Output:** 

```
2
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)
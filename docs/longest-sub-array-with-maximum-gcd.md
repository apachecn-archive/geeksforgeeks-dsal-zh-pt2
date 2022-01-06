# GCD 最大的最长子阵列

> 原文:[https://www . geeksforgeeks . org/最长子阵列带最大值-gcd/](https://www.geeksforgeeks.org/longest-sub-array-with-maximum-gcd/)

给定一个长度为 **N** 的数组 **arr[]** ，任务是找到具有最大可能 GCD 值的最长子数组的长度。

**示例:**

> **输入:** arr[] = {1，2，2}
> **输出:** 2
> 这里是所有可能的子阵列，那里是 GCD:
> 1){ 1 }->1
> 2){ 2 }->2
> 3){ 2 }->2
> 4){ 1，2} - > 1
> 5) {2，2} - > 2 【T11
> 由此可见，答案是{2，2}。
> 
> **输入:** arr[] = {3，3，3，3 }
> T3】输出: 4

**天真的方法:**生成所有可能的子阵列，并分别找到每个子阵列的 GCD，以便找到最长的这样的子阵列。这种方法需要 O(N <sup>3</sup> 时间来解决问题。

**更好的方法:**最大 GCD 值将始终等于数组中存在的最大数字。假设阵列中出现的最大数量是 **X** 。现在，任务是找到拥有所有 **X** 的最大子阵列。使用[双指针](https://www.geeksforgeeks.org/two-pointers-technique/)方法也可以做到这一点。下面是算法:

*   找出数组中最大的数字。让我们把这个号码叫做 **X** 。
*   从 **i = 0** 开始循环
    *   如果 **arr[i]！= X** 然后递增 **i** 并继续。
    *   否则初始化 **j = i** 。
    *   当 **j < n** 和**arr【j】= X**时，增加 **j** 。
    *   将答案更新为 **ans = max(ans，j–I)**。
    *   将 **i** 更新为 **i = j** 。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the length of
// the largest subarray with
// maximum possible GCD
int findLength(int* arr, int n)
{
    // To store the maximum number
    // present in the array
    int x = 0;

    // Finding the maximum element
    for (int i = 0; i < n; i++)
        x = max(x, arr[i]);

    // To store the final answer
    int ans = 0;

    // Two pointer
    for (int i = 0; i < n; i++) {

        if (arr[i] != x)
            continue;

        // Running a loop from j = i
        int j = i;

        // Condition for incrementing 'j'
        while (arr[j] == x)
            j++;

        // Updating the answer
        ans = max(ans, j - i);
    }

    return ans;
}

// Driver code
int main()
{
    int arr[] = { 1, 2, 2 };
    int n = sizeof(arr) / sizeof(int);

    cout << findLength(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

    // Function to return the length of
    // the largest subarray with
    // maximum possible GCD
    static int findLength(int []arr, int n)
    {
        // To store the maximum number
        // present in the array
        int x = 0;

        // Finding the maximum element
        for (int i = 0; i < n; i++)
            x = Math.max(x, arr[i]);

        // To store the final answer
        int ans = 0;

        // Two pointer
        for (int i = 0; i < n; i++)
        {
            if (arr[i] != x)
                continue;

            // Running a loop from j = i
            int j = i;

            // Condition for incrementing 'j'
            while (arr[j] == x)
            {
                j++;
                if (j >= n )
                break;
            }

            // Updating the answer
            ans = Math.max(ans, j - i);
        }
        return ans;
    }

    // Driver code
    public static void main (String[] args)
    {
        int arr[] = { 1, 2, 2 };
        int n = arr.length;

        System.out.println(findLength(arr, n));
    }
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the length of
# the largest subarray with
# maximum possible GCD
def findLength(arr, n) :

    # To store the maximum number
    # present in the array
    x = 0;

    # Finding the maximum element
    for i in range(n) :
        x = max(x, arr[i]);

    # To store the final answer
    ans = 0;

    # Two pointer
    for i in range(n) :

        if (arr[i] != x) :
            continue;

        # Running a loop from j = i
        j = i;

        # Condition for incrementing 'j'
        while (arr[j] == x) :
            j += 1;

            if j >= n :
                break

        # Updating the answer
        ans = max(ans, j - i);

    return ans;

# Driver code
if __name__ == "__main__" :

    arr = [ 1, 2, 2 ];
    n = len(arr);

    print(findLength(arr, n));

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Function to return the length of
    // the largest subarray with
    // maximum possible GCD
    static int findLength(int []arr, int n)
    {
        // To store the maximum number
        // present in the array
        int x = 0;

        // Finding the maximum element
        for (int i = 0; i < n; i++)
            x = Math.Max(x, arr[i]);

        // To store the final answer
        int ans = 0;

        // Two pointer
        for (int i = 0; i < n; i++)
        {
            if (arr[i] != x)
                continue;

            // Running a loop from j = i
            int j = i;

            // Condition for incrementing 'j'
            while (arr[j] == x)
            {
                j++;
                if (j >= n )
                break;
            }

            // Updating the answer
            ans = Math.Max(ans, j - i);
        }
        return ans;
    }

    // Driver code
    public static void Main ()
    {
        int []arr = { 1, 2, 2 };
        int n = arr.Length;

        Console.WriteLine(findLength(arr, n));
    }
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to return the length of
// the largest subarray with
// maximum possible GCD
function findLength(arr, n)
{
    // To store the maximum number
    // present in the array
    var x = 0;

    // Finding the maximum element
    for (var i = 0; i < n; i++)
        x = Math.max(x, arr[i]);

    // To store the final answer
    var ans = 0;

    // Two pointer
    for (var i = 0; i < n; i++) {

        if (arr[i] != x)
            continue;

        // Running a loop from j = i
        var j = i;

        // Condition for incrementing 'j'
        while (arr[j] == x)
            j++;

        // Updating the answer
        ans = Math.max(ans, j - i);
    }

    return ans;
}

// Driver code
var arr = [1, 2, 2 ];
var n = arr.length;

document.write( findLength(arr, n));

</script>
```

**Output:** 

```
2
```
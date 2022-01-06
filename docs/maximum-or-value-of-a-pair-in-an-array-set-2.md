# 数组中一对的最大或值|集合 2

> 原文:[https://www . geesforgeks . org/数组集对的最大值或最大值-2/](https://www.geeksforgeeks.org/maximum-or-value-of-a-pair-in-an-array-set-2/)

给定一个由 **N** 个正元素组成的数组 **arr[]** ，任务是从给定的数组中找到一对元素的最大[位“或”](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)值。
**示例:**

> **输入:** arr[] = {3，6，8，16}
> **输出:** 24
> **解释:**
> 给出最大 OR 值的对为(8，16)
> 8|16 = 24
> **输入:** arr[] = {8，7，3，12}
> **输出:** 15
> **解释:**T19
> 8|7 = 15

**天真方法:**参考[数组中一对的最大或值](https://www.geeksforgeeks.org/maximum-or-value-of-a-pair-in-an-array/)了解天真方法。
**高效方法:**在本文中，我们将讨论给定问题的优化解决方案。
按照以下步骤解决问题:

*   从数组中找出最大的元素。
*   逐个在最大元素和剩余的数组元素之间执行按位“或”。这是因为最大元素中设置位的排列将有助于从数组元素中获得最大可能的或值。
*   打印执行上述步骤获得的最大或值。

下面是上述方法的实现:

## C++

```
// C++ implementation of
// the approach above

#include <bits/stdc++.h>
using namespace std;

// Function to return the maximum
// bitwise OR for any pair of the
// given array in O(n) time complexity.
int maxOR(int arr[], int n)
{
    // Find the maximum
    // element in the array
    int max_value
        = *max_element(arr,
                       arr + n);

    // Stores the maximum
    // OR value
    int ans = 0;

    // Traverse the array and
    // perform Bitwise OR
    // between every array element
    // with the maximum element
    for (int i = 0; i < n; i++) {
        ans = max(ans, (max_value
                        | arr[i]));
    }
    return ans;
}

// Driver Code
int main()
{
    int arr[] = { 3, 6, 8, 16 };
    int n = sizeof(arr)
            / sizeof(arr[0]);

    cout << maxOR(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of
// the approach above
import java.util.Arrays;
class GFG{

// Function to return the maximum
// bitwise OR for any pair of the
// given array in O(n) time complexity.
static int maxOR(int []arr, int n)
{
    // Find the maximum
    // element in the array
    int max_value = Arrays.stream(arr).max().getAsInt();

    // Stores the maximum
    // OR value
    int ans = 0;

    // Traverse the array and
    // perform Bitwise OR
    // between every array element
    // with the maximum element
    for (int i = 0; i < n; i++)
    {
        ans = Math.max(ans, (max_value | arr[i]));
    }
    return ans;
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = new int[]{ 3, 6, 8, 16 };
    int n = 4;

    System.out.print(maxOR(arr, n));
}
}

// This code is contributed by Ritik Bansal
```

## 蟒蛇 3

```
# Python3 implementation of
# the approach above

# Function to return the maximum
# bitwise OR for any pair of the
# given array in O(n) time complexity.
def maxOR(arr, n):

    # Find the maximum
    # element in
    max_value = max(arr)

    # Stores the maximum
    # OR value the array
    ans = 0

    # Traverse the array and
    # perform Bitwise OR
    # between every array element
    # with the maximum element
    for i in range(n):
        ans = max(ans, (max_value | arr[i]))

    return ans

# Driver Code
if __name__ == "__main__":

    arr = [ 3, 6, 8, 16 ]
    n = len(arr)

    print(maxOR(arr, n))

# This code is contributed by jana_sayantan
```

## C#

```
// C# implementation of
// the approach above
using System;
using System.Linq;

class GFG{

// Function to return the maximum
// bitwise OR for any pair of the
// given array in O(n) time complexity.
static int maxOR(int []arr, int n)
{

    // Find the maximum
    // element in the array
    int max_value = arr.Max();

    // Stores the maximum
    // OR value
    int ans = 0;

    // Traverse the array and
    // perform Bitwise OR
    // between every array element
    // with the maximum element
    for(int i = 0; i < n; i++)
    {
        ans = Math.Max(ans, (max_value |
                             arr[i]));
    }
    return ans;
}

// Driver Code
public static void Main(String[] args)
{
    int []arr = { 3, 6, 8, 16 };
    int n = 4;

    Console.Write(maxOR(arr, n));
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// Javascript implementation of
// the above approach

// Function to return the maximum
// bitwise OR for any pair of the
// given array in O(n) time complexity.
function maxOR(arr, n)
{

    // Find the maximum
    // element in the array
    let max_value = Math.max(...arr);

    // Stores the maximum
    // OR value
    let ans = 0;

    // Traverse the array and
    // perform Bitwise OR
    // between every array element
    // with the maximum element
    for (let i = 0; i < n; i++)
    {
        ans = Math.max(ans, (max_value | arr[i]));
    }
    return ans;
}

    // Driver Code
    let arr = [ 3, 6, 8, 16 ];
    let n = 4;
       document.write(maxOR(arr, n));

// This code is contributed by souravghosh0416.
</script>
```

**Output:** 

```
24
```

***时间复杂度:** O(N)*
***辅助空间:** O(1)*
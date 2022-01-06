# 找到一个 K 长度子阵列，其位异或等于剩余阵列元素的位异或

> 原文:[https://www . geeksforgeeks . org/find-a-k-length-subarray-having-bitwise-xor-等于剩余数组元素数/](https://www.geeksforgeeks.org/find-a-k-length-subarray-having-bitwise-xor-equal-to-that-of-remaining-array-elements/)

给定一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** ，任务是检查数组中是否存在大小为 **K** 的子数组，其**按位异或**等于剩余数组元素的[按位异或](https://www.geeksforgeeks.org/tag/xor/)。如果发现为真，则打印**“是”**。否则，打印**“否”**。

**示例**:

> **输入:** arr[] = { 2，3，3，5，7，7，3，4 }，K = 5
> **输出:** YES
> **解释:**
> 子阵{ 3，3，5，7，7 }的按位异或等于 5
> 对{ 2，3，4 }的按位异或等于 5。
> 因此，要求的输出是 YES。
> 
> **输入:** arr[] = { 2，3，4，5，6，7，4 }，K = 2
> **输出:**否

**天真方法:**解决这个问题最简单的方法就是[生成所有子阵列](https://www.geeksforgeeks.org/generating-subarrays-using-recursion/)大小 **K** 。对于每个子阵列，检查子阵列的按位异或是否等于剩余元素的按位异或。如果发现为真，则打印**“是”**。否则，打印**“否”**。

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*

**有效方法:**上述方法可以使用[滑动窗口技术](https://www.geeksforgeeks.org/window-sliding-technique/)进行优化，观察结果如下:

> 如果 X ^ Y = Z，那么 x ^ z = y
> subarayxor = arr[I]^ arr[I+1]^…^ arr[j]
> total xor = arr[0]^ arr[1]^ arr[2]…..^ arr[n–1]
> 剩余数组元素的按位异或= totalXOR ^子数组 XOR

*   计算所有数组元素的[位异或，比如 **totalXOR** 。](https://www.geeksforgeeks.org/find-xor-of-all-elements-in-an-array/)
*   计算数组第一个 **K** 元素的**位异或**，比如**子矩阵异或**。
*   使用[滑动窗口技术](https://www.geeksforgeeks.org/window-sliding-technique/)，遍历大小为 **K** 的每个子阵列，检查子阵列的**逐位异或**是否等于剩余阵列元素的逐位异或。如果发现是真的，则打印**“是”**。
*   否则，打印**“否”**。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Utility function to check if subarray
// of size K exits whose XOR of elements
// equal to XOR ofremaning array elements
bool isSubarrayExistUtil(int arr[], int K, int N)
{

    int totalXOR = 0;
    int SubarrayXOR = 0;

    // Find XOR of whole array
    for (int i = 0; i < N; i++)
        totalXOR ^= arr[i];

    // Find XOR of first K elements
    for (int i = 0; i < K; i++)
        SubarrayXOR ^= arr[i];
    if (SubarrayXOR == (totalXOR ^ SubarrayXOR))
        return true;

    for (int i = K; i < N; i++) {

        // Adding XOR of next element
        SubarrayXOR ^= arr[i];

        // Removing XOR of previous element
        SubarrayXOR ^= arr[i - 1];

        // Check if XOR of current subarray matches
        // with the XOR of remaining elements or not
        if (SubarrayXOR == (totalXOR ^ SubarrayXOR))
            return true;
    }
    return false;
}

// Function to check if subarray of size
// K exits whose XOR of elements equal
// to XOR ofremaning array elements
void isSubarrayExist(int arr[], int K, int N)
{
    if (isSubarrayExistUtil(arr, K, N))
        cout << "YES\n";
    else
        cout << "NO\n";
}

// Driver Code
int32_t main()
{
    // Given array
    int arr[] = { 2, 3, 3, 5, 7, 7, 3, 4 };

    // Size of the array
    int N = sizeof(arr) / sizeof(arr[0]);

    // Given K
    int K = 5;

    // Function Call
    isSubarrayExist(arr, K, N);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;

class GFG{

// Utility function to check if subarray
// of size K exits whose XOR of elements
// equal to XOR ofremaning array elements
static boolean isSubarrayExistUtil(int arr[],
                                   int K, int N)
{
    int totalXOR = 0;
    int SubarrayXOR = 0;

    // Find XOR of whole array
    for(int i = 0; i < N; i++)
        totalXOR ^= arr[i];

    // Find XOR of first K elements
    for(int i = 0; i < K; i++)
        SubarrayXOR ^= arr[i];
    if (SubarrayXOR == (totalXOR ^ SubarrayXOR))
        return true;

    for(int i = K; i < N; i++)
    {

        // Adding XOR of next element
        SubarrayXOR ^= arr[i];

        // Removing XOR of previous element
        SubarrayXOR ^= arr[i - 1];

        // Check if XOR of current subarray matches
        // with the XOR of remaining elements or not
        if (SubarrayXOR == (totalXOR ^ SubarrayXOR))
            return true;
    }
    return false;
}

// Function to check if subarray of size
// K exits whose XOR of elements equal
// to XOR ofremaning array elements
static void isSubarrayExist(int arr[],
                            int K, int N)
{
    if (isSubarrayExistUtil(arr, K, N))
        System.out.print("YES\n");
    else
        System.out.print("NO\n");
}

// Driver Code
public static void main(String[] args)
{

    // Given array
    int arr[] = { 2, 3, 3, 5, 7, 7, 3, 4 };

    // Size of the array
    int N = arr.length;

    // Given K
    int K = 5;

    // Function Call
    isSubarrayExist(arr, K, N);
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Utility function to check if subarray
# of size K exits whose XOR of elements
# equal to XOR ofremaning array elements
def isSubarrayExistUtil(arr, K, N):
    totalXOR = 0
    SubarrayXOR = 0

    # Find XOR of whole array
    for i in range(N):
        totalXOR ^= arr[i]

    # Find XOR of first K elements
    for i in range(K):
        SubarrayXOR ^= arr[i]
    if (SubarrayXOR == (totalXOR ^ SubarrayXOR)):
        return True

    for i in range(K, N):

        # Adding XOR of next element
        SubarrayXOR ^= arr[i]

        # Removing XOR of previous element
        SubarrayXOR ^= arr[i - 1]

        # Check if XOR of current subarray matches
        # with the XOR of remaining elements or not
        if (SubarrayXOR == (totalXOR ^ SubarrayXOR)):
            return True
    return False

# Function to check if subarray of size
# K exits whose XOR of elements equal
# to XOR ofremaning array elements
def isSubarrayExist(arr, K, N):
    if (isSubarrayExistUtil(arr, K, N)):
        print("YES")
    else:
        print("NO")

# Driver Code
if __name__ == '__main__':

    # Given array
    arr = [2, 3, 3, 5, 7, 7, 3, 4]

    # Size of the array
    N = len(arr)

    # Given K
    K = 5

    # Function Call
    isSubarrayExist(arr, K, N)

    # This code is contributed by mohit kumar 29
```

## C#

```
// C# program to implement
// the above approach
using System;
class GFG
{

// Utility function to check if subarray
// of size K exits whose XOR of elements
// equal to XOR ofremaning array elements
static bool isSubarrayExistUtil(int []arr,
                                   int K, int N)
{
    int totalXOR = 0;
    int SubarrayXOR = 0;

    // Find XOR of whole array
    for(int i = 0; i < N; i++)
        totalXOR ^= arr[i];

    // Find XOR of first K elements
    for(int i = 0; i < K; i++)
        SubarrayXOR ^= arr[i];
    if (SubarrayXOR == (totalXOR ^ SubarrayXOR))
        return true;
    for(int i = K; i < N; i++)
    {

        // Adding XOR of next element
        SubarrayXOR ^= arr[i];

        // Removing XOR of previous element
        SubarrayXOR ^= arr[i - 1];

        // Check if XOR of current subarray matches
        // with the XOR of remaining elements or not
        if (SubarrayXOR == (totalXOR ^ SubarrayXOR))
            return true;
    }
    return false;
}

// Function to check if subarray of size
// K exits whose XOR of elements equal
// to XOR ofremaning array elements
static void isSubarrayExist(int []arr,
                            int K, int N)
{
    if (isSubarrayExistUtil(arr, K, N))
        Console.Write("YES\n");
    else
        Console.Write("NO\n");
}

// Driver Code
public static void Main(String[] args)
{

    // Given array
    int []arr = { 2, 3, 3, 5, 7, 7, 3, 4 };

    // Size of the array
    int N = arr.Length;

    // Given K
    int K = 5;

    // Function Call
    isSubarrayExist(arr, K, N);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// javascript program to implement
// the above approach

    // Utility function to check if subarray
    // of size K exits whose XOR of elements
    // equal to XOR ofremaning array elements
    function isSubarrayExistUtil(arr , K , N)
    {
        var totalXOR = 0;
        var SubarrayXOR = 0;

        // Find XOR of whole array
        for (i = 0; i < N; i++)
            totalXOR ^= arr[i];

        // Find XOR of first K elements
        for (i = 0; i < K; i++)
            SubarrayXOR ^= arr[i];
        if (SubarrayXOR == (totalXOR ^ SubarrayXOR))
            return true;

        for (i = K; i < N; i++) {

            // Adding XOR of next element
            SubarrayXOR ^= arr[i];

            // Removing XOR of previous element
            SubarrayXOR ^= arr[i - 1];

            // Check if XOR of current
            // subarray matches
            // with the XOR of remaining
            // elements or not
            if (SubarrayXOR ==
            (totalXOR ^ SubarrayXOR))
                return true;
        }
        return false;
    }

    // Function to check if subarray of size
    // K exits whose XOR of elements equal
    // to XOR ofremaning array elements
    function isSubarrayExist(arr , K , N) {
        if (isSubarrayExistUtil(arr, K, N))
            document.write("YES\n");
        else
            document.write("NO\n");
    }

    // Driver Code

        // Given array
        var arr = [ 2, 3, 3, 5, 7, 7, 3, 4 ];

        // Size of the array
        var N = arr.length;

        // Given K
        var K = 5;

        // Function Call
        isSubarrayExist(arr, K, N);

// This code contributed by Rajput-Ji

</script>
```

**Output:** 

```
YES
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)
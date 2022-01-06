# 计数具有奇数位异或的子阵列

> 原文:[https://www . geesforgeks . org/count-subarrays-having-odd-bitwise-xor/](https://www.geeksforgeeks.org/count-subarrays-having-odd-bitwise-xor/)

给定一个大小为 **N** 的[阵列](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** ，任务是计算给定阵列中具有奇数[位异或](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)值的[子阵列](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)的数量。

**示例:**

> **输入:** arr[] = {1，4，7，9，10}
> **输出:** 8
> **解释:**具有奇数位异或的子阵列为{1}、{1，4}、{1，4，7，9}、{1，4，7，9，10}、{7}、{9}、{4，7}、{9，10}。
> 
> **输入:** arr[] ={1，5，6}
> **输出:** 3
> **解释:**具有奇数位异或的子阵列为{1}、{1，5}、{1，5，6}。

**天真方法:**解决这个问题最简单的方法是[检查每个子阵列](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)的**按位异或**是否为奇数。如果发现是奇数，则增加计数。最后，打印计数作为结果。

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*

**高效方法:**为了优化上述方法，该思想基于以下观察:只有当子阵列中奇数元素的数量为奇数时，该子阵列的**按位异或**才为奇数。解决问题，从指标 **0** 开始，满足给定条件，求子阵个数。然后，遍历数组并更新从索引 I 开始的满足给定条件的子数组的数量。按照以下步骤解决问题:

*   将变量 **Odd** 、 **C_odd** 初始化为 **0** ，以分别存储第 i <sup>个</sup>索引之前的奇数数量和从第 i <sup>个</sup>索引开始的所需子阵列数量。
*   使用变量 **i** 遍历数组 **arr[]** ，并检查以下步骤:
    *   [如果**arr【I】**的值为奇数](https://www.geeksforgeeks.org/check-whether-given-number-even-odd/)，则将**奇数**的值更新为**！古怪**。
    *   如果**奇数**的值为**非零**，则将**C _ 奇数**增加 **1** 。
*   再次，使用变量 **i** 遍历数组 **arr[]** ，并执行以下操作:
    *   将 **C_odd** 的值添加到变量 **res** 中。
    *   [如果**arr【I】**的值为奇数](https://www.geeksforgeeks.org/check-whether-given-number-even-odd/)，则将 **C_odd** 的值更新为**(N–I–C _ odd)**。
*   完成上述步骤后，打印 **res** 的值作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to count the number of subarrays
// of the given array having odd Bitwise XOR
void oddXorSubarray(int a[], int n)
{
    // Stores number of odd
    // numbers upto i-th index
    int odd = 0;

    // Stores number of required
    // subarrays starting from i-th index
    int c_odd = 0;

    // Store the required result
    int result = 0;

    // Find the number of subarrays having odd
    // Bitwise XOR values starting at 0-th index
    for (int i = 0; i < n; i++) {

        // Check if current element is odd
        if (a[i] & 1) {
            odd = !odd;
        }

        // If the current value of odd is not
        // zero, increment c_odd by 1
        if (odd) {
            c_odd++;
        }
    }

    // Find the number of subarrays having odd
    // bitwise XOR value starting at ith index
    // and add to result
    for (int i = 0; i < n; i++) {

        // Add c_odd to result
        result += c_odd;
        if (a[i] & 1) {
            c_odd = (n - i - c_odd);
        }
    }

    // Print the result
    cout << result;
}

// Driver Code
int main()
{
    // Given array
    int arr[] = { 1, 4, 7, 9, 10 };

    // Stores the size of the array
    int N = sizeof(arr) / sizeof(arr[0]);

    oddXorSubarray(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
class GFG
{

// Function to count the number of subarrays
// of the given array having odd Bitwise XOR
static void oddXorSubarray(int a[], int n)
{

    // Stores number of odd
    // numbers upto i-th index
    int odd = 0;

    // Stores number of required
    // subarrays starting from i-th index
    int c_odd = 0;

    // Store the required result
    int result = 0;

    // Find the number of subarrays having odd
    // Bitwise XOR values starting at 0-th index
    for (int i = 0; i < n; i++)
    {

        // Check if current element is odd
        if (a[i] % 2 != 0)
        {
            odd = (odd == 0) ? 1 : 0;
        }

        // If the current value of odd is not
        // zero, increment c_odd by 1
        if (odd != 0)
        {
            c_odd++;
        }
    }

    // Find the number of subarrays having odd
    // bitwise XOR value starting at ith index
    // and add to result
    for (int i = 0; i < n; i++)
    {

        // Add c_odd to result
        result += c_odd;
        if (a[i] % 2 != 0)
        {
            c_odd = (n - i - c_odd);
        }
    }

    // Print the result
    System.out.println(result);
}

// Driver Code
public static void main (String[] args)
{

      // Given array
    int arr[] = { 1, 4, 7, 9, 10 };

    // Stores the size of the array
    int N = arr.length;
    oddXorSubarray(arr, N);
}
}

// This code is contributed by Dharanendra L V.
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to count the number of subarrays
# of the given array having odd Bitwise XOR
def oddXorSubarray(a, n):

    # Stores number of odd
    # numbers upto i-th index
    odd = 0

    # Stores number of required
    # subarrays starting from i-th index
    c_odd = 0

    # Store the required result
    result = 0

    # Find the number of subarrays having odd
    # Bitwise XOR values starting at 0-th index
    for i in range(n):

        # Check if current element is odd
        if (a[i] & 1):
            odd = not odd

        # If the current value of odd is not
        # zero, increment c_odd by 1
        if (odd):
            c_odd += 1

    # Find the number of subarrays having odd
    # bitwise XOR value starting at ith index
    # and add to result
    for i in range(n):

        # Add c_odd to result
        result += c_odd
        if (a[i] & 1):
            c_odd = (n - i - c_odd)

    # Print the result
    print (result)

# Driver Code
if __name__ == '__main__':

    # Given array
    arr = [1, 4, 7, 9, 10]

    # Stores the size of the array
    N = len(arr)
    oddXorSubarray(arr, N)

    # This code is contributed by mohit kumar 29.
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to count the number of subarrays
// of the given array having odd Bitwise XOR
static void oddXorSubarray(int []a, int n)
{

    // Stores number of odd
    // numbers upto i-th index
    int odd = 0;

    // Stores number of required
    // subarrays starting from i-th index
    int c_odd = 0;

    // Store the required result
    int result = 0;

    // Find the number of subarrays having
    // odd Bitwise XOR values starting at
    // 0-th index
    for(int i = 0; i < n; i++)
    {

        // Check if current element is odd
        if (a[i] % 2 != 0)
        {
            odd = (odd == 0) ? 1 : 0;
        }

        // If the current value of odd is not
        // zero, increment c_odd by 1
        if (odd != 0)
        {
            c_odd++;
        }
    }

    // Find the number of subarrays having odd
    // bitwise XOR value starting at ith index
    // and add to result
    for(int i = 0; i < n; i++)
    {

        // Add c_odd to result
        result += c_odd;

        if (a[i] % 2 != 0)
        {
            c_odd = (n - i - c_odd);
        }
    }

    // Print the result
    Console.WriteLine(result);
}

// Driver Code
public static void Main(String[] args)
{

    // Given array
    int []arr = { 1, 4, 7, 9, 10 };

    // Stores the size of the array
    int N = arr.Length;
    oddXorSubarray(arr, N);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// javascript program for the above approach

    // Function to count the number of subarrays
    // of the given array having odd Bitwise XOR
    function oddXorSubarray(a , n) {

        // Stores number of odd
        // numbers upto i-th index
        var odd = 0;

        // Stores number of required
        // subarrays starting from i-th index
        var c_odd = 0;

        // Store the required result
        var result = 0;

        // Find the number of subarrays having odd
        // Bitwise XOR values starting at 0-th index
        for (i = 0; i < n; i++) {

            // Check if current element is odd
            if (a[i] % 2 != 0) {
                odd = (odd == 0) ? 1 : 0;
            }

            // If the current value of odd is not
            // zero, increment c_odd by 1
            if (odd != 0) {
                c_odd++;
            }
        }

        // Find the number of subarrays having odd
        // bitwise XOR value starting at ith index
        // and add to result
        for (i = 0; i < n; i++) {

            // Add c_odd to result
            result += c_odd;
            if (a[i] % 2 != 0) {
                c_odd = (n - i - c_odd);
            }
        }

        // Print the result
        document.write(result);
    }

    // Driver Code

        // Given array
        var arr = [ 1, 4, 7, 9, 10 ];

        // Stores the size of the array
        var N = arr.length;
        oddXorSubarray(arr, N);

// This code contributed by Rajput-Ji

</script>
```

**Output:** 

```
8
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)
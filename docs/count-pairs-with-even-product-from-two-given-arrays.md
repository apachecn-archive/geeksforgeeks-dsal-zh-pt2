# 从两个给定的数组中用偶数计数对

> 原文:[https://www . geeksforgeeks . org/从两个给定的数组中计数成对的偶数乘积/](https://www.geeksforgeeks.org/count-pairs-with-even-product-from-two-given-arrays/)

给定两个大小分别为 **N** 和 **M** 的[阵列](https://www.geeksforgeeks.org/array-data-structure/)、**arr【】**和**brr【】**，任务是找到对的计数 **(arr[i]，brr[j])** ，使得对的元素乘积为[偶数](https://www.geeksforgeeks.org/check-whether-given-number-even-odd/)。

**示例:**

> **输入:** arr[] = { 1，2，3 }，brr[] = { 1，2 }
> **输出:** 4
> **解释:**
> 偶积对为:{ (arr[0]，brr[1])，(arr[1]，brr[0])，(arr[1]，brr[1])，(arr[2]，brr[1])。
> 因此，要求输出为 4。
> 
> **输入:** arr[] = { 3，2，1，4，4}，brr[] = { 1，4，2，3，1 }
> **输出:** 19

**天真方法:**解决这个问题最简单的方法是[遍历两个数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)和[从两个数组生成所有可能的对](https://www.geeksforgeeks.org/find-all-pairs-possible-from-the-given-array/) **(arr[i]，brr[j])** 。对于每一对， **(arr[i]、brr[j])** 、[检查其产品是否为偶数](https://www.geeksforgeeks.org/check-whether-given-number-even-odd/)。如果发现为真，则增加计数。最后，打印获得的计数。

***时间复杂度:** O(N * M)*
***辅助空间:** O(1)*

**有效方法:**上述方法可以基于两个数乘积的以下性质进行优化:

> 奇数*奇数=奇数
> 偶数*奇数=偶数
> 偶数*偶数=偶数

按照以下步骤解决问题:

*   初始化两个变量，比如 **cntOddArr** 和**cntodbrr**，分别存储数组**arr【】**和**brr【】**中奇数的计数。
*   [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **arr[]** ，对于每个数组元素，[检查是否为奇数](https://www.geeksforgeeks.org/check-whether-given-number-even-odd/)。如果发现为真，则更新 **cntOddArr += 1** 。
*   [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **brr[]** ，对于每个数组元素、索引，[检查 is 是否为奇数](https://www.geeksforgeeks.org/check-whether-given-number-even-odd/)。如果发现为真，则更新**cntoddbr+= 1**。
*   最后，打印**((N * M)–cntOddArr * cntodbrr)**的值。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to count pairs (arr[i], brr[j])
// whose product is an even number
int cntPairsInTwoArray(int arr[], int brr[],
                       int N, int M)
{
    // Stores count of odd
    // numbers in arr[]
    int cntOddArr = 0;

    // Stores count of odd
    // numbers in brr[]
    int cntOddBrr = 0;

    // Traverse the array, arr[]
    for (int i = 0; i < N; i++) {

        // If arr[i] is
        // an odd number
        if (arr[i] & 1) {

            // Update cntOddArr
            cntOddArr += 1;
        }
    }

    // Traverse the array, brr[]
    for (int i = 0; i < M; i++) {

        // If brr[i] is
        // an odd number
        if (brr[i] & 1) {

            // Update cntOddArr
            cntOddBrr += 1;
        }
    }

    // Return pairs whose product
    // is an even number
    return (N * M) - (cntOddArr * cntOddBrr);
}

// Driver Code
int main()
{
    int arr[] = { 1, 2, 3 };
    int N = sizeof(arr) / sizeof(arr[0]);

    int brr[] = { 1, 2 };
    int M = sizeof(brr) / sizeof(brr[0]);

    cout << cntPairsInTwoArray(arr, brr, N, M);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;

class GFG{

// Function to count pairs (arr[i], brr[j])
// whose product is an even number
static int cntPairsInTwoArray(int arr[], int brr[],
                       int N, int M)
{

    // Stores count of odd
    // numbers in arr[]
    int cntOddArr = 0;

    // Stores count of odd
    // numbers in brr[]
    int cntOddBrr = 0;

    // Traverse the array, arr[]
    for (int i = 0; i < N; i++) {

        // If arr[i] is
        // an odd number
        if (arr[i] % 2 == 1) {

            // Update cntOddArr
            cntOddArr += 1;
        }
    }

    // Traverse the array, brr[]
    for (int i = 0; i < M; i++) {

        // If brr[i] is
        // an odd number
        if (brr[i] % 2 == 1) {

            // Update cntOddArr
            cntOddBrr += 1;
        }
    }

    // Return pairs whose product
    // is an even number
    return (N * M) - (cntOddArr * cntOddBrr);
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 1, 2, 3 };
    int N = arr.length;

    int brr[] = { 1, 2 };
    int M = brr.length;

    System.out.print(cntPairsInTwoArray(arr, brr, N, M));

}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to count pairs (arr[i], brr[j])
# whose product is an even number
def cntPairsInTwoArray(arr, brr, N, M):

    # Stores count of odd
    # numbers in arr[]
    cntOddArr = 0

    # Stores count of odd
    # numbers in brr[]
    cntOddBrr = 0

    # Traverse the array, arr[]
    for i in range(N):

        # If arr[i] is
        # an odd number
        if (arr[i] & 1):

            # Update cntOddArr
            cntOddArr += 1

    # Traverse the array, brr[]
    for i in range(M):

        # If brr[i] is
        # an odd number
        if (brr[i] & 1):

            # Update cntOddArr
            cntOddBrr += 1

    # Return pairs whose product
    # is an even number
    return (N * M) - (cntOddArr * cntOddBrr)

# Driver Code
if __name__ == '__main__':

    arr = [ 1, 2, 3 ]
    N = len(arr)

    brr = [ 1, 2 ]
    M = len(brr)

    print(cntPairsInTwoArray(arr, brr, N, M))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program to implement
// the above approach 
using System;

class GFG{

// Function to count pairs (arr[i], brr[j])
// whose product is an even number
static int cntPairsInTwoArray(int[] arr, int[] brr,
                              int N, int M)
{

    // Stores count of odd
    // numbers in arr[]
    int cntOddArr = 0;

    // Stores count of odd
    // numbers in brr[]
    int cntOddBrr = 0;

    // Traverse the array, arr[]
    for(int i = 0; i < N; i++)
    {

        // If arr[i] is
        // an odd number
        if (arr[i] % 2 == 1)
        {

            // Update cntOddArr
            cntOddArr += 1;
        }
    }

    // Traverse the array, brr[]
    for(int i = 0; i < M; i++)
    {

        // If brr[i] is
        // an odd number
        if (brr[i] % 2 == 1)
        {

            // Update cntOddArr
            cntOddBrr += 1;
        }
    }

    // Return pairs whose product
    // is an even number
    return (N * M) - (cntOddArr * cntOddBrr);
}

// Driver Code
public static void Main()
{
    int[] arr = { 1, 2, 3 };
    int N = arr.Length;

    int[] brr = { 1, 2 };
    int M = brr.Length;

    Console.Write(cntPairsInTwoArray(
        arr, brr, N, M));
}
}

// This code is contributed by code_hunt
```

## java 描述语言

```
<script>

// JavaScript program for above approach

// Function to count pairs (arr[i], brr[j])
// whose product is an even number
function cntPairsletwoArray(arr, brr,
                       N, M)
{

    // Stores count of odd
    // numbers in arr[]
    let cntOddArr = 0;

    // Stores count of odd
    // numbers in brr[]
    let cntOddBrr = 0;

    // Traverse the array, arr[]
    for (let i = 0; i < N; i++) {

        // If arr[i] is
        // an odd number
        if (arr[i] % 2 == 1) {

            // Update cntOddArr
            cntOddArr += 1;
        }
    }

    // Traverse the array, brr[]
    for (let i = 0; i < M; i++) {

        // If brr[i] is
        // an odd number
        if (brr[i] % 2 == 1) {

            // Update cntOddArr
            cntOddBrr += 1;
        }
    }

    // Return pairs whose product
    // is an even number
    return (N * M) - (cntOddArr * cntOddBrr);
}

// Driver Code

     let arr = [ 1, 2, 3 ];
    let N = arr.length;

    let brr = [ 1, 2 ];
    let M = brr.length;

    document.write(cntPairsletwoArray(arr, brr, N, M));

</script>
```

**Output:** 

```
4
```

***时间复杂度:** O(N)*
***空间复杂度:** O(1)*
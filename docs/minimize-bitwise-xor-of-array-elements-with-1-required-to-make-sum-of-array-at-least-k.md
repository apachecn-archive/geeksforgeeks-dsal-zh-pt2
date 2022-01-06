# 最小化数组元素与 1 的按位异或运算，使数组之和至少为 K

> 原文:[https://www . geesforgeks . org/最小化-按位异或-数组元素与-1-至少需要-k 个数组的和/](https://www.geeksforgeeks.org/minimize-bitwise-xor-of-array-elements-with-1-required-to-make-sum-of-array-at-least-k/)

给定一个由 **N** 个正整数和一个正整数 **K** 组成的[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** ，任务是计算数组元素与 **1** 的最小[位异或](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)，要求数组的[和至少为 K 。](https://www.geeksforgeeks.org/program-find-sum-elements-given-array/)

**示例:**

> **输入:** arr[] = {0，1，1，0，1}，K = 4
> **输出:** 1
> **解释:**对 arr[0]和 1 执行按位异或将 arr[]修改为{1，1，1，0，1}。现在，数组的和= 1 + 1 + 1 + 0 + 1 = 4(= K)。
> 
> **输入:** arr[] = {14，0，1，0}，K = 20
> T3】输出: -1

**方法:**利用 **1** 与偶数元素的[逐位异或](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)将元素增加 **1** 可以解决给定的问题。
按照以下步骤解决问题:

*   [求给定数组](https://www.geeksforgeeks.org/program-find-sum-elements-given-array/) **arr[]** 的和，并将其存储在一个变量中，比如 **S** 。
*   [计算数组中偶数元素的个数](https://www.geeksforgeeks.org/count-number-even-odd-elements-array/)并将其存储在一个变量中，比如 **E** 。
*   如果 **S** 大于等于 **K** ，则打印 **0** 。
*   否则，如果 **S + E** 的值小于 **K** ，则打印 **-1** 。
*   否则，将**(K–S)**的值打印为需要的数组元素与 **1** 的[按位异或](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)的最小个数。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find minimum number
// of Bitwise XOR of array elements
// with 1 required to make sum of
// the array at least K
int minStepK(int arr[], int N, int K)
{
    // Stores the count of
    // even array elements
    int E = 0;

    // Stores sum of the array
    int S = 0;

    // Traverse the array arr[]
    for (int i = 0; i < N; i++) {

        // Increment sum
        S += arr[i];

        // If array element is even
        if (arr[i] % 2 == 0)

            // Increase count of even
            E += 1;
    }

    // If S is at least K
    if (S >= K)
        return 0;

    // If S + E is less than K
    else if (S + E < K)
        return -1;

    // Otherwise, moves = K - S
    else
        return K - S;
}

// Driver Code
int main()
{
    int arr[] = { 0, 1, 1, 0, 1 };
    int N = sizeof(arr) / sizeof(arr[0]);
    int K = 4;
    cout << minStepK(arr, N, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to find minimum number
// of Bitwise XOR of array elements
// with 1 required to make sum of
// the array at least K
static int minStepK(int arr[], int N, int K)
{

    // Stores the count of
    // even array elements
    int E = 0;

    // Stores sum of the array
    int S = 0;

    // Traverse the array arr[]
    for(int i = 0; i < N; i++)
    {

        // Increment sum
        S += arr[i];

        // If array element is even
        if (arr[i] % 2 == 0)

            // Increase count of even
            E += 1;
    }

    // If S is at least K
    if (S >= K)
        return 0;

    // If S + E is less than K
    else if (S + E < K)
        return -1;

    // Otherwise, moves = K - S
    else
        return K - S;
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 0, 1, 1, 0, 1 };
    int N = arr.length;
    int K = 4;

    System.out.println(minStepK(arr, N, K));
}
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python 3 program for the above approach

# Function to find minimum number
# of Bitwise XOR of array elements
# with 1 required to make sum of
# the array at least K
def minStepK(arr, N, K):

    # Stores the count of
    # even array elements
    E = 0

    # Stores sum of the array
    S = 0

    # Traverse the array arr[]
    for i in range(N):

        # Increment sum
        S += arr[i]

        # If array element is even
        if (arr[i] % 2 == 0):

            # Increase count of even
            E += 1

    # If S is at least K
    if (S >= K):
        return 0

    # If S + E is less than K
    elif (S + E < K):
        return -1

    # Otherwise, moves = K - S
    else:
        return K - S

# Driver Code
if __name__ == "__main__":

    arr = [0, 1, 1, 0, 1]
    N = len(arr)
    K = 4
    print(minStepK(arr, N, K))

    # This code is contributed by ukasp.
```

## C#

```
// C# program for the above approach
using System;
class GFG
{

// Function to find minimum number
// of Bitwise XOR of array elements
// with 1 required to make sum of
// the array at least K
static int minStepK(int[] arr, int N, int K)
{

    // Stores the count of
    // even array elements
    int E = 0;

    // Stores sum of the array
    int S = 0;

    // Traverse the array arr[]
    for(int i = 0; i < N; i++)
    {

        // Increment sum
        S += arr[i];

        // If array element is even
        if (arr[i] % 2 == 0)

            // Increase count of even
            E += 1;
    }

    // If S is at least K
    if (S >= K)
        return 0;

    // If S + E is less than K
    else if (S + E < K)
        return -1;

    // Otherwise, moves = K - S
    else
        return K - S;
}

    // Driver Code
    public static void Main()
    {
    int[] arr= { 0, 1, 1, 0, 1 };
    int N = arr.Length;
    int K = 4;

    Console.WriteLine(minStepK(arr, N, K));

    }
}

// This code is contributed by sanjoy_62.
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to find minimum number
// of Bitwise XOR of array elements
// with 1 required to make sum of
// the array at least K
function minStepK(arr, N, K)
{

    // Stores the count of
    // even array elements
    var E = 0;

    // Stores sum of the array
    var S = 0;

    // Traverse the array arr[]
    for(var i = 0; i < N; i++)
    {

        // Increment sum
        S += arr[i];

        // If array element is even
        if (arr[i] % 2 === 0)

            // Increase count of even
            E += 1;
    }

    // If S is at least K
    if (S >= K)
        return 0;

    // If S + E is less than K
    else if (S + E < K)
        return -1;

    // Otherwise, moves = K - S
    else
        return K - S;
}

// Driver Code
var arr = [ 0, 1, 1, 0, 1 ];
var N = arr.length;
var K = 4;

document.write(minStepK(arr, N, K));

// This code is contributed by rdtank

</script>
```

**Output:** 

```
1
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)
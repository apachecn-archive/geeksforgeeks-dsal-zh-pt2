# 计算在 M 个连续索引处生成具有不同元素的数组的方式

> 原文:[https://www . geesforgeks . org/count-way-to-generate-a-array-with-distinct-elements-at-m-continuous-index/](https://www.geeksforgeeks.org/count-ways-to-generate-an-array-having-distinct-elements-at-m-consecutive-indices/)

给定一个由范围**【0，M】**中的 **N** 个整数和一个整数 **M** 组成的[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】】**，任务是计算用范围**【0，M】**中的非零值替换所有值为 **0** 的数组元素的方法数，以便所有可能的 **M** 个连续元素都是不同的。

**示例:**

> **输入:** arr[] = { 1，0，3，0，0 }，M = 4
> **输出:** 2
> **解释:**
> 用非零值替换 arr[1]，arr[3]和 arr[4]的可能方法，使得没有 M( = 4)个连续元素包含任何重复元素是{ { 1，2，3，4，1 }，{ 1，4，3，2，1 } }。
> 因此，要求的输出为 2。
> 
> **输入:** arr[] = {0，1，2，1，0}，M = 4
> **输出:** 0
> **解释:**不可能有这样的安排。

**方法:**想法是用非零元素替换 **0** s，这样**arr【I】**必须等于**arr【I % M】**。按照以下步骤解决问题:

*   初始化一个大小为 **M + 1** 的数组**B[**，以存储 **M** 个连续的数组元素，使得**arr【I】**等于**B【I % M】**。
*   [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)并检查以下条件:
    *   如果 **arr[i]** 不是 **0** 而**B【I % M】**是 **0** ，那么**B【I % M】**将等于 **arr[i]** ，因为这个数字应该是存在的。
    *   如果**arr【I】**不等于**B【I % M】**，则打印 **0** ，因为不存在这样的安排。
*   计算阵中 **0** s 的个数 **B[]** ，说 **X** 。
*   那么，存在[阶乘](https://www.geeksforgeeks.org/program-for-factorial-of-a-number/) **X** 的可能排列，因此，打印[阶乘](https://www.geeksforgeeks.org/program-for-factorial-of-a-number/) **X** 的值。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Modular function
// to calculate factorial
long long int Fact(int N)
{
    // Stores factorial of N
    long long int result = 1;

    // Iterate over the range [1, N]
    for (int i = 1; i <= N; i++) {

        // Update result
        result = (result * i);
    }

    return result;
}

// Function to count ways to replace array
// elements having 0s with non-zero elements
// such that any M consecutive elements are distinct
void numberOfWays(int M, int arr[], int N)
{

    // Store m consecutive distinct elements
    // such that arr[i] is equal to B[i % M]
    int B[M] = { 0 };

    // Stores frequency of array elements
    int counter[M + 1] = { 0 };

    // Traverse the array arr[]
    for (int i = 0; i < N; i++) {

        // If arr[i] is non-zero
        if (arr[i] != 0) {

            // If B[i % M] is equal to 0
            if (B[i % M] == 0) {

                // Update B[i % M]
                B[i % M] = arr[i];

                // Update frequency of arr[i]
                counter[arr[i]]++;

                // If a duplicate element found
                // in M consecutive elements
                if (counter[arr[i]] > 1) {
                    cout << 0 << endl;
                    return;
                }
            }

            // Handling the case of
            // inequality
            else if (B[i % M] != arr[i]) {

                cout << 0 << endl;
                return;
            }
        }
    }

    // Stores count of 0s
    // in B[]
    int cnt = 0;

    // Traverse the array, B[]
    for (int i = 0; i < M; i++) {

        // If B[i] is 0
        if (B[i] == 0) {

            // Update cnt
            cnt++;
        }
    }

    // Calculate factorial
    cout << Fact(cnt) << endl;
}

// Driver Code
int main()
{

    // Given M
    int M = 4;

    // Given array
    int arr[] = { 1, 0, 3, 0, 0 };

    // Size of the array
    int N = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    numberOfWays(M, arr, N);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;

class GFG{

// Modular function
// to calculate factorial
static int Fact(int N)
{

    // Stores factorial of N
    int result = 1;

    // Iterate over the range [1, N]
    for(int i = 1; i <= N; i++)
    {

        // Update result
        result = (result * i);
    }
    return result;
}

// Function to count ways to replace array
// elements having 0s with non-zero elements
// such that any M consecutive elements are distinct
static void numberOfWays(int M, int[] arr, int N)
{

    // Store m consecutive distinct elements
    // such that arr[i] is equal to B[i % M]
    int[] B = new int[M];

    // Stores frequency of array elements
    int[] counter = new int[M + 1];

    // Traverse the array arr[]
    for(int i = 0; i < N; i++)
    {

        // If arr[i] is non-zero
        if (arr[i] != 0)
        {

            // If B[i % M] is equal to 0
            if (B[i % M] == 0)
            {

                // Update B[i % M]
                B[i % M] = arr[i];

                // Update frequency of arr[i]
                counter[arr[i]]++;

                // If a duplicate element found
                // in M consecutive elements
                if (counter[arr[i]] > 1)
                {
                    System.out.println(0);
                    return;
                }
            }

            // Handling the case of
            // inequality
            else if (B[i % M] != arr[i])
            {
                System.out.println(0);
                return;
            }
        }
    }

    // Stores count of 0s
    // in B[]
    int cnt = 0;

    // Traverse the array, B[]
    for(int i = 0; i < M; i++)
    {

        // If B[i] is 0
        if (B[i] == 0)
        {

            // Update cnt
            cnt++;
        }
    }

    // Calculate factorial
    System.out.println(Fact(cnt));
}

// Driver Code
public static void main(String[] args)
{

    // Given M
    int M = 4;

    // Given array
    int[] arr = new int[]{ 1, 0, 3, 0, 0 };

    // Size of the array
    int N = arr.length;

    // Function Call
    numberOfWays(M, arr, N);
}
}

// This code is contributed by Dharanendra L V
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Modular function
# to calculate factorial
def Fact(N):

    # Stores factorial of N
    result = 1

    # Iterate over the range [1, N]
    for i in range(1, N + 1):

        # Update result
        result = (result * i)

    return result

# Function to count ways to replace array
# elements having 0s with non-zero elements
# such that any M consecutive elements are distinct
def numberOfWays(M, arr, N):

    # Store m consecutive distinct elements
    # such that arr[i] is equal to B[i % M]
    B = [0] * (M)

    # Stores frequency of array elements
    counter = [0] * (M + 1)

    # Traverse the array arr
    for i in range(0, N):

        # If arr[i] is non-zero
        if (arr[i] != 0):

            # If B[i % M] is equal to 0
            if (B[i % M] == 0):

                # Update B[i % M]
                B[i % M] = arr[i]

                # Update frequency of arr[i]
                counter[arr[i]] += 1

                # If a duplicate element found
                # in M consecutive elements
                if (counter[arr[i]] > 1):
                    print(0)
                    return

            # Handling the case of
            # inequality
            elif (B[i % M] != arr[i]):
                print(0)
                return

    # Stores count of 0s
    # in B
    cnt = 0

    # Traverse the array, B
    for i in range(0, M):

        # If B[i] is 0
        if (B[i] == 0):

            # Update cnt
            cnt += 1

    # Calculate factorial
    print(Fact(cnt))

# Driver Code
if __name__ == '__main__':

    # Given M
    M = 4

    # Given array
    arr = [ 1, 0, 3, 0, 0 ]

    # Size of the array
    N = len(arr)

    # Function Call
    numberOfWays(M, arr, N)

# This code is contributed by shikhasingrajput
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Modular function
// to calculate factorial
static int Fact(int N)
{

    // Stores factorial of N
    int result = 1;

    // Iterate over the range [1, N]
    for(int i = 1; i <= N; i++)
    {

        // Update result
        result = (result * i);
    }
    return result;
}

// Function to count ways to replace array
// elements having 0s with non-zero elements
// such that any M consecutive elements are distinct
static void numberOfWays(int M, int[] arr, int N)
{

    // Store m consecutive distinct elements
    // such that arr[i] is equal to B[i % M]
    int[] B = new int[M];

    // Stores frequency of array elements
    int[] counter = new int[M + 1];

    // Traverse the array arr[]
    for(int i = 0; i < N; i++)
    {

        // If arr[i] is non-zero
        if (arr[i] != 0)
        {

            // If B[i % M] is equal to 0
            if (B[i % M] == 0)
            {

                // Update B[i % M]
                B[i % M] = arr[i];

                // Update frequency of arr[i]
                counter[arr[i]]++;

                // If a duplicate element found
                // in M consecutive elements
                if (counter[arr[i]] > 1)
                {
                    Console.WriteLine(0);
                    return;
                }
            }

            // Handling the case of
            // inequality
            else if (B[i % M] != arr[i])
            {
                Console.WriteLine(0);
                return;
            }
        }
    }

    // Stores count of 0s
    // in B[]
    int cnt = 0;

    // Traverse the array, B[]
    for(int i = 0; i < M; i++)
    {

        // If B[i] is 0
        if (B[i] == 0)
        {

            // Update cnt
            cnt++;
        }
    }

    // Calculate factorial
    Console.WriteLine(Fact(cnt));
}

// Driver Code
static public void Main()
{

    // Given M
    int M = 4;

    // Given array
    int[] arr = new int[]{ 1, 0, 3, 0, 0 };

    // Size of the array
    int N = arr.Length;

    // Function Call
    numberOfWays(M, arr, N);
}
}

// This code is contributed by Dharanendra L V
```

## java 描述语言

```
<script>

// Javascript program of the above approach

// Modular function
// to calculate factorial
function Fact(N)
{

    // Stores factorial of N
    let result = 1;

    // Iterate over the range [1, N]
    for(let i = 1; i <= N; i++)
    {

        // Update result
        result = (result * i);
    }
    return result;
}

// Function to count ways to replace array
// elements having 0s with non-zero elements
// such that any M consecutive elements are distinct
function numberOfWays(M, arr, N)
{

    // Store m consecutive distinct elements
    // such that arr[i] is equal to B[i % M]
    let B = new Array(M).fill(0);

    // Stores frequency of array elements
    let counter = new Array(M+1).fill(0);

    // Traverse the array arr[]
    for(let i = 0; i < N; i++)
    {

        // If arr[i] is non-zero
        if (arr[i] != 0)
        {

            // If B[i % M] is equal to 0
            if (B[i % M] == 0)
            {

                // Update B[i % M]
                B[i % M] = arr[i];

                // Update frequency of arr[i]
                counter[arr[i]]++;

                // If a duplicate element found
                // in M consecutive elements
                if (counter[arr[i]] > 1)
                {
                    document.write(0);
                    return;
                }
            }

            // Handling the case of
            // inequality
            else if (B[i % M] != arr[i])
            {
                document.write(0);
                return;
            }
        }
    }

    // Stores count of 0s
    // in B[]
    let cnt = 0;

    // Traverse the array, B[]
    for(let i = 0; i < M; i++)
    {

        // If B[i] is 0
        if (B[i] == 0)
        {

            // Update cnt
            cnt++;
        }
    }

    // Calculate factorial
    document.write(Fact(cnt));
}

    // Driver Code

          // Given M
    let M = 4;

    // Given array
    let arr = [ 1, 0, 3, 0, 0 ];

    // Size of the array
    let N = arr.length;

    // Function Call
    numberOfWays(M, arr, N);

</script>
```

**Output:** 

```
2
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)
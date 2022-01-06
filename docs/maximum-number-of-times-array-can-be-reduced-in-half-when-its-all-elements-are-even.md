# 当数组的所有元素都是偶数时

数组的最大次数可以减半

> 原文:[https://www . geeksforgeeks . org/当数组的所有元素都是偶数时，数组的最大次数可以减半/](https://www.geeksforgeeks.org/maximum-number-of-times-array-can-be-reduced-in-half-when-its-all-elements-are-even/)

给定一个数组 **arr** ，任务是当数组中的所有元素都是偶数时对数组执行操作。一次操作，将数组中的每个整数 **X** 替换为 **X/2** 。找到您可以执行的最大可能操作数。

**示例:**

> **输入:** arr[] = {8，12，40}
> **输出:** 2
> **说明:**最初，{8，12，40}以阵列形式出现。由于所有那些整数都是偶数，
> 你可以执行操作。操作执行一次后，数组变为
> {4，6，20}。因为所有的整数都是偶数，所以我们可以再次进行运算。
> 操作执行两次后，数组变为{2，3，10}。现在数组中有一个奇数
> 号“3”，不能再进行任何操作了。
> 因此，您最多可以执行两次操作。
> 
> **输入:** arr[] = {5，6，8，10}
> **输出:** 0
> **说明:**由于初始数组中有一个奇数 5，所以我们连一次
> 操作都无法执行。

**方法:**给定的问题可以通过一些简单的观察来解决:

*   如果目前数组中所有的整数都是偶数，那么我们把所有的数除以 2。
*   因此，这个问题简化为求一个元素 arr[i]被 2 除的次数。随它去吧。答案是所有 I 的最小值。
*   我们可以通过简单地保留一个变量来更新每个阶段的答案，而不是使用额外的数组 times[]，这将空间复杂度降低到 O(1)，因为我们没有使用任何额外的空间。

以下是上述想法的实现。

## C++

```
// C++ code implementation for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to return the number
// of operations possible
int arrayDivisionByTwo(int arr[], int n)
{
    // counter to store the number of times the
    // current element is divisible by 2
    int cnt = 0;

    // variable to store the final answer
    int ans = INT_MAX;
    for (int i = 0; i < n; i++) {

        // Initialize the counter to zero
        // for each element
        cnt = 0;
        while (arr[i] % 2 == 0) {

            // update the counter till the
            // number is divisible by 2
            arr[i] = arr[i] / 2;
            cnt++;
        }

        // update the answer as
        // the minimum of all the counts
        ans = min(ans, cnt);
    }
    return ans;
}

// Driver code
int main()
{
    int arr[] = { 8, 12, 40 };
    int n = sizeof(arr) / sizeof(arr[0]);

    cout << arrayDivisionByTwo(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code implementation for the above approach
import java.util.*;

class GFG
{

// Function to return the number
// of operations possible
static int arrayDivisionByTwo(int arr[], int n)
{

    // counter to store the number of times the
    // current element is divisible by 2
    int cnt = 0;

    // variable to store the final answer
    int ans = Integer.MAX_VALUE;
    for (int i = 0; i < n; i++) {

        // Initialize the counter to zero
        // for each element
        cnt = 0;
        while (arr[i] % 2 == 0) {

            // update the counter till the
            // number is divisible by 2
            arr[i] = arr[i] / 2;
            cnt++;
        }

        // update the answer as
        // the minimum of all the counts
        ans = Math.min(ans, cnt);
    }
    return ans;
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 8, 12, 40 };
    int n = arr.length;

    System.out.print(arrayDivisionByTwo(arr, n));
}
}

// This code is contributed by Princi Singh
```

## 蟒蛇 3

```
# Python 3 code implementation for the above approach
import sys

# Function to return the number
# of operations possible
def arrayDivisionByTwo(arr, n):

    # counter to store the number of times the
    # current element is divisible by 2
    cnt = 0

    # variable to store the final answer
    ans = sys.maxsize
    for i in range(n):

        # Initialize the counter to zero
        # for each element
        cnt = 0
        while(arr[i] % 2 == 0):

            # update the counter till the
            # number is divisible by 2
            arr[i] = arr[i] // 2
            cnt += 1

        # update the answer as
        # the minimum of all the counts
        ans = min(ans, cnt)
    return ans

# Driver code
if __name__ == '__main__':
    arr = [8, 12, 40]
    n =  len(arr)

    print(arrayDivisionByTwo(arr, n))

    # This code is contributed by ipg2016107.
```

## C#

```
// C# code implementation for the above approach
using System;

class GFG{
// Function to return the number
// of operations possible
static int arrayDivisionByTwo(int []arr, int n)
{

    // counter to store the number of times the
    // current element is divisible by 2
    int cnt = 0;

    // variable to store the final answer
    int ans = Int32.MaxValue;
    for (int i = 0; i < n; i++) {

        // Initialize the counter to zero
        // for each element
        cnt = 0;
        while (arr[i] % 2 == 0) {

            // update the counter till the
            // number is divisible by 2
            arr[i] = arr[i] / 2;
            cnt++;
        }

        // update the answer as
        // the minimum of all the counts
        ans = Math.Min(ans, cnt);
    }
    return ans;
}

// Driver code
public static void Main(String[] args)
{
    int []arr = { 8, 12, 40 };
    int n = arr.Length;

    Console.Write(arrayDivisionByTwo(arr, n));
}
}

// This code is contributed by shivanisinghss2110
```

## java 描述语言

```
<script>
        // JavaScript Program to implement
        // the above approach

        // Function to return the number
        // of operations possible
        function arrayDivisionByTwo(arr, n) {
            // counter to store the number of times the
            // current element is divisible by 2
            let cnt = 0;

            // variable to store the final answer
            let ans = Number.MAX_VALUE;
            for (let i = 0; i < n; i++) {

                // Initialize the counter to zero
                // for each element
                cnt = 0;
                while (arr[i] % 2 == 0) {

                    // update the counter till the
                    // number is divisible by 2
                    arr[i] = Math.floor(arr[i] / 2);
                    cnt++;
                }

                // update the answer as
                // the minimum of all the counts
                ans = Math.min(ans, cnt);
            }
            return ans;
        }

        // Driver code

        let arr = [8, 12, 40];
        let n = arr.length;

        document.write(arrayDivisionByTwo(arr, n));

//This code is contributed by Potta Lokesh
    </script>
```

**Output**

```
2
```

**时间复杂度:**O(32 * n)
T3】空间复杂度: O(1)
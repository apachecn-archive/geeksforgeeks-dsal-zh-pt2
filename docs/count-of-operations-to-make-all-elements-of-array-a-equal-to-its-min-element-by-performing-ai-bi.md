# 通过执行 a[I]–b[I]

使数组 a[]的所有元素等于其最小元素的操作计数

> 原文:[https://www . geeksforgeeks . org/通过执行 ai-bi 使数组的所有元素等于其最小元素的操作计数/](https://www.geeksforgeeks.org/count-of-operations-to-make-all-elements-of-array-a-equal-to-its-min-element-by-performing-ai-bi/)

给定两个大小为 **N** 的数组**a【】**和**b【】**，任务是通过执行**a[I]–b[I]**来打印使数组 **a[i]** 的所有元素等于其最小元素所需的操作计数，其中它总是 **a[i] > = b[i]** 。如果不可能，则返回-1。
**例:**

> **输入:** a[] = {5，7，10，5，15} b[] = {2，2，1，3，5}
> **输出:** 8
> **说明:**
> 输入数组是 a[] = 5，7，10，5，15 和 b[] = 2，2，1，3，5。从[]开始的最小值是 5。
> 现在对于[0]我们不需要执行任何操作，因为它已经是 5 了。
> 对于 i = 1，a[1]–b[1]= 7–2 = 5。(1 次操作)
> 对于 i = 2，a[2]–b[2]= 10–1 = 9–1 = 8–1 = 7–1 = 6–1 = 5(5 次操作)
> 对于 i = 3，a[3] = 5
> 对于 i = 4，a[4]–b[4]= 15–5 = 10–5 = 5(2 次操作)
> 所需操作总数为 8。
> **输入:** a[] = {1，3，2} b[] = {2，3，2}
> **输出:** -1
> **解释:**
> 无法将数组 a[]转换为相等的元素。

**方法:**按照以下步骤解决上述问题:

*   [从数组](https://www.geeksforgeeks.org/program-find-minimum-maximum-element-array/)中找到最小值 a[]。初始化一个变量*和* = -1，存储减法运算的结果。
*   从数组 a[]的最小元素迭代到 0，并将存储计数减法的变量 *curr* 初始化为 0，使数组元素相等。
*   遍历数组并检查 a[i]是否不等于 x，x 是第一个数组中的最小元素，然后使它等于最小否则更新 curr 等于零。
*   检查货币是否不等于 0，然后将 ans 更新为货币，最后返回 **ans** 。

以下是上述方法的实现:

## C++

```
// C++ program to count the operations
// to make all elements of array a[]
// equal to its min element
// by performing a[i] – b[i]

#include <bits/stdc++.h>
using namespace std;

// Function to convert all Element of
// first array equal using second array
int findMinSub(int a[], int b[], int n)
{
    // Get the minimum from first array
    int min = INT_MAX;
    for (int i = 0; i < n; i++) {
        if (a[i] < min)
            min = a[i];
    }

    // Variable that stores count of
    // resultant required subtraction
    // to Convert all elements equal
    int ans = -1;

    for (int x = min; x >= 0; x--)

    {
        // Stores the count subtraction to
        // make the array element
        // equal for each iteration
        int curr = 0;

        // Traverse the array and check if
        // a[i] is not equal to x then
        // Make it equal to minimum else
        // update current equal to zero
        for (int i = 0; i < n; i++) {
            if (a[i] != x) {

                if (b[i] > 0
                    && (a[i] - x) % b[i] == 0) {
                    curr += (a[i] - x) / b[i];
                }
                else {
                    curr = 0;
                    break;
                }
            }
        }
        // Check if curr is not equal to
        // zero then update the answer
        if (curr != 0) {
            ans = curr;
            break;
        }
    }

    return ans;
}

// Driver code
int main()
{

    int a[] = { 5, 7, 10, 5, 15 };
    int b[] = { 2, 2, 1, 3, 5 };

    int n = sizeof(a) / sizeof(a[0]);

    cout << findMinSub(a, b, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count the operations
// to make all elements of array a[]
// equal to its min element
// by performing a[i] – b[i]
import java.util.*;

class GFG{

// Function to convert all element of
// first array equal using second array
static int findMinSub(int a[], int b[], int n)
{

    // Get the minimum from first array
    int min = Integer.MAX_VALUE;
    for(int i = 0; i < n; i++)
    {
    if (a[i] < min)
        min = a[i];
    }

    // Variable that stores count of
    // resultant required subtraction
    // to Convert all elements equal
    int ans = -1;

    for(int x = min; x >= 0; x--)
    {

    // Stores the count subtraction
    // to make the array element
    // equal for each iteration
    int curr = 0;

    // Traverse the array and check
    // if a[i] is not equal to x then
    // Make it equal to minimum else
    // update current equal to zero
    for(int i = 0; i < n; i++)
    {
        if (a[i] != x)
        {
            if (b[i] > 0 &&
                (a[i] - x) % b[i] == 0)
            {
                curr += (a[i] - x) / b[i];
            }
            else
            {
                curr = 0;
                break;
            }
        }
    }

    // Check if curr is not equal to
    // zero then update the answer
    if (curr != 0)
    {
        ans = curr;
        break;
    }
    }
    return ans;
}

// Driver code
public static void main(String[] args)
{
    int a[] = { 5, 7, 10, 5, 15 };
    int b[] = { 2, 2, 1, 3, 5 };
    int n = a.length;

    System.out.print(findMinSub(a, b, n));
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to count the operations
# to make all elements of array a[]
# equal to its min element
# by performing a[i] – b[i]

# Function to convert all element of
# first array equal using second array
def findMinSub(a, b, n):

    # Get the minimum from first array
    min = a[0]
    for i in range(0, n):
        if a[i] < min:
            min = a[i]

    # Variable that stores count of
    # resultant required subtraction
    # to Convert all elements equal
    ans = -1
    for x in range(min, -1, -1):

        # Stores the count subtraction
        # to make the array element
        # equal for each iteration
        curr = 0

        # Traverse the array and check
        # if a[i] is not equal to x then
        # Make it equal to minimum else
        # update current equal to zero
        for i in range(0, n):
            if a[i] != x:

                if (b[i] > 0 and
                   (a[i] - x) % b[i] == 0):
                    curr += (a[i] - x) // b[i]
                else:
                    curr = 0
                    break

        # Check if curr is not equal to
        # zero then update the answer
        if curr != 0:
            ans = curr
            break

    return ans

# Driver code
a = [ 5, 7, 10, 5, 15 ]
b = [ 2, 2, 1, 3, 5 ]
n = len(a)

print(findMinSub(a, b, n))

# This code is contributed by jrishabh99
```

## C#

```
// C# program to count the operations
// to make all elements of array a[]
// equal to its min element
// by performing a[i] – b[i]
using System;
class GFG{

// Function to convert all element of
// first array equal using second array
static int findMinSub(int []a, int []b, int n)
{

    // Get the minimum from first array
    int min = Int32.MaxValue;

    for(int i = 0; i < n; i++)
    {
        if (a[i] < min)
            min = a[i];
    }

    // Variable that stores count of
    // resultant required subtraction
    // to Convert all elements equal
    int ans = -1;

    for(int x = min; x >= 0; x--)
    {

        // Stores the count subtraction
        // to make the array element
        // equal for each iteration
        int curr = 0;

        // Traverse the array and check
        // if a[i] is not equal to x then
        // Make it equal to minimum else
        // update current equal to zero
        for(int i = 0; i < n; i++)
        {
            if (a[i] != x)
            {
                if (b[i] > 0 &&
                    (a[i] - x) % b[i] == 0)
                {
                    curr += (a[i] - x) / b[i];
                }
                else
                {
                    curr = 0;
                    break;
                }
            }
        }

        // Check if curr is not equal to
        // zero then update the answer
        if (curr != 0)
        {
            ans = curr;
            break;
        }
    }
    return ans;
}

// Driver code
public static void Main()
{
    int []a = { 5, 7, 10, 5, 15 };
    int []b = { 2, 2, 1, 3, 5 };
    int n = a.Length;

    Console.Write(findMinSub(a, b, n));
}
}

// This code is contributed by Code_Mech
```

## java 描述语言

```
<script>
// javascript program to count the operations
// to make all elements of array a
// equal to its min element
// by performing a[i] – b[i]

    // Function to convert all element of
    // first array equal using second array
    function findMinSub(a , b , n) {

        // Get the minimum from first array
        var min = Number.MAX_VALUE;
        for (i = 0; i < n; i++) {
            if (a[i] < min)
                min = a[i];
        }

        // Variable that stores count of
        // resultant required subtraction
        // to Convert all elements equal
        var ans = -1;

        for (x = min; x >= 0; x--) {

            // Stores the count subtraction
            // to make the array element
            // equal for each iteration
            var curr = 0;

            // Traverse the array and check
            // if a[i] is not equal to x then
            // Make it equal to minimum else
            // update current equal to zero
            for (i = 0; i < n; i++) {
                if (a[i] != x) {
                    if (b[i] > 0 && (a[i] - x) % b[i] == 0) {
                        curr += (a[i] - x) / b[i];
                    } else {
                        curr = 0;
                        break;
                    }
                }
            }

            // Check if curr is not equal to
            // zero then update the answer
            if (curr != 0) {
                ans = curr;
                break;
            }
        }
        return ans;
    }

    // Driver code
        var a = [ 5, 7, 10, 5, 15 ];
        var b = [ 2, 2, 1, 3, 5 ];
        var n = a.length;

        document.write(findMinSub(a, b, n));

// This code is contributed by aashish1995
</script>
```

**Output:** 

```
8
```
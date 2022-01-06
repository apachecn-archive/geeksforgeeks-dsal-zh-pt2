# 最小化将数组转换为前 N 个自然数的排列所需的数字总和

> 原文:[https://www . geesforgeks . org/minimum-numbers-sum-将数组转换为第一个 n 个自然数的排列所需的数量/](https://www.geeksforgeeks.org/minimize-sum-of-numbers-required-to-convert-an-array-into-a-permutation-of-first-n-natural-numbers/)

给定一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/array-data-structure/)**A【】**，任务是找到需要添加到数组元素的最小数量和，以将数组转换为 **1** 到 **N** 的排列。如果数组不能转换成想要的排列，打印 **-1** 。

**示例:**

> **输入:** A[] = {1，1，1，1，1}
> **输出:** 10
> **解释:**将 A[1]增加 1，A[2]增加 2，A[3]增加 3，A[4]增加 4，这样 A[]，就变成了{1，2，3，4，5}。
> 所需的最小添加量= 1 + 2 + 3 + 4 = 10
> 
> **输入:** A[] = {2，2，3}
> **输出:** -1

**进场:**思路是用[排序](https://www.geeksforgeeks.org/sorting-algorithms/)。请按照以下步骤解决此问题:

*   初始化一个变量**和**来存储需要的结果。
*   [按照递增顺序](https://www.geeksforgeeks.org/c-program-to-sort-an-array-in-ascending-order/)对给定数组 **A[]** 进行排序。
*   [使用变量 **i** 遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)、 **A[]**
    *   如果**A【I】>I+1**的值，更新 **ans** 为 **-1** 和[脱离循环](https://www.geeksforgeeks.org/break-statement-cc/)。
    *   否则按 **i+1** 和**A【I】**的差值增加**和**。
*   打印**和**的值作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum additions required 
// to convert the array into a permutation of 1 to N
int minimumAdditions(int a[], int n)
{
    // Sort the array in increasing order
    sort(a, a + n);
    int ans = 0;

    // Traverse the array
    for (int i = 0; i < n; i++) {

        // If a[i] > i + 1, then return -1
        if ((i + 1) - a[i] < 0) {
            return -1;
        }
        if ((i + 1) - a[i] > 0) {

            // Update answer
            ans += (i + 1 - a[i]);
        }
    }

    // Return the required result
    return ans;
}

// Driver Code
int main()
{
    // Given Input
    int A[] = { 1, 1, 1, 1, 1 };
    int n = sizeof(A) / sizeof(A[0]);

    // Function Call
    cout << minimumAdditions(A, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.Arrays;

public class GFG {

    // Function to find the minimum additions required 
    // to convert the array into a permutation of 1 to N
    static int minimumAdditions(int a[], int n)
    {
        // Sort the array in increasing order
        Arrays.sort(a);
        int ans = 0;

        // Traverse the array
        for (int i = 0; i < n; i++) {

            // If a[i] > i + 1, then return -1
            if ((i + 1) - a[i] < 0) {
                return -1;
            }
            if ((i + 1) - a[i] > 0) {

                // Update answer
                ans += (i + 1 - a[i]);
            }
        }

        // Return the required result
        return ans;
    }

    // Driver code
    public static void main(String[] args)
    {

      // Given Input
        int A[] = { 1, 1, 1, 1, 1 };
        int n = A.length;

        // Function Call
        System.out.println(minimumAdditions(A, n));
    }
}

// This code is contributed by abhinavjain194
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the minimum additions
# required to convert the array into a
# permutation of 1 to N
def minimumAdditions(a, n):

    # Sort the array in increasing order
    a = sorted(a)
    ans = 0

    # Traverse the array
    for i in range(n):

        # If a[i] > i + 1, then return -1
        if ((i + 1) - a[i] < 0):
            return -1

        if ((i + 1) - a[i] > 0):

            # Update answer
            ans += (i + 1 - a[i])

    # Return the required result
    return ans

# Driver Code
if __name__ == '__main__':

    # Given Input
    A = [ 1, 1, 1, 1, 1 ]
    n = len(A)

    # Function Call
    print(minimumAdditions(A, n))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to find the minimum additions
// required to convert the array into a
// permutation of 1 to N
static int minimumAdditions(int []a, int n)
{

    // Sort the array in increasing order
    Array.Sort(a);
    int ans = 0;

    // Traverse the array
    for(int i = 0; i < n; i++)
    {

        // If a[i] > i + 1, then return -1
        if ((i + 1) - a[i] < 0)
        {
            return -1;
        }

        if ((i + 1) - a[i] > 0)
        {

            // Update answer
            ans += (i + 1 - a[i]);
        }
    }

    // Return the required result
    return ans;
}

// Driver code
static void Main()
{

    // Given Input
    int[] A = { 1, 1, 1, 1, 1 };
    int n = A.Length;

    // Function Call
    Console.Write(minimumAdditions(A, n));
}
}

// This code is contributed by SoumikMondal
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to find the minimum additions required
    // to convert the array into a permutation of 1 to N
function minimumAdditions(a, n)
{

    // Sort the array in increasing order
        a.sort(function(a, b){return a-b;});
        let ans = 0;

        // Traverse the array
        for (let i = 0; i < n; i++) {

            // If a[i] > i + 1, then return -1
            if ((i + 1) - a[i] < 0) {
                return -1;
            }
            if ((i + 1) - a[i] > 0) {

                // Update answer
                ans += (i + 1 - a[i]);
            }
        }

        // Return the required result
        return ans;
}

// Driver code
// Given Input
let A = [ 1, 1, 1, 1, 1 ];
let n = A.length;

// Function Call
document.write(minimumAdditions(A, n));

// This code is contributed by unknown2108
</script>
```

**Output:** 

```
10
```

***时间复杂度:** O(N* log(N))*
***辅助空间:** O(1)*
# 最大化数组的第一个元素，使得平均值保持不变

> 原文:[https://www . geeksforgeeks . org/最大化数组的第一个元素，使得平均值保持不变/](https://www.geeksforgeeks.org/maximize-the-first-element-of-the-array-such-that-average-remains-constant/)

给定一个长度为 **N** 的数组**arr【】**和一个整数 **X** ，任务是找到更新后的第一个元素的最大值 **R** ，使得数组的平均值保持不变，并且数组中没有元素变成负数。第一个元素的最大值应该在范围 arr[0] < = R < = X
**内示例:**

> **输入:** arr[] = {1，2，3，4}，X = 5
> **输出:** 5
> **解释:**
> 在上面给出的例子中，可以获得的第一个元素
> 的最大值是 5，这样数组的平均值保持不变
> 数组的实际平均值= (1 + 2 + 3 + 4) / 4 = 2.5
> 递增后，数组将采用以下任何形式–
> { 5，2， 3，0}，数组平均值= (5 + 2 + 3 + 0) / 4 = 2.5
> {5，0，1，4}，数组平均值= (5 + 0 + 1 + 4) / 4 = 2.5
> {5，1，0，4}，数组平均值= (5 + 1 + 0 + 4) / 4 = 2.5
> ……还有更多
> **输入:** arr[] = {44，289，21，26} X = 999
> **输出:** 380
> **解释:**
> 在上面给出的例子中，可以得到的第一个元素
> 的最大值是 336，这样数组的平均值保持不变
> 数组的实际平均值= (44 + 289 + 21 + 26) / 4 = 95
> 递增后，数组将采用以下形式–
> { 380，0，0}，的平均值

**逼近**:想法是利用第一个元素可以递增的事实，使得数组的元素保持正，那么每个元素 arr[i]可以在 0 到其初始值 arr[i]的范围内。因此，数组的第一个元素可以达到的最大值将是数组的和，由于 R 的最大值应该在 arr[0] < = R < = X 的范围内，因此 R 将是 S 和 X 之和的最小值。
**算法:**

*   通过从 0 到 length–1 的循环迭代求数组的和(比如 **S** )，其中 length 是数组的长度。
*   找出 X 和 S 之间的最小值，该值将是在 arr[0] <= R <= X 范围内可获得的最大值，这样数组的平均值保持不变。

**举例说明:**

```
Given Array be  - {44, 289, 21, 26} and X = 999
Sum of the Array - 44 + 289 + 21 + 26 = 380

Minimum value of the 380 and X = 999 is 380
The array that can be achieved with value as 380 is
{380, 0, 0, 0}
whereas, The operations are -
Index 0: Add 289 + 21 + 26, which is 336.
Index 1: Subtract 289 from 2nd element.
Index 2: Subtract 21 from 3rd element.
Index 3: Subtract 26 from 4th element.
```

以下是上述方法的实现:

## C++

```
// C++ implementation of to
// maximize the first element of
// the array such that average
// of the array remains constant

#include <bits/stdc++.h>
using namespace std;

// Maximum value of the first
// array element that can be attained
void getmax(int arr[], int n,
                       int x){

    // Variable to store the sum
    int s = 0;

    // Loop to find the sum of array
    for (int i = 0; i < n; i++) {
        s = s + arr[i];
    }

    // Desired maximum value
    cout << min(s, x);
}

// Driver Code
int main()
{
    int arr[] = { 1, 2, 3, 4 };
    int x = 5;
    int arr_size = sizeof(arr) / sizeof(arr[0]);

    getmax(arr, arr_size, x);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of to
// maximize the first element of
// the array such that average
// of the array remains constant
import java.util.*;

class GFG{

// Maximum value of the first
// array element that can be attained
static void getmax(int arr[], int n,
                       int x){

    // Variable to store the sum
    int s = 0;

    // Loop to find the sum of array
    for (int i = 0; i < n; i++) {
        s = s + arr[i];
    }

    // Desired maximum value
    System.out.print(Math.min(s, x));
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 1, 2, 3, 4 };
    int x = 5;
    int arr_size = arr.length;

    getmax(arr, arr_size, x);
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation of to
# maximize the first element of
# the array such that average
# of the array remains constant

# Maximum value of the first
# array element that can be attained
def getmax(arr, n, x):

    # Variable to store the sum
    s = 0

    # Loop to find the sum of array
    for i in range(n):
        s = s + arr[i]

    # Desired maximum value
    print(min(s, x))

# Driver Code
if __name__ == '__main__':
    arr= [1, 2, 3, 4]
    x = 5
    arr_size = len(arr)

    getmax(arr, arr_size, x)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# implementation of to
// maximize the first element of
// the array such that average
// of the array remains constant
using System;

class GFG
{

    // Maximum value of the first
    // array element that can be attained
    static void getmax(int[] arr, int n , int x)
    {
        // Variable to store the sum
        int s = 0;

        // Loop to find the sum of array
        for (int i = 0; i < n; i++)
        {
            s = s + arr[i];
        }

        // Desired maximum value
        Console.WriteLine(Math.Min(s, x));
    }

    // Driver code
    static void Main()
    {
        int[] arr = new int[] { 1, 2, 3, 4 };
        int x = 5;
        int arr_size = arr.Length;

        getmax(arr, arr_size, x);
    }
}

// This code is contributed by shubhamsingh10
```

## java 描述语言

```
<script>
// javascript implementation of to
// maximize the first element of
// the array such that average
// of the array remains constant

// Maximum value of the first
// array element that can be attained
function getmax( arr, n, x)
{

    // Variable to store the sum
    let s = 0;

    // Loop to find the sum of array
    for (let i = 0; i < n; i++)
    {
        s = s + arr[i];
    }

    // Desired maximum value
     document.write(Math.min(s, x));
}

// Driver Code
    let arr = [ 1, 2, 3, 4 ];
    let x = 5;
    let arr_size = arr.length;

    getmax(arr, arr_size, x);

// This code is contributed by Rajput-Ji

</script>
```

**Output:** 

```
5
```

**业绩分析:**

*   **时间复杂度:** O(N)
*   **辅助空间:** O(1)。
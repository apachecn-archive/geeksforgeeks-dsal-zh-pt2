# 通过最多一次转换最大化给定数组中奇数和对的计数

> 原文:[https://www . geeksforgeeks . org/给定最多一次转换数组中奇数和对的最大计数/](https://www.geeksforgeeks.org/maximize-count-of-odd-sum-pairs-in-given-array-with-at-most-one-conversion/)

给定整数大小的[数组](https://www.geeksforgeeks.org/array-data-structure/)**n，**通过最多改变一个数，从数组中找出最大数量的对，使得它们的和为奇数。

**示例:**

> **输入:** N = 6，arr = [1，5，3，6，8，0]
> **输出:** 3
> **说明:**有 3 个偶数和 3 个奇数
> 
> **输入:** N = 8，arr = [1，5，3，6，8，0，2，4]
> **输出:** 4
> **说明:**有 5 个偶数和 3 个奇数，一个偶数可以转换成一个奇数。因此最终输出将是 4。

**方法:**对于元素的[和为奇数，一个数应为奇数，另一个数应为偶数。可以遵循以下步骤:](https://www.geeksforgeeks.org/program-find-sum-elements-given-array/)

*   计算 **x** ，等于奇数的元素数
*   计算等于偶数元素数的 Y。
*   通过 x 和 y 的最小值初始化答案变量
*   如果| x–y | > = 2，则将答案增加 1(即，如果 y–x > = 2，则我们可以将一个奇数转换为偶数，如果 x–y > = 2，则我们可以将一个偶数转换为奇数)
*   结果答案变量是我们需要的答案。

下面是上述方法的实现:

## C++

```
// C++ code implementation for above approach
#include <bits/stdc++.h>
using namespace std;

// To find maximum number of pairs in
// array with conversion of at most one element
int maximumNumberofpairs(int n, int arr[])
{
    // Initialize count of even elements
    int x = 0;

    // Initialize count of odd elements
    int y = 0;
    for (int i = 0; i < n; i++) {

        // If current number is even
        // then increment x by 1
        if (arr[i] % 2 == 0) {
            x++;
        }

        // If current number is odd
        // then increment y by 1
        else {
            y++;
        }
    }

    // Initialize the answer by min(x, y)
    int answer = min(x, y);

    // If difference in count of odd and even
    // is more than 2 than increment answer
    if (abs(x - y) >= 2) {
        answer++;
    }

    // Return final answer
    return answer;
}
// Driver code
int main()
{
    // Given array
    int arr[] = { 1, 2, 4, 6, 5, 10, 12 };
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << maximumNumberofpairs(n, arr) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation for the above approach
import java.io.*;

class GFG
 {

  // To find maximum number of pairs in
// array with conversion of at most one element
static int maximumNumberofpairs(int n, int arr[])
{

    // Initialize count of even elements
    int x = 0;

    // Initialize count of odd elements
    int y = 0;
    for (int i = 0; i < n; i++) {

        // If current number is even
        // then increment x by 1
        if (arr[i] % 2 == 0) {
            x++;
        }

        // If current number is odd
        // then increment y by 1
        else {
            y++;
        }
    }

    // Initialize the answer by min(x, y)
    int answer = Math.min(x, y);

    // If difference in count of odd and even
    // is more than 2 than increment answer
    if (Math.abs(x - y) >= 2) {
        answer++;
    }

    // Return final answer
    return answer;
}

// Driver code
    public static void main (String[] args) {
      // Given array
    int arr[] = { 1, 2, 4, 6, 5, 10, 12 };
    int n = arr.length;

        System.out.println( maximumNumberofpairs(n, arr));
    }
}

// This code is contributed by Potta Lokesh
```

## 计算机编程语言

```
# python 3 code implementation for above approach

# To find maximum number of pairs in
# array with conversion of at most one element
def maximumNumberofpairs(n, arr):
    # Initialize count of even elements
    x = 0

    # Initialize count of odd elements
    y = 0
    for i in range(n):
        # If current number is even
        # then increment x by 1
        if (arr[i] % 2 == 0):
            x += 1

        # If current number is odd
        # then increment y by 1
        else:
            y += 1

    # Initialize the answer by min(x, y)
    answer = min(x, y)

    # If difference in count of odd and even
    # is more than 2 than increment answer
    if (abs(x - y) >= 2):
        answer += 1

    # Return final answer
    return answer

# Driver code
if __name__ == '__main__':
    # Given array
    arr = [1, 2, 4, 6, 5, 10, 12]
    n = len(arr)
    print(maximumNumberofpairs(n, arr))

# This code is contributed by ipg2016107.
```

## C#

```
// C# implementation for the above approach

using System;

public class GFG
 {

  // To find maximum number of pairs in
// array with conversion of at most one element
static int maximumNumberofpairs(int n, int []arr)
{

    // Initialize count of even elements
    int x = 0;

    // Initialize count of odd elements
    int y = 0;
    for (int i = 0; i < n; i++) {

        // If current number is even
        // then increment x by 1
        if (arr[i] % 2 == 0) {
            x++;
        }

        // If current number is odd
        // then increment y by 1
        else {
            y++;
        }
    }

    // Initialize the answer by min(x, y)
    int answer = Math.Min(x, y);

    // If difference in count of odd and even
    // is more than 2 than increment answer
    if (Math.Abs(x - y) >= 2) {
        answer++;
    }

    // Return final answer
    return answer;
}

// Driver code
    public static void Main (string[] args) {

    // Given array
    int []arr = { 1, 2, 4, 6, 5, 10, 12 };
    int n = arr.Length;

        Console.WriteLine(maximumNumberofpairs(n, arr));
    }
}

// This code is contributed by AnkThon
```

## Java Script 语言

```
<script>
// JavaScript implementation for the above approach

// To find maximum number of pairs in
// array with conversion of at most one element
function maximumNumberofpairs(n, arr)
{

    // Initialize count of even elements
    var x = 0;

    // Initialize count of odd elements
    var y = 0;
    for (var i = 0; i < n; i++) {

        // If current number is even
        // then increment x by 1
        if (arr[i] % 2 == 0) {
            x++;
        }

        // If current number is odd
        // then increment y by 1
        else {
            y++;
        }
    }

    // Initialize the answer by min(x, y)
    var answer = Math.min(x, y);

    // If difference in count of odd and even
    // is more than 2 than increment answer
    if (Math.abs(x - y) >= 2) {
        answer++;
    }

    // Return final answer
    return answer;
}

// Driver code
// Given array
var arr = [ 1, 2, 4, 6, 5, 10, 12 ];
var n = arr.length;

document.write( maximumNumberofpairs(n, arr));

// This code is contributed by shivanisinghss2110

</script>
```

**Output:**

```
3

```

**时间复杂度:**O(N)
T3】辅助空间: O(1)
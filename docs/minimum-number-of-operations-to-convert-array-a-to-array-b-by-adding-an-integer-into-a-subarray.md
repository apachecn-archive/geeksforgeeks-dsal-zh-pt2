# 将一个整数加到一个子数组中，将数组 A 转换为数组 B 的最小运算次数

> 原文:[https://www . geesforgeks . org/通过在子数组中添加一个整数将数组 a 转换为数组 b 的最小操作数/](https://www.geeksforgeeks.org/minimum-number-of-operations-to-convert-array-a-to-array-b-by-adding-an-integer-into-a-subarray/)

给定两个长度为 **N** 的数组**A【】**和**B【】**，任务是找到数组 **A** 可以转换为数组 **B** 的最小操作数，其中每个操作包括将整数 K 添加到从 L 到 r 的子数组中

**示例:**

> **输入:** A[] = {3，7，1，4，1，2}，B[] = {3，7，3，6，3，2}
> **输出:** 1
> **说明:**
> 在上面给出的例子中，从 A 转换为 B 只需要一个操作:L = 3，R = 5 和 K = 2
> 数组经过以下操作:
> **索引 0:** A[0] = 3，B[0] B[1] = 7
> **指数 2:** A[2] = 1 + 2 = 3，B[2] = 3
> **指数 3:** A[3] = 4 + 2 = 6，B[3] = 6
> **指数 4:** A[4] = 1 + 2 = 3，B[4] = 3
> **指数 5:** A[5] = 2，B[5] = 2
> 
> **输入:** A[] = {1，1，1，1，1}，B[] = {1，2，1，3，1}
> **输出:** 2
> **解释:**
> 在上面给出的例子中，从 A 到 B 的转换只需要一个操作–
> **操作 1:** 加 1 到 L = 2 到 R = 2
> **操作 2:** 加 2 到 L = 4 到 R = 4

**方法:**想法是计算数组 A 中与数组 b 中相应元素具有相等差异的连续元素

*   从数组 A 和数组 B 中找出对应元素的区别:

```
Difference = A[i] - B[i]
```

*   如果相应元素的差值等于 0，则继续检查下一个索引。
*   否则，增加索引，直到连续元素之间的差异不等于连续元素的前一个差异
*   将计数增加 1，直到所有索引都以相同的差异迭代。
*   最后，返回计数作为最小操作数。

下面是上述方法的实现:

## C++

```
// C++ implementation to find the
// minimum number of operations in
// which the array A can be converted
// to another array B

#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum
// number of operations in which
// array A can be converted to array B
void checkArray(int a[], int b[], int n)
{
    int operations = 0;
    int i = 0;

    // Loop to iterate over the array
    while (i < n) {

        // if both elements are equal
        // then move to next element
        if (a[i] - b[i] == 0) {
            i++;
            continue;
        }

        // Calculate the difference
        // between two elements
        int diff = a[i] - b[i];
        i++;

        // loop while the next pair of
        // elements have same difference
        while (i < n &&
           a[i] - b[i] == diff) {
            i++;
        }

        // Increase the number of
        // operations by 1
        operations++;
    }

    // Print the number of
    // operations required
    cout << operations << "\n";
}

// Driver Code
int main()
{
    int a[] = { 3, 7, 1, 4, 1, 2 };
    int b[] = { 3, 7, 3, 6, 3, 2 };
    int size = sizeof(a) / sizeof(a[0]);

    checkArray(a, b, size);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find the
// minimum number of operations in
// which the array A can be converted
// to another array B
class GFG {

    // Function to find the minimum
    // number of operations in which
    // array A can be converted to array B
    static void checkArray(int a[], int b[], int n)
    {
        int operations = 0;
        int i = 0;

        // Loop to iterate over the array
        while (i < n) {

            // if both elements are equal
            // then move to next element
            if (a[i] - b[i] == 0) {
                i++;
                continue;
            }

            // Calculate the difference
            // between two elements
            int diff = a[i] - b[i];
            i++;

            // loop while the next pair of
            // elements have same difference
            while (i < n &&
               a[i] - b[i] == diff) {
                i++;
            }

            // Increase the number of
            // operations by 1
            operations++;
        }

        // Print the number of
        // operations required
        System.out.println(operations);
    }

    // Driver Code
    public static void main (String[] args)
    {
        int a[] = { 3, 7, 1, 4, 1, 2 };
        int b[] = { 3, 7, 3, 6, 3, 2 };
        int size = a.length;

        checkArray(a, b, size);
    }
}

// This code is contributed by AnkitRai01
```

## C#

```
// C# implementation to find the
// minimum number of operations in
// which the array A can be converted
// to another array B
using System;

class GFG {

    // Function to find the minimum
    // number of operations in which
    // array A can be converted to array B
    static void checkArray(int []a, int []b, int n)
    {
        int operations = 0;
        int i = 0;

        // Loop to iterate over the array
        while (i < n) {

            // if both elements are equal
            // then move to next element
            if (a[i] - b[i] == 0) {
                i++;
                continue;
            }

            // Calculate the difference
            // between two elements
            int diff = a[i] - b[i];
            i++;

            // loop while the next pair of
            // elements have same difference
            while (i < n &&
               a[i] - b[i] == diff) {
                i++;
            }

            // Increase the number of
            // operations by 1
            operations++;
        }

        // Print the number of
        // operations required
        Console.WriteLine(operations);
    }

    // Driver Code
    public static void Main (string[] args)
    {
        int []a = { 3, 7, 1, 4, 1, 2 };
        int []b = { 3, 7, 3, 6, 3, 2 };
        int size = a.Length;

        checkArray(a, b, size);
    }
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 implementation to find the
# minimum number of operations in
# which the array A can be converted
# to another array B

# Function to find the minimum
# number of operations in which
# array A can be converted to array B
def checkArray(a, b, n) :

    operations = 0;
    i = 0;

    # Loop to iterate over the array
    while (i < n) :

        # if both elements are equal
        # then move to next element
        if (a[i] - b[i] == 0) :
            i += 1;
            continue;

        # Calculate the difference
        # between two elements
        diff = a[i] - b[i];
        i += 1;

        # loop while the next pair of
        # elements have same difference
        while (i < n and a[i] - b[i] == diff) :
            i += 1;

        # Increase the number of
        # operations by 1
        operations += 1;

    # Print the number of
    # operations required
    print(operations);

# Driver Code
if __name__ == "__main__" :

    a = [ 3, 7, 1, 4, 1, 2 ];
    b = [ 3, 7, 3, 6, 3, 2 ];
    size = len(a);

    checkArray(a, b, size);

# This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>
// javascript implementation to find the
// minimum number of operations in
// which the array A can be converted
// to another array B   
// Function to find the minimum
    // number of operations in which
    // array A can be converted to array B
    function checkArray(a , b , n) {
        var operations = 0;
        var i = 0;

        // Loop to iterate over the array
        while (i < n) {

            // if both elements are equal
            // then move to next element
            if (a[i] - b[i] == 0) {
                i++;
                continue;
            }

            // Calculate the difference
            // between two elements
            var diff = a[i] - b[i];
            i++;

            // loop while the next pair of
            // elements have same difference
            while (i < n && a[i] - b[i] == diff) {
                i++;
            }

            // Increase the number of
            // operations by 1
            operations++;
        }

        // Print the number of
        // operations required
        document.write(operations);
    }

    // Driver Code

        var a = [ 3, 7, 1, 4, 1, 2 ];
        var b = [ 3, 7, 3, 6, 3, 2 ];
        var size = a.length;

        checkArray(a, b, size);

// This code contributed by Rajput-Ji
</script>
```

**性能分析:**

*   **时间复杂度:**和上面的方法一样，在最坏的情况下，只有一个占用 O(N)时间的循环。因此，时间复杂性将是 **O(N)** 。
*   **辅助空间复杂度:**和上面的方法一样，没有使用额外的空间。因此，辅助空间的复杂性将是 **O(1)** 。
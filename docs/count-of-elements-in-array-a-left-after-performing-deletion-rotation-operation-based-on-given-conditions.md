# 根据给定条件执行删除/旋转操作后剩余的数组 A 中的元素计数

> 原文:[https://www . geesforgeks . org/基于给定条件执行删除-旋转-操作后的左数组元素计数/](https://www.geeksforgeeks.org/count-of-elements-in-array-a-left-after-performing-deletion-rotation-operation-based-on-given-conditions/)

给定两个大小分别为 **N** 的[二进制数组](https://www.geeksforgeeks.org/sort-binary-array-using-one-traversal/)、 **A[]** 和 **B[]** ，任务是查找数组 **A[]** 中在执行以下操作后剩余的元素数量，直到没有元素可以删除:

1.  如果数组 **A[]** 和 **B[]** 的起始元素相等，则删除这两个元素。
2.  否则，删除后，将数组 **A[]** 的起始字符追加到数组的末尾， **A[]** 。

**示例:**

> **输入:** A[] = {1，1，0，1}，B[] = {1，0，1，1}，N = 4
> **输出:** 0
> **说明:**
> 操作如下:
> 
> 1.  A[0]( =1) = B[0]( =1):删除元素。此后，数组分别被修改为{1，0，1}和{0，1，1}。
> 2.  A[0](=1)！= B[0](= 0):将 A[0]移动到数组 A[]的末尾。此后，数组分别被修改为{0，1，1}和{ 0，1，1}。
> 3.  A[0]( =0) = B[0]( =0):删除元素。此后，数组分别被修改为{1，1}和{1，1}。
> 4.  A[0]( =1) = B[0]( =1):删除元素。此后，数组分别被修改为{1}和{1}。
> 5.  A[0]( =1) = B[0]( =1):删除元素。此后，两个数组都变成了空的。
> 
> 因此，数组 A[]中没有剩余任何元素。
> 
> **输入:** A[] = {1，0，1，1，1，1}，B[] = {1，1，0，1，0，1}，N = 6
> **输出:** 2

**方法:**给定的问题可以通过去掉常见的 0 和 1，然后计算两个数组中 0 和 1 的唯一个数来解决。考虑以下观察结果:

1.  只要数组 **A[]** 中还有一个等于 **B[]** 第一个元素的元素，就可以删除这些元素。
2.  还可以观察到 **A[]** 的元素顺序很容易改变。
3.  因此，想法是保留 **A[]** 中剩余的 **0** s 和 **1** s 的数量的计数，如果在 **B[]** 中遇到一个元素，使得相同的元素不再存在于 **A[]** 中，则不能执行更多的操作。

按照以下步骤解决问题:

*   [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)、**A【】**统计变量中 **0** s、 **1** s 的总数并存储在变量中，分别说**零**和**一**。
*   初始化一个变量，比如说**将**计数为0，以存储执行的删除总数。
*   [使用变量 **i** 遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)、 **B[]** ，并执行以下操作:
    *   如果 **B[i]** 等于 **0** 和**零> 0** ，那么将**计数**的值增加 **1** ，将**零**减少 **1** 。
    *   否则，如果 **B[i]** 等于 **1** 和**1>0**，则**的值递增**计数 **1** ，递减**1**计数 **1** 。
    *   否则，[退出循环](https://www.geeksforgeeks.org/break-statement-cc/)，因为不能再进行操作。
*   最后，完成以上步骤后，打印 **N** 和**计数**的差值作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to calculate minimum size
// of the array A[] after performing
// the given operations
int minimumSizeAfterDeletion(int A[], int B[], int N)
{
    // Stores the count of 0s and 1s
    int zero = 0, one = 0;

    // Stores the total deletions performed
    int count = 0;

    // Traverse the array A[]
    for (int i = 0; i < N; i++) {
        if (A[i] == 0) {
            zero++;
        }
        else {
            one++;
        }
    }

    // Traverse array B[]
    for (int i = 0; i < N; i++) {

        // If the B[i] is 0 and zero is
        // greater than 0
        if (B[i] == 0 && zero > 0) {
            // Increment count by 1
            count++;
            // Decrement zero by 1
            zero--;
        }

        // Else if the B[i] is 1 and one is
        // greater than 0
        else if (B[i] == 1 && one > 0) {
            // Increment count by 1
            count++;
            // Decrement one by 1
            one--;
        }

        // Otherwise
        else {
            break;
        }
    }

    // Return the answer
    return N - count;
}

// Driver Code
int main()
{

    // Given Input
    int A[] = { 1, 0, 1, 1, 1, 1 };
    int B[] = { 1, 1, 0, 1, 0, 1 };
    int N = 6;

    // Function Call
    cout << minimumSizeAfterDeletion(A, B, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;

class GFG{

// Function to calculate minimum size
// of the array A[] after performing
// the given operations
static int minimumSizeAfterDeletion(int A[], int B[],
                                    int N)
{

    // Stores the count of 0s and 1s
    int zero = 0, one = 0;

    // Stores the total deletions performed
    int count = 0;

    // Traverse the array A[]
    for(int i = 0; i < N; i++)
    {
        if (A[i] == 0)
        {
            zero++;
        }
        else
        {
            one++;
        }
    }

    // Traverse array B[]
    for(int i = 0; i < N; i++)
    {

        // If the B[i] is 0 and zero is
        // greater than 0
        if (B[i] == 0 && zero > 0)
        {

            // Increment count by 1
            count++;

            // Decrement zero by 1
            zero--;
        }

        // Else if the B[i] is 1 and one is
        // greater than 0
        else if (B[i] == 1 && one > 0)
        {

            // Increment count by 1
            count++;

            // Decrement one by 1
            one--;
        }

        // Otherwise
        else
        {
            break;
        }
    }

    // Return the answer
    return N - count;
}

// Driver Code
public static void main(String[] args)
{

    // Given Input
    int A[] = { 1, 0, 1, 1, 1, 1 };
    int B[] = { 1, 1, 0, 1, 0, 1 };
    int N = 6;

    // Function Call
    minimumSizeAfterDeletion(A, B, N);
    System.out.println(minimumSizeAfterDeletion(A, B, N));
}
}

// This code is contributed by Potta Lokesh
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to calculate minimum size
# of the array A[] after performing
# the given operations
def minimumSizeAfterDeletion(A, B, N):

    # Stores the count of 0s and 1s
    zero = 0
    one = 0

    # Stores the total deletions performed
    count = 0

    # Traverse the array A[]
    for i in range(N):
        if A[i] == 0:
            zero += 1
        else:
            one += 1

    # Traverse array B[]       
    for i in range(N):

        # If the B[i] is 0 and zero is
        # greater than 0
        if B[i] == 0 and zero > 0:

            # Increment count by 1
            count += 1

            # Decrement zero by 1
            zero -= 1

        # Else if the B[i] is 1 and one is
        # greater than 0
        elif B[i] == 1 and one > 0:

            # Increment count by 1
            count += 1

            # Decrement one by 1
            one -= 1

        # Otherwise
        else:
            break

    # Return the answer   
    return N - count

# Driver code

# Given input
A = [ 1, 0, 1, 1, 1, 1 ]
B = [ 1, 1, 0, 1, 0, 1 ]
N = 6

# Function call
print(minimumSizeAfterDeletion(A, B, N))

# This code is contributed by Parth Manchanda
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to calculate minimum size
// of the array A[] after performing
// the given operations
static int minimumSizeAfterDeletion(int []A, int []B, int N)
{
    // Stores the count of 0s and 1s
    int zero = 0, one = 0;

    // Stores the total deletions performed
    int count = 0;

    // Traverse the array A[]
    for (int i = 0; i < N; i++) {
        if (A[i] == 0) {
            zero++;
        }
        else {
            one++;
        }
    }

    // Traverse array B[]
    for (int i = 0; i < N; i++) {

        // If the B[i] is 0 and zero is
        // greater than 0
        if (B[i] == 0 && zero > 0) {
            // Increment count by 1
            count++;
            // Decrement zero by 1
            zero--;
        }

        // Else if the B[i] is 1 and one is
        // greater than 0
        else if (B[i] == 1 && one > 0) {
            // Increment count by 1
            count++;
            // Decrement one by 1
            one--;
        }

        // Otherwise
        else {
            break;
        }
    }

    // Return the answer
    return N - count;
}

// Driver Code
public static void Main()
{

    // Given Input
    int []A = { 1, 0, 1, 1, 1, 1 };
    int []B = { 1, 1, 0, 1, 0, 1 };
    int N = 6;

    // Function Call
    Console.Write(minimumSizeAfterDeletion(A, B, N));
}
}

// This code is contributed by ipg2016107.
```

## java 描述语言

```
<script>
// Javascript program for the above approach
// Function to calculate minimum size
// of the array A[] after performing
// the given operations
function minimumSizeAfterDeletion(A, B, N)
{

    // Stores the count of 0s and 1s
    var zero = 0, one = 0;

    // Stores the total deletions performed
    var count = 0;

    // Traverse the array A[]
    for(var i = 0; i < N; i++)
    {
        if (A[i] == 0)
        {
            zero++;
        }
        else
        {
            one++;
        }
    }

    // Traverse array B[]
    for(var i = 0; i < N; i++)
    {

        // If the B[i] is 0 and zero is
        // greater than 0
        if (B[i] == 0 && zero > 0)
        {

            // Increment count by 1
            count++;

            // Decrement zero by 1
            zero--;
        }

        // Else if the B[i] is 1 and one is
        // greater than 0
        else if (B[i] == 1 && one > 0)
        {

            // Increment count by 1
            count++;

            // Decrement one by 1
            one--;
        }

        // Otherwise
        else
        {
            break;
        }
    }

    // Return the answer
    return N - count;
}

// Driver Code
    // Given Input
    var A = [ 1, 0, 1, 1, 1, 1 ];
    var B = [ 1, 1, 0, 1, 0, 1 ];
    var N = 6;

    // Function Call
    minimumSizeAfterDeletion(A, B, N);
    document.write(minimumSizeAfterDeletion(A, B, N));

// This code is contributed by shivanisinghss2110
</script>
```

**Output**

```
2
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)
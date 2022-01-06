# 由给定范围内的元素组成的字典上最大的 N 长度双音素序列

> 原文:[https://www . geeksforgeeks . org/按字典顺序排列的最大 n 长度双音素序列-由给定范围的元素组成/](https://www.geeksforgeeks.org/lexicographically-largest-n-length-bitonic-sequence-made-up-of-elements-from-given-range/)

给定三个整数 **N** 、**低**和**高**，任务是找到字典上最大的[双音素序列](https://www.geeksforgeeks.org/program-to-check-if-an-array-is-bitonic-or-not/)，该序列由位于范围**【低，高】**中的 **N** 元素组成。如果无法生成这样的序列，则打印**“不可能”**。

**示例:**

> **输入:** N = 5，low = 2，high = 6
> **输出:** 5 6 5 4 3
> **解释:**
> 序列{arr[0]，arr[1]}是严格递增后剩余元素严格递减的序列。该序列是字典中最大的可能序列，所有元素都在[2，6]范围内，并且该序列的长度为 5。
> 
> **输入:** N = 10，低= 4，高= 10
> T3】输出: 7 8 9 10 9 8 7 6 5 4

**方法:**想法是在结果序列中找到合适的**高**指数，然后在序列中相邻元素之间保持 **1** 的差异，使得所形成的双音素序列是字典上最大的可能。按照以下步骤解决问题:

*   初始化一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **A[]** ，以存储结果序列。
*   初始化一个变量 **high_index = -1** 将 **high** 的索引存储在 **A[]** 中，并设置**high _ index = N–(high–low+1)**。
*   如果**高 _ 指数****>****(N–1)/2**，则剩余的 **N/2** 元素不能按照严格递增的顺序放置。所以，打印“不可能”。
*   否则，请执行以下步骤:
    *   如果**高指数≤ 0** ，则设置**高指数= 1** ，因为开始时必须有严格的递增顺序。
    *   保持严格的递减顺序，从值**高**开始，与范围**【高 _ 指数，0】**相差 **1** 。
    *   从数值**(高-1)**开始，保持严格的递减顺序，与范围**【高 _ 指数+ 1，N-1】**相差 **1** 。
*   完成以上步骤后，打印数组 **A[]** 中的所有元素。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the lexicographically
// largest bitonic sequence of size N
// elements lies in the range[low, high]
void LargestArray(int N, int low, int high)
{
    // Store index of highest element
    int high_index = N - (high - low + 1);

    // If high_index > (N-1)/2, then
    // remaining N/2 elements cannot
    // be placed in bitonic order
    if (high_index > (N - 1) / 2) {
        cout << "Not Possible";
        return;
    }

    // If high_index <= 0, then
    // set high_index as 1
    if (high_index <= 0)
        high_index = 1;

    // Stores the resultant sequence
    int A[N];

    // Store the high value
    int temp = high;

    // Maintain strictly decreasing
    // sequence from index high_index
    // to 0 starting with temp
    for (int i = high_index; i >= 0; i--) {

        // Store the value and decrement
        // the temp variable by 1
        A[i] = temp--;
    }

    // Maintain the strictly decreasing
    // sequence from index high_index + 1
    // to N - 1 starting with high - 1
    high -= 1;

    for (int i = high_index + 1; i < N; i++)

        // Store the value and decrement
        // high by 1
        A[i] = high--;

    // Print the resultant sequence
    for (int i = 0; i < N; i++) {
        cout << A[i] << ' ';
    }
}

// Driver Code
int main()
{
    int N = 5, low = 2, high = 6;

    // Function Call
    LargestArray(N, low, high);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to find the lexicographically
// largest bitonic sequence of size N
// elements lies in the range[low, high]
static void LargestArray(int N, int low,
                         int high)
{

    // Store index of highest element
    int high_index = N - (high - low + 1);

    // If high_index > (N-1)/2, then
    // remaining N/2 elements cannot
    // be placed in bitonic order
    if (high_index > (N - 1) / 2)
    {
        System.out.print("Not Possible");
        return;
    }

    // If high_index <= 0, then
    // set high_index as 1
    if (high_index <= 0)
        high_index = 1;

    // Stores the resultant sequence
    int[] A = new int[N];

    // Store the high value
    int temp = high;

    // Maintain strictly decreasing
    // sequence from index high_index
    // to 0 starting with temp
    for(int i = high_index; i >= 0; i--)
    {

        // Store the value and decrement
        // the temp variable by 1
        A[i] = temp--;
    }

    // Maintain the strictly decreasing
    // sequence from index high_index + 1
    // to N - 1 starting with high - 1
    high -= 1;

    for(int i = high_index + 1; i < N; i++)

        // Store the value and decrement
        // high by 1
        A[i] = high--;

    // Print the resultant sequence
    for(int i = 0; i < N; i++)
    {
        System.out.print(A[i] + " ");
    }
}

// Driver Code
public static void main(String[] args)
{
    int N = 5, low = 2, high = 6;

    // Function Call
    LargestArray(N, low, high);
}
}

// This code is contributed by susmitakundugoaldanga
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the lexicographically
# largest bitonic sequence of size N
# elements lies in the range[low, high]
def LargestArray(N, low, high):

    # Store index of highest element
    high_index = N - (high - low + 1)

    # If high_index > (N-1)/2, then
    # remaining N/2 elements cannot
    # be placed in bitonic order
    if (high_index > (N - 1) // 2):
        print("Not Possible")
        return

    # If high_index <= 0, then
    # set high_index as 1
    if (high_index <= 0):
        high_index = 1

    # Stores the resultant sequence
    A = [0] * N

    # Store the high value
    temp = high

    # Maintain strictly decreasing
    # sequence from index high_index
    # to 0 starting with temp
    for i in range(high_index, -1, -1):

        # Store the value and decrement
        # the temp variable by 1
        A[i] = temp
        temp = temp - 1

    # Maintain the strictly decreasing
    # sequence from index high_index + 1
    # to N - 1 starting with high - 1
    high -= 1

    for i in range(high_index + 1, N):

        # Store the value and decrement
        # high by 1
        A[i] = high
        high = high - 1

    # Print the resultant sequence
    for i in range(N):
        print(A[i], end = " ")

# Driver Code
N = 5
low = 2
high = 6

# Function Call
LargestArray(N, low, high)

# This code is contributed by code_hunt
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to find the lexicographically
// largest bitonic sequence of size N
// elements lies in the range[low, high]
static void LargestArray(int N, int low,
                        int high)
{

    // Store index of highest element
    int high_index = N - (high - low + 1);

    // If high_index > (N-1)/2, then
    // remaining N/2 elements cannot
    // be placed in bitonic order
    if (high_index > (N - 1) / 2)
    {
        Console.Write("Not Possible");
        return;
    }

    // If high_index <= 0, then
    // set high_index as 1
    if (high_index <= 0)
        high_index = 1;

    // Stores the resultant sequence
    int[] A = new int[N];

    // Store the high value
    int temp = high;

    // Maintain strictly decreasing
    // sequence from index high_index
    // to 0 starting with temp
    for(int i = high_index; i >= 0; i--)
    {

        // Store the value and decrement
        // the temp variable by 1
        A[i] = temp--;
    }

    // Maintain the strictly decreasing
    // sequence from index high_index + 1
    // to N - 1 starting with high - 1
    high -= 1;

    for(int i = high_index + 1; i < N; i++)

        // Store the value and decrement
        // high by 1
        A[i] = high--;

    // Print the resultant sequence
    for(int i = 0; i < N; i++)
    {
        Console.Write(A[i] + " ");
    }
}

// Driver Code
public static void Main(String[] args)
{
    int N = 5, low = 2, high = 6;

    // Function Call
    LargestArray(N, low, high);
}
}

// This code is contributed by shivanisinghss2110
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to find the lexicographically
// largest bitonic sequence of size N
// elements lies in the range[low, high]
function LargestArray(N, low, high)
{

    // Store index of highest element
    let high_index = N - (high - low + 1);

    // If high_index > (N-1)/2, then
    // remaining N/2 elements cannot
    // be placed in bitonic order
    if (high_index > (N - 1) / 2)
    {
        document.write("Not Possible");
        return;
    }

    // If high_index <= 0, then
    // set high_index as 1
    if (high_index <= 0)
        high_index = 1;

    // Stores the resultant sequence
    let A = [];

    // Store the high value
    let temp = high;

    // Maintain strictly decreasing
    // sequence from index high_index
    // to 0 starting with temp
    for(let i = high_index; i >= 0; i--)
    {

        // Store the value and decrement
        // the temp variable by 1
        A[i] = temp--;
    }

    // Maintain the strictly decreasing
    // sequence from index high_index + 1
    // to N - 1 starting with high - 1
    high -= 1;

    for(let i = high_index + 1; i < N; i++)

        // Store the value and decrement
        // high by 1
        A[i] = high--;

    // Print the resultant sequence
    for(let i = 0; i < N; i++)
    {
        document.write(A[i] + " ");
    }
}

// Driver Code

      let N = 5, low = 2, high = 6;

    // Function Call
    LargestArray(N, low, high);

</script>
```

**Output:** 

```
5 6 5 4 3
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)
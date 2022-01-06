# 计算大小至少为 3 的数组中的算术序列

> 原文:[https://www . geeksforgeeks . org/count-the-the-算术-序列-in-array-size-3/](https://www.geeksforgeeks.org/count-the-arithmetic-sequences-in-the-array-of-size-at-least-3/)

给定一个大小为 **N** 的数组 **arr[]** ，任务是找出数组中所有[算术序列](https://www.geeksforgeeks.org/count-arithmetic-progression-subsequences-array/)的计数。

**示例:**

> **输入:** arr = [1，2，3，4]
> **输出:** 3
> **解释:**
> arr 中的算术序列是[1，2，3]，[2，3，4]和[1，2，3，4]本身。
> 
> **输入:** arr = [1，3，5，6，7，8]
> **输出:** 4
> **解释:**
> arr 中的算术序列为[1，3，5]，[5，6，7]，[5，6，7，8]和[6，7，8]。

**天真的方法:**

*   运行两个循环，检查每个长度至少为 3 的序列。
*   如果序列是[算术序列](https://www.geeksforgeeks.org/arithmetic-progression/)，则答案增加 1。
*   最后，返回大小至少为 3 的所有算术子阵列的计数。

***时间复杂度:O(N<sup>2</sup>)**T5】*

**有效方法:**我们将使用[动态编程](https://www.geeksforgeeks.org/dynamic-programming/)方法来保持所有算术序列的计数直到任何位置。

*   初始化一个变量，用 **0** 重置。它将存储序列的计数。
*   初始化一个变量，用 **0** 计数。它将存储序列的大小减 2。
*   如果当前元素形成算术序列，则增加 count 的值，否则使其为零。
*   如果当前元素 L[i]正在用 L[i-1]和 L[i-2]生成一个算术序列，那么直到第 I 次迭代的算术序列的数量由下式给出:

> res = 真 + 计数

*   最后，返回 **res** 变量。

下面是上述方法的实现:

## C++

```
// C++ program to find all arithmetic
// sequences of size atleast 3

#include <bits/stdc++.h>
using namespace std;

// Function to find all arithmetic
// sequences of size atleast 3
int numberOfArithmeticSequences(int L[], int N)
{

    // If array size is less than 3
    if (N <= 2)
        return 0;

    // Finding arithmetic subarray length
    int count = 0;

    // To store all arithmetic subarray
    // of length at least 3
    int res = 0;

    for (int i = 2; i < N; ++i) {

        // Check if current element makes
        // arithmetic sequence with
        // previous two elements
        if (L[i] - L[i - 1] == L[i - 1] - L[i - 2]) {
            ++count;
        }

        // Begin with a new element for
        // new arithmetic sequences
        else {
            count = 0;
        }

        // Accumulate result in till i.
        res += count;
    }

    // Return final count
    return res;
}

// Driver code
int main()
{

    int L[] = { 1, 3, 5, 6, 7, 8 };
    int N = sizeof(L) / sizeof(L[0]);

    // Function to find arithmetic sequences
    cout << numberOfArithmeticSequences(L, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find all arithmetic
// sequences of size atleast 3

class GFG{

// Function to find all arithmetic
// sequences of size atleast 3
static int numberOfArithmeticSequences(int L[], int N)
{

    // If array size is less than 3
    if (N <= 2)
        return 0;

    // Finding arithmetic subarray length
    int count = 0;

    // To store all arithmetic subarray
    // of length at least 3
    int res = 0;

    for (int i = 2; i < N; ++i) {

        // Check if current element makes
        // arithmetic sequence with
        // previous two elements
        if (L[i] - L[i - 1] == L[i - 1] - L[i - 2]) {
            ++count;
        }

        // Begin with a new element for
        // new arithmetic sequences
        else {
            count = 0;
        }

        // Accumulate result in till i.
        res += count;
    }

    // Return final count
    return res;
}

// Driver code
public static void main(String[] args)
{

    int L[] = { 1, 3, 5, 6, 7, 8 };
    int N = L.length;

    // Function to find arithmetic sequences
    System.out.print(numberOfArithmeticSequences(L, N));

}
}

// This code contributed by sapnasingh4991
```

## 蟒蛇 3

```
# Python3 program to find all arithmetic
# sequences of size atleast 3

# Function to find all arithmetic
# sequences of size atleast 3
def numberOfArithmeticSequences(L, N) :

    # If array size is less than 3
    if (N <= 2) :
        return 0

    # Finding arithmetic subarray length
    count = 0

    # To store all arithmetic subarray
    # of length at least 3
    res = 0

    for i in range(2,N):

        # Check if current element makes
        # arithmetic sequence with
        # previous two elements
        if ( (L[i] - L[i - 1]) == (L[i - 1] - L[i - 2])) :
            count += 1

        # Begin with a new element for
        # new arithmetic sequences
        else :
            count = 0

        # Accumulate result in till i.
        res += count

    # Return final count
    return res

# Driver code

L = [ 1, 3, 5, 6, 7, 8 ]
N = len(L)

# Function to find arithmetic sequences
print(numberOfArithmeticSequences(L, N))

# This code is contributed by Sanjit_Prasad
```

## C#

```
// C# program to find all arithmetic
// sequences of size atleast 3
using System;

class GFG{

// Function to find all arithmetic
// sequences of size atleast 3
static int numberOfArithmeticSequences(int []L,
                                       int N)
{

    // If array size is less than 3
    if (N <= 2)
        return 0;

    // Finding arithmetic subarray length
    int count = 0;

    // To store all arithmetic subarray
    // of length at least 3
    int res = 0;

    for(int i = 2; i < N; ++i)
    {

       // Check if current element makes
       // arithmetic sequence with
       // previous two elements
       if (L[i] - L[i - 1] ==
           L[i - 1] - L[i - 2])
       {
           ++count;
       }

       // Begin with a new element for
       // new arithmetic sequences
       else
       {
           count = 0;
       }

       // Accumulate result in till i.
       res += count;
    }

    // Return readonly count
    return res;
}

// Driver code
public static void Main(String[] args)
{
    int []L = { 1, 3, 5, 6, 7, 8 };
    int N = L.Length;

    // Function to find arithmetic sequences
    Console.Write(numberOfArithmeticSequences(L, N));
}
}

// This code is contributed by amal kumar choubey
```

## java 描述语言

```
<script>
//Javascript program to find all arithmetic
// sequences of size atleast 3

 // Function to find all arithmetic
// sequences of size atleast 3
function numberOfArithmeticSequences( L, N)
{

    // If array size is less than 3
    if (N <= 2)
        return 0;

    // Finding arithmetic subarray length
    var count = 0;

    // To store all arithmetic subarray
    // of length at least 3
    var res = 0;

    for (var i = 2; i < N; ++i) {

        // Check if current element makes
        // arithmetic sequence with
        // previous two elements
        if (L[i] - L[i - 1] == L[i - 1] - L[i - 2]) {
            ++count;
        }

        // Begin with a new element for
        // new arithmetic sequences
        else {
            count = 0;
        }

        // Accumulate result in till i.
        res += count;
    }

    // Return final count
    return res;
}

var L = [ 1, 3, 5, 6, 7, 8 ];
    var N = L.length;

// Function to find arithmetic sequences
 document.write(numberOfArithmeticSequences(L, N));

  // This code contributed by SoumikMondal
</script>
```

**Output:** 

```
4
```

***时间复杂度:**O(N)*T4】
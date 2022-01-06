# 计算用给定数组的偶积构造数组的方法，使得相同索引元素的绝对差最多为 1

> 原文:[https://www . geeksforgeeks . org/count-way-构造给定数组的偶积数组-这样，相同索引元素的绝对差最多为 1/](https://www.geeksforgeeks.org/count-ways-to-construct-array-with-even-product-from-given-array-such-that-absolute-difference-of-same-indexed-elements-is-at-most-1/)

给定一个大小为 **N** 的数组**A【】**，任务是计算构造大小为 **N** 的数组**B【】**的方式数，使得相同索引元素的绝对差必须小于或等于 **1** ，即[**ABS(A[I]–B[I])**](https://www.geeksforgeeks.org/program-to-find-absolute-value-of-a-given-number/)**≤1**，以及元素的乘积

**示例:**

> **输入:** A[] = { 2，3 }
> **输出:** 7
> **解释:**
> 数组 B[]的可能值为{ { 1，2 }、{ 1，4 }、{ 2，2 }、{ 2，4 }、{ 3，2 }、{ 3，4 } }
> 因此，需要的输出为 7。
> 
> **输入:** A[] = { 90，52，56，71，44，8，13，30，57，84 }
> **输出:** 58921

**方法:**思路是先数一数构造数组的方式， **B[]** 这样**ABS(A[I]–B[I])<= 1**然后去掉那些元素乘积不是[偶数](https://www.geeksforgeeks.org/check-whether-given-number-even-odd/)的数组。按照以下步骤解决问题:

*   **B[i]** 的可能值，使得**腹肌(A[I]–B[I])<= 1**为 **{ A[i]，A[i] + 1，A[I]–1 }**。因此，构造数组的方式总数 **B[]** 使得**ABS(A[I]–B[I])**小于或等于 **1** 为 **3 <sup>N</sup>** 。
*   [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)并将[偶数](https://www.geeksforgeeks.org/check-whether-given-number-even-odd/)的计数存入数组 **A[]** 说， **X** 。
*   如果 **A[i]** 是偶数，那么**(A[I]–1)**和 **(A[i] + 1)** 一定是[奇数](https://www.geeksforgeeks.org/check-whether-given-number-even-odd/)。因此，构造数组的方法总数，乘积不是偶数的 **B[]** 是 **2 <sup>X</sup>** 。
*   最后，打印(**3<sup>N</sup>–2<sup>X</sup>**的值)。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find count the ways to construct
// an array, B[] such that abs(A[i] - B[i]) <=1
// and product of elements of B[] is even
void cntWaysConsArray(int A[], int N)
{

    // Stores count of arrays B[] such
    // that abs(A[i] - B[i]) <=1
    int total = 1;

    // Stores count of arrays B[] whose
    // product of elements is not even
    int oddArray = 1;

    // Traverse the array
    for (int i = 0; i < N; i++) {

        // Update total
        total = total * 3;

        // If A[i] is an even number
        if (A[i] % 2 == 0) {

            // Update oddArray
            oddArray *= 2;
        }
    }

    // Print 3^N - 2^X
    cout << total - oddArray << "\n";
}

// Driver Code
int main()
{
    int A[] = { 2, 4 };
    int N = sizeof(A) / sizeof(A[0]);

    cntWaysConsArray(A, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to implement the
// above approach
import java.util.*;
class GFG
{

// Function to find count the ways to construct
// an array, B[] such that abs(A[i] - B[i]) <=1
// and product of elements of B[] is even
static void cntWaysConsArray(int A[], int N)
{

    // Stores count of arrays B[] such
    // that abs(A[i] - B[i]) <=1
    int total = 1;

    // Stores count of arrays B[] whose
    // product of elements is not even
    int oddArray = 1;

    // Traverse the array
    for (int i = 0; i < N; i++)
    {

        // Update total
        total = total * 3;

        // If A[i] is an even number
        if (A[i] % 2 == 0)
        {

            // Update oddArray
            oddArray *= 2;
        }
    }

    // Print 3^N - 2^X
    System.out.println( total - oddArray);
}

// Driver Code
public static void main(String[] args)
{
    int A[] = { 2, 4 };
    int N = A.length;
    cntWaysConsArray(A, N);
}
}

// This code is contributed by code_hunt.
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to find count the ways to construct
# an array, B[] such that abs(A[i] - B[i]) <=1
# and product of elements of B[] is even
def cntWaysConsArray(A, N) :

    # Stores count of arrays B[] such
    # that abs(A[i] - B[i]) <=1
    total = 1;

    # Stores count of arrays B[] whose
    # product of elements is not even
    oddArray = 1;

    # Traverse the array
    for i in range(N) :

        # Update total
        total = total * 3;

        # If A[i] is an even number
        if (A[i] % 2 == 0) :

            # Update oddArray
            oddArray *= 2;

    # Print 3^N - 2^X
    print(total - oddArray);

# Driver Code
if __name__ == "__main__" :
    A = [ 2, 4 ];
    N = len(A);
    cntWaysConsArray(A, N);

    # This code is contributed by AnkThon
```

## C#

```
// C# program to implement the
// above approach
using System;

class GFG{

// Function to find count the ways to construct
// an array, []B such that abs(A[i] - B[i]) <=1
// and product of elements of []B is even
static void cntWaysConsArray(int []A, int N)
{

    // Stores count of arrays []B such
    // that abs(A[i] - B[i]) <=1
    int total = 1;

    // Stores count of arrays []B whose
    // product of elements is not even
    int oddArray = 1;

    // Traverse the array
    for(int i = 0; i < N; i++)
    {

        // Update total
        total = total * 3;

        // If A[i] is an even number
        if (A[i] % 2 == 0)
        {

            // Update oddArray
            oddArray *= 2;
        }
    }

    // Print 3^N - 2^X
    Console.WriteLine(total - oddArray);
}

// Driver Code
public static void Main(String[] args)
{
    int []A = { 2, 4 };
    int N = A.Length;

    cntWaysConsArray(A, N);
}
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>

// Javascript Program to implement the
// above approach

// Function to find count the ways to construct
// an array, B such that abs(A[i] - B[i]) <=1
// and product of elements of B is even
function cntWaysConsArray(A, N)
{

    // Stores count of arrays B such
    // that abs(A[i] - B[i]) <=1
    var total = 1;

    // Stores count of arrays B whose
    // product of elements is not even
    var oddArray = 1;

    // Traverse the array
    for(i = 0; i < N; i++)
    {

        // Update total
        total = total * 3;

        // If A[i] is an even number
        if (A[i] % 2 == 0)
        {

            // Update oddArray
            oddArray *= 2;
        }
    }

    // Print var 3^N - 2^X
    document.write(total - oddArray);
}

// Driver Code
var A = [ 2, 4 ];
var N = A.length;

cntWaysConsArray(A, N);

// This code is contributed by umadevi9616

</script>
```

**Output:** 

```
5
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)
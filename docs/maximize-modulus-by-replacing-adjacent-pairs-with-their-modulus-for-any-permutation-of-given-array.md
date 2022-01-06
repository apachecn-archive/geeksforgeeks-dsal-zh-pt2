# 对于给定数组的任何排列，通过用相邻对的模数替换相邻对来最大化模数

> 原文:[https://www . geeksforgeeks . org/通过用给定数组的任意排列的模替换相邻对来最大化模/](https://www.geeksforgeeks.org/maximize-modulus-by-replacing-adjacent-pairs-with-their-modulus-for-any-permutation-of-given-array/)

给定一个由不同元素组成的数组 **A[]** ，任务是从第一个元素开始，为给定数组的任何可能的排列[，在用它们的模数重复替换相邻元素之后，获得剩余的最大可能的模数值。](https://www.geeksforgeeks.org/iterative-approach-to-print-all-permutations-of-an-array/)

> **([(a[1]mod a[2])mod a[3])……。)修改 a〔n〕〔t1〕**

**示例:**

> **输入:** A[] = {7，10，12}
> **输出:** 7
> **解释:**给定数组所有排列中给定表达式的所有可能值如下:
> {7，10，12} = ((7 % 10) % 12) = 7
> {10，12 ^ 7 } =((10% 12)% 7)= 3
> { 7，12，10 } = = 12} = ((10 % 7) % 12) = 3
> {12，7，10} = ((12 % 7) % 10) = 5
> {12，10，7} = ((12 % 10) % 7) = 2
> 因此，最大可能值为 7。
> 
> **输入:** A[] = {20，30}
> **输出:** 20
> **解释:**
> 给定数组所有排列的最大可能值是 20。

**天真法:**解决问题最简单的方法是[生成给定数组的所有置换](https://www.geeksforgeeks.org/iterative-approach-to-print-all-permutations-of-an-array/)并为所有置换找到给定表达式的值。最后，打印得到的表达式的最大值。
***时间复杂度:** O(N * N！)*
***辅助空间:** O(N)*

**高效方法:**要优化上述方法，需要进行以下观察:

> *   For any arrangement **a <sub>1</sub> ... a <sub>n</sub>** , the value of the expression always lies in the range **[0, min (a <sub>2</sub> ... a <sub>n</sub> )-1] 【**
> *   Considering that **k** is the smallest element in the array, the value of the expression will always be k for the arrangement with k as the first element.
> *   For all other permutations, the value of the expression will always be less than **k** , as shown in the above example. Therefore, **k** is the maximum possible value of the expression with arbitrary array.
> *   Therefore, the maximum possible value will always be equal to the smallest element of the array.

因此，要解决问题，只需[遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)和[找到数组](https://www.geeksforgeeks.org/maximum-and-minimum-in-an-array/)中存在的最小元素，并将其打印为所需答案。

下面是上述方法的实现:

## C++

```
// C++ Program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum
// of two numbers
int min(int a, int b)
{
    return (a > b) ? b : a;
}

// Function to find the maximum value
// possible of the given expression
// from all permutations of the array
int maximumModuloValue(int A[], int n)
{
    // Stores the minimum value
    // from the array
    int mn = INT_MAX;
    for (int i = 0; i < n; i++) {
        mn = min(A[i], mn);
    }

    // Return the answer
    return mn;
}

// Driver Code
int main()
{
    int A[] = { 7, 10, 12 };

    int n = (sizeof(A) / (sizeof(A[0])));

    cout << maximumModuloValue(A, n)
         << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to implement
// the above approach
import java.io.*;
class GFG{

    // Function to find the maximum value
    // possible of the given expression
    // from all permutations of the array
    static int maximumModuloValue(int A[], int n)
    {
        // Stores the minimum value
        // from the array
        int mn = Integer.MAX_VALUE;

        for (int i = 0; i < n; i++)
        {
            mn = Math.min(A[i], mn);
        }

        // Return the answer
        return mn;
    }

    // Driver Code
    public static void main(String[] args)
    {
        int A[] = {7, 10, 12};
        int n = A.length;
        System.out.println(maximumModuloValue(A, n));
    }
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach
import sys

# Function to find the maximum value
# possible of the given expression
# from all permutations of the array
def maximumModuloValue(A, n):

    # Stores the minimum value
    # from the array
    mn = sys.maxsize
    for i in range(n):
        mn = min(A[i], mn)

    # Return the answer
    return mn

# Driver Code

# Given array arr[]
A = [ 7, 10, 12 ]

n = len(A)

# Function call
print(maximumModuloValue(A, n))

# This code is contributed by Shivam Singh
```

## C#

```
// C# Program to implement
// the above approach
using System;
class GFG{

  // Function to find the maximum value
  // possible of the given expression
  // from all permutations of the array
  static int maximumModuloValue(int []A,
                                int n)
  {
    // Stores the minimum value
    // from the array
    int mn = int.MaxValue;

    for (int i = 0; i < n; i++)
    {
      mn = Math.Min(A[i], mn);
    }

    // Return the answer
    return mn;
  }

  // Driver Code
  public static void Main(String[] args)
  {
    int []A = {7, 10, 12};
    int n = A.Length;
    Console.WriteLine(maximumModuloValue(A, n));
  }
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>
// javascript Program to implement
// the above approach

    // Function to find the maximum value
    // possible of the given expression
    // from all permutations of the array
    function maximumModuloValue(A , n) {
        // Stores the minimum value
        // from the array
        var mn = Number.MAX_VALUE;

        for (i = 0; i < n; i++) {
            mn = Math.min(A[i], mn);
        }

        // Return the answer
        return mn;
    }

    // Driver Code

        var A = [ 7, 10, 12 ];
        var n = A.length;
        document.write(maximumModuloValue(A, n));

// This code contributed by umadevi9616
</script>
```

**Output:** 

```
7
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)
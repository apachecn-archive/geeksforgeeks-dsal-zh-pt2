# 计算生成的大小为 N * N 的矩阵中某个元素的出现次数，使得每个元素等于其索引的乘积

> 原文:[https://www . geeksforgeeks . org/count-一个元素在 n-n-n-生成的大小矩阵中的出现次数，使得每个元素等于其索引的乘积/](https://www.geeksforgeeks.org/count-occurrences-of-an-element-in-a-matrix-of-size-n-n-generated-such-that-each-element-is-equal-to-product-of-its-indices/)

给定两个正整数 **N** 和 **X** ，任务是计算给定整数 **X** 在**N**-长度[正方形矩阵](https://www.geeksforgeeks.org/multidimensional-arrays-c-cpp/)中的出现次数，该矩阵的每个元素都等于其行和列索引的乘积(*基于 1 的索引*)。

**示例:**

> **输入:** N = 5，X = 6
> **输出:** 2
> **解释:**
> 形成的 2D 数组等于:
> 1 2 3 4 5
> 2 4 6 8 10
> 3 6 9 12 15
> 4 8 12 16 20
> 5 10 15 20 25
> 生成的数组中元素 X(= 6)出现了 2 次。
> 
> **输入:** N = 7，X = 12
> T3】输出: 4

**朴素方法:**最简单的方法是通过将行索引和列索引相乘来构造给定的矩阵，以获得每个矩阵元素。生成矩阵后，打印矩阵中 **X** 的出现次数。

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(N <sup>2</sup> )*

**高效法:**对上述方法进行优化，思路是基于矩阵中每个元素都是 2 个数字的[积的观察。因此，通过检查](https://www.geeksforgeeks.org/product-2-numbers-using-recursion/)[的方式数 **X** 可以表示为 2 个数字的乘积](https://www.geeksforgeeks.org/ways-express-number-product-two-different-factors/)，并选择那些位于范围**【1，N】**内的对，给出结果。按照以下步骤解决问题:

*   初始化一个变量，比如**计数**，将 **X** 的出现次数存储在生成的矩阵中。
*   [使用变量 **i** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【1，√X】**，并执行以下步骤:
    *   如果 **i** 的值除以 **X** ，将通过将 **X** 除以 **i** 得到的商存储在一个变量中，比如 **b** 。
    *   如果 **i** 和 **b** 的值都在**【1，N】**的范围内，则执行以下步骤:
        *   检查 **i** 是否等于 **b** 。如果发现是真的，说明 **X** 是一个[完美的正方形](https://www.geeksforgeeks.org/check-if-a-given-number-is-a-perfect-square-using-binary-search/)，行列会出现一次。因此，将**计数**增加 **1** 。
        *   否则，这意味着它们将出现两次，一次在一行，另一次在一列。因此，将**计数**增加 **2** 。
*   完成上述步骤后，打印**计数**的值作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include<bits/stdc++.h>
using namespace std;

// Function to count the occurrences
// of X in the generated square matrix
int countOccurrences(int N, int X)
{

    // Stores the required result
    int count = 0;

    //Iterate upto square root of X
    for (int i = 1; i < sqrt(X); i++)
    {

        // Check if i divides X
        if (X % i == 0)
        {

            // Store the quotient obtained
            // on dividing X by i
            int a = i;
            int b = X / i;

            // If both the numbers fall in
            // the range, update count
            if (a <= N && b <= N)
            {
                if (a == b)
                    count += 1;
                else
                    count += 2;
            }
        }
    }

    // Return the result
    return count;
}

// Driver code
int main()
{

    // Given N and X
    int N = 7;
    int X = 12;

    // Function Call
    cout << countOccurrences(N, X);

    return 0;
}

// This code is contributed by mohit kumar 29
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.lang.*;
import java.util.*;

class GFG {

  // Function to count the occurrences
  // of X in the generated square matrix
  static int countOccurrences(int N, int X)
  {

    // Stores the required result
    int count = 0;

    // Iterate upto square root of X
    for (int i = 1; i < Math.sqrt(X); i++) {

      // Check if i divides X
      if (X % i == 0) {

        // Store the quotient obtained
        // on dividing X by i
        int a = i;
        int b = X / i;

        // If both the numbers fall in
        // the range, update count
        if (a <= N && b <= N) {
          if (a == b)
            count += 1;
          else
            count += 2;
        }
      }
    }

    // Return the result
    return count;
  }

  // Driver code
  public static void main(String[] args)
  {

    // Given N and X
    int N = 7;
    int X = 12;

    // Function Call
    System.out.println(countOccurrences(N, X));
  }
}

// This code is contributed by Kingsh.
```

## 蟒蛇 3

```
# Python3 program for the above approach
from math import sqrt

# Function to count the occurrences
# of X in the generated square matrix
def countOccurrences(N, X):

    # Stores the required result
    count = 0

    # Iterate upto square root of X
    for i in range(1, int(sqrt(X))+1):

        # Check if i divides X
        if X % i == 0:

            # Store the quotient obtained
            # on dividing X by i
            a = i
            b = X//i

            # If both the numbers fall in
            # the range, update count
            if a <= N and b <= N:
                if a == b:
                    count += 1
                else:
                    count += 2

    # Return the result
    return count

# Driver Code
if __name__ == '__main__':

    # Given N and X
    N = 7
    X = 12

    # Function Call
    print(countOccurrences(N, X))
```

## C#

```
// C# program for above approach
using System;
public class GFG
{

  // Function to count the occurrences
  // of X in the generated square matrix
  static int countOccurrences(int N, int X)
  {

    // Stores the required result
    int count = 0;

    // Iterate upto square root of X
    for (int i = 1; i < Math.Sqrt(X); i++) {

      // Check if i divides X
      if (X % i == 0) {

        // Store the quotient obtained
        // on dividing X by i
        int a = i;
        int b = X / i;

        // If both the numbers fall in
        // the range, update count
        if (a <= N && b <= N) {
          if (a == b)
            count += 1;
          else
            count += 2;
        }
      }
    }

    // Return the result
    return count;
  }

  // Driver code
  public static void Main(String[] args)
  {
    // Given N and X
    int N = 7;
    int X = 12;

    // Function Call
    Console.Write(countOccurrences(N, X));
  }
}

// This code is contributed by code_hunt.
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to count the occurrences
// of X in the generated square matrix
function countOccurrences(N, X)
{

    // Stores the required result
    var count = 0;

    //Iterate upto square root of X
    for (var i = 1; i < Math.sqrt(X); i++)
    {

        // Check if i divides X
        if (X % i == 0)
        {

            // Store the quotient obtained
            // on dividing X by i
            var a = i;
            var b = X / i;

            // If both the numbers fall in
            // the range, update count
            if (a <= N && b <= N)
            {
                if (a == b)
                    count += 1;
                else
                    count += 2;
            }
        }
    }

    // Return the result
    return count;
}

// Driver code
// Given N and X
var N = 7;
var X = 12;

// Function Call
document.write( countOccurrences(N, X));

</script>
```

**Output:** 

```
4
```

***时间复杂度:** O(√X)*
***辅助空间:** O(1)*
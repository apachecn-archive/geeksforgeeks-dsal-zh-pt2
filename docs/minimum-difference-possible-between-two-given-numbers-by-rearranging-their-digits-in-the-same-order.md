# 通过以相同顺序重新排列两个给定数字之间的最小可能差异

> 原文:[https://www . geeksforgeeks . org/通过按相同顺序重新排列两个给定数字之间的最小可能差异/](https://www.geeksforgeeks.org/minimum-difference-possible-between-two-given-numbers-by-rearranging-their-digits-in-the-same-order/)

给定两个 **N** 位正整数 **X** 和 **Y** ，任务是通过以相同的顺序重新排列两个整数的位数来找到两个整数之间的最小绝对差。

**示例:**

> ***输入:** X = 5181* ，Y = 3663
> ***输出:** 1482*
> ***解释:***
> 按照(3，2，4，1)的顺序重新排列两个给定整数的数字，将 X 和 Y 的值分别修改为 8115 和 6633。
> 因此，两者的绝对差值为(8115–6633)= 1482，这是可能的最小差值。
> 
> ***输入:** X = 37198* ，Y = 44911
> T5**输出:** 1278

**方法:**给定的问题可以通过求 **X** 和 **Y** 的每个[排列](https://www.geeksforgeeks.org/write-a-c-program-to-print-all-permutations-of-a-given-string/)之间的绝对差来解决，这两个排列具有相同的数字重排顺序。按照以下步骤解决问题:

*   初始化一个 [2D 数组](https://www.geeksforgeeks.org/multidimensional-arrays-c-cpp/)**arr【2】【N】**，分别存储数字 **X** 和 **Y** 的位数。
*   初始化一个数组，比如说 **P[]** ，存储数字【0，N–1】的[排列。](https://www.geeksforgeeks.org/generate-a-random-permutation-of-1-to-n/)
*   初始化一个变量，比如说 **minDIff** ，它存储了 **X** 和 **Y** 之间的最小差值。
*   [遍历 **P[]** 的所有可能的排列](https://www.geeksforgeeks.org/iterative-approach-to-print-all-permutations-of-an-array/)，并执行以下步骤:
    *   根据排列重新排列 **X** 和 **Y** 的数字，并将它们之间的绝对差值存储在一个变量中，比如**差值**。
    *   完成上述步骤后，将 **minDIff** 的值更新为 **minDiff** 和**差值**的最小值。
*   完成以上步骤后，打印 **minDIff** 的值作为最小差值。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find minimum difference
// between X and Y after rearranging
// their digits in the same order
int minDifference(int X, int Y)
{
    // Stores the minimum difference
    int minDiff = INT_MAX;

    // Stores the number X as string
    string x = to_string(X);

    // Stores the number Y as string
    string y = to_string(Y);

    // Stores number of digits
    int n = x.size();

    // Store the digits
    int a[2][n];

    // Traverse the range [0, 1]
    for (int i = 0; i < 2; i++) {

        // Traverse the range [0, N - 1]
        for (int j = 0; j < n; j++) {

            // If the value of i is 0
            if (i == 0)
                a[i][j] = x[j] - '0';

            // Otherwise
            else
                a[i][j] = y[j] - '0';
        }
    }

    // Stores the permutation of [1, N]
    int p[n];

    // Initialize the permutation array
    for (int i = 0; i < n; i++)
        p[i] = i;

    // Generate all possible permutation
    do {

        // Stores the maximum of X and Y
        int xx = INT_MIN;

        // Stores the minimum of X and Y
        int yy = INT_MAX;

        // Traverse the range [0, 1]
        for (int i = 0; i < 2; i++) {

            // Stores the number
            // after rearranging
            int num = 0;

            // Traverse the range [0, N - 1]
            for (int j = 0; j < n; j++)

                // Update the value of num
                num = num * 10 + a[i][p[j]];

            // Update the value of xx
            xx = max(xx, num);

            // Update the value of yy
            yy = min(yy, num);
        }

        // Update the value of minDiff
        minDiff = min(minDiff, xx - yy);

    } while (next_permutation(p, p + n));

    // Return the minimum difference
    return minDiff;
}

// Driver Code
int main()
{
    int X = 37198, Y = 44911;
    cout << minDifference(X, Y);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

import java.util.*;

class GFG{

// Function to find minimum difference
// between X and Y after rearranging
// their digits in the same order
static int minDifference(int X, int Y)
{
    // Stores the minimum difference
    int minDiff = Integer.MAX_VALUE;

    // Stores the number X as String
    String x = String.valueOf(X);

    // Stores the number Y as String
    String y = String.valueOf(Y);

    // Stores number of digits
    int n = x.length();

    // Store the digits
    int [][]a = new int[2][n];

    // Traverse the range [0, 1]
    for (int i = 0; i < 2; i++) {

        // Traverse the range [0, N - 1]
        for (int j = 0; j < n; j++) {

            // If the value of i is 0
            if (i == 0)
                a[i][j] = x.charAt(j) - '0';

            // Otherwise
            else
                a[i][j] = y.charAt(j) - '0';
        }
    }

    // Stores the permutation of [1, N]
    int []p = new int[n];

    // Initialize the permutation array
    for (int i = 0; i < n; i++)
        p[i] = i;

    // Generate all possible permutation
    do {

        // Stores the maximum of X and Y
        int xx = Integer.MIN_VALUE;

        // Stores the minimum of X and Y
        int yy = Integer.MAX_VALUE;

        // Traverse the range [0, 1]
        for (int i = 0; i < 2; i++) {

            // Stores the number
            // after rearranging
            int num = 0;

            // Traverse the range [0, N - 1]
            for (int j = 0; j < n; j++)

                // Update the value of num
                num = num * 10 + a[i][p[j]];

            // Update the value of xx
            xx = Math.max(xx, num);

            // Update the value of yy
            yy = Math.min(yy, num);
        }

        // Update the value of minDiff
        minDiff = Math.min(minDiff, xx - yy);

    } while (next_permutation(p));

    // Return the minimum difference
    return minDiff;
}
static boolean next_permutation(int[] p) {
      for (int a = p.length - 2; a >= 0; --a)
        if (p[a] < p[a + 1])
          for (int b = p.length - 1;; --b)
            if (p[b] > p[a]) {
              int t = p[a];
              p[a] = p[b];
              p[b] = t;
              for (++a, b = p.length - 1; a < b; ++a, --b) {
                t = p[a];
                p[a] = p[b];
                p[b] = t;
              }
              return true;
            }
      return false;
    }
// Driver Code
public static void main(String[] args)
{
    int X = 37198, Y = 44911;
    System.out.print(minDifference(X, Y));

}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program for the above approach
import itertools

# Function to find minimum difference
# between X and Y after rearranging
# their digits in the same order
def minDifference(X, Y):

    # Stores the minimum difference
    minDiff = float("inf")

    # Stores the number X as string
    x = str(X)

    # Stores the number Y as string
    y = str(Y)

    # Stores no of digits
    n = len(x)

    # store the digits
    a = [[0 for j in range(n)]
            for i in range(2)]

    # Traverse the range [0, 1]
    for i in range(0, 2):

        # Traverse the range [0, N - 1]
        for j in range(n):

            # If the value of i is 0
            if i == 0:
                a[i][j] = ord(x[j]) - ord('0')
            elif i == 1:
                a[i][j] = ord(y[j]) - ord('0')

    # Stores the permutation of [1, N]
    p = [0 for i in range(n)]

    # Initialize the permutation array
    for i in range(n):
        p[i] = i

    # Generating all the permutations
    # of p using itertools
    l = itertools.permutations(p, n)

    # Permutations list below stores
    # all the permutations genenerated
    permutations = []
    for i in l:
        permutations.append(list(i))

    p = permutations[0]
    n1 = len(permutations)
    k = 1

    # Generate all possible permutation
    while True:

        # Stores the maximum of X and Y
        xx = float("-inf")

        # Stores the minimum of X and Y
        yy = float("inf")

        # Traverse the range [0, 1]
        for i in range(0, 2):

            # Stores the number
            # after rearranging
            num = 0

            # Traverse the range [0, N - 1]
            for j in range(0, n):

              # Update the value of num
                num = num * 10 + a[i][p[j]]

            # Update the value of xx
            xx = max(xx, num)

            # Update the value of yy
            yy = min(yy, num)

        minDiff = min(minDiff, xx - yy)

        # Break the while loop when we have
        # iterated over all the permutations
        if k >= n1:
            break

        # Use the next permutation
        p = permutations[k]
        k += 1

    # Return the minimum difference
    return minDiff

# Driver code
if __name__ == '__main__':

    X = 37198
    Y = 44911

    print(minDifference(X, Y))

# This code is contributed by MuskanKalra1
```

## C#

```
// C# program for the above approach
using System;
class GFG {

    // Function to find minimum difference
    // between X and Y after rearranging
    // their digits in the same order
    static int minDifference(int X, int Y)
    {
        // Stores the minimum difference
        int minDiff = Int32.MaxValue;

        // Stores the number X as String
        string x = X.ToString();

        // Stores the number Y as String
        string y = Y.ToString();

        // Stores number of digits
        int n = x.Length;

        // Store the digits
        int[, ] a = new int[2, n];

        // Traverse the range [0, 1]
        for (int i = 0; i < 2; i++) {

            // Traverse the range [0, N - 1]
            for (int j = 0; j < n; j++) {

                // If the value of i is 0
                if (i == 0)
                    a[i, j] = x[j] - '0';

                // Otherwise
                else
                    a[i, j] = y[j] - '0';
            }
        }

        // Stores the permutation of [1, N]
        int[] p = new int[n];

        // Initialize the permutation array
        for (int i = 0; i < n; i++)
            p[i] = i;

        // Generate all possible permutation
        do {

            // Stores the maximum of X and Y
            int xx = Int32.MinValue;

            // Stores the minimum of X and Y
            int yy = Int32.MaxValue;

            // Traverse the range [0, 1]
            for (int i = 0; i < 2; i++) {

                // Stores the number
                // after rearranging
                int num = 0;

                // Traverse the range [0, N - 1]
                for (int j = 0; j < n; j++)

                    // Update the value of num
                    num = num * 10 + a[i, p[j]];

                // Update the value of xx
                xx = Math.Max(xx, num);

                // Update the value of yy
                yy = Math.Min(yy, num);
            }

            // Update the value of minDiff
            minDiff = Math.Min(minDiff, xx - yy);

        } while (next_permutation(p));

        // Return the minimum difference
        return minDiff;
    }
    static bool next_permutation(int[] p)
    {
        for (int a = p.Length - 2; a >= 0; --a)
            if (p[a] < p[a + 1])
                for (int b = p.Length - 1;; --b)
                    if (p[b] > p[a]) {
                        int t = p[a];
                        p[a] = p[b];
                        p[b] = t;
                        for (++a, b = p.Length - 1; a < b;
                             ++a, --b) {
                            t = p[a];
                            p[a] = p[b];
                            p[b] = t;
                        }
                        return true;
                    }
        return false;
    }

    // Driver Code
    public static void Main(string[] args)
    {
        int X = 37198, Y = 44911;
        Console.WriteLine(minDifference(X, Y));
    }
}

// This code is contributed by ukasp.
```

## java 描述语言

```
<script>
       // Javascript program for
       // the above approach

       // Function to find minimum difference
       // between X and Y after rearranging
       // their digits in the same order

       function minDifference(X, Y)
       {
           // Stores the minimum difference
           let minDiff = Number.MAX_SAFE_INTEGER;

           // Stores the number X as String
           let x = X.toString();

           // Stores the number Y as String
           let y = Y.toString();

           // Stores number of digits
           let n = x.length;

           // Store the digits
           let a = [];
           for (let i = 0; i < 2; i++) {
               a[i] = new Array(n);
           }
           //Traverse the range [0, 1]
           for (let i = 0; i < 2; i++) {

               // Traverse the range [0, N - 1]
               for (let j = 0; j < n; j++) {

                   // If the value of i is 0
                   if (i == 0)
                       a[i][j] = x.charAt(j) - '0';

                   // Otherwise
                   else
                       a[i][j] = y.charAt(j) - '0';
               }
           }

           // Stores the permutation of [1, N]
           let p = [];

           // Initialize the permutation array
           for (let i = 0; i < n; i++)
               p[i] = i;

           // Generate all possible permutation
           do {

               // Stores the maximum of X and Y
               let xx = Number.MIN_SAFE_INTEGER;

               // Stores the minimum of X and Y
               let yy = Number.MAX_SAFE_INTEGER;

               // Traverse the range [0, 1]
               for (let i = 0; i < 2; i++) {

                   // Stores the number
                   // after rearranging
                   let num = 0;

                   // Traverse the range [0, N - 1]
                   for (let j = 0; j < n; j++)

                       // Update the value of num
                       num = num * 10 + a[i][p[j]];

                   // Update the value of xx
                   xx = Math.max(xx, num);

                   // Update the value of yy
                   yy = Math.min(yy, num);
               }

               // Update the value of minDiff
               minDiff = Math.min(minDiff, xx - yy);

           } while (next_permutation(p));

           // Return the minimum difference
           return minDiff;
       }
       function next_permutation(p) {
           for (let a = p.length - 2; a >= 0; --a)
               if (p[a] < p[a + 1])
                   for (let b = p.length - 1; ; --b)
                       if (p[b] > p[a]) {
                           let t = p[a];
                           p[a] = p[b];
                           p[b] = t;
                           for (++a, b = p.length - 1;
                           a < b; ++a, --b)
                           {
                               t = p[a];
                               p[a] = p[b];
                               p[b] = t;
                           }
                           return true;
                       }
           return false;
       }
       // Driver Code

       let X = 37198, Y = 44911;
       document.write(minDifference(X, Y));

       // This code is contributed by Hritik

   </script>
```

**Output**

```
1278
```

***时间复杂度:** O(N！)*
***辅助空间:** O(1)*
# 使用第二个数组

使所有元素相等的最小运算

> 原文:[https://www . geeksforgeeks . org/最小操作使用第二个数组使所有元素相等/](https://www.geeksforgeeks.org/minimum-operations-to-make-all-elements-equal-using-the-second-array/)

给定两个数组 **A[]** 和 **B[]** ，两个数组都有 **N** 元素。找出使 A 的所有元素等于第二个数组 b 的最小操作数。一个操作包括:

```
A[i] = A[i] - B[i], 0 <= i <= n-1 
```

**注意:**如果无法使数组元素等于 print -1。
**例:**

> **输入:** A[] = {5，7，10，5，15}，B[] = {2，2，1，3， 5}
> **输出:** 8
> **说明:**
> 操作如下:
> 1)选择指标 1 - > 5 5 10 5 15
> 2)选择指标 2 - > 5 5 9 5 15
> 3)选择指标 2->5 8 5 15
> 4)选择指标 2->5 7 5 15
> 5)选择指标 2 - > 选择指数 2 - > 5 5 5 5 15
> 7)选择指数 4->5 5 5 10
> 8)选择指数 4->5 5 5 5 5
> T18】输入: A[] = {3，5，8，2}，B[] = {1，2，1，1}
> **输出:** 12

**进场:**

*   可以观察到，如果 A 的所有元素都可以相等，那么最大可能值就是 A 的最小元素

*   所以我们可以迭代最终值 x，当 A 的所有元素都相等时。使用以上观察–0<= x <= min(A[i]). For each x, traverse A and check whether A[i] can be made equal to x using B[i] : 

```
A[i] - k*B[i] = x
Take mod with B[i] on both sides
A[i] %B[i] = x %B[i]  ->  
must be satisfied for A[i] to be converted to x
```

*   如果满足条件，则该元素所需的操作数=(A[I]–x)/B[I]

以下是上述方法的实现:

## C++

```
// C++ implementation to find the
// minimum operations make all elements
// equal using the second array

#include <bits/stdc++.h>

using namespace std;

// Function to find the minimum
// operations required to make
// all elements of the array equal
int minOperations(int a[], int b[], int n)
{
    // Minimum element of A[]
    int minA = *min_element(a, a + n);

    // Traverse through all final values
    for (int x = minA; x >= 0; x--) {

        // Variable indicating
        // whether all elements
        // can be converted to x or not
        bool check = 1;

        // Total operations
        int operations = 0;

        // Traverse through
        // all array elements
        for (int i = 0; i < n; i++) {
            if (x % b[i] == a[i] % b[i]) {
                operations +=
                    (a[i] - x) / b[i];
            }

            // All elements can't
            // be converted to x
            else {
                check = 0;
                break;
            }
        }
        if (check)
            return operations;
    }
    return -1;
}

// Driver Code
int main()
{
    int N = 5;
    int A[N] = { 5, 7, 10, 5, 15 };
    int B[N] = { 2, 2, 1, 3, 5 };

    cout << minOperations(A, B, N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find the
// minimum operations make all elements
// equal using the second array
import java.util.*;
class GFG{

// Function to find the minimum
// operations required to make
// all elements of the array equal
static int minOperations(int a[], int b[], int n)
{
    // Minimum element of A[]
    int minA = Arrays.stream(a).min().getAsInt();

    // Traverse through all final values
    for (int x = minA; x >= 0; x--)
    {

        // Variable indicating
        // whether all elements
        // can be converted to x or not
        boolean check = true;

        // Total operations
        int operations = 0;

        // Traverse through
        // all array elements
        for (int i = 0; i < n; i++)
        {
            if (x % b[i] == a[i] % b[i])
            {
                operations += (a[i] - x) / b[i];
            }

            // All elements can't
            // be converted to x
            else
            {
                check = false;
                break;
            }
        }
        if (check)
            return operations;
    }
    return -1;
}

// Driver Code
public static void main(String[] args)
{
    int N = 5;
    int A[] = { 5, 7, 10, 5, 15 };
    int B[] = { 2, 2, 1, 3, 5 };

    System.out.print(minOperations(A, B, N));
}
}

// This code is contributed by AbhiThakur
```

## 蟒蛇 3

```
# Python3 implementation to find the
# minimum operations make all elements
# equal using the second array

# Function to find the minimum
# operations required to make
# all elements of the array equal
def minOperations(a, b, n):

    # Minimum element of A
    minA = min(a);

    # Traverse through all final values
    for x in range(minA, -1, -1):

        # Variable indicating
        # whether all elements
        # can be converted to x or not
        check = True;

        # Total operations
        operations = 0;

        # Traverse through
        # all array elements
        for i in range(n):
            if (x % b[i] == a[i] % b[i]):
                operations += (a[i] - x) / b[i];

            # All elements can't
            # be converted to x
            else:
                check = False;
                break;

        if (check):
            return operations;

    return -1;

# Driver Code
if __name__ == '__main__':

    N = 5;
    A = [ 5, 7, 10, 5, 15 ];
    B = [ 2, 2, 1, 3, 5 ];

    print(int(minOperations(A, B, N)));

# This code is contributed by amal kumar choubey
```

## C#

```
// C# implementation to find the
// minimum operations make all elements
// equal using the second array
using System;
using System.Linq;

class GFG{

// Function to find the minimum
// operations required to make
// all elements of the array equal
static int minOperations(int []a, int []b, int n)
{

    // Minimum element of A[]
    int minA = a.Max();

    // Traverse through all final values
    for(int x = minA; x >= 0; x--)
    {

       // Variable indicating
       // whether all elements
       // can be converted to x or not
       bool check = true;

       // Total operations
       int operations = 0;

       // Traverse through
       // all array elements
       for(int i = 0; i < n; i++)
       {
          if (x % b[i] == a[i] % b[i])
          {
              operations += (a[i] - x) / b[i];
          }

          // All elements can't
          // be converted to x
          else
          {
              check = false;
              break;
          }
       }
       if (check)
           return operations;
    }
    return -1;
}

// Driver Code
public static void Main(string[] args)
{
    int N = 5;
    int []A = { 5, 7, 10, 5, 15 };
    int []B = { 2, 2, 1, 3, 5 };

    Console.WriteLine(minOperations(A, B, N));
}
}

// This code is contributed by SoumikMondal
```

## java 描述语言

```
<script>
// javascript implementation to find the
// minimum operations make all elements
// equal using the second array

    // Function to find the minimum
    // operations required to make
    // all elements of the array equal
    function minOperations(a , b , n)
    {

        // Minimum element of A
        var minA = Math.max.apply(Math,a);;

        // Traverse through all final values
        for (x = minA; x >= 0; x--) {

            // Variable indicating
            // whether all elements
            // can be converted to x or not
            var check = true;

            // Total operations
            var operations = 0;

            // Traverse through
            // all array elements
            for (i = 0; i < n; i++) {
                if (x % b[i] == a[i] % b[i]) {
                    operations += (a[i] - x) / b[i];
                }

                // All elements can't
                // be converted to x
                else {
                    check = false;
                    break;
                }
            }
            if (check)
                return operations;
        }
        return -1;
    }

    // Driver Code
        var N = 5;
        var A = [ 5, 7, 10, 5, 15 ];
        var B = [ 2, 2, 1, 3, 5 ];

        document.write(minOperations(A, B, N));

// This code is contributed by Rajput-Ji
</script>
```

**Output:** 

```
8
```

**时间复杂度:***O(N * min(A<sub>I</sub>)*

**辅助空间:** O(1)
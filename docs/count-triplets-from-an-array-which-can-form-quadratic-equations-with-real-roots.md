# 从一个可以形成带实根的二次方程的数组中计算三元组

> 原文:[https://www . geeksforgeeks . org/count-triples-from-from-a-array-form-quadrant-equations-with-real-root/](https://www.geeksforgeeks.org/count-triplets-from-an-array-which-can-form-quadratic-equations-with-real-roots/)

给定一个由 **N** 个不同正整数组成的[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】**，任务是找出三元组 **(a，b，c)** 的个数，使得二次方程 **aX <sup>2</sup> + bX + c = 0** 具有*实根*。

**示例:**

> **输入:** arr[] = { 2，3，6，8 }
> **输出:** 6
> **解释:**
> 对于三胞胎(a = 2，b = 6，c = 3)，(a = 3，b = 6，c = 2)，(a = 2，b = 8，c = 3)，(a = 3，b = 8，c = 2)，(a = 2，b = 8，c = 6)，(a = 6，b = 8，c = 2)}，二次方程
> 
> **输入:** arr[] = [1，2，3，4，5]
> **输出:** 14

**天真方法:**如果二次方程的**行列式小于或等于 0** ，则该方程具有实根。因此， **a * c ≤ b * b / 4** 。这个问题可以通过使用这个属性来解决。
按照下面给出的步骤解决问题:

*   使用变量迭代范围**【0，N–1】**，比如 **b** ，并执行以下步骤:
    1.  对于 **b** 的每个值，运行从 **a = 0** 到**N–1**的循环，检查 **b** 和 **a** 是否相等。如果发现为真，则[继续](https://www.geeksforgeeks.org/continue-statement-cpp/)循环。
    2.  现在，使用一个变量迭代范围**【0，N–1】**，比如说 **c** ，检查是否两个 **b = c** 或 **a = c** 都满足。如果发现是真的，则[继续](https://www.geeksforgeeks.org/continue-statement-cpp/)循环。
    3.  如果**arr[a]* arr[C]≤arr[b]* arr[b]/4**，则递增计数。
*   最后，返回**计数**。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find count of triplets (a, b, c)
// such that the equations ax^2 + bx + c = 0
// has real roots
int getCount(int arr[], int N)
{

    // Stores count of triplets(a, b, c) such
    // that ax^2 + bx + c = 0 has real roots
    int count = 0;

    // Base case
    if (N < 3)
        return 0;

    // Generate all possible triplets(a, b, c)
    for (int b = 0; b < N; b++) {
        for (int a = 0; a < N; a++) {

            // If the coefficient of
            // X^2 and X are equal
            if (a == b)
                continue;

            for (int c = 0; c < N; c++) {

                // If coefficient of X^2
                // or x are equal to the
                // constant
                if (c == a || c == b)
                    continue;

                int d = arr[b] * arr[b] / 4;

                // Condition for having
                // real roots
                if (arr[a] * arr <= d)
                    count++;
            }
        }
    }
    return count;
}

// Driver Code
int main()
{
    int arr[] = { 1, 2, 3, 4, 5 };
    int N = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    cout << getCount(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
class GFG{

// Function to find count of triplets (a, b, c)
// such that the equations ax^2 + bx + c = 0
// has real roots
static int getCount(int arr[], int N)
{

    // Stores count of triplets(a, b, c) such
    // that ax^2 + bx + c = 0 has real roots
    int count = 0;

    // Base case
    if (N < 3)
        return 0;

    // Generate all possible triplets(a, b, c)
    for (int b = 0; b < N; b++)
    {
        for (int a = 0; a < N; a++)
        {

            // If the coefficient of
            // X^2 and X are equal
            if (a == b)
                continue;

            for (int c = 0; c < N; c++)
            {

                // If coefficient of X^2
                // or x are equal to the
                // constant
                if (c == a || c == b)
                    continue;
                int d = arr[b] * arr[b] / 4;

                // Condition for having
                // real roots
                if (arr[a] * arr <= d)
                    count++;
            }
        }
    }
    return count;
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 1, 2, 3, 4, 5 };
    int N = arr.length;

    // Function Call
    System.out.print(getCount(arr, N));
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python Program for the above approach

# Function to find the count of triplets(a,b,c)
# Such that the equations ax^2 + bx + c = 0
# has real roots

def getcount(arr,N):

    # store count of triplets(a,b,c) such
    # that ax^2 + bx + c = 0 has real roots
    count = 0

    # base case
    if (N < 3):
        return 0

    # Generate all possible triplets (a,b,c)
    for b in range(0, N):
        for a in range(0, N):

            # if the coefficient of X^2
            # and x are equal
            if (a == b):
                continue
            for c in range(0, N):

                # if coefficient of X^2
                # or x are equal to the
                # constant
                if (c == a or c == b):
                    continue
                d = arr[b] * arr[b] // 4

                # condition for having
                # real roots
                if (arr[a] * arr) <= d:
                    count += 1
    return count

# Driver code
arr = [1,2,3,4,5]
N = len(arr)
print(getcount(arr, N))

# This code is contributed by Virusbuddah
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

public class GFG
{

  // Function to find count of triplets (a, b, c)
  // such that the equations ax^2 + bx + c = 0
  // has real roots
  static int getCount(int[] arr, int N)
  {

    // Stores count of triplets(a, b, c) such
    // that ax^2 + bx + c = 0 has real roots
    int count = 0;

    // Base case
    if (N < 3)
      return 0;

    // Generate all possible triplets(a, b, c)
    for (int b = 0; b < N; b++)
    {
      for (int a = 0; a < N; a++)
      {

        // If the coefficient of
        // X^2 and X are equal
        if (a == b)
          continue;

        for (int c = 0; c < N; c++)
        {

          // If coefficient of X^2
          // or x are equal to the
          // constant
          if (c == a || c == b)
            continue;
          int d = arr[b] * arr[b] / 4;

          // Condition for having
          // real roots
          if (arr[a] * arr <= d)
            count++;
        }
      }
    }
    return count;
  }

  // Driver Code
  static public void Main()
  {
    int[] arr = { 1, 2, 3, 4, 5 };
    int N = arr.Length;

    // Function Call
    Console.WriteLine(getCount(arr, N));
  }
}

// This code is contributed by sanjoy_62.
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to find count of triplets (a, b, c)
// such that the equations ax^2 + bx + c = 0
// has real roots
function getCount(arr, N)
{

    // Stores count of triplets(a, b, c) such
    // that ax^2 + bx + c = 0 has real roots
    var count = 0;

    // Base case
    if (N < 3)
        return 0;

    // Generate all possible triplets(a, b, c)
    for(var b = 0; b < N; b++)
    {
        for(var a = 0; a < N; a++)
        {

            // If the coefficient of
            // X^2 and X are equal
            if (a == b)
                continue;

            for(var c = 0; c < N; c++)
            {

                // If coefficient of X^2
                // or x are equal to the
                // constant
                if (c == a || c == b)
                    continue;

                var d = arr[b] * arr[b] / 4;

                // Condition for having
                // real roots
                if (arr[a] * arr <= d)
                    count++;
            }
        }
    }
    return count;
}

// Driver Code
var arr = [ 1, 2, 3, 4, 5 ];
var N = arr.length;

// Function Call
document.write(getCount(arr, N));

// This code is contributed by Ankita saini

</script>
```

**Output:** 

```
14
```

***时间复杂度:**O(N<sup>3</sup>)*
***辅助空间:** O(1)*

**高效途径**:使用[排序](https://www.geeksforgeeks.org/sort-algorithms-the-c-standard-template-library-stl/)和[两个指针算法](https://www.geeksforgeeks.org/two-pointers-technique/)可以高效解决问题。
按照以下步骤解决问题:

*   [按升序排列给定数组**arr[]**](https://www.geeksforgeeks.org/c-program-to-sort-an-array-in-ascending-order/)。
*   从 **b = 0** 到数组的[大小运行一个循环。](https://www.geeksforgeeks.org/how-to-find-size-of-array-in-cc-without-using-sizeof-operator/)
    1.  将两个变量 **a** 和 **c** 初始化为 **0** ，数组大小分别等于 **-1** 。
    2.  当 **a < c** 成立时运行一个循环，并检查以下条件:
        1.  如果 **a = b** ，则增加 **a** 和[继续](https://www.geeksforgeeks.org/continue-statement-cpp/)循环。
        2.  如果 **c = b** ，则递减 **c** 和[继续](https://www.geeksforgeeks.org/continue-statement-cpp/)循环。
        3.  如果 **arr[a] * arr[C] ≤ d** ，则检查以下情况:
            *   如果 **a < b < c** ，则根据它们之间的元素数量增加**计数**–1(*除了 arr【b】*)。
            *   否则，根据它们之间的元素数量增加计数。
        4.  否则，递减 **c** 。
*   对于每对，两个值可能是 **a** 和 **c** 。所以返回**计数* 2** 。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to count the number of triplets
// (a, b, c) such that the equation
// ax^2 + bx + c = 0 has real roots
int getCount(int arr[], int N)
{
    // Sort the array in
    // ascending order
    sort(arr, arr + N);

    // Stores count of triplets(a, b, c) such
    // that ax^2 + bx + c = 0 has real roots
    int count = 0;

    // Base case
    if (N < 3)
        return 0;

    // Traverse the given array
    for (int b = 0; b < N; b++) {

        int a = 0, c = N - 1;
        int d = arr[b] * arr[b] / 4;

        while (a < c) {

            // If values of a and
            // c are equal to b
            if (a == b) {

                // Increment a
                a++;
                continue;
            }
            if (c == b) {

                // Decrement c
                c--;
                continue;
            }

            // Condition for having real
            // roots for a quadratic equation
            if (arr[a] * arr <= d) {

                // If b lies in
                // between a and c
                if (a < b && b < c) {

                    // Update count
                    count += c - a - 1;
                }
                else {

                    // Update count
                    count += c - a;
                }

                // Increment a
                a++;
            }
            else {

                // Decrement c
                c--;
            }
        }
    }

    // For each pair two values
    // are possible of a and c
    return count * 2;
}

// Driver Code
int main()
{
    int arr[] = { 3, 6, 10, 13, 21 };
    int N = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    cout << getCount(arr, N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
class GFG
{

// Function to count the number of triplets
// (a, b, c) such that the equation
// ax^2 + bx + c = 0 has real roots
static int getCount(int arr[], int N)
{

    // Sort the array in
    // ascending order
    Arrays.sort(arr);

    // Stores count of triplets(a, b, c) such
    // that ax^2 + bx + c = 0 has real roots
    int count = 0;

    // Base case
    if (N < 3)
        return 0;

    // Traverse the given array
    for (int b = 0; b < N; b++)
    {
        int a = 0, c = N - 1;
        int d = arr[b] * arr[b] / 4;
        while (a < c)
        {

            // If values of a and
            // c are equal to b
            if (a == b)
            {

                // Increment a
                a++;
                continue;
            }
            if (c == b)
            {

                // Decrement c
                c--;
                continue;
            }

            // Condition for having real
            // roots for a quadratic equation
            if (arr[a] * arr <= d)
            {

                // If b lies in
                // between a and c
                if (a < b && b < c)
                {

                    // Update count
                    count += c - a - 1;
                }
                else
                {

                    // Update count
                    count += c - a;
                }

                // Increment a
                a++;
            }
            else {

                // Decrement c
                c--;
            }
        }
    }

    // For each pair two values
    // are possible of a and c
    return count * 2;
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 3, 6, 10, 13, 21 };
    int N = arr.length;

    // Function Call
    System.out.print(getCount(arr, N));
}
}

// This code is contributed by code_hunt.
```

## 蟒蛇 3

```
# Python3 Program for the above approach

# Function to  count the number of triplets(a,b,c)
# Such that the equations ax^2 + bx + c = 0
# has real roots
def getcount(arr, N):

    # sort he array in
    # ascending order
    arr.sort()

    # store count of triplets (a,b,c) such
    # that ax^2 + bx + c = 0 has real roots
    count = 0

    # base case
    if (N < 3):
        return 0

    # Traverse the given array
    for b in range(0, N):
        a = 0
        c = N - 1
        d = arr[b] * arr[b] // 4
        while(a < c):

            # if value of a and
            # c are equal to b
            if (a == b):

                # increment a
                a += 1
                continue
            if (c == b):

                # Decrement c
                c -= 1
                continue

            # condition for having real
            # roots for a quadratic equation
            if (arr[a] * arr) <= d:

                # if b lies in
                # between a and c
                if (a < b and b < c):

                    # update count
                    count += c - a - 1
                else:

                    # update count
                    count += c - a

                # increment a
                a += 1
            else:

                # Decrement c
                c -= 1

    # for each pair two values
    # are possible of a and c           
    return count * 2

# Driver code
arr = [3,6,10,13,21]
N = len(arr)
print(getcount(arr,N))

# This code is contributed by Virusbuddah
```

## C#

```
// C# program for the above approach
using System;

class GFG{

  // Function to count the number of triplets
  // (a, b, c) such that the equation
  // ax^2 + bx + c = 0 has real roots
  static int getCount(int[] arr, int N)
  {

    // Sort the array in
    // ascending order
    Array.Sort(arr);

    // Stores count of triplets(a, b, c) such
    // that ax^2 + bx + c = 0 has real roots
    int count = 0;

    // Base case
    if (N < 3)
      return 0;

    // Traverse the given array
    for (int b = 0; b < N; b++)
    {
      int a = 0, c = N - 1;
      int d = arr[b] * arr[b] / 4;
      while (a < c)
      {

        // If values of a and
        // c are equal to b
        if (a == b)
        {

          // Increment a
          a++;
          continue;
        }
        if (c == b)
        {

          // Decrement c
          c--;
          continue;
        }

        // Condition for having real
        // roots for a quadratic equation
        if (arr[a] * arr <= d)
        {

          // If b lies in
          // between a and c
          if (a < b && b < c)
          {

            // Update count
            count += c - a - 1;
          }
          else
          {

            // Update count
            count += c - a;
          }

          // Increment a
          a++;
        }
        else {

          // Decrement c
          c--;
        }
      }
    }

    // For each pair two values
    // are possible of a and c
    return count * 2;
  }

  // Driver Code
  static public void Main()
  {
    int[] arr = { 3, 6, 10, 13, 21 };
    int N = arr.Length;

    // Function Call
    Console.Write(getCount(arr, N));
  }
}

// This code is contributed by susmitakundugoaldanga.
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to count the number of triplets
// (a, b, c) such that the equation
// ax^2 + bx + c = 0 has real roots
function getCount(arr, N)
{

    // Sort the array in
    // ascending order
    arr.sort();

    // Stores count of triplets(a, b, c) such
    // that ax^2 + bx + c = 0 has real roots
    var count = 0;

    // Base case
    if (N < 3)
        return 0;

    // Traverse the given array
    for(var b = 0; b < N; b++)
    {
        var a = 0, c = N - 1;
        var d = arr[b] * arr[b] / 4;
        while (a < c)
        {

            // If values of a and
            // c are equal to b
            if (a == b)
            {

                // Increment a
                a++;
                continue;
            }
            if (c == b)
            {

                // Decrement c
                c--;
                continue;
            }

            // Condition for having real
            // roots for a quadratic equation
            if (arr[a] * arr <= d)
            {

                // If b lies in
                // between a and c
                if (a < b && b < c)
                {

                    // Update count
                    count += c - a - 1;
                }
                else
                {

                    // Update count
                    count += c - a;
                }

                // Increment a
                a++;
            }
            else
            {

                // Decrement c
                c--;
            }
        }
    }

    // For each pair two values
    // are possible of a and c
    return count * 2;
}

// Driver Code
var arr = [ 3, 6, 10, 13, 21 ];
var N = arr.length;

// Function Call
document.write(getCount(arr, N));

// This code is contributed by Ankita saini

</script>
```

**Output:** 

```
16
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*
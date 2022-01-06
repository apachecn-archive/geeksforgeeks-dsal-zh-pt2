# 指数对的计数，使得这些指数的元素乘积等于指数的绝对差值

> 原文:[https://www . geesforgeks . org/index-count-of-pairs-这样，这些指数的元素乘积等于指数的绝对差值/](https://www.geeksforgeeks.org/count-of-indices-pairs-such-that-product-of-elements-at-these-indices-is-equal-to-absolute-difference-of-indices/)

给定一个由 **N** 个正整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**，任务是找到对 **(i，j)** 的数量，使得 **i < j** 和这些指数处的元素乘积等于它们指数的绝对差。

**示例:**

> **输入:** arr[] = {1，1，2，4}
> **输出:** 2
> **解释:**
> 以下是可能的配对:
> 
> 1.  **(0，1):** 这些指数之和为 0 + 1 = 1，这些指数处元素的乘积为 arr[0]*arr[1] = 1*1 = 1。
> 2.  **(0，2):** 这些指数之和为 0 + 2 = 2，这些指数处元素的乘积为 arr[0]*arr[1] = 1*2 = 2。
> 
> 因此，对的总数是 2。
> 
> **输入:** arr[] = {1，2，1 }
> T3】输出: 0

**天真方法:**解决给定问题的简单方法是[生成给定数组](https://www.geeksforgeeks.org/find-all-pairs-possible-from-the-given-array/)的所有可能对，并对满足给定标准的对进行计数。检查所有对后，打印获得的总数**计数**。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to count the number of
// pairs (i, j) such that arr[i]*arr[j]
// is equal to abs(i - j)
int getPairsCount(int a[], int n)
{
    // Stores the resultant number
    // of pairs
    int count = 0;

    // Generate all possible pairs
    // from the array arr[]
    for (int i = 0; i < n - 1; i++) {
        for (int j = i + 1; j < n; j++) {

            // If the given condition
            // satisfy then increment
            // the value of count
            if ((a[i] * a[j]) == abs(i - j))
                count++;
        }
    }

    // Return the resultant count
    return count;
}

// Driver Code
int main()
{
    int arr[] = { 1, 1, 2, 4 };
    int N = sizeof(arr) / sizeof(arr[0]);
    cout << getPairsCount(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to count the number of
// pairs (i, j) such that arr[i]*arr[j]
// is equal to abs(i - j)
static int getPairsCount(int a[], int n)
{

    // Stores the resultant number
    // of pairs
    int count = 0;

    // Generate all possible pairs
    // from the array arr[]
    for(int i = 0; i < n - 1; i++)
    {
        for(int j = i + 1; j < n; j++)
        {

            // If the given condition
            // satisfy then increment
            // the value of count
            if ((a[i] * a[j]) == Math.abs(i - j))
                count++;
        }
    }

    // Return the resultant count
    return count;
}

// Driver Code
public static void main(String args[])
{
    int arr[] = { 1, 1, 2, 4 };
    int N = arr.length;

    System.out.print(getPairsCount(arr, N));
}
}

// This code is contributed by avijitmondal1998
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to count the number of
# pairs (i, j) such that arr[i]*arr[j]
# is equal to abs(i - j)
def getPairsCount(a, n):

    # Stores the resultant number
    # of pairs
    count = 0

    # Generate all possible pairs
    # from the array arr[]
    for i in range(n - 1):
        for j in range(i + 1, n):

            # If the given condition
            # satisfy then increment
            # the value of count
            if ((a[i] * a[j]) == abs(i - j)):
                count += 1

    # Return the resultant count
    return count

# Driver Code
if __name__ == '__main__':

    arr = [ 1, 1, 2, 4 ]
    N = len(arr)

    print(getPairsCount(arr, N))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to count the number of
// pairs (i, j) such that arr[i]*arr[j]
// is equal to abs(i - j)
static int getPairsCount(int[] a, int n)
{

    // Stores the resultant number
    // of pairs
    int count = 0;

    // Generate all possible pairs
    // from the array arr[]
    for(int i = 0; i < n - 1; i++)
    {
        for(int j = i + 1; j < n; j++)
        {

            // If the given condition
            // satisfy then increment
            // the value of count
            if ((a[i] * a[j]) == Math.Abs(i - j))
                count++;
        }
    }

    // Return the resultant count
    return count;
}

// Driver Code
public static void Main()
{
    int[] arr = { 1, 1, 2, 4 };
    int N = arr.Length;

    Console.Write(getPairsCount(arr, N));
}
}

// This code is contributed by subhammahato348
```

## java 描述语言

```
<script>

        // JavaScript program for the above approach

        // Function to count the number of
        // pairs (i, j) such that arr[i]*arr[j]
        // is equal to abs(i - j)
        function getPairsCount(a, n) {
            // Stores the resultant number
            // of pairs
            let count = 0;

            // Generate all possible pairs
            // from the array arr[]
            for (let i = 0; i < n - 1; i++) {
                for (let j = i + 1; j < n; j++) {

                    // If the given condition
                    // satisfy then increment
                    // the value of count
                    if ((a[i] * a[j]) == Math.abs(i - j))
                        count++;
                }
            }

            // Return the resultant count
            return count;
        }

        // Driver Code

        let arr = [1, 1, 2, 4];
        let N = arr.length;
        document.write(getPairsCount(arr, N));

    // This code is contributed by Potta Lokesh
    </script>
```

**Output:** 

```
2
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*

**高效方法:**上述方法也可以通过优化上述步骤中使用的内环来优化。想法是在第一个循环中[迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，N–1】**，在第二个循环中使用变量 **j** 从**arr[I]–(I % arr[I])**开始迭代，并将 **j** 的值增加 **arr[i]** 直到 **N** ，然后检查给定的标准。按照以下步骤解决问题:

*   初始化变量，说**计数**为 **0** ，存储结果对的计数。
*   [使用变量 **i** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，N】**，并执行以下步骤:
    *   [使用变量 **j** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【arr[I]–(I % arr[I])，N】**，增量为 **arr[i]** ，如果 **i** 小于 **j** 且 **arr[i]*arr[j]** 等于**ABS(I–j)**，则增加**计数的值**
*   **完成上述步骤后，打印**计数**的值作为结果。**

**下面是上述方法的实现。**

## **C++**

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to count the number of
// pairs (i, j) such that arr[i]*arr[j]
// is equal to abs(i - j)
int getPairsCount(int arr[], int n)
{
    // Stores the resultant number
    // of pairs
    int count = 0;

    // Iterate over the range [0, N)
    for (int i = 0; i < n; i++) {

        // Now, iterate from the value
        // arr[i]-(i%arr[i]) till N
        // with an increment of arr[i]
        for (int j = arr[i] - (i % arr[i]);
             j < n;
             j += arr[i]) {

            // If the given criteria
            // satisfy then increment
            // the value of count
            if (i < j && (arr[i] * arr[j]) == abs(i - j)) {
                count++;
            }
        }
    }

    // Return the resultant count
    return count;
}

// Driver Code
int main()
{
    int arr[] = { 1, 1, 2, 4 };
    int N = sizeof(arr) / sizeof(arr[0]);
    cout << getPairsCount(arr, N);

    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to count the number of
// pairs (i, j) such that arr[i]*arr[j]
// is equal to abs(i - j)
static int getPairsCount(int []arr, int n)
{
    // Stores the resultant number
    // of pairs
    int count = 0;

    // Iterate over the range [0, N)
    for (int i = 0; i < n; i++) {

        // Now, iterate from the value
        // arr[i]-(i%arr[i]) till N
        // with an increment of arr[i]
        for (int j = arr[i] - (i % arr[i]);
             j < n;
             j += arr[i]) {

            // If the given criteria
            // satisfy then increment
            // the value of count
            if (i < j && (arr[i] * arr[j]) == Math.abs(i - j)) {
                count++;
            }
        }
    }

    // Return the resultant count
    return count;
}

// Driver Code
public static void main(String args[])
{
    int []arr = { 1, 1, 2, 4 };
    int N = arr.length;
    System.out.print(getPairsCount(arr, N));
}
}

// This code isontributed by SURENDRA_GANGWAR.
```

## **蟒蛇 3**

```
# Python3 program for the above approach

# Function to count the number of
# pairs(i, j) such that arr[i]*arr[j]
# is equal to abs(i - j)
def getPairsCount(arr, n):

    # Stores the resultant number
    # of pairs
    count = 0

    # Iterate over the range[0, N)
    for i in range(0, n):

        # Now, iterate from the value
        #  arr[i]-(i % arr[i]) till N
        #  with an increment of arr[i]
        s = arr[i]-(i % arr[i])
        for j in range(s, n):

            # If the given criteria
            # satisfy then increment
            # the value of count
            if (i < j and (arr[i] * arr[j]) ==
                            abs(i - j)):
                count += 1

    # Return the resultant count
    return count

#  Driver Code
arr = [ 1, 1, 2, 4 ]
N = len(arr)

print(getPairsCount(arr, N))

# This code is contributed by amreshkumar3
```

## **C#**

```
// C# program for the above approach
using System;

class GFG{

// Function to count the number of
// pairs (i, j) such that arr[i]*arr[j]
// is equal to abs(i - j)
static int getPairsCount(int[] arr, int n)
{

    // Stores the resultant number
    // of pairs
    int count = 0;

    // Iterate over the range [0, N)
    for(int i = 0; i < n; i++)
    {

        // Now, iterate from the value
        // arr[i]-(i%arr[i]) till N
        // with an increment of arr[i]
        for(int j = arr[i] - (i % arr[i]);
                j < n; j += arr[i])
        {

            // If the given criteria
            // satisfy then increment
            // the value of count
            if (i < j && (arr[i] * arr[j]) ==
                Math.Abs(i - j))
            {
                count++;
            }
        }
    }

    // Return the resultant count
    return count;
}

// Driver Code
public static void Main()
{
    int[] arr = { 1, 1, 2, 4 };
    int N = arr.Length;

    Console.Write(getPairsCount(arr, N));
}
}

// This code is contributed by ukasp
```

## **java 描述语言**

```
<script>
// Javascript program for the above approach

// Function to count the number of
// pairs (i, j) such that arr[i]*arr[j]
// is equal to abs(i - j)
function getPairsCount(arr, n)
{

  // Stores the resultant number
  // of pairs
  let count = 0;

  // Iterate over the range [0, N)
  for (let i = 0; i < n; i++)
  {

    // Now, iterate from the value
    // arr[i]-(i%arr[i]) till N
    // with an increment of arr[i]
    for (let j = arr[i] - (i % arr[i]); j < n; j += arr[i])
    {

      // If the given criteria
      // satisfy then increment
      // the value of count
      if (i < j && arr[i] * arr[j] == Math.abs(i - j)) {
        count++;
      }
    }
  }

  // Return the resultant count
  return count;
}

// Driver Code

let arr = [1, 1, 2, 4];
let N = arr.length;
document.write(getPairsCount(arr, N));

// This code is contributed by gfgking.
</script>
```

****Output:** 

```
2
```** 

*****时间复杂度:** O(N*log N)*
***辅助空间:** O(1)***
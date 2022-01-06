# 数组中任何一对可能的最大值(arr[I]* arr[j])+(arr[j]–arr[I])

> 原文:[https://www . geeksforgeeks . org/arri-arrj-arri-arri-阵列中任意对的最大值/](https://www.geeksforgeeks.org/maximum-value-of-arri-arrj-arrj-arri-possible-for-any-pair-in-an-array/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，任务是为任意一对 **(i，j)** 找到表达式**(arr[I]* arr[j])+(arr[j]–arr[I])**的最大可能值，使得 **i ≠ j** 和 **0 ≤ (i，j) < N** 。

**示例:**

> **输入:** arr[] = {-2，-8，0，1，2，3，4}
> **输出:** 22
> **解释:**
> 对于对(-8，-2)表达式的值(arr[I]* arr[j])+(arr[j]–arr[I])=(-2)*(-8)+(-2 –(-8)))= 22，这是所有可能对中最大的。
> 
> **输入:** arr[] = {-47，0，12 }
> T3】输出: 47

**天真方法:**解决给定问题的最简单方法是[生成数组的所有可能对](https://www.geeksforgeeks.org/find-all-pairs-possible-from-the-given-array/)并为每个对找到给定表达式**(arr[I]* arr[j])+(arr[j]–arr[I])**的值，并打印任何对获得的最大值。

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*

**高效方法:**上述方法也可以优化，这是基于观察到表达式的最大值将通过选择阵列的成对的[最大值和第二最大值](https://www.geeksforgeeks.org/find-second-largest-element-array/)或最小值和第二最小值来获得。按照以下步骤解决问题:

*   初始化一个变量，比如**和**，来存储最终的最大值。
*   [按升序排列数组](https://www.geeksforgeeks.org/c-program-to-sort-an-array-in-ascending-order/)。
*   找到数组的最大值和[次大值元素，分别说出 **X** 和 **Y** ，将 **ans** 的值更新为 **ans** 的最大值，将表达式的值更新为值 **X** 和 **Y** 。](https://www.geeksforgeeks.org/find-second-largest-element-array/)
*   [求数组](https://www.geeksforgeeks.org/to-find-smallest-and-second-smallest-element-in-an-array/)的最小和次最小元素，分别说 **X** 和 **Y** ，将 **ans** 的值更新为 **ans** 的最大值，表达式的值为 **X** 和 **Y** 。
*   完成上述步骤后，打印**和**的值作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the value of
// the expression a * b + (b - a)
int calc(int a, int b)
{
    return a * b + (b - a);
}

// Function to find the maximum value
// of the expression a * b + (b - a)
// possible for any pair (a, b)
int findMaximum(vector<int> arr, int N)
{
    // Sort the vector in ascending order
    sort(arr.begin(), arr.end());

    // Stores the maximum value
    int ans = -1e9;

    // Update ans by choosing the pair
    // of the minimum and 2nd minimum
    ans = max(ans, calc(arr[0], arr[1]));

    // Update ans by choosing the pair
    // of maximum and 2nd maximum
    ans = max(ans, calc(arr[N - 2],
                        arr[N - 1]));

    // Return the value of ans
    return ans;
}

// Driver Code
int main()
{
    vector<int> arr = { 0, -47, 12 };
    int N = (int)arr.size();
    cout << findMaximum(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG {

// Function to find the value of
// the expression a * b + (b - a)
static int calc(int a, int b)
{
    return a * b + (b - a);
}

// Function to find the maximum value
// of the expression a * b + (b - a)
// possible for any pair (a, b)
static int findMaximum(int[] arr, int N)
{

    // Sort the vector in ascending order
    Arrays.sort(arr);

    // Stores the maximum value
    int ans = (int)-1e9;

    // Update ans by choosing the pair
    // of the minimum and 2nd minimum
    ans = Math.max(ans, calc(arr[0], arr[1]));

    // Update ans by choosing the pair
    // of maximum and 2nd maximum
    ans = Math.max(ans, calc(arr[N - 2],
                             arr[N - 1]));

    // Return the value of ans
    return ans;
}   

// Driver Code
public static void main(String[] args)
{

    // Given inputs
    int[] arr = { 0, -47, 12 };
    int N = arr.length;

    System.out.println(findMaximum(arr, N));
}
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the value of
# the expression a * b + (b - a)
def calc(a, b):
    return a * b + (b - a)

# Function to find the maximum value
# of the expression a * b + (b - a)
# possible for any pair (a, b)
def findMaximum(arr, N):

    # Sort the vector in ascending order
    arr = sorted(arr)

    # Stores the maximum value
    ans = -10**9

    # Update ans by choosing the pair
    # of the minimum and 2nd minimum
    ans = max(ans, calc(arr[0], arr[1]))

    # Update ans by choosing the pair
    # of maximum and 2nd maximum
    ans = max(ans, calc(arr[N - 2],arr[N - 1]))

    # Return the value of ans
    return ans

# Driver Code
if __name__ == '__main__':
    arr = [0, -47, 12]
    N = len(arr)
    print (findMaximum(arr, N))

# This code is contributed by mohit kumar 29.
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;
class GFG
{

    // Function to find the value of
    // the expression a * b + (b - a)
    static int calc(int a, int b)
    {
        return a * b + (b - a);
    }

    // Function to find the maximum value
    // of the expression a * b + (b - a)
    // possible for any pair (a, b)
    static int findMaximum(List<int> arr, int N)
    {

        // Sort the vector in ascending order
        arr.Sort();

        // Stores the maximum value
        int ans = -1000000000;

        // Update ans by choosing the pair
        // of the minimum and 2nd minimum
        ans = Math.Max(ans, calc(arr[0], arr[1]));

        // Update ans by choosing the pair
        // of maximum and 2nd maximum
        ans = Math.Max(ans, calc(arr[N - 2], arr[N - 1]));

        // Return the value of ans
        return ans;
    }

    // Driver Code
    public static void Main()
    {
        List<int> arr = new List<int>{ 0, -47, 12 };
        int N = (int)arr.Count;
        Console.Write(findMaximum(arr, N));
    }
}

// This code is contributed by ukasp..
```

## java 描述语言

```
<script>
        // Javascript program for the above approach

        // Function to find the value of
        // the expression a * b + (b - a)
        function calc(a, b) {
            return (a * b) + (b - a);
        }

        // Function to find the maximum value
        // of the expression a * b + (b - a)
        // possible for any pair (a, b)
        function findMaximum(arr, N) {

            // Sohe vector in ascending order
            arr.sort(function(a, b){return a - b})

            // Stores the maximum value
            let ans = Number.MIN_VALUE;

            // Update ans by choosing the pair
            // of the minimum and 2nd minimum
            ans = Math.max(ans, calc(arr[0], arr[1]));

            // Update ans by choosing the pair
            // of maximum and 2nd maximum
            ans = Math.max(ans, calc(arr[N - 2],
                arr[N - 1]));

            // Return the value of ans
            return ans;
        }

        // Driver Code

        // Given inputs
        let arr = [-47, 0, 12]

        let N = arr.length;

        document.write(findMaximum(arr, N));

        // This code is contributed by Hritik
    </script>
```

**Output:** 

```
47
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)
# 最大化获得给定总和所需的数组元素的数量

> 原文:[https://www . geeksforgeeks . org/最大化数组元素计数-需要获得给定的总和/](https://www.geeksforgeeks.org/maximize-count-of-array-elements-required-to-obtain-given-sum/)

给定一个整数 **V** 和一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】**，任务是从数组**arr【】**中找出可以选择的最大数组元素个数，得到和 **V** 。每个数组元素可以被选择任意次。如果无法得到总和，打印 **-1** 。

**示例:**

> **输入:** arr[] = {25，10，5}，V = 30
> **输出:** 6
> **解释:**
> 要获得总和 30，选择 arr[2] (= 5)，6 次。
> 因此，计数为 6。
> 
> **输入:** arr[] = {9，6，4，3}，V = 11
> **输出:** 3
> **解释:**
> 为了得到和 11，可能的组合是:4，4，3
> 因此，计数是 3

**天真方法:**最简单的方法是[递归](https://www.geeksforgeeks.org/recursion/)找到最大数量的数组元素，使用来自索引 **0** 到 **j** 的数组元素生成总和 **V** ，然后使用来自索引 **0** 到 **i** 的元素找到生成 **V** 所需的最大元素数量，其中 **j < i < N** 。完成上述步骤后，打印获得给定总和所需的数组元素个数 **V** 。

***时间复杂度:**O(V<sup>N</sup>)*
***辅助空间:** O(N)*

**高效途径:**优化上述途径，思路是使用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)。按照以下步骤解决问题:

*   初始化一个大小为 **V + 1** 的数组**表[]** ，其中**表【I】**将存储最优解以获得和 **i** 。
*   用 **-1** 初始化**表【】**，用 **0** 初始化**表【0】**为 **0** 需要数组元素才能得到值 **0** 。
*   对于从 **i = 0 到 V** 的每个值，计算以下 DP 转换所需的数组元素的最大数量:

> **表[i] = Max(表[I–arr[j]]，表[i])** ，其中表[i-arr[j]]！=-1
> 其中 1 ≤ i ≤ V，0 ≤ j ≤ N

*   完成上述步骤后，打印所需答案**表【V】**的值。

下面是上述方法的实现:

## C++14

```
// C++14 program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function that count the maximum
// number of elements to obtain sum V
int maxCount(vector<int> arr, int m, int V)
{

    // Stores the maximum number of
    // elements required to obtain V
    vector<int> table(V + 1);

    // Base Case
    table[0] = 0;

    // Initialize all table values
    // as Infinite
    for (int i = 1; i <= V; i++)
        table[i] = -1;

    // Find the max arr required
    // for all values from 1 to V
    for (int i = 1; i <= V; i++) {

        // Go through all arr
        // smaller than i
        for (int j = 0; j < m; j++) {

            // If current coin value
            // is less than i
            if (arr[j] <= i) {
                int sub_res = table[i - arr[j]];

                // Update table[i]
                if (sub_res != -1 && sub_res + 1 > table[i])
                    table[i] = sub_res + 1;
            }
        }
    }

    // Return the final count
    return table[V];
}

// Driver Code
int main()
{

    // Given array
    vector<int> arr = { 25, 10, 5 };
    int m = arr.size();

    // Given sum V
    int V = 30;

    // Function call
    cout << (maxCount(arr, m, V));

    return 0;
}

// This code is contributed by mohit kumar 29
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;

class GFG {

    // Function that count the maximum
    // number of elements to obtain sum V
    static int maxCount(int arr[], int m, int V)
    {
        // Stores the maximum number of
        // elements required to obtain V
        int table[] = new int[V + 1];

        // Base Case
        table[0] = 0;

        // Initialize all table values
        // as Infinite
        for (int i = 1; i <= V; i++)
            table[i] = -1;

        // Find the max arr required
        // for all values from 1 to V
        for (int i = 1; i <= V; i++) {

            // Go through all arr
            // smaller than i
            for (int j = 0; j < m; j++) {

                // If current coin value
                // is less than i
                if (arr[j] <= i) {

                    int sub_res = table[i - arr[j]];

                    // Update table[i]
                    if (sub_res != -1
                        && sub_res + 1 > table[i])
                        table[i] = sub_res + 1;
                }
            }
        }

        // Return the final count
        return table[V];
    }

    // Driver Code
    public static void main(String[] args)
    {
        // Given array
        int arr[] = { 25, 10, 5 };
        int m = arr.length;

        // Given sum V
        int V = 30;

        // Function Call
        System.out.println(maxCount(arr, m, V));
    }
}
```

## 蟒蛇 3

```
# Python program for the
# above approach

# Function that count
# the maximum number of
# elements to obtain sum V
def maxCount(arr, m, V):
    '''
    You can assume array elements as domination
    which are provided to you in infinite quantity
    just like in coin change problem.
    I made a small change in logic on coin change
    problem (minimum number of coins required).
    There we use to take min(table[i-arr[j]]+1,table[i]),
    here min is changed with max function.
    Dry run:
    assume : taget = 10, arr = [2,3,5]

    table   0  1  2  3  4  5  6  7  8  9  10
            0 -1 -1 -1 -1 -1 -1 -1 -1 -1 -1

    taking first domination = 2

    table    0  1  2  3  4  5  6  7  8  9  10
             0 -1  1 -1  2 -1  3 -1  4 -1  5

    taking second domination = 3

    table    0  1  2  3  4  5  6  7  8  9  10 
             0 -1  1  1  2 -1  3 -1  4  3  5  
    here for i = 6 we have max(table[i-dom]+1,table[i])        
    hence
    => max(table[6-3]+1,table[6])
    => max(2,3) => 3

    taking third domination = 5

    table    0  1  2  3  4  5  6  7  8  9  10 
             0 -1  1  1  2  1  3 -1  4  3  5 

    Hence total 5 coins are required (2,2,2,2,2)
    '''
    # Stores the maximum
    # number of elements
    # required to obtain V
    table = [0 for i in range(V+1)]

    # Base Case
    table[0] = 0

    # Initialize all table
    # values as Infinite
    for i in range(1, V + 1, 1):
        table[i] = -1

        # Find the max arr required
        # for all values from 1 to V
        for i in range(1, V + 1, 1):

            # Go through all arr
            # smaller than i
            for j in range(0, m, 1):

                # If current coin value
                # is less than i
                if (arr[j] <= i):
                    sub_res = table[i - arr[j]]

                    # Update table[i]
                    if (sub_res != -1 and
                        sub_res + 1 > table[i]):
                        table[i] = sub_res + 1

    # Return the final count
    return table[V]

# Driver Code
if __name__ == '__main__':

    # Given array
    arr = [25, 10, 5]
    m = len(arr)

    # Given sum V
    V = 30

    # Function Call
    print(f'Maximum number of array elements required :
                                 {maxCount(arr, m, V)}')

# This code is contributed by Aaryaman Sharma
```

## C#

```
// C# program for the
// above approach
using System;
class GFG{

// Function that count the
// maximum number of elements
// to obtain sum V
static int maxCount(int[] arr,
                    int m, int V)
{
  // Stores the maximum number of
  // elements required to obtain V
  int[] table = new int[V + 1];

  // Base Case
  table[0] = 0;

  // Initialize all table
  // values as Infinite
  for (int i = 1; i <= V; i++)
    table[i] = -1;

  // Find the max arr required
  // for all values from 1 to V
  for (int i = 1; i <= V; i++)
  {
    // Go through all arr
    // smaller than i
    for (int j = 0; j < m; j++)
    {
      // If current coin value
      // is less than i
      if (arr[j] <= i)
      {
        int sub_res = table[i - arr[j]];

        // Update table[i]
        if (sub_res != -1 &&
            sub_res + 1 > table[i])
          table[i] = sub_res + 1;
      }
    }
  }

  // Return the final count
  return table[V];
}

// Driver code
static void Main()
{
  // Given array
  int[] arr = {25, 10, 5};
  int m = arr.Length;

  // Given sum V
  int V = 30;

  // Function Call
  Console.WriteLine(maxCount(arr,
                             m, V));
}
}

// This code is contributed by divyeshrabadiya07
```

## java 描述语言

```
<script>

// Javascript program for the above approach

    // Function that count the maximum
    // number of elements to obtain sum V
    function maxCount(arr, m, V)
    {
        // Stores the maximum number of
        // elements required to obtain V
        let table = [];

        // Base Case
        table[0] = 0;

        // Initialize all table values
        // as Infinite
        for (let i = 1; i <= V; i++)
            table[i] = -1;

        // Find the max arr required
        // for all values from 1 to V
        for (let i = 1; i <= V; i++) {

            // Go through all arr
            // smaller than i
            for (let j = 0; j < m; j++) {

                // If current coin value
                // is less than i
                if (arr[j] <= i) {

                    let sub_res = table[i - arr[j]];

                    // Update table[i]
                    if (sub_res != -1
                        && sub_res + 1 > table[i])
                        table[i] = sub_res + 1;
                }
            }
        }

        // Return the final count
        return table[V];
    }

// Driver Code

        // Given array
        let arr = [ 25, 10, 5 ];
        let m = arr.length;

        // Given sum V
        let V = 30;

        // Function Call
        document.write(maxCount(arr, m, V));

</script>
```

**Output**

```
6
```

***时间复杂度:** O(N * V)*
***辅助空间:** O(N)*
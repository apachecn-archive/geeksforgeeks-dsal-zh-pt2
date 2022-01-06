# 一对相邻元素之间的最大差异，排除每个元素一次

> 原文:[https://www . geeksforgeeks . org/一对相邻元素之间的最大差异-排除每个元素一次/](https://www.geeksforgeeks.org/maximum-difference-between-a-pair-of-adjacent-elements-by-excluding-every-element-once/)

给定一个由正整数组成的[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** ，每个数组元素的任务是找出除该元素之外的任意两个相邻数组之间的**最大**差。

***例:***

> ***输入:** arr[]* = {1，3，4，7，8}
> **输出:** 3，4，4
> **解释:**
> 排除 i = 2，arr[] = {1，4，7，8}。因此，最大相邻元素差异为 3。
> 不包括 i = 3，arr[] = {1，3，7，8}。因此，最大相邻元素差异为 4。
> 不包括 i = 4，arr[] = {1，3，4，8}。因此，最大相邻元素差异为 4。
> 
> **输入:** arr[] = {1，2，7 }
> T3】输出: 6

**天真方法:**最简单的方法是使用[遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，对于每个元素，计算除该元素之外的相邻元素之间的差异，并打印得到的最大差异。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to calculate maximum
// difference between adjacent elements
// excluding every array element once
void maxAdjacent(int* arr, int N)
{
    vector<int> res;

    // Traverse the array
    for (int i = 1; i < N - 1; i++) {

        int prev = arr[0];

        // Stores the maximum diff
        int maxi = INT_MIN;

        // Check for maximum
        // adjacent element
        for (int j = 1; j < N; j++) {

            // Exclude current element
            if (i == j)
                continue;

            // Update maximum difference
            maxi = max(maxi, abs(arr[j] - prev));

            // Update previous value
            prev = arr[j];
        }

        // Append the result
        // into a vector
        res.push_back(maxi);
    }

    // Print the result
    for (auto x : res)
        cout << x << " ";
    cout << endl;
}

// Driver Code
int main()
{
    int arr[] = { 1, 3, 4, 7, 8 };
    int N = sizeof(arr) / sizeof(arr[0]);
    maxAdjacent(arr, N);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of above approach 
import java.util.*;
class GFG
{

  // Function to calculate maximum
  // difference between adjacent elements
  // excluding every array element once
  static void maxAdjacent(int[] arr, int N)
  {
    ArrayList<Integer> res = new ArrayList<Integer>();

    // Traverse the array
    for (int i = 1; i < N - 1; i++)
    {
      int prev = arr[0];

      // Stores the maximum diff
      int maxi = Integer.MIN_VALUE;

      // Check for maximum
      // adjacent element
      for (int j = 1; j < N; j++)
      {

        // Exclude current element
        if (i == j)
          continue;

        // Update maximum difference
        maxi = Math.max(maxi, Math.abs(arr[j] - prev));

        // Update previous value
        prev = arr[j];
      }

      // Append the result
      // into a vector
      res.add(maxi);
    }

    // Print the result
    for (int x : res)
    {
      System.out.print(x + " ");
    }
    System.out.println();
  }
  // Driver code
  public static void main(String[] args)
  {
    int[] arr = { 1, 3, 4, 7, 8 };
    int N = arr.length;
    maxAdjacent(arr, N);
  }
}

// This code is contributed by sanjoy_62.
```

## 蟒蛇 3

```
# Python program for the above approach

# Function to calculate maximum
# difference between adjacent elements
# excluding every array element once
def maxAdjacent(arr, N):
    res = []

    # Traverse the array
    for i in range(1, N - 1):
        prev = arr[0]

        # Stores the maximum diff
        maxi = -1* float('inf')

        # Check for maximum
        # adjacent element
        for j in range(1,N):

            # Exclude current element
            if (i == j):
                continue

            # pdate maximum difference
            maxi = max(maxi, abs(arr[j] - prev))

            # Update previous value
            prev = arr[j]

        # Append the result
        # into a vector
        res.append(maxi)

    # Print the result
    for x in res:
        print(x,end=' ')
    print()

# Driver Code
arr = [ 1, 3, 4, 7, 8 ]
N = len(arr)
maxAdjacent(arr, N)

# This code is contributed by rohitsingh07052.
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

public class GFG
{

  // Function to calculate maximum
  // difference between adjacent elements
  // excluding every array element once
  static void maxAdjacent(int[] arr, int N)
  {
    List<int> res = new List<int>();

    // Traverse the array
    for (int i = 1; i < N - 1; i++)
    {
      int prev = arr[0];

      // Stores the maximum diff
      int maxi = Int32.MinValue;

      // Check for maximum
      // adjacent element
      for (int j = 1; j < N; j++)
      {

        // Exclude current element
        if (i == j)
          continue;

        // Update maximum difference
        maxi = Math.Max(maxi, Math.Abs(arr[j] - prev));

        // Update previous value
        prev = arr[j];
      }

      // Append the result
      // into a vector
      res.Add(maxi);
    }

    // Print the result
    foreach (int x in res)
    {
      Console.Write(x + " ");
    }
    Console.WriteLine();
  }

// Driver Code
static public void Main ()
{
    int[] arr = { 1, 3, 4, 7, 8 };
    int N = arr.Length;
    maxAdjacent(arr, N);
}
}

// This code is contributed by code_hunt.
```

## java 描述语言

```
<script>
//Javascript program for
//the above approach

// Function to calculate maximum
// difference between adjacent elements
// excluding every array element once
function maxAdjacent(arr, N)
{
    var res = [];

    // Traverse the array
    for (var i = 1; i < N - 1; i++) {

        var prev = arr[0];

        // Stores the maximum diff
        var maxi = Number.MIN_VALUE;

        // Check for maximum
        // adjacent element
        for (var j = 1; j < N; j++) {

            // Exclude current element
            if (i == j)
                continue;

            // Update maximum difference
            maxi = Math.max(maxi, Math.abs(arr[j] - prev));

            // Update previous value
            prev = arr[j];
        }

        // Append the result
        // into a vector
        res.push(maxi);
    }

    // Print the result
    for (var j = 0; j < res.length; j++)
        document.write(res[j] + " ");
    document.write("<br>");
}

var arr = [ 1, 3, 4, 7, 8 ];
var N = arr.length;
maxAdjacent(arr, N);

// This code is contributed by SoumikMondal
</script>
```

**Output:** 

```
3 4 4
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*

**高效方法:**可以清楚地观察到，如果一个元素被排除在数组之外，那么最大差值要么保持不变，要么等于被排除元素的下一个和上一个之间的差值。按照以下步骤解决问题:

1.  计算数组相邻元素之间的最大差异。
2.  [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)并执行以下操作:
    1.  评估前一个元素和被排除元素旁边的数组元素之间的差异。
    2.  如果计算的最大相邻差超过上一步获得的差，将整个数组的最大相邻差插入向量 **res** 。
    3.  否则，将被排除元素旁边的前一个数组元素和后一个数组元素之间的差插入到向量 **res** 中。
3.  打印矢量 **res** 。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to calculate maximum
// difference between adjacent elements
// excluding every array element once
void maxAdjacent(int* arr, int N)
{
    vector<int> res;

    int arr_max = INT_MIN;

    // Compute maximum adjacent
    // difference for whole array
    for (int i = 1; i < N; i++) {

        arr_max = max(arr_max,
                      abs(arr[i - 1] - arr[i]));
    }

    for (int i = 1; i < N - 1; i++) {

        int curr_max = abs(arr[i - 1]
                           - arr[i + 1]);

        // Store the maximum between
        // arr_max and curr_max
        int ans = max(curr_max, arr_max);

        // Append the result
        // into a vector
        res.push_back(ans);
    }

    // Print the result
    for (auto x : res)
        cout << x << " ";
    cout << endl;
}

// Driver Code
int main()
{
    int arr[] = { 1, 3, 4, 7, 8 };
    int N = sizeof(arr) / sizeof(arr[0]);
    maxAdjacent(arr, N);

}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
class GFG
{

  // Function to calculate maximum
  // difference between adjacent elements
  // excluding every array element once
  static void maxAdjacent(int []arr, int N)
  {
    Vector<Integer> res = new Vector<Integer>();
    int arr_max = Integer.MIN_VALUE;

    // Compute maximum adjacent
    // difference for whole array
    for (int i = 1; i < N; i++)
    {
      arr_max = Math.max(arr_max,
                         Math.abs(arr[i - 1] - arr[i]));
    }

    for (int i = 1; i < N - 1; i++)
    {
      int curr_max = Math.abs(arr[i - 1]
                              - arr[i + 1]);

      // Store the maximum between
      // arr_max and curr_max
      int ans = Math.max(curr_max, arr_max);

      // Append the result
      // into a vector
      res.add(ans);
    }

    // Print the result
    for (int x : res)
      System.out.print(x + " ");
    System.out.println();
  }

  // Driver Code
  public static void main(String[] args)
  {
    int arr[] = { 1, 3, 4, 7, 8 };
    int N = arr.length;
    maxAdjacent(arr, N);
  }
}

// This code is contributed by shikhasingrajput
```

## 蟒蛇 3

```
# Python 3 program for the above approach
import sys

# Function to calculate maximum
# difference between adjacent elements
# excluding every array element once
def maxAdjacent(arr, N):
    res = []
    arr_max = -sys.maxsize - 1

    # Compute maximum adjacent
    # difference for whole array
    for i in range(1, N):

        arr_max = max(arr_max,
                      abs(arr[i - 1] - arr[i]))
    for i in range(1, N - 1):
        curr_max = abs(arr[i - 1]
                       - arr[i + 1])

        # Store the maximum between
        # arr_max and curr_max
        ans = max(curr_max, arr_max)

        # Append the result
        # into a vector
        res.append(ans)

    # Print the result
    for x in res:
        print(x, end=" ")
    print()

# Driver Code
if __name__ == "__main__":

    arr = [1, 3, 4, 7, 8]
    N = len(arr)
    maxAdjacent(arr, N)

    # This code is contributed by chitranayal.
```

## C#

```
// C# Program to implement
// the above approach
using System;
using System.Collections.Generic;

class GFG
{
  // Function to calculate maximum
  // difference between adjacent elements
  // excluding every array element once
  static void maxAdjacent(int []arr, int N)
  {
    List<int> res = new List<int>();
    int arr_max = Int32.MinValue;

    // Compute maximum adjacent
    // difference for whole array
    for (int i = 1; i < N; i++)
    {
      arr_max = Math.Max(arr_max,
                         Math.Abs(arr[i - 1] - arr[i]));
    }

    for (int i = 1; i < N - 1; i++)
    {
      int curr_max = Math.Abs(arr[i - 1]
                              - arr[i + 1]);

      // Store the maximum between
      // arr_max and curr_max
      int ans = Math.Max(curr_max, arr_max);

      // Append the result
      // into a vector
      res.Add(ans);
    }

    // Print the result
    foreach (int x in res)
    Console.Write(x + " ");
    Console.WriteLine();
  }

// Driver Code
public static void Main(String[] args)
{
    int[] arr = { 1, 3, 4, 7, 8 };
    int N = arr.Length;
    maxAdjacent(arr, N);
}
}

// This code is contributed by susmitakundugoaldanga.
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to calculate maximum
// difference between adjacent elements
// excluding every array element once
function maxAdjacent(arr,N)
{
    let res = [];
    let arr_max = Number.MIN_VALUE;

    // Compute maximum adjacent
    // difference for whole array
    for (let i = 1; i < N; i++)
    {
      arr_max = Math.max(arr_max,
                         Math.abs(arr[i - 1] - arr[i]));
    }

    for (let i = 1; i < N - 1; i++)
    {
      let curr_max = Math.abs(arr[i - 1]
                              - arr[i + 1]);

      // Store the maximum between
      // arr_max and curr_max
      let ans = Math.max(curr_max, arr_max);

      // Append the result
      // into a vector
      res.push(ans);
      }

    // Print the result
    document.write(res.join(" "));
}

// Driver Code
let arr=[1, 3, 4, 7, 8];
let N = arr.length;
maxAdjacent(arr, N);

// This code is contributed by avanitrachhadiya2155
</script>
```

***Output:** *

```
*3 4 4*
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)
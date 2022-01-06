# 查找乘积小于或等于 K 的所有可能的子阵列

> 原文:[https://www . geeksforgeeks . org/find-all-可能性-子阵列-具有小于或等于 k 的乘积/](https://www.geeksforgeeks.org/find-all-possible-subarrays-having-product-less-than-or-equal-to-k/)

给定一个数组 **arr[]** ，任务是[打印所有可能的子数组](https://www.geeksforgeeks.org/generating-subarrays-using-recursion/)，其元素的乘积小于或等于 **K** 。

> **输入:** arr[] = {2，1，3，4，5，6，2}，K = 10
> **输出:** [[2]，[1]，[2，1]，[3]，[1，3]，[2，1，3]，[4]，[5]，[6]，[2]]
> **解释:**
> 所有可能的积≤ K 的子阵列为{2}、{1}、{2，1}、{3}
> 
> **输入:** arr[] = {2，7，1，4}，K = 7
> **输出:** [[2]，[7]，[1]，[7，1]，[4]，[1，4]]

**天真方法:**解决问题最简单的方法是[从给定的阵列生成所有可能的子阵列](https://www.geeksforgeeks.org/generating-subarrays-using-recursion/)，对于每个子阵列，检查其乘积是否小于或等于 **K** 并相应打印。

***时间复杂度:**O(N<sup>3</sup>)*
***辅助空间:** O(N)*

**高效方法:**上述方法可以通过观察以下内容进行优化:

> 如果一个子阵列的所有元素的乘积小于或等于 **K** ，那么这个子阵列中所有可能的子阵列也有小于或等于 K 的乘积，因此，这些子阵列也需要包含在答案中。

按照以下步骤解决问题:

1.  初始化指向数组第一个索引的指针**开始**。
2.  迭代数组，继续计算数组元素的乘积，并将其存储在一个变量中，比如 **multi** 。
3.  **如果 multi 超过 K:** 继续将 **multi** 除以 **arr【开始】**并继续递增 **start** 直到 **multi** 减少到≤ **K** 。
4.  **如果 multi ≤ K:** 从当前索引迭代到**开始**，并将子阵列存储在[数组列表](https://www.geeksforgeeks.org/arraylist-in-java/)中。
5.  最后，一旦生成所有子阵列，打印包含所有获得的子阵列的**数组列表**。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach
#include<bits/stdc++.h>
using namespace std;

// Function to return all possible
// subarrays having product less
// than or equal to K
vector<vector<int>> maxSubArray(int arr[], int n,
                                int K)
{

    // Store the required subarrays
    vector<vector<int>> solution;

    // Stores the product of
    // current subarray
    int multi = 1;

    // Stores the starting index
    // of the current subarray
    int start = 0;

    // Check for empty array
    if (n <= 1 || K < 0)
    {
        return solution;
    }

    // Iterate over the array
    for(int i = 0; i < n; i++)
    {

        // Calculate product
        multi = multi * arr[i];

        // If product exceeds K
        while (multi > K)
        {

            // Reduce product
            multi = multi / arr[start];

            // Increase starting index
            // of current subarray
            start++;
        }

        // Stores the subarray elements
        vector<int> list;

        // Store the subarray elements
        for(int j = i; j >= start; j--)
        {
            list.insert(list.begin(), arr[j]);

            // Add the subarrays
            // to the list
            solution.push_back(list);
        }
    }

    // Return the final
    // list of subarrays
    return solution;
}

// Driver Code
int main()
{
    int arr[] = { 2, 7, 1, 4 };
    int n = sizeof(arr) / sizeof(arr[0]);
    int K = 7;

    vector<vector<int>> v = maxSubArray(arr, n, K);
    cout << "[";

    bool first = true;
    for(auto x : v)
    {
        if (!first)
        {
            cout << ", ";
        }
        else
        {
            first = false;
        }
        cout << "[";

        bool ff = true;
        for(int y : x)
        {
            if (!ff)
            {
                cout << ", ";
            }
            else
            {
                ff = false;
            }
            cout << y;
        }
        cout << "]";
    }
    cout << "]";

    return 0;
}

// This code is contributed by rutvik_56
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to implement
// the above approach

import java.io.*;
import java.util.*;

class GFG {

    // Function to return all possible
    // subarrays having product less
    // than or equal to K
    public static List<List<Integer> > maxSubArray(
        int[] arr, int K)
    {

        // Store the required subarrays
        List<List<Integer> > solution
            = new ArrayList<>();

        // Stores the product of
        // current subarray
        int multi = 1;

        // Stores the starting index
        // of the current subarray
        int start = 0;

        // Check for empty array
        if (arr.length <= 1 || K < 0) {
            return new ArrayList<>();
        }

        // Iterate over the array
        for (int i = 0; i < arr.length; i++) {

            // Calculate product
            multi = multi * arr[i];

            // If product exceeds K
            while (multi > K) {

                // Reduce product
                multi = multi / arr[start];

                // Increase starting index
                // of current subarray
                start++;
            }

            // Stores the subarray elements
            List<Integer> list
                = new ArrayList<>();

            // Store the subarray elements
            for (int j = i; j >= start; j--) {

                list.add(0, arr[j]);

                // Add the subarrays
                // to the list
                solution.add(
                    new ArrayList<>(list));
            }
        }

        // Return the final
        // list of subarrays
        return solution;
    }

    // Driver Code
    public static void main(String[] args)
    {
        int[] arr = { 2, 7, 1, 4 };
        int K = 7;

        System.out.println(maxSubArray(arr, K));
    }
}
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to return all possible
# subarrays having product less
# than or equal to K
def maxSubArray(arr, n, K):

    # Store the required subarrays
    solution = []

    # Stores the product of
    # current subarray
    multi = 1

    # Stores the starting index
    # of the current subarray
    start = 0

    # Check for empty array
    if (n <= 1 or K < 0):
        return solution

    # Iterate over the array
    for i in range(n):

        # Calculate product
        multi = multi * arr[i]

        # If product exceeds K
        while (multi > K):

            # Reduce product
            multi = multi // arr[start]

            # Increase starting index
            # of current subarray
            start += 1

        # Stores the subarray elements
        li = []

        j = i

        # Store the subarray elements
        while(j >= start):       
            li.insert(0, arr[j])

            # Add the subarrays
            # to the li
            solution.append(list(li))
            j -= 1

    # Return the final
    # li of subarrays
    return solution

# Driver Code
if __name__=='__main__':

    arr = [ 2, 7, 1, 4 ]
    n = len(arr)
    K = 7

    v = maxSubArray(arr, n, K)

    print(v)

# This code is contributed by pratham76
```

## C#

```
// C# Program to implement
// the above approach
using System;
using System.Collections.Generic;
class GFG{

// Function to return all possible
// subarrays having product less
// than or equal to K
public static List<List<int>> maxSubArray(int[] arr,
                                          int K)
{
  // Store the required subarrays
  List<List<int> > solution = new List<List<int>>();

  // Stores the product of
  // current subarray
  int multi = 1;

  // Stores the starting index
  // of the current subarray
  int start = 0;

  // Check for empty array
  if (arr.Length <= 1 || K < 0)
  {
    return new List<List<int>>();
  }

  // Iterate over the array
  for (int i = 0; i < arr.Length; i++)
  {
    // Calculate product
    multi = multi * arr[i];

    // If product exceeds K
    while (multi > K)
    {
      // Reduce product
      multi = multi / arr[start];

      // Increase starting index
      // of current subarray
      start++;
    }

    // Stores the subarray elements
    List<int> list = new List<int>();

    // Store the subarray elements
    for (int j = i; j >= start; j--)
    {
      list.Insert(0, arr[j]);

      // Add the subarrays
      // to the list
      solution.Add(new List<int>(list));
    }
  }

  // Return the final
  // list of subarrays
  return solution;
}

// Driver Code
public static void Main(String[] args)
{
  int[] arr = {2, 7, 1, 4};
  int K = 7;
  List<List<int> > list = maxSubArray(arr, K);
  foreach(List<int> i in list)
  {
    Console.Write("[");
    foreach(int j in i)
    {
      Console.Write(j);
      if(i.Count > 1)
        Console.Write(",");
    }
    Console.Write("]");
  }
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// js program to implement
// the above approach

// Function to return all possible
// subarrays having product less
// than or equal to K
function maxSubArray(arr,  n, K)
{

    // Store the required subarrays
    let solution = [];

    // Stores the product of
    // current subarray
    let multi = 1;

    // Stores the starting index
    // of the current subarray
    let start = 0;

    // Check for empty array
    if (n <= 1 || K < 0)
    {
        return solution;
    }

    // Iterate over the array
    for(let i = 0; i < n; i++)
    {

        // Calculate product
        multi = multi * arr[i];

        // If product exceeds K
        while (multi > K)
        {

            // Reduce product
            multi =Math.floor( multi / arr[start]);

            // Increase starting index
            // of current subarray
            start++;
        }

        // Stores the subarray elements
        let list = [];

        // Store the subarray elements
        for(let j = i; j >= start; j--)
        {
            list.unshift(arr[j]);

            // Add the subarrays
            // to the list
            solution.push(list);
        }
    }

    // Return the final
    // list of subarrays
    return solution;
}

// Driver Code
    let arr = [ 2, 7, 1, 4 ];
    let n = arr.length;
    let K = 7;

    let v = maxSubArray(arr, n, K);
    document.write( "[");

    let first = true;
    for(let x=0;x< v.length;x++)
    {
        if (!first)
        {
            document.write(", ");
        }
        else
        {
            first = false;
        }
        document.write( "[");

        let ff = true;
        for(let y =0;y<v[x].length;y++)
        {
            if (!ff)
            {
                document.write(", ");
            }
            else
            {
                ff = false;
            }
            document.write(v[x][y]);
        }
        document.write("]");
    }
    document.write( "]");

</script>
```

**Output:** 

```
[[2], [7], [1], [7, 1], [4], [1, 4]]
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*
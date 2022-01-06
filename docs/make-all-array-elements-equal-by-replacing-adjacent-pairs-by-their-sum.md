# 用相邻对的和替换相邻对，使所有数组元素相等

> 原文:[https://www . geeksforgeeks . org/通过用它们的总和替换相邻对来使所有数组元素相等/](https://www.geeksforgeeks.org/make-all-array-elements-equal-by-replacing-adjacent-pairs-by-their-sum/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**，任务是用它们的和替换最少数量的相邻元素对，使[个数组元素相等](https://www.geeksforgeeks.org/all-elements-in-an-array-are-same-or-not/)。打印所需的最小操作次数。

**示例:**

> **输入:** arr[] = {1，2，3}
> **输出:** 1
> **解释:**用 arr[0]和 arr[1]的和替换它们。因此，数组修改为{3，3}。
> 完成上述操作后，所有数组元素变得相等。
> 因此，所需操作次数为 1。
> 
> **输入:** arr[] = {4，4，4 }
> T3】输出: 0

**方法:**给定的问题可以使用[前缀和数组](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/)技术来解决。按照以下步骤解决给定的问题:

*   初始化一个变量，比如**计数**，以存储对于任何给定的和值可以获得的子阵列的最大计数。
*   初始化一个辅助数组**前缀[]** ，大小为 **N** ，并在其中存储给定数组 **arr[]** 的[前缀和。](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/)
*   [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **前缀[]** ，对于每个元素**前缀【I】**，执行以下步骤:
    *   检查给定的数组 **arr[]** 是否可以划分为带有和**前缀【I】**的子数组。如果发现**为真**，则将这些子阵列的计数存储在一个变量中，比如**和**。
    *   更新**计数**的值为**计数**和 **ans** 的最大值。
*   完成上述步骤后，打印**(N–count)**的值作为所需的最小操作次数。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to count the minimum number
// of pairs of adjacent elements required
// to be replaced by their sum to make all
// array elements equal
int minSteps(vector<int> a, int n)
{

    // Stores the prefix sum of the array
    vector<int> prefix_sum(n);
    prefix_sum[0] = a[0];

    // Calculate the prefix sum array
    for (int i = 1; i < n; i++)
        prefix_sum[i] += prefix_sum[i - 1] + a[i];

    // Stores the maximum number of subarrays
    // into which the array can be split
    int mx = -1;

    // Iterate over all possible sums
    for (int subgroupsum :prefix_sum)
    {

        int sum = 0;
        int i = 0;
        int grp_count = 0;

        // Traverse the array
        while (i < n)
        {
            sum += a[i];

            // If the sum is equal to
            // the current prefix sum
            if (sum == subgroupsum)
            {
                // Increment count
                // of groups by 1
                grp_count += 1;
                sum = 0;
              }

            // Otherwise discard
            // this subgroup sum
            else if(sum > subgroupsum)
            {

                grp_count = -1;
                break;
              }
            i += 1;
          }

        // Update the maximum
        // this of subarrays
        if (grp_count > mx)
            mx = grp_count;
      }

    // Return the minimum
    // number of operations
    return n - mx;
}

// Driver Code
int main()
{
  vector<int> A = {1, 2, 3, 2, 1, 3};
  int N = A.size();

  // Function Call
  cout << minSteps(A, N);

  return 0;
}

// This code is contributed by mohit kumar 29.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to count the minimum number
// of pairs of adjacent elements required
// to be replaced by their sum to make all
// array elements equal
static int minSteps(ArrayList<Integer> a, int n)
{

    // Stores the prefix sum of the array
    int []prefix_sum = new int[n];
    prefix_sum[0] = a.get(0);

    // Calculate the prefix sum array
    for(int i = 1; i < n; i++)
        prefix_sum[i] += prefix_sum[i - 1] + a.get(i);

    // Stores the maximum number of subarrays
    // into which the array can be split
    int mx = -1;

    // Iterate over all possible sums
    for(int subgroupsum : prefix_sum)
    {
        int sum = 0;
        int i = 0;
        int grp_count = 0;

        // Traverse the array
        while (i < n)
        {
            sum += a.get(i);

            // If the sum is equal to
            // the current prefix sum
            if (sum == subgroupsum)
            {

                // Increment count
                // of groups by 1
                grp_count += 1;
                sum = 0;
            }

            // Otherwise discard
            // this subgroup sum
            else if(sum > subgroupsum)
            {
                grp_count = -1;
                break;
            }
            i += 1;
        }

        // Update the maximum
        // this of subarrays
        if (grp_count > mx)
            mx = grp_count;
    }

    // Return the minimum
    // number of operations
    return n - mx;
}

// Driver Code
public static void main(String[] args)
{  
   ArrayList<Integer>A = new ArrayList<Integer>();
   A.add(1);
   A.add(2);
   A.add(3);
   A.add(2);
   A.add(1);
   A.add(3);

  int N = A.size();

  // Function Call
  System.out.print(minSteps(A, N));
}
}

// This code is contributed by sanjoy_62
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to count the minimum number
# of pairs of adjacent elements required
# to be replaced by their sum to make all
# arrat elements equal
def minSteps(a, n):

    # Stores the prefix sum of the array   
    prefix_sum = a[:]

    # Calculate the prefix sum array
    for i in range(1, n):
        prefix_sum[i] += prefix_sum[i-1]

    # Stores the maximum number of subarrays
    # into which the array can be split
    mx = -1

    # Iterate over all possible sums
    for subgroupsum in prefix_sum:

        sum = 0
        i = 0
        grp_count = 0

        # Traverse the array
        while i < n:
            sum += a[i]

            # If the sum is equal to
            # the current prefix sum
            if sum == subgroupsum:

                # Increment count
                # of groups by 1
                grp_count += 1
                sum = 0

            # Otherwise discard
            # this subgroup sum
            elif sum > subgroupsum:

                grp_count = -1
                break

            i += 1

        # Update the maximum
        # this of subarrays      
        if grp_count > mx:
            mx = grp_count

    # Return the minimum
    # number of operations   
    return n - mx

# Driver Code
if __name__ == '__main__':

    A = [1, 2, 3, 2, 1, 3]
    N = len(A)

    # Function Call
    print(minSteps(A, N))
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;
class GFG
{

   // Function to count the minimum number
// of pairs of adjacent elements required
// to be replaced by their sum to make all
// array elements equal
static int minSteps(List<int> a, int n)
{

    // Stores the prefix sum of the array
    int []prefix_sum = new int[n];
    prefix_sum[0] = a[0];

    // Calculate the prefix sum array
    for (int i = 1; i < n; i++)
        prefix_sum[i] += prefix_sum[i - 1] + a[i];

    // Stores the maximum number of subarrays
    // into which the array can be split
    int mx = -1;

    // Iterate over all possible sums
    foreach (int subgroupsum in prefix_sum)
    {

        int sum = 0;
        int i = 0;
        int grp_count = 0;

        // Traverse the array
        while (i < n)
        {
            sum += a[i];

            // If the sum is equal to
            // the current prefix sum
            if (sum == subgroupsum)
            {
                // Increment count
                // of groups by 1
                grp_count += 1;
                sum = 0;
              }

            // Otherwise discard
            // this subgroup sum
            else if(sum > subgroupsum)
            {

                grp_count = -1;
                break;
              }
            i += 1;
          }

        // Update the maximum
        // this of subarrays
        if (grp_count > mx)
            mx = grp_count;
      }

    // Return the minimum
    // number of operations
    return n - mx;
}

// Driver Code
public static void Main()
{
  List<int> A = new List<int>(){1, 2, 3, 2, 1, 3};
  int N = A.Count;

  // Function Call
  Console.Write(minSteps(A, N));
}
}

// This code is contributed by SURENDRA_GANGWAR.
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to count the minimum number
// of pairs of adjacent elements required
// to be replaced by their sum to make all
// array elements equal
function minSteps(a, n)
{

    // Stores the prefix sum of the array
    var prefix_sum = Array(n).fill(0);
    prefix_sum[0] = a[0];

    // Calculate the prefix sum array
    for (var i = 1; i < n; i++)
        prefix_sum[i] += prefix_sum[i - 1] + a[i];

    // Stores the maximum number of subarrays
    // into which the array can be split
    var mx = -1;

    // Iterate over all possible sums
    for (var subgroupsum =0;
    subgroupsum<prefix_sum.length; subgroupsum++)
    {

        var sum = 0;
        var i = 0;
        var grp_count = 0;

        // Traverse the array
        while (i < n)
        {
            sum += a[i];

            // If the sum is equal to
            // the current prefix sum
            if (sum == prefix_sum[subgroupsum])
            {
                // Increment count
                // of groups by 1
                grp_count += 1;
                sum = 0;
            }

            // Otherwise discard
            // this subgroup sum
            else if(sum > prefix_sum[subgroupsum])
            {

                grp_count = -1;
                break;
            }
            i += 1;
        }

        // Update the maximum
        // this of subarrays
        if (grp_count > mx)
            mx = grp_count;
    }

    // Return the minimum
    // number of operations
    return n - mx;
}

// Driver Code
var A = [1, 2, 3, 2, 1, 3];
var N = A.length;

// Function Call
document.write( minSteps(A, N));

</script>
```

**Output:** 

```
2
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(N)*
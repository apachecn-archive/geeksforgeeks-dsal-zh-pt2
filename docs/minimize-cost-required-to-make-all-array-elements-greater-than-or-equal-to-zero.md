# 最小化使所有数组元素大于或等于零所需的成本

> 原文:[https://www . geesforgeks . org/minimum-制作所有数组元素所需的成本-大于或等于零/](https://www.geeksforgeeks.org/minimize-cost-required-to-make-all-array-elements-greater-than-or-equal-to-zero/)

给定一个由 **N** 个整数和一个整数 **X** 组成的[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】】**，任务是通过多次执行以下操作，找到使所有数组元素大于或等于 **0** 所需的最小成本:

*   将任何数组元素增加 1。成本= 1。
*   将所有数组元素增加 1。成本= X。

**示例:**

> **输入:** arr[] = {-1，-3，3，4，5}，X = 2
> **输出:** 4
> **解释:**
> 将 arr[0]增加 1。数组 arr[]修改为{0，-3，3，4，5}。成本= 1。
> 将 arr[1]增加 1 三倍。数组 arr[]修改为{0，0，3，4，5}。因此，成本= 4。
> 因此，所需总成本为 4。
> 
> **输入:** arr[] = {-3，-2，-1，-5，7}，X = 2
> T3】输出: 8

**进场:**思路是用[贪婪进场](https://www.geeksforgeeks.org/greedy-algorithms/)解决问题。按照以下步骤解决问题:

*   [按升序排列数组 **arr[]** 。](https://www.geeksforgeeks.org/c-program-to-sort-an-array-in-ascending-order/)
*   初始化一个辅助[向量](https://www.geeksforgeeks.org/vector-in-cpp-stl/)，比如**列表，**来存储负数组元素。
*   初始化一个变量 **cost = 0，**存储制作当前数组元素 **0** 所需的成本，另一个变量 **min_cost = INT_MAX** 存储制作所有数组元素 **> = 0** 所需的最终最小成本。
*   [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)**arr【】**并尝试通过应用合适的操作转换列表 **> = 0** 中的所有数组元素，并相应地更新 **min_cost** 。
*   打印 **min_cost** 的值作为答案。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum
// cost to make all array elements
// greater than or equal to 0
void minCost(int arr[], int N, int X)
{
    // Sort the array in
    // ascending order
    sort(arr, arr + N);

    int sum = 0;

    // Stores the cost to make
    // current array element >= 0
    int cost = 0;

    // Stores the cost to make
    // all array elements >= 0
    int min_cost = INT_MAX;

    // Traverse the array and insert all the
    // elements which are < 0
    for (int i = 0; i < N; i++) {

        // If current array element
        // is negative
        if (arr[i] < 0) {

            // Cost to make all array
            // elements >= 0
            cost = abs(arr[i]) * X
                   + (sum - abs(arr[i]) * i);
            sum += abs(arr[i]);

            // Update curr if ans is minimum
            min_cost = min(min_cost, cost);
        }
    }

    // Print the minimum cost
    cout << min_cost;
}

// Driver Code
int main()
{
    // Given array
    int arr[] = { -1, -3, -2, 4, -1 };

    // Size of the array
    int N = sizeof(arr) / sizeof(arr[0]);

    // Given value of X
    int X = 2;

    // Function call to find minimum
    // cost to make all array elements >= 0
    minCost(arr, N, X);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.Arrays;
public class GFG
{   

  // Function to find the minimum
  // cost to make all array elements
  // greater than or equal to 0
  static void minCost(int arr[], int N, int X)
  {

    // Sort the array in
    // ascending order
    Arrays.sort(arr) ;

    int sum = 0;

    // Stores the cost to make
    // current array element >= 0
    int cost = 0;

    int INT_MAX = Integer.MAX_VALUE;

    // Stores the cost to make
    // all array elements >= 0
    int min_cost = INT_MAX;

    // Traverse the array and insert all the
    // elements which are < 0
    for (int i = 0; i < N; i++) {

      // If current array element
      // is negative
      if (arr[i] < 0) {

        // Cost to make all array
        // elements >= 0
        cost = Math.abs(arr[i]) * X
          + (sum - Math.abs(arr[i]) * i);
        sum += Math.abs(arr[i]);

        // Update curr if ans is minimum
        min_cost = Math.min(min_cost, cost);
      }
    }

    // Print the minimum cost
    System.out.print(min_cost);
  }

  // Driver Code
  public static void main (String[] args)
  {

    // Given array
    int arr[] = { -1, -3, -2, 4, -1 };

    // Size of the array
    int N = arr.length;

    // Given value of X
    int X = 2;

    // Function call to find minimum
    // cost to make all array elements >= 0
    minCost(arr, N, X);

  }

}

// This code is contributed by AnkThon
```

## 蟒蛇 3

```
# Python3 program for the above approach
import sys

# Function to find the minimum
# cost to make all array of elements
# greater than or equal to 0
def mincost(arr, N, X):

    # sort the array in
    # ascending order
    arr.sort()
    sum = 0

    # stores the count to make
    # current array element >=0
    cost = 0

    # stores the cost to make
    # all array elements >=0
    min_cost = sys.maxsize

    # Traverse the array and insert all the
    # elements which are <=0
    for i in range(0, N):

        # if current array element
        # is negative
        if (arr[i] < 0):

            # cost to make all array
            # elements >=0
            cost = abs(arr[i]) * x + (sum - abs(arr[i]) * i)
            sum += abs(arr[i])

            # update curr if ans is minimum
            min_cost = min(min_cost,cost)

    # return minimum cost
    return min_cost

# Driver code
arr = [-1, -3, -2, 4, -1]

# size of the array
N = len(arr)

# Given value of x
x = 2

# Function call to find minimum
# cost to make all array elements >=0
print(mincost(arr, N, x))

# This code is contributed by Virusbuddah
```

## C#

```
// C# program for the above approach
using System;
class GFG{

// Function to find the minimum
// cost to make all array elements
// greater than or equal to 0
static void minCost(int[] arr, int N, int X)
{

    // Sort the array in
    // ascending order
    Array.Sort(arr) ;

    int sum = 0;

    // Stores the cost to make
    // current array element >= 0
    int cost = 0;

    //int INT_MAX = Int32.MaxValue;

    // Stores the cost to make
    // all array elements >= 0
    int min_cost = Int32.MaxValue;

    // Traverse the array and insert all the
    // elements which are < 0
    for(int i = 0; i < N; i++)
    {

        // If current array element
        // is negative
        if (arr[i] < 0)
        {

            // Cost to make all array
            // elements >= 0
            cost = Math.Abs(arr[i]) * X + 
            (sum - Math.Abs(arr[i]) * i);
            sum += Math.Abs(arr[i]);

            // Update curr if ans is minimum
            min_cost = Math.Min(min_cost, cost);
        }
    }

    // Print the minimum cost
    Console.Write(min_cost);
}

// Driver Code
static public void Main ()
{

    // Given array
    int[] arr = { -1, -3, -2, 4, -1 };

    // Size of the array
    int N = arr.Length;

    // Given value of X
    int X = 2;

    // Function call to find minimum
    // cost to make all array elements >= 0
    minCost(arr, N, X);
}
}

// This code is contributed by susmitakundugoaldanga
```

## java 描述语言

```
<script>
// javascript program for the above approach

  // Function to find the minimum
  // cost to make all array elements
  // greater than or equal to 0
  function minCost(arr , N , X)
  {

    // Sort the array in
    // ascending order
    arr.sort() ;

    var sum = 0;

    // Stores the cost to make
    // current array element >= 0
    var cost = 0;

    var INT_MAX = Number.MAX_VALUE;

    // Stores the cost to make
    // all array elements >= 0
    var min_cost = INT_MAX;

    // Traverse the array and insert all the
    // elements which are < 0
    for (i = 0; i < N; i++) {

      // If current array element
      // is negative
      if (arr[i] < 0) {

        // Cost to make all array
        // elements >= 0
        cost = Math.abs(arr[i]) * X
          + (sum - Math.abs(arr[i]) * i);
        sum += Math.abs(arr[i]);

        // Update curr if ans is minimum
        min_cost = Math.min(min_cost, cost);
      }
    }

    // Print the minimum cost
    document.write(min_cost);
  }

  // Driver Code
//Given array
  var arr = [ -1, -3, -2, 4, -1 ];

  // Size of the array
  var N = arr.length;

  // Given value of X
  var X = 2;

  // Function call to find minimum
  // cost to make all array elements >= 0
  minCost(arr, N, X);

// This code is contributed by 29AjayKumar
</script>
```

**Output:** 

```
5
```

***时间复杂度:** O(N * logN)*
***辅助空间:** O(1)*
# 将完成所有流程所需的成本降至最低

> 原文:[https://www . geesforgeks . org/minimum-完成所有流程所需的成本/](https://www.geeksforgeeks.org/minimize-cost-required-to-complete-all-processes/)

给定一个 [2D 数组](https://www.geeksforgeeks.org/multidimensional-arrays-c-cpp/)**arr【】【】**表格的每一行 **{ X，Y }** ，其中 **Y** 和 **X** 分别代表启动一个流程所需的最小成本和完成该流程所花费的总成本。任务是找到完成给定阵列的所有进程所需的最小成本(如果进程可以以任何顺序完成)。

**示例**:

> **输入:** arr[][] = { { 1，2 }，{ 2，4 }，{ 4，8 } }
> **输出:** 8
> **解释:**
> 考虑 8 的初始成本。
> 启动流程 arr[2]完成流程后，剩余成本= 8–4 = 4
> 启动流程 arr[1]完成流程后，剩余成本= 4–2 = 2
> 启动流程 arr[0]完成流程后，剩余成本= 2–1 = 1
> 因此，所需输出为 8。
> 
> **输入:** arr[][] = { { 1，7 }、{ 2，8 }、{ 3，9 }、{ 4，10 }、{ 5，11 }、{ 6，12 } }
> **输出:** 27

**方法:**使用[贪婪手法](https://www.geeksforgeeks.org/greedy-algorithms/)可以解决问题。按照以下步骤解决问题:

*   [按 Y](https://www.geeksforgeeks.org/sorting-2d-array-according-values-given-column-java/) 降序排列数组。
*   初始化一个变量，比如 **minCost** ，存储完成所有过程所需的最小成本。
*   初始化一个变量，比如 **minCostInit** ，来存储启动一个过程的最小成本。
*   [使用变量 **i** 遍历数组](https://www.geeksforgeeks.org/iterate-over-a-list-in-python/)。每次 **i <sup>第</sup>** 次迭代，检查 **minCostInit** 是否小于 **arr[i][1]** 。如果发现为真，则将**最小成本**的值增加**(arr[I][1]–最小成本初始化)**并更新**最小成本初始化= arr[i][1]** 。
*   在每次 **i <sup>第</sup>T3】次迭代中也更新 **minCostInit -= arr[i][0]** 的值。**
*   最后打印 **minCost** 的值。

下面是上述方法的实现。

## C++

```
// C++ program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

bool func(pair<int, int> i1,
          pair<int, int> i2)
{
    return (i1.first - i1.second <
            i2.first - i2.second);
}

// Function to find minimum cost required
// to complete all the process
int minimumCostReqToCompthePrcess(
    vector<pair<int, int>> arr)
{

    // Sort the array on descending order of Y
    sort(arr.begin(), arr.end(), func);

    // Stores length of array
    int n = arr.size();

    // Stores minimum cost required to
    // complete all the process
    int minCost = 0;

    // Stores minimum cost to initiate
    // any process
    int minCostInit = 0;

    // Traverse the array
    for(int i = 0; i < n; i++)
    {

        // If minCostInit is less than
        // the cost to initiate the process
        if (arr[i].second > minCostInit)
        {

            // Update minCost
            minCost += (arr[i].second -
                        minCostInit);

            // Update minCostInit
            minCostInit = arr[i].second;
        }

        // Update minCostInit
        minCostInit -= arr[i].first;
    }

    // Return minCost
    return minCost;
}

// Driver Code
int main()
{
    vector<pair<int, int>> arr = { { 1, 2 },
                                   { 2, 4 },
                                   { 4, 8 } };

    // Function Call
    cout << (minimumCostReqToCompthePrcess(arr));
}

// This code is contributed by grand_master
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG
{

  // Function to find minimum cost required
  // to complete all the process
  static int minimumCostReqToCompthePrcess(
    int[][] arr)
  {

    // Sort the array on descending order of Y
    Arrays.sort(arr, (a, b)->b[1]-a[1]);

    // Stores length of array
    int n = arr.length;

    // Stores minimum cost required to
    // complete all the process
    int minCost = 0;

    // Stores minimum cost to initiate
    // any process
    int minCostInit = 0;

    // Traverse the array
    for(int i = 0; i < n; i++)
    {

      // If minCostInit is less than
      // the cost to initiate the process
      if (arr[i][1] > minCostInit)
      {

        // Update minCost
        minCost += (arr[i][1] -
                    minCostInit);

        // Update minCostInit
        minCostInit = arr[i][1];
      }

      // Update minCostInit
      minCostInit -= arr[i][0];
    }

    // Return minCost
    return minCost;
  }

  // Driver code
  public static void main (String[] args)
  {
    int[][] arr = { { 1, 2 },
                   { 2, 4 },
                   { 4, 8 } };

    // Function Call
    System.out.println(minimumCostReqToCompthePrcess(arr));
  }
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to find minimum cost required
# to complete all the process
def minimumCostReqToCompthePrcess(arr):

    # Sort the array on descending order of Y
    arr.sort(key = lambda x: x[0] - x[1])

    # Stores length of array
    n = len(arr)

    # Stores minimum cost required to
    # complete all the process
    minCost = 0

    # Stores minimum cost to initiate
    # any process
    minCostInit = 0

    # Traverse the array
    for i in range(n):

        # If minCostInit is less than
        # the cost to initiate the process
        if arr[i][1] > minCostInit:

            # Update minCost
            minCost += (arr[i][1]
                       - minCostInit)

            # Update minCostInit
            minCostInit = arr[i][1]

        # Update minCostInit
        minCostInit -= arr[i][0]

    # Return minCost
    return minCost

# Driver Code
if __name__ == "__main__":
    arr = [[1, 2], [2, 4], [4, 8]]

    # Function Call
    print(minimumCostReqToCompthePrcess(arr))
```

## java 描述语言

```
<script>

// Javascript program to implement
// the above approach

// Function to find minimum cost required
// to complete all the process
function minimumCostReqToCompthePrcess(arr)
{

    // Sort the array on descending order of Y
    arr=arr.map(row=>row).reverse()

    // Stores length of array
    var n = arr.length;

    // Stores minimum cost required to
    // complete all the process
    var minCost = 0;

    // Stores minimum cost to initiate
    // any process
    var minCostInit = 0;

    // Traverse the array
    for(var i = 0; i < n; i++)
    {

        // If minCostInit is less than
        // the cost to initiate the process
        if (arr[i][1] > minCostInit)
        {

            // Update minCost
            minCost += (arr[i][1] -
                        minCostInit);

            // Update minCostInit
            minCostInit = arr[i][1];
        }

        // Update minCostInit
        minCostInit -= arr[i][0];
    }

    // Return minCost
    return minCost;
}

// Driver Code
var arr = [ [ 1, 2 ],
                               [ 2, 4 ],
                               [ 4, 8 ] ];
// Function Call
document.write(minimumCostReqToCompthePrcess(arr));

// This code is contributed by rutvik_56.
</script>
```

**Output:** 

```
8
```

***时间复杂度:** O(N * log(N))*
***辅助空间:** O(1)*
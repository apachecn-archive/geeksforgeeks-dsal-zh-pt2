# 每个玩家来自不同国家的最大可能人数为 K 的队伍

> 原文:[https://www . geeksforgeeks . org/每名来自不同国家/地区的玩家可以参加的最大规模团队数量/](https://www.geeksforgeeks.org/maximum-number-of-teams-of-size-k-possible-with-each-player-from-different-country/)

给定一个由 **N** 正整数和一个正整数 **K** 组成的数组 **arr[]** ，这样就有了 **N** 个国家，每个国家都有 **arr[i]** 个玩家，任务是通过组建大小为 **K** 个团队，使团队中的每个玩家都来自不同的国家，从而找到可以组建的团队的最大数量。

**示例:**

> **输入:** N = 4，K = 3，arr[] = {4，3，5，3}
> **输出:** 5
> **解释:**
> 考虑国家被命名为 A、B、C 和 D，可能的组队方式有{A、B、C}、{A、C、D}、{A、B、C}、{B、C、D}、{A、C、D}这样在每一套中一个人不超过一个
> 
> 因此，组成的团队总数为 5 个。
> 
> **输入:** N = 3，K = 2，arr[] = {2，3，4}
> **输出:** 4
> **解释:**
> 考虑将国家命名为 A、B、C 和 d，可能的组队方式有{B，C}、{B，C}、{A，C}、({A，B}或{A，C}或{B，C})这样在每一套中来自一个国家的人数不超过 1 人。
> 
> 因此，组成的团队总数为 4 个。

**进场:**给定的问题可以用[二分搜索法](https://www.geeksforgeeks.org/binary-search/)来解决，思路是在可以组建的队伍数量上执行二分搜索法。让这个变量为 **T** 。对于 **T** 的每个值，检查是否有可能从给定的每个国家的选手名单中组建 **T** 队。 **T** 如果所有 **i** 在**【0，N–1】**范围内的**arr【I】**或 **T** 的最小值之和大于等于 **T*K** ，则可以组成团队。请按照以下步骤解决此问题:

*   定义一个[函数](https://www.geeksforgeeks.org/functions-in-c/)，比如说**是可能的(arr，mid，K)** 来检查一个 **mid** 数量的团队是否可以组成。
    *   将变量**和**初始化为 **0** ，以存储数组元素的[和。](https://www.geeksforgeeks.org/program-find-sum-elements-given-array/)
    *   [迭代一个范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，N】**并执行以下任务:
        *   将变量**和的最小值**中间值**或**arr【I】**相加。**
    *   如果**之和**大于等于**中*K** ，则返回**真**。否则，返回**假**。
*   初始化变量，说 **lb** 和 **ub** 为 **0** 和 **1e9** 为可以组成的队伍数量的下限和上限。
*   [迭代一段时间循环](https://www.geeksforgeeks.org/c-c-while-loop-with-examples/)直到 **lb** 小于等于 **ub** 并执行以下步骤:
    *   初始化变量，说**中间**为 **ub** 和 **lb** 的平均值。
    *   调用[函数](https://www.geeksforgeeks.org/functions-in-c/) **是可能的(arr，mid，K)** ，如果函数返回**真**，则检查范围的上半部分。否则，检查范围的下半部分。
*   执行上述步骤后，打印**中间**的值作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find if T number of teams
// can be formed or not
bool is_possible(vector<int>& teams,
                 int T, int k)
{
    // Store the sum of array elements
    int sum = 0;

    // Traverse the array teams[]
    for (int i = 0; i < teams.size(); i++) {
        sum += min(T, teams[i]);
    }

    // Required Condition
    return (sum >= (T * k));
}

// Function to find the maximum number
// of teams possible
int countOfTeams(vector<int>& teams_list,
                 int N, int K)
{
    // Lower and Upper part of the range
    int lb = 0, ub = 1e9;

    // Perform the Binary Search
    while (lb <= ub) {

        // Find the value of mid
        int mid = lb + (ub - lb) / 2;

        // Perform the Binary Search
        if (is_possible(teams_list, mid, K)) {

            if (!is_possible(
                    teams_list, mid + 1, K)) {
                return mid;
            }

            // Otherwise, update the
            // search range
            else {
                lb = mid + 1;
            }
        }

        // Otherwise, update the
        // search range
        else {
            ub = mid - 1;
        }
    }
    return 0;
}

// Driver Code
int main()
{
    vector<int> arr = { 2, 3, 4 };
    int K = 2;
    int N = arr.size();
    cout << countOfTeams(arr, N, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG {

    // Function to find if T number of teams
    // can be formed or not
    public static boolean is_possible(int[] teams, int T, int k)
    {

        // Store the sum of array elements
        int sum = 0;

        // Traverse the array teams[]
        for (int i = 0; i < teams.length; i++) {
            sum += Math.min(T, teams[i]);
        }

        // Required Condition
        return (sum >= (T * k));
    }

    // Function to find the maximum number
    // of teams possible
    public static int countOfTeams(int[] teams_list, int N, int K)
    {

        // Lower and Upper part of the range
        int lb = 0;
        double ub = 1e9;

        // Perform the Binary Search
        while (lb <= ub) {

            // Find the value of mid
            int mid = lb + (int) (ub - lb) / 2;

            // Perform the Binary Search
            if (is_possible(teams_list, mid, K)) {

                if (!is_possible(teams_list, mid + 1, K)) {
                    return mid;
                }

                // Otherwise, update the
                // search range
                else {
                    lb = mid + 1;
                }
            }

            // Otherwise, update the
            // search range
            else {
                ub = mid - 1;
            }
        }
        return 0;
    }

    // Driver Code
    public static void main(String args[]) {
        int[] arr = { 2, 3, 4 };
        int K = 2;
        int N = arr.length;
        System.out.println(countOfTeams(arr, N, K));

    }
}

// This code is contributed by _saurabh_jaiswal.
```

## 蟒蛇 3

```
# Python 3 program for the above approach

# Function to find if T number of teams
# can be formed or not
def is_possible(teams, T, k):
    # Store the sum of array elements
    sum = 0

    # Traverse the array teams[]
    for i in range(len(teams)):
        sum += min(T, teams[i])

    # Required Condition
    return (sum >= (T * k))

# Function to find the maximum number
# of teams possible

def countOfTeams(teams_list, N, K):
    # Lower and Upper part of the range
    lb = 0
    ub = 1000000000

    # Perform the Binary Search
    while (lb <= ub):

        # Find the value of mid
        mid = lb + (ub - lb) // 2

        # Perform the Binary Search
        if (is_possible(teams_list, mid, K)):
            if (is_possible(teams_list, mid + 1, K)==False):
                return mid

            # Otherwise, update the
            # search range
            else:
                lb = mid + 1

        # Otherwise, update the
        # search range
        else:
            ub = mid - 1
    return 0

# Driver Code
if __name__ == '__main__':
    arr = [2, 3, 4]
    K = 2
    N = len(arr)
    print(countOfTeams(arr, N, K))

    # This code is contributed by ipg2016107.
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to find if T number of teams
// can be formed or not
public static bool is_possible(int[] teams,
                               int T, int k)
{

    // Store the sum of array elements
    int sum = 0;

    // Traverse the array teams[]
    for(int i = 0; i < teams.Length; i++)
    {
        sum += Math.Min(T, teams[i]);
    }

    // Required Condition
    return (sum >= (T * k));
}

// Function to find the maximum number
// of teams possible
public static int countOfTeams(int[] teams_list,
                               int N, int K)
{

    // Lower and Upper part of the range
    int lb = 0;
    double ub = 1e9;

    // Perform the Binary Search
    while (lb <= ub)
    {

        // Find the value of mid
        int mid = lb + (int) (ub - lb) / 2;

        // Perform the Binary Search
        if (is_possible(teams_list, mid, K))
        {
            if (!is_possible(teams_list, mid + 1, K))
            {
                return mid;
            }

            // Otherwise, update the
            // search range
            else
            {
                lb = mid + 1;
            }
        }

        // Otherwise, update the
        // search range
        else
        {
            ub = mid - 1;
        }
    }
    return 0;
}

// Driver Code
public static void Main(String[] args)
{
    int[] arr = { 2, 3, 4 };
    int K = 2;
    int N = arr.Length;

    Console.WriteLine(countOfTeams(arr, N, K));
}
}

// This code is contributed by code_hunt
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to find if T number of teams
// can be formed or not
function is_possible(teams, T, k) {
  // Store the sum of array elements
  let sum = 0;

  // Traverse the array teams[]
  for (let i = 0; i < teams.length; i++) {
    sum += Math.min(T, teams[i]);
  }

  // Required Condition
  return sum >= T * k;
}

// Function to find the maximum number
// of teams possible
function countOfTeams(teams_list, N, K) {
  // Lower and Upper part of the range
  let lb = 0,
    ub = 1e9;

  // Perform the Binary Search
  while (lb <= ub) {
    // Find the value of mid
    let mid = Math.floor(lb + (ub - lb) / 2);

    // Perform the Binary Search
    if (is_possible(teams_list, mid, K)) {
      if (!is_possible(teams_list, mid + 1, K)) {
        return mid;
      }

      // Otherwise, update the
      // search range
      else {
        lb = mid + 1;
      }
    }

    // Otherwise, update the
    // search range
    else {
      ub = mid - 1;
    }
  }
  return 0;
}

// Driver Code

let arr = [2, 3, 4];
let K = 2;
let N = arr.length;
document.write(countOfTeams(arr, N, K));

</script>
```

**Output:** 

```
4
```

***时间复杂度:** O(N*log N)*
***辅助空间:** O(1)*
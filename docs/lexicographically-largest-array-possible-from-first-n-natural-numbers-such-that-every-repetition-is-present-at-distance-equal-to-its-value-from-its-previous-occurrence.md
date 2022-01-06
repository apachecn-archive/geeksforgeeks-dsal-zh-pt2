# 从第一个 N 个自然数中可能出现的字典上最大的数组，这样每次重复出现的距离等于其与前一次出现的距离

> 原文:[https://www . geesforgeks . org/从第一个 n 个自然数开始按字典顺序排列最大可能数组，这样每次重复出现的距离都等于其先前出现的值/](https://www.geeksforgeeks.org/lexicographically-largest-array-possible-from-first-n-natural-numbers-such-that-every-repetition-is-present-at-distance-equal-to-its-value-from-its-previous-occurrence/)

给定一个正整数 **N** ，任务是构造由第一个 **N** 个自然数组成的大小为**(2 * N–1)**的字典上最大的[数组](https://www.geeksforgeeks.org/array-data-structure/)，使得每个元素出现两次，除了 **1** ，并且在构造的数组中 **X** 的重复正好是 **X** 的间隔距离。

**示例:**

> ***输入:*** N = 4
> ***输出:*** 4 2 3 2 4 3 1
> **解释:**
> 对于生成的数组{4，2，3，2，4，3，1}每个重复元素(比如 X)都在距离 X 处
> 
> ***输入:*** N = 5
> ***输出:*** 5 3 1 4 3 5 2 4 2

**方法:**使用[回溯](https://www.geeksforgeeks.org/backtracking-algorithms/)可以解决问题。其思想是[根据给定的条件生成所有可能的排列](https://www.geeksforgeeks.org/write-a-c-program-to-print-all-permutations-of-a-given-string/)，并打印出满足给定条件的排列。按照以下步骤解决问题:

*   在每个索引处初始化一个大小为**(2 * N–1)****0**的数组，比如 **ans[]** ，以及一个 [HashMap](https://www.geeksforgeeks.org/java-util-hashmap-in-java-with-examples/) ，以存储分配给构造的数组的所有元素。
*   定义函数**构造数组(I，N)** ，通过执行以下步骤生成结果数组:
    *   如果 **i** 的值为**(2 * N–1)**，则生成一个可能的排列。所以，还**真**。
    *   否则，如果当前索引处的值已经赋值，则[递归调用](https://www.geeksforgeeks.org/recursive-functions/)进行下一次迭代**构造一个(i+1，N)** 。
    *   否则，请执行以下操作:
        *   从 **N** 开始，在**【1，N】**范围内放置每个未访问的号码。
        *   如果在上述步骤中选择的值没有导致数组的可能组合，则从数组中移除当前值，并通过分配该范围中的其他元素来尝试其他可能的组合。
        *   如果没有得到可能的组合，则返回**假**。
*   完成上述步骤后，打印获得的数组**和**。

下面是上述方法的实现:

## C++

```
// C++14 program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;
const int N = 4;

// Stores the required sequence
vector<int> ans(2 * N - 1, 0);

// Stores the visited and unvisited values
set<int> visited;

// Function to construct the array
// according to the given conditions
bool constructArray(int i)
{

    // Base Case
    if (i == ans.size()) {
        return true;
    }

    // If a value is already assigned
    // at current index, then recursively
    // call for the next index
    if (ans[i] != 0)
        return constructArray(i + 1);

    else {

        // Iterate over the range[N, 1]
        for (int val = N; val >= 1; val--) {

            // If the current value is
            // already visited, continue
            if (visited.find(val) != visited.end())
                continue;

            // Otherwise, mark this value as
            // visited and set ans[i] = val
            visited.insert(val);
            ans[i] = val;

            // If val is equal to 1, then
            // recursively call for the
            // next index
            if (val == 1) {
                bool found = constructArray(i + 1);

                // If solution is found,
                // then return true
                if (found)
                    return true;
            }

            // For all other values, assign
            // ans[i + val] to val if the
            // i + val < ans.length
            else if (i + val < ans.size()
                     && ans[i + val] == 0) {
                ans[val + i] = val;

                // Recursively call for
                // next index to check if
                // solution can be found
                bool found = constructArray(i + 1);

                // If solution is found then
                // return true
                if (found)
                    return true;

                // BackTracking step
                ans[i + val] = 0;
            }

            // BackTracking step
            ans[i] = 0;
            visited.erase(val);
        }
    }

    // In all other cases, return false
    return false;
}

// Driver code
int main()
{

    // Function Call
    constructArray(0);

    // Print the resultant array
    for (int X : ans)
        cout << X << " ";
    return 0;
}

// This code is contributed by kingash.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.util.*;

class GFG {

    // Stores the required sequence
    static int ans[];

    // Stores the visited and unvisited values
    static HashSet<Integer> visited;

    // Function to construct the array
    // according to the given conditions
    public static boolean
    constructArray(int i, int N)
    {

        // Base Case
        if (i == ans.length) {
            return true;
        }

        // If a value is already assigned
        // at current index, then recursively
        // call for the next index
        if (ans[i] != 0)
            return constructArray(i + 1, N);

        else {

            // Iterate over the range[N, 1]
            for (int val = N; val >= 1; val--) {

                // If the current value is
                // already visited, continue
                if (visited.contains(val))
                    continue;

                // Otherwise, mark this value as
                // visited and set ans[i] = val
                visited.add(val);
                ans[i] = val;

                // If val is equal to 1, then
                // recursively call for the
                // next index
                if (val == 1) {
                    boolean found
                        = constructArray(i + 1, N);

                    // If solution is found,
                    // then return true
                    if (found)
                        return true;
                }

                // For all other values, assign
                // ans[i + val] to val if the
                // i + val < ans.length
                else if (i + val < ans.length
                         && ans[i + val] == 0) {
                    ans[val + i] = val;

                    // Recursively call for
                    // next index to check if
                    // solution can be found
                    boolean found
                        = constructArray(i + 1, N);

                    // If solution is found then
                    // return true
                    if (found)
                        return true;

                    // BackTracking step
                    ans[i + val] = 0;
                }

                // BackTracking step
                ans[i] = 0;
                visited.remove(val);
            }
        }

        // In all other cases, return false
        return false;
    }

    // Driver Code
    public static void main(String[] args)
    {
        int N = 4;

        ans = new int[2 * N - 1];
        visited = new HashSet<>();

        // Function Call
        constructArray(0, N);

        // Print the resultant array
        for (int X : ans)
            System.out.print(X + " ");
    }
}
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to construct the array
# according to the given conditions
def constructArray(i, N):
    global ans, visited

    # Base Case
    if (i == len(ans)):
        return True

    # If a value is already assigned
    # at current index, then recursively
    # call for the next index
    if (ans[i] != 0):
        return constructArray(i + 1, N)
    else:

        # Iterate over the range[N, 1]
        for val in range(N, 0, -1):

            # If the current value is
            # already visited, continue
            if (val in visited):
                continue

            # Otherwise, mark this value as
            # visited and set ans[i] = val
            visited[val] = 1
            ans[i] = val

            # If val is equal to 1, then
            # recursively call for the
            # next index
            if (val == 1):
                found = constructArray(i + 1, N)

                # If solution is found,
                # then return true
                if (found):
                    return True

            # For all other values, assign
            # ans[i + val] to val if the
            # i + val < ans.length
            elif (i + val < len(ans) and ans[i + val] == 0):
                ans[val + i] = val

                # Recursively call for
                # next index to check if
                # solution can be found
                found = constructArray(i + 1, N)

                # If solution is found then
                # return true
                if (found):
                    return True

                # BackTracking step
                ans[i + val] = 0

            # BackTracking step
            ans[i] = 0
            del visited[val]

    # In all other cases, return false
    return False

# Driver Code
if __name__ == '__main__':
    N = 4
    ans = [0]*(2 * N - 1)
    visited = {}

    # Function Call
    constructArray(0, N)

    # Print the resultant array
    for x in ans:
        print(x,end=" ")

        # this code is contributed by mohit kumar 29.
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;
using System.Linq;

class GFG{

  // Stores the required sequence
  static int[] ans;

  // Stores the visited and unvisited values
  static HashSet<int> visited;

  // Function to construct the array
  // according to the given conditions
  public static bool
    constructArray(int i, int N)
  {

    // Base Case
    if (i == ans.Length) {
      return true;
    }

    // If a value is already assigned
    // at current index, then recursively
    // call for the next index
    if (ans[i] != 0)
      return constructArray(i + 1, N);

    else {

      // Iterate over the range[N, 1]
      for (int val = N; val >= 1; val--) {

        // If the current value is
        // already visited, continue
        if (visited.Contains(val))
          continue;

        // Otherwise, mark this value as
        // visited and set ans[i] = val
        visited.Add(val);
        ans[i] = val;

        // If val is equal to 1, then
        // recursively call for the
        // next index
        if (val == 1) {
          bool found
            = constructArray(i + 1, N);

          // If solution is found,
          // then return true
          if (found)
            return true;
        }

        // For all other values, assign
        // ans[i + val] to val if the
        // i + val < ans.length
        else if (i + val < ans.Length
                 && ans[i + val] == 0) {
          ans[val + i] = val;

          // Recursively call for
          // next index to check if
          // solution can be found
          bool found
            = constructArray(i + 1, N);

          // If solution is found then
          // return true
          if (found)
            return true;

          // BackTracking step
          ans[i + val] = 0;
        }

        // BackTracking step
        ans[i] = 0;
        visited.Remove(val);
      }
    }

    // In all other cases, return false
    return false;
  }

  // Driver Code
  static public void Main()
  {
    int N = 4;

    ans = new int[2 * N - 1];
    visited = new HashSet<int>();

    // Function Call
    constructArray(0, N);

    // Print the resultant array
    foreach (int X in ans)
      Console.Write(X + " ");
  }
}

// This code is contributed by code_hunt.
```

## java 描述语言

```
<script>
      // JavaScript program for the above approach
      // Stores the required sequence
      var ans = [];

      // Stores the visited and unvisited values
      var visited = [];

      // Function to construct the array
      // according to the given conditions
      function constructArray(i, N) {
        // Base Case
        if (i === ans.length) {
          return true;
        }

        // If a value is already assigned
        // at current index, then recursively
        // call for the next index
        if (ans[i] !== 0) return constructArray(i + 1, N);
        else {
          // Iterate over the range[N, 1]
          for (var val = N; val >= 1; val--) {
            // If the current value is
            // already visited, continue
            if (visited.includes(val)) continue;

            // Otherwise, mark this value as
            // visited and set ans[i] = val
            visited.push(val);
            ans[i] = val;

            // If val is equal to 1, then
            // recursively call for the
            // next index
            if (val === 1) {
              var found = constructArray(i + 1, N);

              // If solution is found,
              // then return true
              if (found) return true;
            }

            // For all other values, assign
            // ans[i + val] to val if the
            // i + val < ans.length
            else if (i + val < ans.length && ans[i + val] === 0) {
              ans[val + i] = val;

              // Recursively call for
              // next index to check if
              // solution can be found
              var found = constructArray(i + 1, N);

              // If solution is found then
              // return true
              if (found) return true;

              // BackTracking step
              ans[i + val] = 0;
            }

            // BackTracking step
            ans[i] = 0;
            var index = visited.indexOf(val);
            if (index !== -1) {
              visited.splice(index, 1);
            }
          }
        }

        // In all other cases, return false
        return false;
      }

      // Driver Code
      var N = 4;

      ans = new Array(2 * N - 1).fill(0);
      visited = [];

      // Function Call
      constructArray(0, N);

      // Print the resultant array
      for (const X of ans) {
        document.write(X + " ");
      }
    </script>
```

**Output:** 

```
4 2 3 2 4 3 1
```

**时间复杂度:** O(N！)
**辅助空间:** O(N)
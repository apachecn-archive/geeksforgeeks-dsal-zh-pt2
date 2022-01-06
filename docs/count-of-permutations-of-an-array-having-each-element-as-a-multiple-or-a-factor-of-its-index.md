# 将每个元素作为其索引的倍数或因子的数组的排列计数

> 原文:[https://www . geeksforgeeks . org/数组排列计数将每个元素作为其索引的倍数或因子/](https://www.geeksforgeeks.org/count-of-permutations-of-an-array-having-each-element-as-a-multiple-or-a-factor-of-its-index/)

给定一个整数 **N** ，任务是计算生成数组的方式数， **arr[]** 由 **N** 个整数组成，使得对于每个索引 **i** (基于 1 的索引) **arr[i]** 要么是 **i** 的因子或倍数，要么是两者。 **arr[]** 必须是**【1，N】**范围内所有数字的排列。

**示例:**

> **输入:** N=2
> **输出:** 2
> **解释:**
> 两种可能的排列是{1，2}和{2，1}
> 
> **输入:** N=3
> **输出:** 3
> **解释:**
> 6 种可能的排列是{1，2，3}、{2，1，3}、{3，2，1}、{3，1，2}、{2，3，1}和{1，3，2}。
> 其中，有效排列为{1，2，3}、{2，1，3}和{3，2，1}。

**逼近**:使用[回溯技术](https://www.geeksforgeeks.org/backtracking-algorithms/)和[的概念使用递归打印所有排列可以解决问题。](https://www.geeksforgeeks.org/write-a-c-program-to-print-all-permutations-of-a-given-string/)按照以下步骤查找递归关系:

1.  遍历**【1，N】**范围。
2.  对于当前索引 **pos** ，如果 **i % pos == 0** 和 **i % pos == 0** ，则在排列中插入 I，并使用回溯的概念来寻找有效的排列。
3.  拆下 **i** 。
4.  对**【1，N】**范围内的所有值重复上述步骤，最后打印有效排列数。

下面是上述方法的实现:

## C++

```
// C++ Program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the count of
// desired permutations
int findPermutation(unordered_set<int>& arr,
                    int N)
{
    int pos = arr.size() + 1;

    // Base case
    if (pos > N)
        return 1;

    int res = 0;

    for (int i = 1; i <= N; i++) {

        // If i has not been inserted
        if (arr.find(i) == arr.end()) {

            // Backtrack
            if (i % pos == 0 or pos % i == 0) {

                // Insert i
                arr.insert(i);

                // Recur to find valid permutations
                res += findPermutation(arr, N);

                // Remove i
                arr.erase(arr.find(i));
            }
        }
    }

    // Return the final count
    return res;
}

// Driver Code
int main()
{
    int N = 5;
    unordered_set<int> arr;
    cout << findPermutation(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;

class GFG{

// Function to find the count of
// desired permutations
static int findPermutation(Set<Integer>arr,
                           int N)
{
    int pos = arr.size() + 1;

    // Base case
    if (pos > N)
        return 1;

    int res = 0;

    for(int i = 1; i <= N; i++)
    {

        // If i has not been inserted
        if (! arr.contains(i))
        {

            // Backtrack
            if (i % pos == 0 || pos % i == 0)
            {

                // Insert i
                arr.add(i);

                // Recur to find valid permutations
                res += findPermutation(arr, N);

                // Remove i
                arr.remove(i);
            }
        }
    }

    // Return the final count
    return res;
}

// Driver Code
public static void main(String []args)
{
    int N = 5;
    Set<Integer> arr = new HashSet<Integer>();

    System.out.print(findPermutation(arr, N));
}
}

// This code is contributed by chitranayal
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to find the count of
# desired permutations
def findPermutation(arr, N):

    pos = len(arr) + 1

    # Base case
    if(pos > N):
        return 1

    res = 0

    for i in range(1, N + 1):

        # If i has not been inserted
        if(i not in arr):

            # Backtrack
            if(i % pos == 0 or pos % i == 0):

                # Insert i
                arr.add(i)

                # Recur to find valid permutations
                res += findPermutation(arr, N)

                # Remove i
                arr.remove(i)

    # Return the final count
    return res

# Driver Code
N = 5
arr = set()

# Function call
print(findPermutation(arr, N))

# This code is contributed by Shivam Singh
```

## C#

```
// C# program to implement
// the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to find the count of
// desired permutations
static int findPermutation(HashSet<int>arr,
                           int N)
{
    int pos = arr.Count + 1;

    // Base case
    if (pos > N)
        return 1;

    int res = 0;

    for(int i = 1; i <= N; i++)
    {

        // If i has not been inserted
        if (! arr.Contains(i))
        {

            // Backtrack
            if (i % pos == 0 || pos % i == 0)
            {

                // Insert i
                arr.Add(i);

                // Recur to find valid permutations
                res += findPermutation(arr, N);

                // Remove i
                arr.Remove(i);
            }
        }
    }

    // Return the readonly count
    return res;
}

// Driver Code
public static void Main(String []args)
{
    int N = 5;
    HashSet<int> arr = new HashSet<int>();

    Console.Write(findPermutation(arr, N));
}
}

// This code is contributed by gauravrajput1
```

## java 描述语言

```
<script>

// Javascript program to implement
// the above approach

// Function to find the count of
// desired permutations
function findPermutation(arr, N)
{
    var pos = arr.size + 1;

    // Base case
    if (pos > N)
        return 1;

    var res = 0;

    for(var i = 1; i <= N; i++)
    {

        // If i has not been inserted
        if (!arr.has(i))
        {

            // Backtrack
            if (i % pos == 0 || pos % i == 0)
            {

                // Insert i
                arr.add(i);

                // Recur to find valid permutations
                res += findPermutation(arr, N);

                // Remove i
                arr.delete(i);
            }
        }
    }

    // Return the final count
    return res;
}

// Driver Code
var N = 5;
var arr = new Set();

document.write(findPermutation(arr, N));

// This code is contributed by importantly

</script>
```

**Output:** 

```
10
```

***时间复杂度:** O(N×N！)*
***辅助空间:** O(N)*
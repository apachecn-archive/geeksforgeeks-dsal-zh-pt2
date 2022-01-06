# 找到所有的完美正方形组合，这些组合加起来有 N 个副本

> 原文:[https://www . geeksforgeeks . org/find-all-组合-完美平方-求和-n-与-重复/](https://www.geeksforgeeks.org/find-all-combinations-of-perfect-squares-that-sum-up-to-n-with-duplicates/)

给定一个正整数 **N** ，任务是打印所有可能的完美正方形的和，使得所有完美正方形的总[和](https://www.geeksforgeeks.org/sum-of-all-perfect-squares-lying-in-the-range-l-r-for-q-queries/)等于**N**

**示例:**

> **输入:** N=8
> **输出:**4 4
> 1 1 1 1 4
> 1 1 1 1 1 1
> T8】解释:有三种可能的方法可以使和等于 N
> 
> **输入:**N = 3
> T3】输出: 1 1 1

**方法:**给定的问题可以使用[递归](http://www.geeksforgeeks.org/recursion/)和[回溯](http://www.geeksforgeeks.org/backtracking-algorithms/)来解决。其思想是生成一个小于 **N** 的[完美平方](https://www.geeksforgeeks.org/count-ways-to-represent-a-number-as-sum-of-perfect-squares/)的列表，然后计算完美平方和的可能[组合](https://www.geeksforgeeks.org/permutation-and-combination-gq/)，它们等于**N。**在递归函数中，在每个索引处，元素可以被选择用于列表，也可以不被选择。按照以下步骤解决问题:

*   初始化一个数组列表来存储所有小于 **N** 的完美正方形
*   使用变量 **i** 将整数 **N** 从 1 迭代到**N**T5**T7】的平方根**
    *   如果 **i** 的平方小于或等于 **N，**则在列表中添加 **i * i**
*   使用[递归](http://www.geeksforgeeks.org/recursion/)和[回溯](http://www.geeksforgeeks.org/backtracking-algorithms/)计算等于 **N** 的完美平方和
*   在每一个指数**处，找到**做以下事情:
    *   不要在当前索引中包含元素，并对下一个索引进行递归调用
    *   在当前索引中包含元素，并对同一索引进行递归调用
*   递归函数需要以下两种基本情况:
    *   如果 **N** 变得小于零，或者如果 **ind** 到达列表末尾，则返回
    *   如果 **N** 变为零，则打印列表

以下是上述方法的实现:

## C++

```
// C++ code for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to print all combinations of
// sum of perfect squares equal to N
void combinationSum(
    vector<int> list, int N,
    int ind, vector<int> perfSquares)
{

    // Sum of perfect squares exceeded N
    if (N < 0 || ind == list.size())
        return;

    // Sum of perfect squares is equal to N
    // therefore a combination is found
    if (N == 0)
    {

        for (int i : perfSquares)
        {
            cout << i << " ";
        }
        cout << endl;
        return;
    }

    // Do not include the current element
    combinationSum(list, N,
                   ind + 1, perfSquares);

    // Include the element at current index
    perfSquares.push_back(list[ind]);

    combinationSum(list, N - list[ind],
                   ind, perfSquares);

    // Remove the current element
    perfSquares.pop_back();
}

// Funcition to check whether the
// number is a perfect square or not
void sumOfPerfectSquares(int N)
{

    // Initialize an arraylist to store
    // all perfect squares less than N
    vector<int> list;
    int sqrtN = (int)(sqrt(N));

    // Iterate till square root of N
    for (int i = 1; i <= sqrtN; i++)
    {

        // Add all perfect squares
        // to the list
        list.push_back(i * i);
    }
    vector<int> perfSquares;
    combinationSum(list, N, 0,
                   perfSquares);
}

// Driver code
int main()
{
    int N = 8;

    // Call the function
    sumOfPerfectSquares(N);
    return 0;
}

// This code is contributed by Potta Lokesh
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation for the above approach

import java.io.*;
import java.util.*;
import java.lang.Math;

class GFG {

    // Funcition to check whether the
    // number is a perfect square or not
    public static void
    sumOfPerfectSquares(int N)
    {

        // Initialize an arraylist to store
        // all perfect squares less than N
        ArrayList<Integer> list = new ArrayList<>();
        int sqrtN = (int)(Math.sqrt(N));

        // Iterate till square root of N
        for (int i = 1; i <= sqrtN; i++) {

            // Add all perfect squares
            // to the list
            list.add(i * i);
        }

        combinationSum(list, N, 0,
                       new ArrayList<>());
    }

    // Function to print all combinations of
    // sum of perfect squares equal to N
    static void combinationSum(
        List<Integer> list, int N,
        int ind, List<Integer> perfSquares)
    {

        // Sum of perfect squares exceeded N
        if (N < 0 || ind == list.size())
            return;

        // Sum of perfect squares is equal to N
        // therefore a combination is found
        if (N == 0) {

            for (int i : perfSquares) {
                System.out.print(i + " ");
            }
            System.out.println();
            return;
        }

        // Do not include the current element
        combinationSum(list, N,
                       ind + 1, perfSquares);

        // Include the element at current index
        perfSquares.add(list.get(ind));

        combinationSum(list, N - list.get(ind),
                       ind, perfSquares);

        // Remove the current element
        perfSquares.remove(perfSquares.size() - 1);
    }

    // Driver code
    public static void main(String[] args)
    {
        int N = 8;

        // Call the function
        sumOfPerfectSquares(N);
    }
}
```

## 蟒蛇 3

```
# Python code for the above approach

# Function to print all combinations of
# sum of perfect squares equal to N
import math

def combinationSum(lst, N, ind, perfSquares):

    # Sum of perfect squares exceeded N
    if N < 0 or ind == len(lst):
        return

    # Sum of perfect squares is equal to N
    # therefore a combination is found
    if N == 0:
        for i in perfSquares:
            print(i, end = ' ')
        print('')
        return;

    # Do not include the current element
    combinationSum(lst,N,ind+1,perfSquares)

    # Include the element at current index
    perfSquares.append(lst[ind])

    combinationSum(lst, N  - lst[ind], ind, perfSquares)

    # Remove the current element
    perfSquares.pop()

# Funcition to check whether the
# number is a perfect square or not   
def sumOfPerfectSquares(N):

    # Initialize an arraylist to store
    # all perfect squares less than N
    lst = []
    sqrtN = int(math.sqrt(N))

    # Iterate till square root of N
    for i in range(1, sqrtN + 1):

        # Add all perfect squares
        # to the list
        lst.append(i*i)

    perfSquares = []
    combinationSum(lst, N, 0, perfSquares)

# Driver code   
N = 8

# Call the function
sumOfPerfectSquares(N)

# This code is contributed by rdtank.
```

## C#

```
// C# implementation for the above approach
using System;
using System.Collections.Generic;

class GFG {

    // Funcition to check whether the
    // number is a perfect square or not
    public static void sumOfPerfectSquares(int N)
    {

        // Initialize an arraylist to store
        // all perfect squares less than N
        List<int> list = new List<int>();
        int sqrtN = (int)(Math.Sqrt(N));

        // Iterate till square root of N
        for (int i = 1; i <= sqrtN; i++) {

            // Add all perfect squares
            // to the list
            list.Add(i * i);
        }

        combinationSum(list, N, 0, new List<int>());
    }

    // Function to print all combinations of
    // sum of perfect squares equal to N
    static void combinationSum(List<int> list, int N,
                               int ind,
                               List<int> perfSquares)
    {

        // Sum of perfect squares exceeded N
        if (N < 0 || ind == list.Count)
            return;

        // Sum of perfect squares is equal to N
        // therefore a combination is found
        if (N == 0) {

            foreach(int i in perfSquares)
            {
                Console.Write(i + " ");
            }
            Console.WriteLine();
            return;
        }

        // Do not include the current element
        combinationSum(list, N, ind + 1, perfSquares);

        // Include the element at current index
        perfSquares.Add(list[ind]);

        combinationSum(list, N - list[ind], ind,
                       perfSquares);

        // Remove the current element
        perfSquares.RemoveAt(perfSquares.Count - 1);
    }

    // Driver code
    public static void Main(string[] args)
    {
        int N = 8;

        // Call the function
        sumOfPerfectSquares(N);
    }
}

// This code is contributed by ukasp.
```

## java 描述语言

```
<script>
// Javascript code for the above approach

// Function to print all combinations of
// sum of perfect squares equal to N
function combinationSum(list, N, ind, perfSquares)
{

    // Sum of perfect squares exceeded N
    if (N < 0 || ind == list.length)
        return;

    // Sum of perfect squares is equal to N
    // therefore a combination is found
    if (N == 0)
    {

        for (let i = 0; i < perfSquares.length; i++)
        {
            document.write(perfSquares[i] + " ");
        }
        document.write("\n");
        return;
    }

    // Do not include the current element
    combinationSum(list, N,
                   ind + 1, perfSquares);

    // Include the element at current index
    perfSquares.push(list[ind]);

    combinationSum(list, N - list[ind],
                   ind, perfSquares);

    // Remove the current element
    perfSquares.pop();
}

// Funcition to check whether the
// number is a perfect square or not
function sumOfPerfectSquares(N)
{

    // Initialize an arraylist to store
    // all perfect squares less than N
    let list = [];
    let sqrtN = Math.sqrt(N);

    // Iterate till square root of N
    for (let i = 1; i <= sqrtN; i++)
    {

        // Add all perfect squares
        // to the list
        list.push(i * i);
    }
    let perfSquares = [];
    combinationSum(list, N, 0,
                   perfSquares);
}

// Driver code
  let N = 8;

    // Call the function
    sumOfPerfectSquares(N);

// This code is contributed by Samim Hossain Mondal.
</script>
```

**Output**

```
4 4 
1 1 1 1 4 
1 1 1 1 1 1 1 1 
```

**时间复杂度:** O(N * 2^N)，其中 n 是给定的数字
**辅助空间:** O(N)
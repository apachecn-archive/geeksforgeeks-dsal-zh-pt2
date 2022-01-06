# 计数为 1 的最大子矩阵面积比计数为 0 的多一个

> 原文:[https://www . geesforgeks . org/maximum-sub-matrix-area-具有 1 的计数比 0 的计数多 1/](https://www.geeksforgeeks.org/maximum-sub-matrix-area-having-count-of-1s-one-more-than-count-of-0s/)

给定一个**N×N**二进制矩阵。问题是找到计数为 1 的最大面积子矩阵比计数为 0 的子矩阵多一个。
**示例:**

```
Input : mat[][] = { {1, 0, 0, 1},
                    {0, 1, 1, 1},
                    {1, 0, 0, 0},
                    {0, 1, 0, 1} }
Output : 9
The sub-matrix defined by the boundary values (1, 1) and (3, 3).
{ {1, 0, 0, 1},
  {0, 1, 1, 1},
  {1, 0, 0, 0},
  {0, 1, 0, 1} }
```

**天真方法:**检查给定 2D 矩阵中的每个可能的矩形。该解决方案需要 4 个嵌套循环，并且该解决方案的时间复杂度是 O(n^4).

**有效的方法:**有效的方法是使用[最长的子阵列，其 1 的计数比 0 的计数多一个](https://www.geeksforgeeks.org/longest-subarray-count-1s-one-count-0s/),这降低了 O(n^3).的时间复杂度其思想是逐个固定左列和右列，并为每个左列和右列对找到最大长度的连续行，这些行的 1 的计数比 0 的计数多 1。为每个固定的左右列对查找顶部和底部行号(具有最大长度)。要查找上下行号，请从左到右计算每一行中元素的总和，并将这些总和存储在一个数组中，比如 temp[](添加时将 0 视为-1)。所以 temp[i]表示第 I 行从左到右的元素之和，使用[中计数为 1 的最长子阵列比计数为 0 的最长子阵列](https://www.geeksforgeeks.org/longest-subarray-count-1s-one-count-0s/)中的方法，temp[]数组被用来通过获得起始和结束行号来获得计数为 1 的最大长度子阵列，然后这些值可以用来寻找以左和右为边界列的最大可能区域。要获得总的最大面积，请将该面积与迄今为止的最大面积进行比较。

下面是上述方法的实现:

## C++

```
// C++ implementation to find
// the maximum area sub-matrix
// having count of 1's
// one more than count of 0's
#include <bits/stdc++.h>

using namespace std;

#define SIZE 10

// function to find the length of longest
// subarray having count of 1's one more
// than count of 0's
int lenOfLongSubarr(int arr[], int n,
                    int& start, int& finish)
{
    // unordered_map 'um' implemented as
    // hash table
    unordered_map<int, int> um;
    int sum = 0, maxLen = 0;

    // traverse the given array
    for (int i = 0; i < n; i++) {

        // accumulating sum
        sum += arr[i];

        // when subarray starts form index '0'
        if (sum == 1) {
            start = 0;
            finish = i;
            maxLen = i + 1;
        }

        // make an entry for 'sum' if it is
        // not present in 'um'
        else if (um.find(sum) == um.end())
            um[sum] = i;

        // check if 'sum-1' is present in 'um'
        // or not
        if (um.find(sum - 1) != um.end()) {

            // update 'start', 'finish'
            // and maxLength
            if (maxLen < (i - um[sum - 1]))
                start = um[sum - 1] + 1;
            finish = i;
            maxLen = i - um[sum - 1];
        }
    }

    // required maximum length
    return maxLen;
}

// function to find the maximum
// area sub-matrix having
// count of 1's one more than count of 0's
void largestSubmatrix(int mat[SIZE][SIZE], int n)
{
    // variables to store final
    // and intermediate results
    int finalLeft, finalRight, finalTop, finalBottom;
    int temp[n], maxArea = 0, len, start, finish;

    // set the left column
    for (int left = 0; left < n; left++) {

        // Initialize all elements of temp as 0
        memset(temp, 0, sizeof(temp));

        // Set the right column for the
        // left column set by outer loop
        for (int right = left; right < n; right++) {

            // Calculate sum between current left and right
            // for every row 'i', consider '0' as '-1'
            for (int i = 0; i < n; ++i)
                temp[i] += mat[i][right] == 0 ? -1 : 1;

            // function to set the 'start' and 'finish'
            // variables having index values of
            // temp[] which contains the longest
            // subarray of temp[] having count of 1's
            // one more than count of 0's
            len = lenOfLongSubarr(temp, n, start, finish);

            // Compare with maximum area
            // so far and accordingly update the
            // final variables
            if ((len != 0) && (maxArea < (finish - start + 1)
                                             * (right - left + 1))) {
                finalLeft = left;
                finalRight = right;
                finalTop = start;
                finalBottom = finish;
                maxArea = (finish - start + 1) * (right - left + 1);
            }
        }
    }

    // Print final values
    cout << "(Top, Left): (" << finalTop << ", "
         << finalLeft << ")\n";

    cout << "(Bottom, Right): (" << finalBottom << ", "
         << finalRight << ")\n";

    cout << "Maximum area: " << maxArea;
}

// Driver Code
int main()
{
    int mat[SIZE][SIZE] = { { 1, 0, 0, 1 },
                            { 0, 1, 1, 1 },
                            { 1, 0, 0, 0 },
                            { 0, 1, 0, 1 } };
    int n = 4;
    largestSubmatrix(mat, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find
// the maximum area sub-matrix
// having count of 1's
// one more than count of 0's
import java.util.*;

class GFG
{

static int start, finish;

// Function to find the length of longest
// subarray having count of 1's one more
// than count of 0's
static int lenOfLongSubarr(int []arr, int n)
{

    // unordered_map 'um' implemented as
    // hash table
    HashMap<Integer,Integer> um = new HashMap<Integer, Integer>();

    int sum = 0, maxLen = 0;

    // Traverse the given array
    for(int i = 0; i < n; i++)
    {

        // Accumulating sum
        sum += arr[i];

        // When subarray starts form index '0'
        if (sum == 1)
        {
            start = 0;
            finish = i;
            maxLen = i + 1;
        }

        // Make an entry for 'sum' if it is
        // not present in 'um'
        else if (!um.containsKey(sum))
            um.put(sum,i);

        // Check if 'sum-1' is present in 'um'
        // or not
        if (um.containsKey(sum - 1))
        {

            // Update 'start', 'finish'
            // and maxLength
            if (maxLen < (i - um.get(sum - 1)))
                start = um.get(sum - 1) + 1;

            finish = i;
            maxLen = i - um.get(sum - 1);
        }
    }

    // Required maximum length
    return maxLen;
}

// Function to find the maximum
// area sub-matrix having
// count of 1's one more than count of 0's
static void largestSubmatrix(int [][]mat, int n)
{

    // Variables to store final
    // and intermediate results
    int finalLeft = 0, finalRight = 0,
        finalTop = 0, finalBottom = 0;
    int maxArea = 0, len;
    finish = 0;
    start=0;

    int []temp = new int[n];

    // Set the left column
    for(int left = 0; left < n; left++)
    {

        // Initialize all elements of temp as 0
        Arrays.fill(temp, 0);

        // Set the right column for the
        // left column set by outer loop
        for(int right = left; right < n; right++)
        {

            // Calculate sum between current left
            // and right for every row 'i',
            // consider '0' as '-1'
            for(int i = 0; i < n; ++i)
                temp[i] += mat[i][right] == 0 ? -1 : 1;

            // Function to set the 'start' and 'finish'
            // variables having index values of
            // temp[] which contains the longest
            // subarray of temp[] having count of 1's
            // one more than count of 0's
            len = lenOfLongSubarr(temp, n);

            // Compare with maximum area
            // so far and accordingly update the
            // final variables
            if ((len != 0) &&
                (maxArea < (finish - start + 1) *
                            (right - left + 1)))
            {
                finalLeft = left;
                finalRight = right;
                finalTop = start;
                finalBottom = finish;
                maxArea = (finish - start + 1) *
                            (right - left + 1);
            }
        }
    }

    // Print final values
    System.out.print("(Top, Left): (" + finalTop +
                ", " + finalLeft + ")\n");

    System.out.print("(Bottom, Right): (" + finalBottom +
                    ", " + finalRight + ")\n");

    System.out.print("Maximum area: " + maxArea);

}

// Driver code
public static void main(String[] args)
{
    int [][]mat = new int[][]{ { 1, 0, 0, 1 },
                            { 0, 1, 1, 1 },
                            { 1, 0, 0, 0 },
                            { 0, 1, 0, 1 } };
    int n = 4;

    largestSubmatrix(mat, n);
}
}

// This code is contributed by pratham76
```

## 蟒蛇 3

```
# Python implementation to find
# the maximum area sub-matrix
# having count of 1's
# one more than count of 0's

# function to find the length of longest
# subarray having count of 1's one more
# than count of 0's
def lenOfLongSubarr(arr, n, start, finish):

  # unordered_map 'um' implemented as
  # hash table
  um = {}
  sum = 0
  maxLen = 0

  # traverse the given array
  for i in range(n):

    # accumulating sum
    sum += arr[i]

    # when subarray starts form index '0'
    if (sum == 1):
      start = 0
      finish = i
      maxLen = i + 1

    # make an entry for 'sum' if it is
    # not present in 'um'
    elif (sum not in um):
      um[sum] = i

    # check if 'sum-1' is present in 'um'
    # or not
    if (sum - 1 in um):

      # update 'start', 'finish'
      # and maxLength
      if (maxLen < (i - um[sum - 1])):
        start = um[sum - 1] + 1
        finish = i
        maxLen = i - um[sum - 1]

  # required maximum length
  return [maxLen,start,finish]

# function to find the maximum
# area sub-matrix having
# count of 1's one more than count of 0's
def largestSubmatrix(mat, n):

  # variables to store final
  # and intermediate results
  temp = []
  maxArea = 0

  # set the left column
  for left in range(n):

    # Initialize all elements of temp as 0
    temp = [0 for i in range(n)]

    # Set the right column for the
    # left column set by outer loop
    for right in range(left, n):

      # Calculate sum between current left and right
      # for every row 'i', consider '0' as '-1'
      for i in range(n):
        if mat[i][right] == 0:
          temp[i] -= 1
        else:
          temp[i] += 1

      # function to set the 'start' and 'finish'
      # variables having index values of
      # temp[] which contains the longest
      # subarray of temp[] having count of 1's
      # one more than count of 0's
      start = 0
      finish = 0
      fc = lenOfLongSubarr(temp, n, start, finish)
      len = fc[0]
      start = fc[1]
      finish = fc[2]

      # Compare with maximum area
      # so far and accordingly update the
      # final variables
      if ((len != 0) and (maxArea < (finish - start + 1) * (right - left + 1))):
        finalLeft = left
        finalRight = right
        finalTop = start
        finalBottom = finish
        maxArea = (finish - start + 1) * (right - left + 1)

  # Print final values
  print("(Top, Left): (",finalTop,", ",finalLeft,")")
  print("(Bottom, Right): (",finalBottom, ", ",finalRight,")")
  print("Maximum area: ", maxArea)

# Driver Code
mat = [[1, 0, 0, 1 ], [ 0, 1, 1, 1 ], [ 1, 0, 0, 0 ], [ 0, 1, 0, 1 ]]
n = 4
largestSubmatrix(mat, n)

# This code is contributed by rohitsingh07052
```

## C#

```
// C# implementation to find
// the maximum area sub-matrix
// having count of 1's
// one more than count of 0's
using System;
using System.Collections.Generic;
using System.Collections;

class GFG{

// Function to find the length of longest
// subarray having count of 1's one more
// than count of 0's
static int lenOfLongSubarr(int []arr, int n,
                       ref int start, ref int finish)
{

    // unordered_map 'um' implemented as
    // hash table
    Dictionary<int,
               int> um = new Dictionary<int,
                                        int>();

    int sum = 0, maxLen = 0;

    // Traverse the given array
    for(int i = 0; i < n; i++)
    {

        // Accumulating sum
        sum += arr[i];

        // When subarray starts form index '0'
        if (sum == 1)
        {
            start = 0;
            finish = i;
            maxLen = i + 1;
        }

        // Make an entry for 'sum' if it is
        // not present in 'um'
        else if (!um.ContainsKey(sum))
            um[sum] = i;

        // Check if 'sum-1' is present in 'um'
        // or not
        if (um.ContainsKey(sum - 1))
        {

            // Update 'start', 'finish'
            // and maxLength
            if (maxLen < (i - um[sum - 1]))
                start = um[sum - 1] + 1;

            finish = i;
            maxLen = i - um[sum - 1];
        }
    }

    // Required maximum length
    return maxLen;
}

// Function to find the maximum
// area sub-matrix having
// count of 1's one more than count of 0's
static void largestSubmatrix(int [,]mat, int n)
{

    // Variables to store final
    // and intermediate results
    int finalLeft = 0, finalRight = 0,
         finalTop = 0, finalBottom = 0;
    int maxArea = 0, len, start = 0, finish = 0;

    int []temp = new int[n];

    // Set the left column
    for(int left = 0; left < n; left++)
    {

        // Initialize all elements of temp as 0
        Array.Fill(temp, 0);

        // Set the right column for the
        // left column set by outer loop
        for(int right = left; right < n; right++)
        {

            // Calculate sum between current left
            // and right for every row 'i',
            // consider '0' as '-1'
            for(int i = 0; i < n; ++i)
                temp[i] += mat[i, right] == 0 ? -1 : 1;

            // Function to set the 'start' and 'finish'
            // variables having index values of
            // temp[] which contains the longest
            // subarray of temp[] having count of 1's
            // one more than count of 0's
            len = lenOfLongSubarr(temp, n, ref start,
                                           ref finish);

            // Compare with maximum area
            // so far and accordingly update the
            // final variables
            if ((len != 0) &&
                (maxArea < (finish - start + 1) *
                             (right - left + 1)))
            {
                finalLeft = left;
                finalRight = right;
                finalTop = start;
                finalBottom = finish;
                maxArea = (finish - start + 1) *
                            (right - left + 1);
            }
        }
    }

    // Print final values
    Console.Write("(Top, Left): (" + finalTop +
                  ", " + finalLeft + ")\n");

    Console.Write("(Bottom, Right): (" + finalBottom +
                     ", " + finalRight + ")\n");

    Console.Write("Maximum area: " + maxArea);

}

// Driver code
public static void Main(string[] args)
{
    int [,]mat = new int[,]{ { 1, 0, 0, 1 },
                             { 0, 1, 1, 1 },
                             { 1, 0, 0, 0 },
                             { 0, 1, 0, 1 } };
    int n = 4;

    largestSubmatrix(mat, n);
}
}

// This code is contributed by rutvik_56
```

**Output:** 

```
(Top, Left): (1, 1)
(Bottom, Right): (3, 3)
Maximum area: 9
```

**时间复杂度:** O(N <sup>3</sup> )。
**辅助空间:** O(N)。
# 通过移位操作最大化奇数和偶数索引数组元素之间的差异

> 原文:[https://www . geeksforgeeks . org/通过移位操作最大化奇数和偶数索引数组元素之间的差异/](https://www.geeksforgeeks.org/maximize-difference-between-odd-and-even-indexed-array-elements-by-shift-operations/)

给定一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** ，任务是通过任意次数的数组元素的[左移或右移](https://www.geeksforgeeks.org/left-shift-right-shift-operators-c-cpp/)来最大化偶数索引元素的和与奇数索引元素的和之间的绝对差。

**示例:**

> **输入:** arr[] = {332，421，215，584，232}
> **输出:** 658
> **解释:**
> 将数组转换为{233，421，152，845，223}，
> 奇数索引元素之和= 608。
> 偶数索引元素之和= 1266。
> 所以差等于 658。
> 
> **输入:** arr[] = {11，22，33，44，55 }
> T3】输出: 33

**方法:**想法是最小化偶数或奇数索引数组元素中任何一个的值，最大化另一个的值，以便最大化它们的绝对差。按照以下步骤解决问题:

*   存在两种可能的情况。要么最小化偶数索引数组元素并最大化奇数索引数组元素，要么最小化奇数索引数组元素并最大化偶数索引数组元素。
*   为了最小化一个元素，应用所有的移位操作并取最小可能值。类似地，要最大化一个元素，应用所有的移位操作并取最大可能值。
*   取两种情况的最大差值。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to minimize array
// elements by shift operations
int minimize(int n)
{
  int optEle = n;
  string strEle = to_string(n);

  // For checking all the
  // left shift operations
  for (int idx = 0; idx < strEle.length();idx++)
  {

    // Left shift
    int temp = stoi(strEle.substr(idx) +
                    strEle.substr(0, idx));

    // Consider the minimum possible value
    optEle = min(optEle, temp);
  }

  return optEle;
}

// Function to maximize array
// elements by shift operations
int maximize(int n)
{
  int optEle = n;
  string strEle = to_string(n);

  // For checking all the
  // left shift operations
  for (int idx = 0; idx < strEle.length();idx++)
  {

    // Left shift
    int temp = stoi(strEle.substr(idx) +
                    strEle.substr(0, idx));

    // Consider the maximum possible value
    optEle = max(optEle, temp);
  }

  return optEle;
}

// Function to maximize the absolute
// difference between even and odd
// indexed array elements
void minimumDifference(int arr[], int N)
{

  int caseOne = 0;
  int minVal = 0;
  int maxVal = 0;

  // To calculate the difference of
  // odd indexed elements
  // and even indexed elements
  for (int i = 0; i < N; i++)
  {
    if (i % 2 == 0)
      minVal += minimize(arr[i]);
    else
      maxVal += maximize(arr[i]);
  }
  caseOne = abs(maxVal - minVal);
  int caseTwo = 0;
  minVal = 0;
  maxVal = 0;

  // To calculate the difference
  // between odd and even indexed
  // array elements
  for (int i = 0; i < N; i++)
  {

    if (i % 2 == 0)
      maxVal += maximize(arr[i]);
    else
      minVal += minimize(arr[i]);
    caseTwo = abs(maxVal - minVal);
  }

  // Print the maximum value
  cout << max(caseOne, caseTwo) << endl;
}

// Driver code
int main()
{
  int arr[] = { 332, 421, 215, 584, 232 };
  int N = sizeof(arr) / sizeof(arr[0]);
  minimumDifference(arr, N);

  return 0;
}

// This code is contributed by divyesh072019.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
class GFG
{

  // Function to minimize array
  // elements by shift operations
  static int minimize(int n)
  {
    int optEle = n;
    String strEle = Integer.toString(n);

    // For checking all the
    // left shift operations
    for (int idx = 0; idx < strEle.length(); idx++)
    {

      // Left shift
      int temp
        = Integer.parseInt(strEle.substring(idx)
                           + strEle.substring(0, idx));

      // Consider the minimum possible value
      optEle = Math.min(optEle, temp);
    }

    return optEle;
  }

  // Function to maximize array
  // elements by shift operations
  static int maximize(int n)
  {
    int optEle = n;
    String strEle = Integer.toString(n);

    // For checking all the
    // left shift operations
    for (int idx = 0; idx < strEle.length(); idx++)
    {

      // Left shift
      int temp
        = Integer.parseInt(strEle.substring(idx)
                           + strEle.substring(0, idx));

      // Consider the maximum possible value
      optEle = Math.max(optEle, temp);
    }
    return optEle;
  }

  // Function to maximize the absolute
  // difference between even and odd
  // indexed array elements
  static void minimumDifference(int[] arr)
  {

    int caseOne = 0;
    int minVal = 0;
    int maxVal = 0;

    // To calculate the difference of
    // odd indexed elements
    // and even indexed elements
    for (int i = 0; i < arr.length; i++)
    {
      if (i % 2 == 0)
        minVal += minimize(arr[i]);
      else
        maxVal += maximize(arr[i]);
    }
    caseOne = Math.abs(maxVal - minVal);
    int caseTwo = 0;
    minVal = 0;
    maxVal = 0;

    // To calculate the difference
    // between odd and even indexed
    // array elements
    for (int i = 0; i < arr.length; i++)
    {
      if (i % 2 == 0)
        maxVal += maximize(arr[i]);
      else
        minVal += minimize(arr[i]);
      caseTwo = Math.abs(maxVal - minVal);
    }

    // Print the maximum value
    System.out.println(Math.max(caseOne, caseTwo));
  }

  // Driver Code
  public static void main(String[] args)
  {

    // Given array
    int[] arr = { 332, 421, 215, 584, 232 };
    minimumDifference(arr);
  }
}

// This code is contributed by Dharanendra L V.
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to minimize array
# elements by shift operations
def minimize(n):
  optEle = n
  strEle = str(n)

  # For checking all the
  # left shift operations
  for idx in range(len(strEle)):

    # Left shift
    temp = int(strEle[idx:] + strEle[:idx])

    # Consider the minimum possible value
    optEle = min(optEle, temp)

  return optEle

# Function to maximize array
# elements by shift operations
def maximize(n):
  optEle = n
  strEle = str(n)

  # For checking all the
  # left shift operations
  for idx in range(len(strEle)):

    # Left shift
    temp = int(strEle[idx:] + strEle[:idx])

    # Consider the maximum possible value
    optEle = max(optEle, temp)

  return optEle

# Function to maximize the absolute
# difference between even and odd
# indexed array elements
def minimumDifference(arr):

  caseOne = 0
  minVal = 0
  maxVal = 0

  # To calculate the difference of
  # odd indexed elements
  # and even indexed elements
  for i in range(len(arr)):
    if i % 2:
      minVal += minimize(arr[i])
    else:
      maxVal += maximize(arr[i])
  caseOne = abs(maxVal - minVal)
  caseTwo = 0
  minVal = 0
  maxVal = 0

  # To calculate the difference
  # between odd and even indexed
  # array elements
  for i in range(len(arr)):

    if i % 2:
      maxVal += maximize(arr[i])
    else:
      minVal += minimize(arr[i])
  caseTwo = abs(maxVal - minVal)

  # Print the maximum value
  print (max(caseOne, caseTwo))

# Given array
arr = [ 332, 421, 215, 584, 232 ]
minimumDifference(arr)
```

## C#

```
// C# program for the above approach
using System;
class GFG
{

    // Function to minimize array
    // elements by shift operations
    static int minimize(int n)
    {
        int optEle = n;
        string strEle = n.ToString();

        // For checking all the
        // left shift operations
        for (int idx = 0; idx < strEle.Length;idx++)
        {

            // Left shift
            int temp = Int32.Parse(strEle.Substring(idx) +
                                   strEle.Substring(0, idx));

            // Consider the minimum possible value
            optEle = Math.Min(optEle, temp);
        }

        return optEle;
    }

    // Function to maximize array
    // elements by shift operations
    static int maximize(int n)
    {
        int optEle = n;
        string strEle = n.ToString();

        // For checking all the
        // left shift operations
        for (int idx = 0; idx < strEle.Length;idx++)
        {

            // Left shift
            int temp = Int32.Parse(strEle.Substring(idx) +
                                   strEle.Substring(0, idx));

            // Consider the maximum possible value
            optEle = Math.Max(optEle, temp);
        }

        return optEle;
    }

    // Function to maximize the absolute
    // difference between even and odd
    // indexed array elements
    static void minimumDifference(int[] arr)
    {

        int caseOne = 0;
        int minVal = 0;
        int maxVal = 0;

        // To calculate the difference of
        // odd indexed elements
        // and even indexed elements
        for (int i = 0; i < arr.Length; i++)
        {
            if (i % 2 == 0)
                minVal += minimize(arr[i]);
            else
                maxVal += maximize(arr[i]);
        }
        caseOne = Math.Abs(maxVal - minVal);
        int caseTwo = 0;
        minVal = 0;
        maxVal = 0;

        // To calculate the difference
        // between odd and even indexed
        // array elements
        for (int i = 0; i < arr.Length; i++)
        {

            if (i % 2 == 0)
                maxVal += maximize(arr[i]);
            else
                minVal += minimize(arr[i]);
            caseTwo = Math.Abs(maxVal - minVal);
        }

        // Print the maximum value
        Console.WriteLine(Math.Max(caseOne, caseTwo));
    }

    // Given array
    public static void Main()
    {
        int[] arr = { 332, 421, 215, 584, 232 };
        minimumDifference(arr);
    }
}

// This code is contributed by chitranayal.
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to minimize array
  // elements by shift operations
function minimize(n)
{
    let optEle = n;
    let strEle = (n).toString();

    // For checking all the
    // left shift operations
    for (let idx = 0; idx < strEle.length; idx++)
    {

      // Left shift
      let temp
        = parseInt(strEle.substring(idx)
                           + strEle.substring(0, idx));

      // Consider the minimum possible value
      optEle = Math.min(optEle, temp);
    }

    return optEle;
}

// Function to maximize array
  // elements by shift operations
function maximize(n)
{
    let optEle = n;
    let strEle = n.toString();

    // For checking all the
    // left shift operations
    for (let idx = 0; idx < strEle.length; idx++)
    {

      // Left shift
      let temp
        = parseInt(strEle.substring(idx)
                           + strEle.substring(0, idx));

      // Consider the maximum possible value
      optEle = Math.max(optEle, temp);
    }
    return optEle;
}

// Function to maximize the absolute
  // difference between even and odd
  // indexed array elements
function minimumDifference(arr)
{
    let caseOne = 0;
    let minVal = 0;
    let maxVal = 0;

    // To calculate the difference of
    // odd indexed elements
    // and even indexed elements
    for (let i = 0; i < arr.length; i++)
    {
      if (i % 2 == 0)
        minVal += minimize(arr[i]);
      else
        maxVal += maximize(arr[i]);
    }
    caseOne = Math.abs(maxVal - minVal);
    let caseTwo = 0;
    minVal = 0;
    maxVal = 0;

    // To calculate the difference
    // between odd and even indexed
    // array elements
    for (let i = 0; i < arr.length; i++)
    {
      if (i % 2 == 0)
        maxVal += maximize(arr[i]);
      else
        minVal += minimize(arr[i]);
      caseTwo = Math.abs(maxVal - minVal);
    }

    // Print the maximum value
    document.write(Math.max(caseOne, caseTwo)+"<Br>");
}

// Given array
let arr=[332, 421, 215, 584, 232 ];
minimumDifference(arr);

// This code is contributed by avanitrachhadiya2155
</script>
```

**Output:** 

```
658
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)
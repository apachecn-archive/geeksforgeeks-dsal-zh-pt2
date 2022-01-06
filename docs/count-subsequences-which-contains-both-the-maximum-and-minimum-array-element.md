# 计数包含最大和最小数组元素的子序列

> 原文:[https://www . geesforgeks . org/count-subseries-其中包含最大和最小数组元素/](https://www.geeksforgeeks.org/count-subsequences-which-contains-both-the-maximum-and-minimum-array-element/)

给定一个由 **N** 个整数组成的数组 **arr[]** ，任务是找出给定数组中包含最大和最小元素的子序列的数量。

**示例:**

> **输入:** arr[] = {1，2，3，4}
> **输出:** 4
> **解释:**
> 共有 4 个子序列{1，4}、{1，2，4}、{1，3，4}、{1，2，3，4}包含最大数组元素(= 4)和最小数组元素(= 1)。
> 
> **输入:** arr[] = {4，4，4，4 }
> T3】输出: 15

**天真法:**最简单的方法是，首先[遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)找到数组的最大值和[最小值，然后](https://www.geeksforgeeks.org/program-find-minimum-maximum-element-array/)[生成给定数组](https://www.geeksforgeeks.org/generating-all-possible-subsequences-using-recursion/)的所有可能的子序列。对于每个子序列，检查其是否包含 ***最大*** 和 ***最小*** 数组元素。对于所有这样的子序列，将计数增加 1。最后，打印此类子序列的计数。

***时间复杂度:**O(2<sup>N</sup>)*
***辅助空间:** O(N)*

**高效方法:**按照以下步骤优化上述方法:

*   计算最大元素和最小元素的出现次数。设 I 和 j 分别为计数。
*   检查最大和最小元素是否相同。如果发现为真，那么可能的子序列都是非空的数组子序列。
*   否则，为了满足子序列的条件，它应该包含至少 1 个来自 **i** 的元素和至少 1 个来自 **j** 的元素。因此，所需的子序列数由以下等式给出:

> **(pow(2，i) -1 ) * ( pow(2，j) -1 ) * pow(2，n-i-j)**

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include<bits/stdc++.h>
using namespace std;

int count(int arr[], int n, int value);

// Function to calculate the
// count of subsequences
double countSubSequence(int arr[], int n)
{

    // Find the maximum
    // from the array
    int maximum = *max_element(arr, arr + n);

    // Find the minimum
    // from the array
    int minimum = *min_element(arr, arr + n);

    // If array contains only
    // one distinct element
    if (maximum == minimum)
        return pow(2, n) - 1;

    // Find the count of maximum
    int i = count(arr, n, maximum);

    // Find the count of minimum
    int j = count(arr, n, minimum);

    // Finding the result
    // with given condition
    double res = (pow(2, i) - 1) *
                 (pow(2, j) - 1) *
                  pow(2, n - i - j);

    return res;
}

int count(int arr[], int n, int value)
{
    int sum = 0;

    for(int i = 0; i < n; i++)
        if (arr[i] == value)
            sum++;

    return sum;
}

// Driver Code
int main()
{
    int arr[] = { 1, 2, 3, 4 };
    int n = sizeof(arr) / sizeof(arr[0]);

    // Function call
    cout << countSubSequence(arr, n) << endl;
}

// This code is contributed by rutvik_56
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.Arrays;

class GFG{

// Function to calculate the
// count of subsequences
static double countSubSequence(int[] arr, int n)
{

    // Find the maximum
    // from the array
    int maximum = Arrays.stream(arr).max().getAsInt();

    // Find the minimum
    // from the array
    int minimum = Arrays.stream(arr).min().getAsInt();

    // If array contains only
    // one distinct element
    if (maximum == minimum)
        return Math.pow(2, n) - 1;

    // Find the count of maximum
    int i = count(arr, maximum);

    // Find the count of minimum
    int j = count(arr, minimum);

    // Finding the result
    // with given condition
    double res = (Math.pow(2, i) - 1) *
                 (Math.pow(2, j) - 1) *
                  Math.pow(2, n - i - j);

    return res;
}

static int count(int[] arr, int value)
{
    int sum = 0;

    for(int i = 0; i < arr.length; i++)
        if (arr[i] == value)
            sum++;

    return sum;
}

// Driver Code
public static void main(String[] args)
{
    int[] arr = { 1, 2, 3, 4 };
    int n = arr.length;

    // Function call
    System.out.println(countSubSequence(arr, n));
}
}

// This code is contributed by Amit Katiyar
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to calculate the
# count of subsequences
def countSubSequence(arr, n):

    # Find the maximum
    # from the array
    maximum = max(arr)

    # Find the minimum
    # from the array
    minimum = min(arr)

    # If array contains only
    # one distinct element
    if maximum == minimum:
        return pow(2, n)-1

    # Find the count of maximum
    i = arr.count(maximum)

    # Find the count of minimum
    j = arr.count(minimum)

    # Finding the result
    # with given condition
    res = (pow(2, i) - 1) * (pow(2, j) - 1) * pow(2, n-i-j)

    return res

# Driver Code
arr = [1, 2, 3, 4]
n = len(arr)

# Function call
print(countSubSequence(arr, n))
```

## C#

```
// C# program for
// the above approach
using System;
using System.Linq;
class GFG{

// Function to calculate the
// count of subsequences
static double countSubSequence(int[] arr,
                               int n)
{   
  // Find the maximum
  // from the array
  int maximum = arr.Max();

  // Find the minimum
  // from the array
  int minimum = arr.Min();

  // If array contains only
  // one distinct element
  if (maximum == minimum)
    return Math.Pow(2, n) - 1;

  // Find the count of maximum
  int i = count(arr, maximum);

  // Find the count of minimum
  int j = count(arr, minimum);

  // Finding the result
  // with given condition
  double res = (Math.Pow(2, i) - 1) *
               (Math.Pow(2, j) - 1) *
                Math.Pow(2, n - i - j);
  return res;
}

static int count(int[] arr, int value)
{
  int sum = 0;

  for(int i = 0; i < arr.Length; i++)
    if (arr[i] == value)
      sum++;

  return sum;
}

// Driver Code
public static void Main(String[] args)
{
  int[] arr = {1, 2, 3, 4};
  int n = arr.Length;

  // Function call
  Console.WriteLine(countSubSequence(arr, n));
}
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to calculate the
// count of subsequences
function countSubSequence(arr, n)
{

    // Find the maximum
    // from the array
    let maximum = Math.max(...arr);

    // Find the minimum
    // from the array
    let minimum = Math.min(...arr);

    // If array contains only
    // one distinct element
    if (maximum == minimum)
        return Math.pow(2, n) - 1;

    // Find the count of maximum
    let i = count(arr, maximum);

    // Find the count of minimum
    let j = count(arr, minimum);

    // Finding the result
    // with given condition
    let res = (Math.pow(2, i) - 1) *
                 (Math.pow(2, j) - 1) *
                  Math.pow(2, n - i - j);

    return res;
}

function count(arr, value)
{
    let sum = 0;

    for(let i = 0; i < arr.length; i++)
        if (arr[i] == value)
            sum++;

    return sum;
}

// Driver Code

    let arr = [ 1, 2, 3, 4 ];
    let n = arr.length;

    // Function call
    document.write(countSubSequence(arr, n));

// This code is contributed by souravghosh0416.
</script>
```

**Output:** 

```
4
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)
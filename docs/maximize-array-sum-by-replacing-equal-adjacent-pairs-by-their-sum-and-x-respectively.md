# 通过将相等的相邻对分别替换为它们的和和 X 来最大化数组和

> 原文:[https://www . geesforgeks . org/通过分别用它们的和和 x 替换相等的相邻对来最大化数组和/](https://www.geeksforgeeks.org/maximize-array-sum-by-replacing-equal-adjacent-pairs-by-their-sum-and-x-respectively/)

给定两个整数 **N** 和 **X** ，分别表示一个[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**的大小和所有数组元素的初始值，任务是在执行下列操作任意多次后，从给定数组中找到最大可能和。

> 选择任何有效的索引 **i** ，其中 **arr[i] = arr[i + 1]** ，并更新 **arr[i] = arr[i] + arr[i + 1]** 和 **arr[i + 1] = X** 。

**示例:**

> **输入:** N = 3，X = 5
> **输出:** 35
> **解释:**
> 初始 arr[] = [5，5，5]
> 在 i = 1 上执行给定操作，arr[] = [10，5，5]
> 在 i = 2 上执行给定操作，arr[] = [10，10，5]
> 在 i = 1 上执行给定操作，arr[] = [20，5，5]
> 
> 因此，该数组的最大可能和为 35。
> 
> **输入:** N = 2，X = 3
> **输出:** 9
> **解释:**
> 最初 arr[] = [3，3]
> 对 i = 1，arr[] = [6，3]
> 执行给定操作数组中不存在相邻的相等元素。
> 因此，该数组的最大可能和为 9。

**天真方法:**想法是对初始数组中的每个有效索引执行给定的操作，并从所有可能的数组重排中找到最大可能和。

***时间复杂度:**O(2<sup>N</sup>)*
***辅助空间:** O(1)*

**高效方法:**上述方法可以通过使用以下观察来优化:

*   从上述例子可以看出，最终数组中索引 **i** 处的元素的值由:
    给出

> x * 2<sup>(N–I–1)</sup>

*   因此，对于每个有效索引 **i** ，最终数组的和将等于系列**X * 2<sup>(N–I–1)</sup>**的和。
*   以上级数之和由
    给出

> 级数之和= X *(2<sup>N</sup>–1)

因此，只需打印**X *(2<sup>N</sup>–1)**作为所需答案。
以下是上述方法的实施:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to calculate x ^ y
int power(int x, int y)
{
    int temp;

    // Base Case
    if (y == 0)
        return 1;

    // Find the value in temp
    temp = power(x, y / 2);

    // If y is even
    if (y % 2 == 0)
        return temp * temp;
    else
        return x * temp * temp;
}

// Function that find the maximum
// possible sum of the array
void maximumPossibleSum(int N, int X)
{

    // Print the result using
    // the formula
    cout << (X * (power(2, N) - 1)) << endl;
}

// Driver code
int main()
{
    int N = 3, X = 5;

    // Function call
    maximumPossibleSum(N, X);
}

// This code is contributed by rutvik_56
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

import java.io.*;

class GFG {

    // Function to calculate x ^ y
    static int power(int x, int y)
    {
        int temp;

        // Base Case
        if (y == 0)
            return 1;

        // Find the value in temp
        temp = power(x, y / 2);

        // If y is even
        if (y % 2 == 0)
            return temp * temp;
        else
            return x * temp * temp;
    }

    // Function that find the maximum
    // possible sum of the array
    public static void
    maximumPossibleSum(int N, int X)
    {
        // Print the result using
        // the formula
        System.out.println(
            X * (power(2, N) - 1));
    }

    // Driver Code
    public static void
        main(String[] args)
    {
        int N = 3, X = 5;

        // Function Call
        maximumPossibleSum(N, X);
    }
}
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to calculate x ^ y
def power(x, y):

    # Base Case
    if(y == 0):
        return 1

    # Find the value in temp
    temp = power(x, y // 2)

    # If y is even
    if(y % 2 == 0):
        return temp * temp
    else:
        return x * temp * temp

# Function that find the maximum
# possible sum of the array
def maximumPossibleSum(N, X):

    # Print the result using
    # the formula
    print(X * (power(2, N) - 1))

# Driver Code
N = 3
X = 5

# Function call
maximumPossibleSum(N, X)

# This code is contributed by Shivam Singh
```

## C#

```
// C# program for
// the above approach
using System;
class GFG{

// Function to calculate x ^ y
static int power(int x, int y)
{
  int temp;

  // Base Case
  if (y == 0)
    return 1;

  // Find the value in temp
  temp = power(x, y / 2);

  // If y is even
  if (y % 2 == 0)
    return temp * temp;
  else
    return x * temp * temp;
}

// Function that find the maximum
// possible sum of the array
public static void maximumPossibleSum(int N,
                                      int X)
{
  // Print the result using
  // the formula
  Console.WriteLine(X * (power(2, N) - 1));
}

// Driver Code
public static void Main(String[] args)
{
  int N = 3, X = 5;

  // Function Call
  maximumPossibleSum(N, X);
}
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>

// Javascript program for the above approach   

// Function to calculate x ^ y
    function power(x , y) {
        var temp;

        // Base Case
        if (y == 0)
            return 1;

        // Find the value in temp
        temp = power(x, parseInt(y / 2));

        // If y is even
        if (y % 2 == 0)
            return temp * temp;
        else
            return x * temp * temp;
    }

    // Function that find the maximum
    // possible sum of the array
    function maximumPossibleSum(N , X)
    {
        // Print the result using
        // the formula
        document.write(X * (power(2, N) - 1));
    }

    // Driver Code

        var N = 3, X = 5;

        // Function Call
        maximumPossibleSum(N, X);

// This code contributed by aashish1995

</script>
```

**Output:** 

```
35
```

***时间复杂度:** O(log N)*
***空间复杂度:** O(1)*
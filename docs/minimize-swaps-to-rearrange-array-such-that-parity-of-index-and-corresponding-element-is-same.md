# 最小化交换以重新排列数组，使得索引和对应元素的奇偶性相同

> 原文:[https://www . geeksforgeeks . org/minimum-swaps-to-重排-array-so-索引和对应元素的奇偶校验相同/](https://www.geeksforgeeks.org/minimize-swaps-to-rearrange-array-such-that-parity-of-index-and-corresponding-element-is-same/)

给定一个数组 **A[]，**任务是找到修改给定数组 A[]所需的最小交换操作，使得对于数组中的每个索引，**奇偶性(i) =奇偶性(A[i])** ，其中**奇偶性(x) = x % 2** 。如果不可能获得这样的排列，那么打印-1。

**示例:**

> **输入:** A[] = { 2，4，3，1，5，6 }
> **输出:** 2
> **解释:**
> 交换(4，3)和(5，6)将数组修改为[2，3，4，1，6，5]，这样 I 和 A[i]的奇偶性对于所有索引都是相同的。
> 
> **输入:** A[] = {1，2，5，7}
> **输出:** -1
> **说明:**
> 给定数组不能按要求条件重新排列。

**方法:**
解决上述问题的最佳方法是选择这样一个指数，其中**宇称(i)** 和**宇称(A[I)】**不相同。

*   初始化两个变量 ***needodd*** 和 ***needeven*** 到 **0** ，存储每个元素的奇偶性。检查索引的奇偶校验，如果是奇数，则将*需要的奇数*值增加 1，否则将*需要的偶数*增加 1。
*   如果*需要奇数*和*需要偶数*不一样，那么所需的安排是不可能的。
*   否则，最终结果由 **needodd** 变量获得，因为它是所需的操作数。这是因为，在任何时刻，我们选择一个奇偶性与其索引的奇偶性不相同的奇偶性元素，并同样选择一个偶性元素并交换它们。

下面是上述方法的实现:

## C++

```
// C++ implementation to minimize
// swaps required to rearrange
// array such that parity of index and
// corresponding element is same
#include <bits/stdc++.h>
using namespace std;

// Function to return the
// parity of number
int parity(int x)
{
    return x % 2;

}

// Function to return minimum
// number of operations required
int solve(int a[], int size)
{

    // Initialize needodd and
    // needeven value by 0
    int needeven = 0;
    int needodd = 0;

    for(int i = 0; i < size; i++)
    {
        if(parity(i) != parity(a[i]))
        {

            // Check if parity(i) is odd
            if(parity(i) % 2)
            {

                // increase needodd
                // as we need odd no
                // at that position.
                needodd++;
            }
            else
            {

                // increase needeven
                // as we need even
                // number at that position
                needeven++;
            }
        }
    }

    // If needeven and needodd are unequal
    if(needeven != needodd)
        return -1;
    else
        return needodd;
}

// Driver Code
int main()
{
    int a[] = { 2, 4, 3, 1, 5, 6};
    int n = sizeof(a) / sizeof(a[0]);

    // Function call
    cout << solve(a, n) << endl;

    return 0;
}

// This code is contributed by venky07
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to minimize 
// swaps required to rearrange 
// array such that parity of index and 
// corresponding element is same
import java.util.*;

class GFG{

// Function to return the
// parity of number
static int parity(int x)
{
    return x % 2;
}

// Function to return minimum
// number of operations required
static int solve(int a[], int size)
{

    // Initialize needodd and
    // needeven value by 0
    int needeven = 0;
    int needodd = 0;

    for(int i = 0; i < size; i++)
    {
        if(parity(i) != parity(a[i]))
        {

            // Check if parity(i) is odd
            if(parity(i) % 2 == 1)
            {

                // Increase needodd
                // as we need odd no
                // at that position.
                needodd++;
            }
            else
            {

                // Increase needeven
                // as we need even
                // number at that position
                needeven++;
            }
        }
    }

    // If needeven and needodd are unequal
    if(needeven != needodd)
        return -1;
    else
        return needodd;
}

// Driver Code
public static void main (String[] args)
{
    int a[] = { 2, 4, 3, 1, 5, 6};
    int n = a.length;

    // Function call
    System.out.println(solve(a, n));
}
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python3 implementation to minimize
# swaps required to rearrange
# array such that parity of index and
# corresponding element is same

# Function to return the
# parity of number
def parity(x):
    return x % 2

# Function to return minimum
# number of operations required

def solve(a, size):

    # Initialize needodd and
    # needeven value by 0
    needeven = 0
    needodd = 0
    for i in range(size):

        if parity(i)!= parity(a[i]):

            # Check if parity(i) is odd
            if parity(i) % 2:

                # increase needodd
                # as we need odd no
                # at that position.
                needodd+= 1
            else:
                # increase needeven
                # as we need even
                # number at that position
                needeven+= 1

    # If needeven and needodd are unequal
    if needodd != needeven:
        return -1

    return needodd

# Driver code    
if __name__ =="__main__":

    a = [2, 4, 3, 1, 5, 6]
    n = len(a)
    print(solve(a, n))
```

## C#

```
// C# implementation to minimize 
// swaps required to rearrange 
// array such that parity of index and 
// corresponding element is same
using System;
class GFG{

// Function to return the
// parity of number
static int parity(int x)
{
  return x % 2;
}

// Function to return minimum
// number of operations required
static int solve(int[] a, int size)
{    
  // Initialize needodd and
  // needeven value by 0
  int needeven = 0;
  int needodd = 0;

  for(int i = 0; i < size; i++)
  {
    if(parity(i) != parity(a[i]))
    {
      // Check if parity(i) is odd
      if(parity(i) % 2 == 1)
      {
        // Increase needodd
        // as we need odd no
        // at that position.
        needodd++;
      }
      else
      {
        // Increase needeven
        // as we need even
        // number at that position
        needeven++;
      }
    }
  }

  // If needeven and needodd are unequal
  if(needeven != needodd)
    return -1;
  else
    return needodd;
}

// Driver Code
public static void Main ()
{
  int[] a = {2, 4, 3, 1, 5, 6};
  int n = a.Length;

  // Function call
  Console.Write(solve(a, n));
}
}

// This code is contributed by Chitranayal
```

## java 描述语言

```
<script>

// Javascript implementation to minimize
// swaps required to rearrange array such
// that parity of index and corresponding
// element is same

// Function to return the
// parity of number
function parity(x)
{
    return x % 2;
}

// Function to return minimum
// number of operations required
function solve(a, size)
{

    // Initialize needodd and
    // needeven value by 0
    let needeven = 0;
    let needodd = 0;

    for(let i = 0; i < size; i++)
    {
        if (parity(i) != parity(a[i]))
        {

            // Check if parity(i) is odd
            if (parity(i) % 2 == 1)
            {

                // Increase needodd
                // as we need odd no
                // at that position.
                needodd++;
            }
            else
            {

                // Increase needeven
                // as we need even
                // number at that position
                needeven++;
            }
        }
    }

    // If needeven and needodd are unequal
    if (needeven != needodd)
        return -1;
    else
        return needodd;
}

// Driver code
let a = [ 2, 4, 3, 1, 5, 6 ];
let n = a.length;

// Function call
document.write(solve(a, n));

// This code is contributed by rameshtravel07

</script>
```

**Output:** 

```
2
```
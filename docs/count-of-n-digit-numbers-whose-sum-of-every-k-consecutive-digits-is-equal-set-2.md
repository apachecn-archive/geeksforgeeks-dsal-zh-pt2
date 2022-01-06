# 每 K 个连续数字之和相等的 N 位数计数|设置 2

> 原文:[https://www . geeksforgeeks . org/n 位数的计数-其每 k 个连续位数的总和等于-set-2/](https://www.geeksforgeeks.org/count-of-n-digit-numbers-whose-sum-of-every-k-consecutive-digits-is-equal-set-2/)

给定两个整数 **N** 和 **K** ，任务是找出所有可能的 **N 位**数的计数，这些数的每一个 **K** 连续数字的和都相等。
**举例:**

> **输入:** N = 2，K=1
> **输出:** 9
> **说明:**
> 所有满足要求条件的两位数均为{11，22，33，44，55，66，77，88，99}
> **输入:** N = 3，K = 2
> **输出:** 90

**简单和滑动窗口方法:**参考[计数每 K 个连续数字之和相等的 N 个数字](https://www.geeksforgeeks.org/count-of-n-digit-numbers-whose-sum-of-every-k-consecutive-digits-is-equal/)的最简单方法和[滑动窗口技术](https://www.geeksforgeeks.org/window-sliding-technique/)为基础的方法。
**对数方法:**
对于 **K** 的和-连续元素总是相等的，整个数字由它的第一个 **K** 数字控制。

*   第**I**位数字将等于第 **(i-k) <sup>第</sup>** 位数字，以满足每个 **K** 连续数字的总和相同的条件。

> **说明:**
> N = 5 和 K = 2
> 如果前两位数字是 1 和 2，那么数字必须是 12121，这样每 2 个连续数字的和就是 3。
> 观察前 2 位，即前 **K** 位重复出现。

因此，要解决这个问题，现在的任务是找出等于**10<sup>K</sup>–10<sup>(K-1)</sup>**的 **K 位**数字的总数。因此，打印计算值作为答案。
以下是上述方法的实施:

## C++

```
// C++ Program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to count the number of
// N-digit numbers such that sum of
// every K consecutive digits are equal
void count(int n, int k)
{
    long count = (long)(pow(10, k) - pow(10, k - 1));

    // Print the answer
    cout << (count);
}

// Driver Code
int main()
{
    int n = 2, k = 1;
    count(n, k);
}

// This code is contributed by Ritik Bansal
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to implement
// the above approach
class GFG {

    // Function to count the number of
    // N-digit numbers such that sum of
    // every K consecutive digits are equal
    public static void count(int n, int k)
    {
        long count
            = (long)(Math.pow(10, k)
                     - Math.pow(10, k - 1));

        // Print the answer
        System.out.print(count);
    }

    // Driver Code
    public static void main(String[] args)
    {
        int n = 2, k = 1;
        count(n, k);
    }
}
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to count the number of
# N-digit numbers such that sum of
# every K consecutive digits are equal
def count(n, k):

    count = (pow(10, k) - pow(10, k - 1));

    # Print the answer
    print(count);

# Driver Code
if __name__ == '__main__':

    n = 2;
    k = 1;

    count(n, k);

# This code is contributed by 29AjayKumar
```

## C#

```
// C# Program to implement
// the above approach
using System;
class GFG{

  // Function to count the number of
  // N-digit numbers such that sum of
  // every K consecutive digits are equal
  public static void count(int n, int k)
  {
    long count = (long)(Math.Pow(10, k) -
                        Math.Pow(10, k - 1));

    // Print the answer
    Console.Write(count);
  }

  // Driver Code
  public static void Main(String[] args)
  {
    int n = 2, k = 1;
    count(n, k);
  }
}

// This code is contributed by Rohit_ranjan
```

## java 描述语言

```
<script>
// Javascript Program to implement
// the above approach

// Function to count the number of
// N-digit numbers such that sum of
// every K consecutive digits are equal
function count(n, k)
{
    let count = Math.pow(10, k) - Math.pow(10, k - 1);

    // Print the answer
    document.write(count);
}

// Driver Code
let n = 2, k = 1;
count(n, k);

// This code is contributed by souravmahato348.
</script>
```

**Output:** 

```
9
```

***时间复杂度:** O(log K)*
***辅助空间:** O(1)*
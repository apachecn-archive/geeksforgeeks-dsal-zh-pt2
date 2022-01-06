# 设置第 Kth 位后计数至 N 的数字

> 原文:[https://www . geesforgeks . org/count-numbers-up-n-having-kth-bit-set/](https://www.geeksforgeeks.org/count-numbers-up-to-n-having-kth-bit-set/)

给定两个整数 **N** 和 **K，**的任务是找到设置了**K-第**位的 **N** 之前的数字计数。

**示例:**

> ***输入:** N = 14，K = 2*
> ***输出:** 7*
> ***解释:***
> *小于等于 14 的数字，具有 2 <sup>nd</sup> 位组，分别为 4、5、6、7、12、13 和 14。*
> 
> ***输入:** N = 6，K = 1*
> ***输出:** 3*
> ***解释** :*
> *小于等于 6 的数字有 1 个 <sup>st</sup> 位组，分别为 1、3、5。*

**天真法:**最简单的方法是从 **1** 遍历到 **N** ，检查每个数字的第 K 位是否置位。

***时间复杂度:*** O(N)
***辅助空间:*** O(1)

**高效方法:**上述方法可以通过将任务分为两部分来优化:

1.  首先[右移](https://www.geeksforgeeks.org/left-shift-right-shift-operators-c-cpp/) **N** 、 **K+1** 次，然后[左移](https://www.geeksforgeeks.org/left-shift-right-shift-operators-c-cpp/)次，结果 **K** 次，给出满足给定条件的数的计数，直到[最近的 2 次方小于 N](https://www.geeksforgeeks.org/highest-power-2-less-equal-given-number/) 。
2.  现在，检查第位的 **K <sup>位是否设置在 **N** 位。</sup>**
3.  如果在 **N、**中设置了 **K <sup>第</sup>** 位，则将[最近的 2 次幂小于 N](https://www.geeksforgeeks.org/highest-power-2-less-equal-given-number/) 的数字的计数加到答案中。

下面是上述方法的实现:

## C++

```
// C++ program for above approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the count
// of number of 1's at ith bit
// in a range [1, n - 1]
long long getcount(long long n, int k)
{
    // Store count till nearest
    // power of 2 less than N
    long long res = (n >> (k + 1)) << k;

    // If K-th bit is set in N
    if ((n >> k) & 1)

        // Add to result the nearest
        // power of 2 less than N
        res += n & ((1ll << k) - 1);

    // Return result
    return res;
}

// Driver Code
int main()
{

    long long int N = 14;
    int K = 2;

    // Function Call
    cout << getcount(N + 1, K) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for above approach
class GFG
{

  // Function to return the count
  // of number of 1's at ith bit
  // in a range [1, n - 1]
  static long getcount(long n, int k)
  {

    // Store count till nearest
    // power of 2 less than N
    long res = (n >> (k + 1)) << k;

    // If K-th bit is set in N
    if (((n >> k) & 1) != 0)

      // Add to result the nearest
      // power of 2 less than N
      res += n & ((1 << k) - 1);

    // Return result
    return res;
  }

  // Driver code
  public static void main(String[] args)
  {
    long N = 14;
    int K = 2;

    // Function Call
    System.out.println(getcount(N + 1, K));
  }
}

// This code is contributed by divyesh072019
```

## 蟒蛇 3

```
# Python3 program for above approach

# Function to return the count
# of number of 1's at ith bit
# in a range [1, n - 1]
def getcount(n, k):

    # Store count till nearest
    # power of 2 less than N
    res = (n >> (k + 1)) << k

    # If K-th bit is set in N
    if ((n >> k) & 1):

        # Add to result the nearest
        # power of 2 less than N
        res += n & ((1 << k) - 1)

    # Return result
    return res

# Driver Code
if __name__ == '__main__':

    N = 14
    K = 2

    # Function Call
    print (getcount(N + 1, K))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for above approach
using System;

class GFG{

// Function to return the count
// of number of 1's at ith bit
// in a range [1, n - 1]
static long getcount(long n, int k)
{

    // Store count till nearest
    // power of 2 less than N
    long res = (n >> (k + 1)) << k;

    // If K-th bit is set in N
    if (((n >> k) & 1) != 0)

        // Add to result the nearest
        // power of 2 less than N
        res += n & ((1 << k) - 1);

    // Return result
    return res;
}

// Driver Code 
static void Main()
{
    long N = 14;
    int K = 2;

    // Function Call
    Console.WriteLine(getcount(N + 1, K));
}
}

// This code is contributed by divyeshrabadiya07
```

## java 描述语言

```
<script>

    // Javascript program for above approach

    // Function to return the count
    // of number of 1's at ith bit
    // in a range [1, n - 1]
    function getcount(n, k)
    {

        // Store count till nearest
        // power of 2 less than N
        let res = (n >> (k + 1)) << k;

        // If K-th bit is set in N
        if (((n >> k) & 1) != 0)

            // Add to result the nearest
            // power of 2 less than N
            res += n & ((1 << k) - 1);

        // Return result
        return res;
    }

    let N = 14;
    let K = 2;

    // Function Call
    document.write(getcount(N + 1, K));

</script>
```

**Output:** 

```
7
```

***时间复杂度:**O(1)*
T5**辅助空间:** O(1)
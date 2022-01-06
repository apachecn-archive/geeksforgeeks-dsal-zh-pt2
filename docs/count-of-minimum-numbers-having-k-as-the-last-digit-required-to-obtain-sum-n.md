# 以 K 为最后一位数字的最小数字计数，以获得总和 N

> 原文:[https://www . geeksforgeeks . org/count-of-minimum-numbers-having-k-as-最后一位数字-需要获得-sum-n/](https://www.geeksforgeeks.org/count-of-minimum-numbers-having-k-as-the-last-digit-required-to-obtain-sum-n/)

给定一个正整数 **N** 和一个数字 **K** ，任务是找到以数字 **K** 结尾的数字的最小计数，使得这些数字的总和为 **N** 。如果不存在总和为 **K** 的数字，则打印 **"-1"** 。

**示例:**

> **输入:** N = 42，K = 3
> **输出:** 4
> **说明:**
> 给定的数字 N(= 43)可以表示为 3 + 3 + 13 + 23，这样所有的数字都以数字 K(= 3)结尾。因此，计数分裂数字 4。
> 
> **输入:** N = 17，K = 3
> **输出:** -1

**方法:**给定的问题可以通过一个观察来解决，如果一个数可以表示为以数字 **K** 结尾的数的和，那么结果将是 10 的最大值。按照以下步骤解决问题:

*   如果数字 **K** 为偶数，整数 **N** 为奇数，则打印“**-1”**，因为不可能得到偶数的奇数和。
*   对于数字 **K** ，在范围**【0，9】**内找到以数字 **i** 结尾的最小数字。如果不可能，则设置值为 [**INT_MAX**](https://www.geeksforgeeks.org/int_max-int_min-cc-applications/) 。
*   此外，对于每个数字 **K** 找到创建以数字 **i** 结束的数字所需的最小步骤，范围为**【0，9】**。
*   现在，如果以数字 **i** 结尾的最小数字大于以**单位数字 i** 结尾的 **N** ，则打印 **"-1"** ，因为不可能将数字之和设为 **N** 。
*   否则，答案将是创建以数字 **i** 结尾的数字的最小步骤，该数字与 **N** 的单位数字相同，因为剩余的数字可以通过将这些数字插入到构成答案的任何数字中来获得。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

int minCount(int N, int K)
{
    // Stores the smallest number that
    // ends with digit i (0, 9)
    int SmallestNumber[10];

    // Stores the minimum number of
    // steps to create a number ending
    // with digit i
    int MinimumSteps[10];

    // Initialize elements as infinity
    for (int i = 0; i <= 9; i++) {
        SmallestNumber[i] = INT_MAX;
        MinimumSteps[i] = INT_MAX;
    }

    for (int i = 1; i <= 10; i++) {

        int num = K * i;

        // Minimum number
        // ending with digit i
        SmallestNumber[num % 10]
            = min(
                SmallestNumber[num % 10],
                num);

        // Minimum steps to create a
        // number ending with digit i
        MinimumSteps[num % 10]
            = min(
                MinimumSteps[num % 10], i);
    }

    // If N < SmallestNumber then,
    // return -1
    if (N < SmallestNumber[N % 10]) {
        return -1;
    }

    // Otherwise, return answer
    else {
        return MinimumSteps[N % 10];
    }
}

// Driver Code
int main()
{
    int N = 42, K = 7;
    cout << minCount(N, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for above approach
import java.util.*;

class GFG{

static int minCount(int N, int K)
{

    // Stores the smallest number that
    // ends with digit i (0, 9)
    int SmallestNumber[] = new int[10];

    // Stores the minimum number of
    // steps to create a number ending
    // with digit i
    int MinimumSteps[] = new int[10];

    // Initialize elements as infinity
    for(int i = 0; i <= 9; i++)
    {
        SmallestNumber[i] = Integer.MAX_VALUE;
        MinimumSteps[i] = Integer.MAX_VALUE;
    }

    for(int i = 1; i <= 10; i++)
    {
        int num = K * i;

        // Minimum number
        // ending with digit i
        SmallestNumber[num % 10] = Math.min(
            SmallestNumber[num % 10], num);

        // Minimum steps to create a
        // number ending with digit i
        MinimumSteps[num % 10] = Math.min(
            MinimumSteps[num % 10], i);
    }

    // If N < SmallestNumber then,
    // return -1
    if (N < SmallestNumber[N % 10])
    {
        return -1;
    }

    // Otherwise, return answer
    else
    {
        return MinimumSteps[N % 10];
    }
}

// Driver Code
public static void main(String[] args)
{
    int N = 42, K = 7;

    System.out.println(minCount(N, K));
}
}

// This code is contributed by hritikrommie
```

## 蟒蛇 3

```
# Python3 program for the above approach
import sys

def minCount(N, K):

    # Stores the smallest number that
    # ends with digit i (0, 9)
    SmallestNumber = [0 for i in range(10)]

    # Stores the minimum number of
    # steps to create a number ending
    # with digit i
    MinimumSteps = [0 for i in range(10)]

    # Initialize elements as infinity
    for i in range(10):
        SmallestNumber[i] = sys.maxsize;
        MinimumSteps[i] = sys.maxsize

    for i in range(1,11,1):
        num = K * i

        # Minimum number
        # ending with digit i
        SmallestNumber[num % 10] = min(SmallestNumber[num % 10],num)

        # Minimum steps to create a
        # number ending with digit i
        MinimumSteps[num % 10] = min(MinimumSteps[num % 10], i)

    # If N < SmallestNumber then,
    # return -1
    if (N < SmallestNumber[N % 10]):
        return -1

    # Otherwise, return answer
    else:
        return MinimumSteps[N % 10]

# Driver Code
if __name__ == '__main__':
    N = 42
    K = 7
    print(minCount(N, K))

    # This code is contributed by SURENDRA_GANGWAR.
```

## C#

```
// C# program for the above approach
using System;

public class GFG{

    static int minCount(int N, int K)
    {

        // Stores the smallest number that
        // ends with digit i (0, 9)
        int[] SmallestNumber = new int[10];

        // Stores the minimum number of
        // steps to create a number ending
        // with digit i
        int[] MinimumSteps = new int[10];

        // Initialize elements as infinity
        for(int i = 0; i <= 9; i++)
        {
            SmallestNumber[i] = Int32.MaxValue;
            MinimumSteps[i] = Int32.MaxValue;
        }

        for(int i = 1; i <= 10; i++)
        {
            int num = K * i;

            // Minimum number
            // ending with digit i
            SmallestNumber[num % 10] = Math.Min(
                SmallestNumber[num % 10], num);

            // Minimum steps to create a
            // number ending with digit i
            MinimumSteps[num % 10] = Math.Min(
                MinimumSteps[num % 10], i);
        }

        // If N < SmallestNumber then,
        // return -1
        if (N < SmallestNumber[N % 10])
        {
            return -1;
        }

        // Otherwise, return answer
        else
        {
            return MinimumSteps[N % 10];
        }
    }

    // Driver Code
    static public void Main ()
    {
        int N = 42, K = 7;

        Console.Write(minCount(N, K));
    }
}

// This code is contributed by shubhamsingh10
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

function minCount(N, K)
{
    // Stores the smallest number that
    // ends with digit i (0, 9)
    let SmallestNumber = new Array(10);

    // Stores the minimum number of
    // steps to create a number ending
    // with digit i
    let MinimumSteps = new Array(10);

    // Initialize elements as infinity
    for (let i = 0; i <= 9; i++) {
        SmallestNumber[i] = Number.MAX_VALUE;
        MinimumSteps[i] = Number.MAX_VALUE;
    }

    for (let i = 1; i <= 10; i++) {

        let num = K * i;

        // Minimum number
        // ending with digit i
        SmallestNumber[num % 10]
            = Math.min(
                SmallestNumber[num % 10],
                num);

        // Minimum steps to create a
        // number ending with digit i
        MinimumSteps[num % 10]
            = Math.min(
                MinimumSteps[num % 10], i);
    }

    // If N < SmallestNumber then,
    // return -1
    if (N < SmallestNumber[N % 10]) {
        return -1;
    }

    // Otherwise, return answer
    else {
        return MinimumSteps[N % 10];
    }
}

// Driver Code
    let N = 42, K = 7;
    document.write(minCount(N, K));

</script>
```

**Output:** 

```
6
```

**时间复杂度:**O(1)
T3】辅助空间: O(1)
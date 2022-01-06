# 等于给定数量的元素的最小计数

> 原文:[https://www . geeksforgeeks . org/给定数字的最小元素数/](https://www.geeksforgeeks.org/minimum-count-of-elements-that-sums-to-a-given-number/)

给定无限个形式元素![10^n  ](img/d7b63bb8dc4127a11a0d452dd5d84e00.png "Rendered by QuickLaTeX.com")和![25*100^n  ](img/d6eb3f0ce4d6f4740b798142b0cac9c1.png "Rendered by QuickLaTeX.com") ( n > = 0)。任务是找到所选元素的最小数量，使得总和等于 **K** 。
**例:**

> **输入:** K = 48
> **输出:** 6
> 所选元素为:(1 + 1 + 1 + 10 + 10 + 25)
> **输入:** 69
> **输出:** 9
> 所选元素为:(1 + 1 + 1 + 1 + 10 + 10 + 10 + 10 + 25)

**进场:**
有无限多以下元素:
1、10、25、100、1000、2500、10000、100000、100000、250000……等等。
贪婪的方法在这里行不通。对于 K = 66，通过贪婪方法，最小计数将为 9，所选元素为 25 + 25 + 10 + 1 + 1 + 1 + 1 + 1 + 1 = 66。但是当选择这些元素时，它的最佳答案是 6:25+10+10+10+10+1 = 66。所以，**动态编程**在这里会起作用。但是简单 DP 不能应用，因为 k 可以上升到 10^9。
动态规划方法:

*   预计算组成总计 99 的所选元素的最小数量，并将其存储在 memo 数组中。
*   此外，高达 99 的和只能由 1、10 和 25 的组合构成。
*   从 K 的末尾开始，遍历每一个最后 2 位数字，以找到所选元素的最小数量，这些元素的总和将达到最后两位数字。
*   将它们相加，找出最小计数。

> 上面方法的说明:
> 让我们取 K = 250166
> 让 min_count = 0，最后 2 位数字= 66
> 将最小元素数加到 min_count，总计为 66(它是从我们预先计算的 memo 数组
> 中计算出来的)。
> min_count = min_count + 6，
> 现在，min_count = 6，最后 2 位数字= 01
> 将最小元素数加到 min_count 总和为 1。
> min_count = min_count + 1，
> 现在，min_count = 7，最后 2 位数字= 25
> 将最小元素数加到 min_count 总和为 25。
> min_count = min_count + 1，
> 现在，min_count = 8。
> 因此，总计为 250166 的所选元素的最小数量是 8。
> 最佳选择元素为(250000，100，25，10，10，10，10，1)

下面是上述方法的实现。

## C++

```
// C++ implementation of the above approach
#include <bits/stdc++.h>
using namespace std;

int minCount(int K)
{
    // we will only store min counts
    // of sum upto 100
    int memo[100];

    // initialize with INT_MAX
    for (int i = 0; i < 100; i++) {
        memo[i] = INT_MAX;
    }

    // memo[0] = 0 as 0 is
    // made from 0 elements
    memo[0] = 0;

    // fill memo array with min counts
    // of elements that will constitute
    // sum upto 100

    for (int i = 1; i < 100; i++) {
        memo[i] = min(memo[i - 1] + 1, memo[i]);
    }

    for (int i = 10; i < 100; i++) {
        memo[i] = min(memo[i - 10] + 1, memo[i]);
    }

    for (int i = 25; i < 100; i++) {
        memo[i] = min(memo[i - 25] + 1, memo[i]);
    }

    // min_count will store min
    // count of elements chosen
    long min_count = 0;

    // starting from end iterate over
    // each 2 digits and add min count
    // of elements to min_count
    while (K > 0) {
        min_count += memo[K % 100];
        K /= 100;
    }

    return min_count;
}

// Driver code
int main()
{

    int K = 69;

    cout << minCount(K) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach

class GFG
{

    static int minCount(int K)
    {
        // we will only store min counts
        // of sum upto 100
        int memo[] = new int[100];

        // initialize with INT_MAX
        for (int i = 0; i < 100; i++)
        {
            memo[i] = Integer.MAX_VALUE;
        }

        // memo[0] = 0 as 0 is
        // made from 0 elements
        memo[0] = 0;

        // fill memo array with min counts
        // of elements that will constitute
        // sum upto 100

        for (int i = 1; i < 100; i++)
        {
            memo[i] = Math.min(memo[i - 1] + 1, memo[i]);
        }

        for (int i = 10; i < 100; i++)
        {
            memo[i] = Math.min(memo[i - 10] + 1, memo[i]);
        }

        for (int i = 25; i < 100; i++)
        {
            memo[i] = Math.min(memo[i - 25] + 1, memo[i]);
        }

        // min_count will store min
        // count of elements chosen
        int min_count = 0;

        // starting from end iterate over
        // each 2 digits and add min count
        // of elements to min_count
        while (K > 0)
        {
            min_count += memo[K % 100];
            K /= 100;
        }

        return min_count;
    }

    // Driver code
    public static void main (String[] args)
    {

                int K = 69;

                System.out.println(minCount(K));
    }
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 implementation of the above approach

def minCount(K):

    # we will only store min counts
    # of sum upto 100
    memo=[10**9 for i in range(100)]

    # memo[0] = 0 as 0 is
    # made from 0 elements
    memo[0] = 0

    # fill memo array with min counts
    # of elements that will constitute
    # sum upto 100

    for i in range(1,100):
        memo[i] = min(memo[i - 1] + 1, memo[i])

    for i in range(10,100):
        memo[i] = min(memo[i - 10] + 1, memo[i])

    for i in range(25,100):
        memo[i] = min(memo[i - 25] + 1, memo[i])

    # min_count will store min
    # count of elements chosen
    min_count = 0

    # starting from end iterate over
    # each 2 digits and add min count
    # of elements to min_count
    while (K > 0):
        min_count += memo[K % 100]
        K //= 100

    return min_count

# Driver code

K = 69

print(minCount(K))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# implementation of the above approach
using System;

class GFG
{

    static int minCount(int K)
    {
        // we will only store min counts
        // of sum upto 100
        int []memo = new int[100];

        // initialize with INT_MAX
        for (int i = 0; i < 100; i++)
        {
            memo[i] = int.MaxValue;
        }

        // memo[0] = 0 as 0 is
        // made from 0 elements
        memo[0] = 0;

        // fill memo array with min counts
        // of elements that will constitute
        // sum upto 100

        for (int i = 1; i < 100; i++)
        {
            memo[i] = Math.Min(memo[i - 1] + 1, memo[i]);
        }

        for (int i = 10; i < 100; i++)
        {
            memo[i] = Math.Min(memo[i - 10] + 1, memo[i]);
        }

        for (int i = 25; i < 100; i++)
        {
            memo[i] = Math.Min(memo[i - 25] + 1, memo[i]);
        }

        // min_count will store min
        // count of elements chosen
        int min_count = 0;

        // starting from end iterate over
        // each 2 digits and add min count
        // of elements to min_count
        while (K > 0)
        {
            min_count += memo[K % 100];
            K /= 100;
        }

        return min_count;
    }

    // Driver code
    static public void Main ()
    {

        int K = 69;
        Console.WriteLine(minCount(K));
    }
}

// This code is contributed by ajit
```

## java 描述语言

```
<script>
    // Javascript implementation of the above approach

    function minCount(K)
    {
        // we will only store min counts
        // of sum upto 100
        let memo = new Array(100);

        // initialize with INT_MAX
        for (let i = 0; i < 100; i++)
        {
            memo[i] = Number.MAX_VALUE;
        }

        // memo[0] = 0 as 0 is
        // made from 0 elements
        memo[0] = 0;

        // fill memo array with min counts
        // of elements that will constitute
        // sum upto 100

        for (let i = 1; i < 100; i++)
        {
            memo[i] = Math.min(memo[i - 1] + 1, memo[i]);
        }

        for (let i = 10; i < 100; i++)
        {
            memo[i] = Math.min(memo[i - 10] + 1, memo[i]);
        }

        for (let i = 25; i < 100; i++)
        {
            memo[i] = Math.min(memo[i - 25] + 1, memo[i]);
        }

        // min_count will store min
        // count of elements chosen
        let min_count = 0;

        // starting from end iterate over
        // each 2 digits and add min count
        // of elements to min_count
        while (K > 0)
        {
            min_count += memo[K % 100];
            K = parseInt(K / 100, 10);
        }

        return min_count;
    }

    let K = 69;
      document.write(minCount(K));

</script>
```

**Output:** 

```
9
```
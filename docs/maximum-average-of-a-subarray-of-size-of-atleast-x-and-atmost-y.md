# 大小至少为 X 和 Y 的子阵列的最大平均值

> 原文:[https://www . geeksforgeeks . org/最大平均尺寸子阵列至少 x 和-Atmos-y/](https://www.geeksforgeeks.org/maximum-average-of-a-subarray-of-size-of-atleast-x-and-atmost-y/)

给定一个数组 **arr[]** 和两个整数 **X** 和 **Y** 。任务是找到具有最大平均值(子阵列元素的平均值)的**大小**的子阵列，至少为 X 和**大气 Y** 。
**示例:**

> **输入:** arr[] = {1，2，3，4，5} X = 2，Y = 3
> **输出:** 4.5
> 我们可以取给我们最大平均值的子数组{4，5}。
> **输入:** arr[] = {6，7，8，3，2，4，2} X = 2，Y = 4
> **输出:** 7.5

**方法:**从 **X** 开始迭代每个大小的子阵列，以确定 **Y** 的大小，并在所有这样的子阵列中找到最大平均值。我们可以使用两个嵌套的 for 循环来迭代大小从 X 到 y 不等的所有子数组，为了降低时间复杂度，我们可以使用前缀和数组来获得 O(1)复杂度中任意子数组的和。
以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the maximum average
// of the sub-array with size
// atleast x and atmost y
double maxAvgSubArray(int a[], int n, int x, int y)
{

    // Calculate the prefix sum array
    int prefix[n];
    prefix[0] = a[0];
    for (int i = 1; i < n; i++)
        prefix[i] = prefix[i - 1] + a[i];

    double maximum = 0;

    // Iterate over all sub-arrays
    for (int i = 0; i < n; i++) {

        // Sub-arrays of size X to Y
        for (int j = i + x - 1; j < i + y && j < n; j++) {

            // Get the sum of the sub-array
            double sum = prefix[j];
            if (i > 0)
                sum -= prefix[i - 1];

            // Find average of sub-array
            double current = sum / (double)(j - i + 1);

            // Store the maximum of average
            maximum = max(maximum, current);
        }
    }

    return maximum;
}

// Driver code
int main()
{
    int a[] = { 6, 7, 8, 3, 2, 4, 2 };
    int X = 2, Y = 4;
    int n = sizeof(a) / sizeof(a[0]);
    cout << maxAvgSubArray(a, n, X, Y);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GfG {

    // Function to return the maximum average
    // of the sub-array with size
    // atleast x and atmost y
    static double maxAvgSubArray(int a[], int n, int x, int y)
    {

        // Calculate the prefix sum array
        int prefix[] = new int[n];
        prefix[0] = a[0];
        for (int i = 1; i < n; i++)
            prefix[i] = prefix[i - 1] + a[i];

        double maximum = 0;

        // Iterate over all sub-arrays
        for (int i = 0; i < n; i++) {

            // Sub-arrays of size X to Y
            for (int j = i + x - 1; j < i + y && j < n; j++) {

                // Get the sum of the sub-array
                double sum = prefix[j];
                if (i > 0)
                    sum -= prefix[i - 1];

                // Find average of sub-array
                double current = sum / (double)(j - i + 1);

                // Store the maximum of average
                maximum = Math.max(maximum, current);
            }
        }

        return maximum;
    }

    // Driver code
    public static void main(String[] args)
    {
        int a[] = { 6, 7, 8, 3, 2, 4, 2 };
        int X = 2, Y = 4;
        int n = a.length;
        System.out.println(maxAvgSubArray(a, n, X, Y));
    }
}
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the maximum average
# of the sub-array with size
# atleast x and atmost y
def maxAvgSubArray(a, n, x, y) :

    # Calculate the prefix sum array
    prefix = [0] * n ;
    prefix[0] = a[0];
    for i in range(1, n) :
        prefix[i] = prefix[i - 1] + a[i];

    maximum = 0;

    # Iterate over all sub-arrays
    for i in range(n) :
        j = i + x - 1

        # Sub-arrays of size X to Y
        while(j < i + y and j < n) :

            # Get the sum of the sub-array
            sum = prefix[j];

            if (i > 0) :
                sum -= prefix[i - 1];

            # Find average of sub-array
            current = sum / (j - i + 1);

            # Store the maximum of average
            maximum = max(maximum, current);

            j += 1
    return maximum;

# Driver code
if __name__ == "__main__" :

    a = [ 6, 7, 8, 3, 2, 4, 2 ];
    X = 2; Y = 4;

    n = len(a);
    print(maxAvgSubArray(a, n, X, Y));

# This code is contributed by Ryuga
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Function to return the maximum
    // average of the sub-array with
    // size atleast x and atmost y
    public static double maxAvgSubArray(int[] a, int n,
                                        int x, int y)
    {

        // Calculate the prefix sum array
        int[] prefix = new int[n];
        prefix[0] = a[0];
        for (int i = 1; i < n; i++)
        {
            prefix[i] = prefix[i - 1] + a[i];
        }

        double maximum = 0;

        // Iterate over all sub-arrays
        for (int i = 0; i < n; i++)
        {

            // Sub-arrays of size X to Y
            for (int j = i + x - 1;
                     j < i + y && j < n; j++)
            {

                // Get the sum of the sub-array
                double sum = prefix[j];
                if (i > 0)
                {
                    sum -= prefix[i - 1];
                }

                // Find average of sub-array
                double current = sum / (double)(j - i + 1);

                // Store the maximum of average
                maximum = Math.Max(maximum, current);
            }
        }

        return maximum;
    }

    // Driver code
    public static void Main(string[] args)
    {
        int[] a = new int[] {6, 7, 8, 3, 2, 4, 2};
        int X = 2, Y = 4;
        int n = a.Length;
        Console.WriteLine(maxAvgSubArray(a, n, X, Y));
    }
}

// This code is contributed by Shrikant13
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to return the maximum average
// of the sub-array with size
// atleast x and atmost y
function maxAvgSubArray($a, $n, $x, $y)
{

    // Calculate the prefix sum array
    $prefix = array();
    $prefix[0] = $a[0];
    for ($i = 1; $i < $n; $i++)
        $prefix[$i] = $prefix[$i - 1] + $a[$i];

    $maximum = 0;

    // Iterate over all sub-arrays
    for ($i = 0; $i < $n; $i++)
    {

        // Sub-arrays of size X to Y
        for ($j = $i + $x - 1;
            $j < $i + $y && $j < $n; $j++)
        {

            // Get the sum of the sub-array
            $sum = $prefix[$j];
            if ($i > 0)
                $sum -= $prefix[$i - 1];

            // Find average of sub-array
            $current = ($sum / ($j - $i + 1));

            // Store the maximum of average
            $maximum = max($maximum, $current);
        }
    }

    return $maximum;
}

// Driver code
$a = array(6, 7, 8, 3, 2, 4, 2);
$X = 2; $Y = 4;
$n = sizeof($a);
echo maxAvgSubArray($a, $n, $X, $Y);

// This code is contributed by Akanksha Rai
?>
```

## java 描述语言

```
<script>

// javascript program for the above approach

    // Function to return the maximum average
    // of the sub-array with size
    // atleast x and atmost y
    function maxAvgSubArray(a, n, x, y)
    {

        // Calculate the prefix sum array
        let prefix = new Array(n).fill(0);
        prefix[0] = a[0];
        for (let i = 1; i < n; i++)
            prefix[i] = prefix[i - 1] + a[i];

        let maximum = 0;

        // Iterate over all sub-arrays
        for (let i = 0; i < n; i++) {

            // Sub-arrays of size X to Y
            for (let j = i + x - 1; j < i + y && j < n; j++) {

                // Get the sum of the sub-array
                let sum = prefix[j];
                if (i > 0)
                    sum -= prefix[i - 1];

                // Find average of sub-array
                let current = sum / (j - i + 1);

                // Store the maximum of average
                maximum = Math.max(maximum, current);
            }
        }

        return maximum;
    }

// Driver Code

        let a = [ 6, 7, 8, 3, 2, 4, 2 ];
        let X = 2, Y = 4;
        let n = a.length;
        document.write(maxAvgSubArray(a, n, X, Y));

</script>
```

**Output:** 

```
7.5
```

**时间复杂度:** O(N * (Y-X))
**辅助空间:** O(N)
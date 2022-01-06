# 通过生成一个大小为 N 的数组并加上 X

可以得到的最大中值

> 原文:[https://www . geeksforgeeks . org/通过生成一个大小为 n 的数组来实现最大可能中值 x/](https://www.geeksforgeeks.org/maximum-median-possible-by-generating-an-array-of-size-n-with-sum-x/)

给定两个正整数 **N** 和 **X** 。任务是通过生成大小为 **N** 和 **X** 的数组来打印**最大中间值**

**示例:**

> **输入:** N = 1，X = 7
> **输出:** 7
> **说明:**阵可为:【7】，中位数为第 1 个元素，即 7。
> 
> **输入:** N = 7，X = 18
> **输出:** 4
> **解释:**可能的数组之一可以是:【0，1，2，3，4，4，4】。中位数= ceil(n/2)第 4 个元素= ceil(7/2) =第 5 个元素，即 4。

**方法:**考虑到中值需要最大化，所以[贪婪的](https://www.geeksforgeeks.org/greedy-algorithms/)方法可以是将**中值**元素的**位置**之前的所有元素设为**零**和**在其余元素之间等分总和** **X** 。
按照以下步骤解决问题:

*   如果 **n = 1** ，则打印 **X** 。
*   对于 **n > = 2。**
*   创建一个变量**中位数 _pos = ceil((double)(n)/2.0)。**
*   递减**中位数 _pos** ，以表示指标值。
*   创建一个变量**中位数= X/(n-中位数 _pos)** 。
*   打印**中间值**。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the maximum median possible
int maximizeMedian(int n, int X)
{
    // If only 1 element present
    if (n == 1) {
        return X;
    }
    else {
        // Position of median
        int median_pos = ceil((double)(n) / (2.0));
        median_pos--;
        int median = X / (n - median_pos);
        return median;
    }
    return 0;
}

// Driver Code
int main()
{
    int n = 1, X = 7;
    cout << maximizeMedian(n, X);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
public class GFG
{

    // Function to find the maximum median possible
    static int maximizeMedian(int n, int X)
    {

        // If only 1 element present
        if (n == 1) {
            return X;
        }
        else {
            // Position of median
            int median_pos
                = (int)Math.ceil((double)(n) / (2.0));
            median_pos--;
            int median = X / (n - median_pos);
            return median;
        }
    }

    // Driver Code
    public static void main(String args[])
    {
        int n = 1, X = 7;
        System.out.println(maximizeMedian(n, X));
    }
}

// This code is contributed by Samim Hossain Mondal.
```

## 蟒蛇 3

```
# Python code for the above approach

# Function to find the maximum median possible
def maximizeMedian(n, X):

    # If only 1 element present
    if (n == 1):
        return X
    else:
        # Position of median
        median_pos = (n) // (2.0)
        median_pos -= 1
        median = X // (n - median_pos)
        return median
    return 0

# Driver Code

n = 1
X = 7
print(maximizeMedian(n, X))

# This code is contributed by gfgking
```

## C#

```
// C# program for the above approach
using System;
class GFG
{

    // Function to find the maximum median possible
    static int maximizeMedian(int n, int X)
    {

        // If only 1 element present
        if (n == 1) {
            return X;
        }
        else {
            // Position of median
            int median_pos
                = (int)Math.Ceiling((double)(n) / (2.0));
            median_pos--;
            int median = X / (n - median_pos);
            return median;
        }
    }

    // Driver Code
    public static void Main()
    {
        int n = 1, X = 7;
        Console.WriteLine(maximizeMedian(n, X));
    }
}

// This code is contributed by ukasp.
```

## java 描述语言

```
<script>
       // JavaScript code for the above approach

       // Function to find the maximum median possible
       function maximizeMedian(n, X)
       {

           // If only 1 element present
           if (n == 1) {
               return X;
           }
           else
           {

               // Position of median
               let median_pos = Math.ceil((n) / (2.0));
               median_pos--;
               let median = X / (n - median_pos);
               return median;
           }
           return 0;
       }

       // Driver Code

       let n = 1, X = 7;
       document.write(maximizeMedian(n, X));

 // This code is contributed by Potta Lokesh
   </script>
```

**Output**

```
7
```

***时间复杂度*****:**O(1)
***辅助空间*** **:** O(1)
# 将数组分成三段后的最大和

> 原文:[https://www . geeksforgeeks . org/将数组分成三段后的最大和/](https://www.geeksforgeeks.org/maximum-sum-of-the-array-after-dividing-it-into-three-segments/)

给定一个大小为 **N** 的数组**。任务是通过将数组分成三个段来找到数组的最大可能和，使得第一个段中的每个元素乘以-1，第二个段中的每个元素乘以 1，第三个段中的每个元素乘以-1。线段可以相交，任何线段都可以包含零。**

****示例:****

> ****输入:** a[] = {-6，10，-3，10，-2}
> **输出:** 25
> 将线段划分为{-6}、{10，-3，10}、{-2)**
> 
> ****输入:** a[] = {-6，-10 }
> T3】输出: 16**

****方法:**
首先，我们需要计算每个第 I 元素的所有可能情况，在这些情况下应该进行划分。**

*   **在第一次遍历中，通过与-1 相乘或保持不变，找出 ith 元素是否产生最大和。**
*   **将所有值存储在数组 **b** 中。**
*   **在第二次遍历中，通过减少**a【I】**并添加**b【I】**来找到最大和。**

**下面是上述方法的实现:**

## **C++**

```
// C++ program to find maximum sum of array
// after dividing it into three segments
#include <bits/stdc++.h>
using namespace std;

// Function to find maximum sum of array
// after dividing it into three segments
int Max_Sum(int a[], int n)
{
    // To store sum upto ith index
    int b[n];
    int S = 0;
    int res = 0;

    // Traverse through the array
    for (int i = 0; i < n; i++)
    {
        b[i] = res;
        res += a[i];
        S += a[i];

        // Get the maximum possible sum
        res = max(res, -S);
    }

    // Store in the required answer
    int ans = S;

    // Maximum sum starting from left segment
    // by choosing between keeping array element as
    // it is or subtracting it
    ans = max(ans, res);

    // Finding maximum sum by decreasing a[i] and
    // adding b[i] to it that means max(multiplying
    // it by -1 or using b[i] value)
    int g = 0;

    // For third segment
    for (int i = n - 1; i >= 0; --i) {
        g -= a[i];
        ans = max(ans, g + b[i]);
    }

    // return the required answer
    return ans;
}

// Driver code
int main()
{
    int a[] = { -6, 10, -3, 10, -2 };

    int n = sizeof(a) / sizeof(a[0]);

    // Function call
    cout << "Maximum sum is: " << Max_Sum(a, n);

    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java program to find maximum sum of array
// after dividing it into three segments
import java.util.*;

class GFG
{

// Function to find maximum sum of array
// after dividing it into three segments
static int Max_Sum(int a[], int n)
{
    // To store sum upto ith index
    int []b = new int[n];
    int S = 0;
    int res = 0;

    // Traverse through the array
    for (int i = 0; i < n; i++)
    {
        b[i] = res;
        res += a[i];
        S += a[i];

        // Get the maximum possible sum
        res = Math.max(res, -S);
    }

    // Store in the required answer
    int ans = S;

    // Maximum sum starting from left segment
    // by choosing between keeping array element as
    // it is or subtracting it
    ans = Math.max(ans, res);

    // Finding maximum sum by decreasing a[i] and
    // adding b[i] to it that means max(multiplying
    // it by -1 or using b[i] value)
    int g = 0;

    // For third segment
    for (int i = n - 1; i >= 0; --i)
    {
        g -= a[i];
        ans = Math.max(ans, g + b[i]);
    }

    // return the required answer
    return ans;
}

// Driver code
public static void main(String[] args)
{
    int a[] = { -6, 10, -3, 10, -2 };

    int n = a.length;

    // Function call
    System.out.println("Maximum sum is: " +
                            Max_Sum(a, n));
}
}

// This code is contributed by Princi Singh
```

## **蟒蛇 3**

```
# Python3 program to find
# maximum sum of array after
# dividing it into three segments

# Function to find maximum sum of array
# after dividing it into three segments
def Max_Sum(a, n):

    # To store sum upto ith index
    b = [0 for i in range(n)]
    S = 0
    res = 0

    # Traverse through the array
    for i in range(n):
        b[i] = res
        res += a[i]
        S += a[i]

        # Get the maximum possible sum
        res = max(res, -S)

    # Store in the required answer
    ans = S

    # Maximum sum starting from
    # left segment by choosing between
    # keeping array element as it is
    # or subtracting it
    ans = max(ans, res)

    # Finding maximum sum by decreasing
    # a[i] and adding b[i] to it
    # that means max(multiplying it
    # by -1 or using b[i] value)
    g = 0

    # For third segment
    for i in range(n - 1, -1, -1):
        g -= a[i]
        ans = max(ans, g + b[i])

    # return the required answer
    return ans

# Driver code
a = [-6, 10, -3, 10, -2]

n = len(a)

# Function call
print("Maximum sum is:",
          Max_Sum(a, n))

# This code is contributed
# by Mohit Kumar
```

## **C#**

```
// C#+ program to find maximum sum of array
// after dividing it into three segments
using System;

class GFG
{

// Function to find maximum sum of array
// after dividing it into three segments
static int Max_Sum(int []a, int n)
{
    // To store sum upto ith index
    int []b = new int[n];
    int S = 0;
    int res = 0;

    // Traverse through the array
    for (int i = 0; i < n; i++)
    {
        b[i] = res;
        res += a[i];
        S += a[i];

        // Get the maximum possible sum
        res = Math.Max(res, -S);
    }

    // Store in the required answer
    int ans = S;

    // Maximum sum starting from left segment
    // by choosing between keeping array element
    // as it is or subtracting it
    ans = Math.Max(ans, res);

    // Finding maximum sum by decreasing a[i] and
    // adding b[i] to it that means max(multiplying
    // it by -1 or using b[i] value)
    int g = 0;

    // For third segment
    for (int i = n - 1; i >= 0; --i)
    {
        g -= a[i];
        ans = Math.Max(ans, g + b[i]);
    }

    // return the required answer
    return ans;
}

// Driver code
public static void Main()
{
    int []a = { -6, 10, -3, 10, -2 };

    int n = a.Length;

    // Function call
    Console.WriteLine("Maximum sum is: " +
                           Max_Sum(a, n));
}
}

// This code is contributed by anuj_67..
```

## **服务器端编程语言（Professional Hypertext Preprocessor 的缩写）**

```
<?php
// PHP program to find maximum sum of array
// after dividing it into three segments

// Function to find maximum sum of array
// after dividing it into three segments
function Max_Sum($a, $n)
{
    // To store sum upto ith index
    $b = array();
    $S = 0;
    $res = 0;

    // Traverse through the array
    for ($i = 0; $i < $n; $i++)
    {
        $b[$i] = $res;
        $res += $a[$i];
        $S += $a[$i];

        // Get the maximum possible sum
        $res = max($res, -$S);
    }

    // Store in the required answer
    $ans = $S;

    // Maximum sum starting from left segment
    // by choosing between keeping array element as
    // it is or subtracting it
    $ans = max($ans, $res);

    // Finding maximum sum by decreasing a[i] and
    // adding b[i] to it that means max(multiplying
    // it by -1 or using b[i] value)
    $g = 0;

    // For third segment
    for ($i = $n - 1; $i >= 0; --$i)
    {
        $g -= $a[$i];
        $ans = max($ans, $g + $b[$i]);
    }

    // return the required answer
    return $ans;
}

// Driver code
$a = array(-6, 10, -3, 10, -2 );

$n = count($a);

// Function call
echo ("Maximum sum is: ");
echo Max_Sum($a, $n);

// This code is contributed by Naman_garg.
?>
```

## **java 描述语言**

```
<script>
    // Javascript program to find maximum sum of array
    // after dividing it into three segments

    // Function to find maximum sum of array
    // after dividing it into three segments
    function Max_Sum(a, n)
    {
        // To store sum upto ith index
        let b = new Array(n);
        let S = 0;
        let res = 0;

        // Traverse through the array
        for (let i = 0; i < n; i++)
        {
            b[i] = res;
            res += a[i];
            S += a[i];

            // Get the maximum possible sum
            res = Math.max(res, -S);
        }

        // Store in the required answer
        let ans = S;

        // Maximum sum starting from left segment
        // by choosing between keeping array element
        // as it is or subtracting it
        ans = Math.max(ans, res);

        // Finding maximum sum by decreasing a[i] and
        // adding b[i] to it that means max(multiplying
        // it by -1 or using b[i] value)
        let g = 0;

        // For third segment
        for (let i = n - 1; i >= 0; --i)
        {
            g -= a[i];
            ans = Math.max(ans, g + b[i]);
        }

        // return the required answer
        return ans;
    }

    let a = [ -6, 10, -3, 10, -2 ];

    let n = a.length;

    // Function call
    document.write("Maximum sum is: " +
                           Max_Sum(a, n));

</script>
```

****Output:** 

```
Maximum sum is: 25
```** 

****时间复杂度:** O(N)**
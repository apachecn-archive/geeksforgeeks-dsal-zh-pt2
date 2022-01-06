# 数组和的上限除以 K 和数组元素的上限除以 K 的和之差

> 原文:[https://www . geesforgeks . org/数组元素之和除以 k 与数组元素之和除以 k 之差/](https://www.geeksforgeeks.org/difference-between-ceil-of-array-sum-divided-by-k-and-sum-of-ceil-of-array-elements-divided-by-k/)

给定一个[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**和一个整数 **K** ，任务是找出数组的总和[的上限](https://www.geeksforgeeks.org/python-math-ceil-function/)除以 **K** 与每个数组元素的上限之和除以 **K** 的绝对差。

**示例:**

> **输入:** arr[] = {1，2，3，4，5，6}，K = 4
> **输出:** 2
> **说明:**数组之和= 21。(数组的和)/ K = 6 的上限。
> 数组元素的上限除以 K 的和=(1/4)+(2/4)+(3/4)+(4/4)+(5/4)+(6/4)= 1+1+1+2+2 = 8。
> 因此，绝对差= 8–6 = 2。
> 
> **输入:** arr[] = {1，2，3}，K = 2
> T3】输出: 1

**方法:**按照以下步骤解决给定问题:

*   初始化两个变量，比如 **totalSum** 和 **perElementSum** ，存储数组的 [total sum 和每个数组元素的上限之和除以 **K** 。](https://www.geeksforgeeks.org/program-find-sum-elements-given-array/)
*   [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)并执行以下操作:
    *   将当前元素**arr【I】**添加到 **totalSum** 中。
    *   加上当前元素的上限除以 **K** ，即**arr【I/K**。
*   完成上述步骤后，打印**总计**和**完成**的绝对值作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find absolute difference
// between array sum divided by x and
// sum of ceil of array elements divided by x
int ceilDifference(int arr[], int n,
                   int x)
{
    // Stores the total sum
    int totalSum = 0;

    // Stores the sum of ceil of
    // array elements divided by x
    int perElementSum = 0;

    // Traverse the array
    for (int i = 0; i < n; i++) {

        // Adding each array element
        totalSum += arr[i];

        // Add the value ceil of arr[i]/x
        perElementSum
            += ceil((double)(arr[i])
                    / (double)(x));
    }

    // Find the ceil of the
    // total sum divided by x
    int totalCeilSum
        = ceil((double)(totalSum)
               / (double)(x));

    // Return absolute difference
    return abs(perElementSum
               - totalCeilSum);
}

// Driver Code
int main()
{
    int arr[] = { 1, 2, 3, 4, 5, 6 };
    int K = 4;
    int N = sizeof(arr) / sizeof(arr[0]);

    cout << ceilDifference(arr, N, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java approach for the above approach
public class GFG{

 // Function to find absolute difference
 // between array sum divided by x and
 // sum of ceil of array elements divided by x
 static int ceilDifference(int arr[], int n,
                    int x)
 {
     // Stores the total sum
     int totalSum = 0;

     // Stores the sum of ceil of
     // array elements divided by x
     int perElementSum = 0;

     // Traverse the array
     for (int i = 0; i < n; i++) {

         // Adding each array element
         totalSum += arr[i];

         // Add the value ceil of arr[i]/x
         perElementSum
             += Math.ceil((double)(arr[i])
                     / (double)(x));
     }

     // Find the ceil of the
     // total sum divided by x
     int totalCeilSum
         = (int) Math.ceil((double)(totalSum)
            / (double)(x));

     // Return absolute difference
     return Math.abs(perElementSum
                - totalCeilSum);
 }

    // Driver Code
    public static void main(String[] args) {
        int arr[] = { 1, 2, 3, 4, 5, 6 };
        int K = 4;
        int N = arr.length;

       System.out.println(ceilDifference(arr, N, K));
    }

}
// This code is contributed by abhinavjain194
```

## 蟒蛇 3

```
# Python3 program for the above approach
from math import ceil

# Function to find absolute difference
# between array sum divided by x and
# sum of ceil of array elements divided by x
def ceilDifference(arr, n, x):
    # Stores the total sum
    totalSum = 0

    # Stores the sum of ceil of
    # array elements divided by x
    perElementSum = 0

    # Traverse the array
    for i in range(n):
        # Adding each array element
        totalSum += arr[i]

        # Add the value ceil of arr[i]/x
        perElementSum += ceil(arr[i]/x)

    # Find the ceil of the
    # total sum divided by x
    totalCeilSum = ceil(totalSum / x)

    # Return absolute difference
    return abs(perElementSum- totalCeilSum)

# Driver Code
if __name__ == '__main__':
    arr =[1, 2, 3, 4, 5, 6]
    K = 4
    N = len(arr)

    print (ceilDifference(arr, N, K))

# This code is contributed by mohit kumar 29.
```

## C#

```
// C# approach for the above approach
using System;

class GFG{

// Function to find absolute difference
// between array sum divided by x and
// sum of ceil of array elements divided by x
static int ceilDifference(int[] arr, int n, int x)
{

    // Stores the total sum
    int totalSum = 0;

    // Stores the sum of ceil of
    // array elements divided by x
    int perElementSum = 0;

    // Traverse the array
    for(int i = 0; i < n; i++)
    {

        // Adding each array element
        totalSum += arr[i];

        // Add the value ceil of arr[i]/x
        perElementSum += (int)Math.Ceiling(
            (double)(arr[i]) / (double)(x));
    }

    // Find the ceil of the
    // total sum divided by x
    int totalCeilSum = (int)Math.Ceiling(
        (double)(totalSum) / (double)(x));

    // Return absolute difference
    return Math.Abs(perElementSum - totalCeilSum);
}

// Driver Code
public static void Main(string[] args)
{
    int[] arr = { 1, 2, 3, 4, 5, 6 };
    int K = 4;
    int N = arr.Length;

    Console.Write(ceilDifference(arr, N, K));
}
}

// This code is contributed by ukasp
```

## java 描述语言

```
<script>

// Javascript approach for the above approach

 // Function to find absolute difference
 // between array sum divided by x and
 // sum of ceil of array elements divided by x
 function ceilDifference(arr , n, x)
 {
     // Stores the total sum
     var totalSum = 0;

     // Stores the sum of ceil of
     // array elements divided by x
     var perElementSum = 0;

     // Traverse the array
     for (var i = 0; i < n; i++) {

         // Adding each array element
         totalSum += arr[i];

         // Add the value ceil of arr[i]/x
         perElementSum
             += parseInt(Math.ceil((arr[i])
                     / (x)));
     }

     // Find the ceil of the
     // total sum divided by x
     var totalCeilSum
         = parseInt( Math.ceil((totalSum)
            / (x)));

     // Return absolute difference
     return Math.abs(perElementSum
                - totalCeilSum);
 }

    // Driver Code

    var arr = [ 1, 2, 3, 4, 5, 6 ];
    var K = 4;
    var N = arr.length;

   document.write(ceilDifference(arr, N, K));

// This code contributed by shikhasingrajput

</script>
```

**Output:** 

```
2
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)
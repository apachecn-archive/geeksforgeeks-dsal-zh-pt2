# 将数组分成两个子集，使得两个子集的和的平方和最大

> 原文:[https://www . geesforgeks . org/divide-array-in-in-two-subset-so-sum-square-sum-is-maximum/](https://www.geeksforgeeks.org/divide-array-in-two-subsets-such-that-sum-of-square-of-sum-of-both-subsets-is-maximum/)

给定一个整数数组 **arr[]** ，任务是将这个数组分成两个非空子集，使得两个子集的和的平方和最大，并且两个子集的大小相差不得超过 1。
**例:**

> **输入:** arr[] = {1，2，3}
> **输出:** 26
> **说明:**
> 子集对之和如下
> (1)<sup>2</sup>+(2+3)<sup>2</sup>= 26
> (2)<sup>2</sup>+(1+3)<sup>2</sup>= 20
> (3)【4】

**方法:**任务是最大化 **a <sup>2</sup> + b <sup>2</sup>** 其中 **a** 和 **b** 是两个子集的和 **a + b = C** (常量)，即整个数组的和。对数组进行排序，将第一个**N/2–1**个较小的元素划分为一个子集，其余 **N/2 + 1** 个元素划分为另一个子集，即可得到最大的和。通过这种方式，可以最大化总和，同时保持大小差异不超过 1。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach

#include <bits/stdc++.h>
using namespace std;

// Function to return the maximum sum of the
// square of the sum of two subsets of an array
int maxSquareSubsetSum(int* A, int N)
{
    // Initialize variables to store
    // the sum of subsets
    int sub1 = 0, sub2 = 0;

    // Sorting the array
    sort(A, A + N);

    // Loop through the array
    for (int i = 0; i < N; i++) {

        // Sum of the first subset
        if (i < (N / 2) - 1)
            sub1 += A[i];

        // Sum of the second subset
        else
            sub2 += A[i];
    }

    // Return the maximum sum of
    // the square of the sum of subsets
    return sub1 * sub1 + sub2 * sub2;
}

// Driver code
int main()
{
    int arr[] = { 7, 2, 13, 4, 25, 8 };
    int N = sizeof(arr) / sizeof(arr[0]);

    cout << maxSquareSubsetSum(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

    // Function to return the maximum sum of the
    // square of the sum of two subsets of an array
    static int maxSquareSubsetSum(int []A, int N)
    {
        // Initialize variables to store
        // the sum of subsets
        int sub1 = 0, sub2 = 0;

        // Sorting the array
        Arrays.sort(A);

        // Loop through the array
        for (int i = 0; i < N; i++)
        {

            // Sum of the first subset
            if (i < (N / 2) - 1)
                sub1 += A[i];

            // Sum of the second subset
            else
                sub2 += A[i];
        }

        // Return the maximum sum of
        // the square of the sum of subsets
        return sub1 * sub1 + sub2 * sub2;
    }

    // Driver code
    public static void main (String[] args)
    {
        int arr[] = { 7, 2, 13, 4, 25, 8 };
        int N = arr.length;

        System.out.println(maxSquareSubsetSum(arr, N));
    }
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the maximum sum of the
# square of the sum of two subsets of an array
def maxSquareSubsetSum(A, N) :

    # Initialize variables to store
    # the sum of subsets
    sub1 = 0; sub2 = 0;

    # Sorting the array
    A.sort();

    # Loop through the array
    for i in range(N) :

        # Sum of the first subset
        if (i < (N // 2) - 1) :
            sub1 += A[i];

        # Sum of the second subset
        else :
            sub2 += A[i];

    # Return the maximum sum of
    # the square of the sum of subsets
    return sub1 * sub1 + sub2 * sub2;

# Driver code
if __name__ == "__main__" :

    arr = [ 7, 2, 13, 4, 25, 8 ];
    N = len(arr);

    print(maxSquareSubsetSum(arr, N));

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Function to return the maximum sum of the
    // square of the sum of two subsets of an array
    static int maxSquareSubsetSum(int []A, int N)
    {
        // Initialize variables to store
        // the sum of subsets
        int sub1 = 0, sub2 = 0;

        // Sorting the array
        Array.Sort(A);

        // Loop through the array
        for (int i = 0; i < N; i++)
        {

            // Sum of the first subset
            if (i < (N / 2) - 1)
                sub1 += A[i];

            // Sum of the second subset
            else
                sub2 += A[i];
        }

        // Return the maximum sum of
        // the square of the sum of subsets
        return sub1 * sub1 + sub2 * sub2;
    }

    // Driver code
    public static void Main()
    {
        int []arr = { 7, 2, 13, 4, 25, 8 };
        int N = arr.Length;

        Console.WriteLine(maxSquareSubsetSum(arr, N));
    }
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>
// javascript implementation of the approach
// Creating the bblSort function
 function bblSort(arr){

 for(var i = 0; i < arr.length; i++){

   // Last i elements are already in place 
   for(var j = 0; j < ( arr.length - i -1 ); j++){

     // Checking if the item at present iteration
     // is greater than the next iteration
     if(arr[j] > arr[j+1]){

       // If the condition is true then swap them
       var temp = arr[j]
       arr[j] = arr[j + 1]
       arr[j+1] = temp
     }
   }
 }
 // return the sorted array
 return arr;
}
    // Function to return the maximum sum of the
    // square of the sum of two subsets of an array
    function maxSquareSubsetSum(A , N) {
        // Initialize variables to store
        // the sum of subsets
        var sub1 = 0, sub2 = 0;

        // Sorting the array
        A = bblSort(A);

        // Loop through the array
        for (i = 0; i < N; i++) {

            // Sum of the first subset
            if (i < (N / 2) - 1)
                sub1 += A[i];

            // Sum of the second subset
            else
                sub2 += A[i];
        }

        // Return the maximum sum of
        // the square of the sum of subsets
        return sub1 * sub1 + sub2 * sub2;
    }

    // Driver code

        var arr = [ 7, 2, 13, 4, 25, 8 ];
        var N = arr.length;

        document.write(maxSquareSubsetSum(arr, N));

// This code is contributed by todaysgaurav
</script>
```

**Output:** 

```
2845
```

**时间复杂度:** O(N*log(N))
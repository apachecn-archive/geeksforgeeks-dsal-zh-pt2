# 数组中三元组(a，b，c)的计数，使得 a 除 b，b 除 c

> 原文:[https://www . geesforgeks . org/三胞胎计数-a-B- c-in-array-so-a-divides-B- and-b-divides-c/](https://www.geeksforgeeks.org/count-of-triplets-a-b-c-in-the-array-such-that-a-divides-b-and-b-divides-c/)

给定大小为 **N** 的正整数的**数组 arr[]** ，任务是计算数组中三元组的数量，使得 **a[i]除 a[j]和 a[j]除 a[k]** 和 **i < j < k.**
**示例:**

> **输入:** arr[] = {1，2，3，4，5，6}
> **输出:** 3
> **解释:**
> 三胞胎是:(1，2，4)，(1，2，6)，(1，3，6)。
> **输入:** arr[] = {1，2，2}
> **输出:** 1
> **解释:**
> 三元组为(1，2，2)

**天真的做法:**为了解决上面提到的问题，我们将尝试实施**蛮力解决方案**。遍历数组中所有三个数字 a[i]、a[j]和 a[k]，并计算满足给定条件的三元组的数量。
***时间复杂度:**O(N<sup>3</sup>)*
***辅助空间复杂度:** O(1)*
**高效方法:**为了优化上述方法，我们可以从索引 1 到 n-2 遍历**中间元素**的数组，对于每个中间元素，我们可以遍历左数组中的一个[i]并计算可能的一个[i]的数量同样，我们可以在正确的数组中遍历，对 a[k]做同样的事情。
以下是上述办法的实施:

## C++

```
// C++ program to find count of triplets
// (a, b, c) in the Array such that
// a divides b and b divides c

#include <bits/stdc++.h>
using namespace std;

// Function to count triplets
int getCount(int arr[], int n)
{
    int count = 0;

    // Iterate for middle element
    for (int j = 1; j < n - 1; j++) {
        int p = 0, q = 0;

        // Iterate left array for a[i]
        for (int i = 0; i < j; i++) {

            if (arr[j] % arr[i] == 0)
                p++;
        }

        // Iterate right array for a[k]
        for (int k = j + 1; k < n; k++) {

            if (arr[k] % arr[j] == 0)
                q++;
        }

        count += p * q;
    }
    // return the final result
    return count;
}

// Driver code
int main()
{
    int arr[] = { 1, 2, 2 };
    int N = sizeof(arr) / sizeof(arr[0]);

    cout << getCount(arr, N) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find count of triplets
// (a, b, c) in the Array such that
// a divides b and b divides c
import java.io.*;
import java.util.*;

class GFG {

// Function to count triplets
static int getCount(int arr[], int n)
{
    int count = 0;

    // Iterate for middle element
    for(int j = 1; j < n - 1; j++)
    {
       int p = 0, q = 0;

       // Iterate left array for a[i]
       for(int i = 0; i < j; i++)
       {
          if (arr[j] % arr[i] == 0)
              p++;
       }

       // Iterate right array for a[k]
       for(int k = j + 1; k < n; k++)
       {
          if (arr[k] % arr[j] == 0)
              q++;
       }

       count += p * q;
    }

    // return the final result
    return count;
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 1, 2, 2 };
    int N = arr.length;

    System.out.println(getCount(arr, N));
}
}

// This code is contributed by coder001
```

## 蟒蛇 3

```
# Python3 program to find the count of
# triplets (a, b, c) in the Array such
# that a divides b and b divides c

# Function to count triplets
def getCount(arr, n):
    count = 0

    # Iterate for middle element
    for j in range(1, n - 1):
        p, q = 0, 0

        # Iterate left array for a[i]
        for i in range(j):

            if (arr[j] % arr[i] == 0):
                p += 1

        # Iterate right array for a[k]
        for k in range(j + 1, n):

            if (arr[k] % arr[j] == 0):
                q += 1

        count += p * q

    # Return the final result
    return count

# Driver code
if __name__ == '__main__':

    arr = [ 1, 2, 2 ]
    N = len(arr)

    print(getCount(arr, N))

# This code is contributed by mohit kumar 29   
```

## C#

```
// C# program to find count of triplets
// (a, b, c) in the Array such that
// a divides b and b divides c
using System;

class GFG{

// Function to count triplets
public static int getCount(int[] arr, int n)
{
    int count = 0;

    // Iterate for middle element
    for(int j = 1; j < n - 1; j++)
    {
        int p = 0, q = 0;

        // Iterate left array for a[i]
        for(int i = 0; i < j; i++)
        {
            if (arr[j] % arr[i] == 0)
                p++;
        }

        // Iterate right array for a[k]
        for(int k = j + 1; k < n; k++)
        {
            if (arr[k] % arr[j] == 0)
                q++;
        }
        count += p * q;
    }

    // return the final result
    return count;
}

// Driver code
public static void Main()
{
    int[] arr = { 1, 2, 2 };
    int N = arr.Length;

    Console.WriteLine(getCount(arr, N));
}
}

// This code is contributed by jrishabh99
```

## java 描述语言

```
<script>

// Javascript program to find count of triplets
// (a, b, c) in the Array such that
// a divides b and b divides c

// Function to count triplets
function getCount(arr, n)
{
    var count = 0;

    // Iterate for middle element
    for(var j = 1; j < n - 1; j++)
    {
       var p = 0, q = 0;

       // Iterate left array for a[i]
       for(var i = 0; i < j; i++)
       {
          if (arr[j] % arr[i] == 0)
              p++;
       }

       // Iterate right array for a[k]
       for(var k = j + 1; k < n; k++)
       {
          if (arr[k] % arr[j] == 0)
              q++;
       }

       count += p * q;
    }

    // return the final result
    return count;
}

// Driver Code
var arr = [ 1, 2, 2 ];
var N = arr.length;

document.write(getCount(arr, N));

// This code is contributed by Khushboogoyal499

</script>
```

**Output:** 

```
1
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间复杂度:** O(1)*
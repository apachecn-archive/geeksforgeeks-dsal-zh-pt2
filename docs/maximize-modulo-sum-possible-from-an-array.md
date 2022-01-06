# 最大化数组中可能的模和

> 原文:[https://www . geeksforgeeks . org/从数组中取模最大可能和/](https://www.geeksforgeeks.org/maximize-modulo-sum-possible-from-an-array/)

给定一个由 **N** 正整数组成的数组 **arr[]** ，任务是求 **∑(M mod arr[i])** 的最大值，其中 **arr[i]** 为任意数组元素，为非负整数 **M** 。

**示例:**

> **输入:** arr[] = {3，4，6}
> **输出:** 10
> **解释:**对于 M = 11，(11 mod 3) + (11 mod 4) + (11 mod 6) =10
> 
> **输入:** arr[]={7，46，11，20，11 }
> T3】输出: 90

**方法:**按照以下步骤解决问题:

*   由于 **A mod B** 是 **A** 除以 **B** 的余数，所以表达式 **∑(M mod arr[i])** 的最大值为:

> (M mod Arr[0]) + (M mod Arr[1]) +。。。+(m mod arr[n-1])=(arr[0]–1)+(arr[1]–1)++(arr[n-1]–1)

*   考虑**K = Arr[0]×Arr[1]×Arr[N–1]**，则 **(K mod Arr[i]) = 0** 对于范围**【0，N–1】**中的每个 **i**
*   因此，((k1)mod Arr[I])= Arr[I]1。因此对于**M = K–1**，可以得到最优结果。

**以下是上述方法的实现:**

## C++

```
// C++ Program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to calculate maximum modulo
// sum possible from a given array
int MaximumModuloSum(int Arr[], int N)
{
    // Stores the sum
    int sum = 0;

    // Traverse the array
    for (int i = 0; i < N; i++) {
        sum += Arr[i] - 1;
    }

    return sum;
}

// Driver Code
int main()
{
    int arr[] = { 3, 4, 6 };
    int N = sizeof(arr) / sizeof(arr[0]);
    cout << MaximumModuloSum(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to implement
// the above approach

import java.io.*;

class GFG {
    public static int MaximumModuloSum(int Arr[], int N)
    {

        // Stores the sum
        int sum = 0;

        // Traverse the array
        for (int i = 0; i < N; i++) {
            sum += Arr[i] - 1;
        }
        return sum;
    }
    public static void main(String[] args)
    {
        int arr[] = { 3, 4, 6 };
        int N = 3;
        System.out.println(MaximumModuloSum(arr, N));
    }
}

// This code is contributed by aditya7409.
```

## 蟒蛇 3

```
# Python 3 Program to implement
# the above approach

# Function to calculate maximum modulo
# sum possible from a given array
def MaximumModuloSum( Arr, N):

    # Stores the sum
    sum = 0;

    # Traverse the array
    for i in range( N ):
        sum += Arr[i] - 1;

    return sum;

# Driver Code
if __name__ == "__main__":

    arr = [ 3, 4, 6 ];
    N = len(arr)
    print(MaximumModuloSum(arr, N))

    # This code is contributed by chitranayal.
```

## C#

```
// C# program for the above approach
using System;
class GFG
{

  public static int MaximumModuloSum(int[] Arr, int N)
  {

    // Stores the sum
    int sum = 0;

    // Traverse the array
    for (int i = 0; i < N; i++) {
      sum += Arr[i] - 1;
    }
    return sum;
  }

  // Driver code
  static void Main()
  {
    int[] arr = { 3, 4, 6 };
    int N = 3;
    Console.WriteLine(MaximumModuloSum(arr, N));
  }
}

// This code is contributed by susmitakundugoaldanga.
```

## java 描述语言

```
<script>

// Javascript Program to implement
// the above approach

// Function to calculate maximum modulo
// sum possible from a given array
    function MaximumModuloSum(Arr, N)
    {

        // Stores the sum
        var sum = 0;

        // Traverse the array
        for (i = 0; i < N; i++)
        {
            sum += Arr[i] - 1;
        }
        return sum;
    }

    // Driver code
    var arr = [ 3, 4, 6 ];
    var N = 3;
    document.write(MaximumModuloSum(arr, N));

// This code is contributed by umadevi9616
</script>
```

**Output:** 

```
10
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)
# 通过执行给定的操作计算一个数组中可以获得的 1 的个数

> 原文:[https://www . geeksforgeeks . org/counts-1s-通过执行给定操作可以在阵列中获得的数量/](https://www.geeksforgeeks.org/counts-1s-that-can-be-obtained-in-an-array-by-performing-given-operations/)

给定一个最初仅由 **0** s 组成的大小为 **N** 的[阵列](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** ，任务是通过执行以下操作 **N** 次来计算阵列中可获得的 **1** s 的数量。

> 在第 i <sup>次</sup>操作中，翻转索引(***1***)是第 I**次**次[次](https://www.geeksforgeeks.org/print-first-m-multiples-of-n-without-using-any-loop-in-python/)的所有数组元素。

**示例:**

> **输入:** arr[] = { 0，0，0，0，0 }
> **输出:** 2
> **解释:**
> 索引为 1 倍数的翻转数组元素将 arr[]修改为{ 1，1，1，1，1，1 }
> 索引为 2 倍数的翻转数组元素将 arr[]修改为{ 1，0，1，0，1 }
> 索引为 3 倍数的翻转数组元素将 arr[]修改为{ 1，0，0，0， 1 }
> 翻转索引为 4 倍数的数组元素将 arr[]修改为{ 1，0，0，1，1 }
> 翻转索引为 5 倍数的数组元素将 arr[]修改为{ 1，0，0，1，0 }
> 因此，所需的输出为 2。
> 
> **输入:** arr[] = { 0，0 }
> T3】输出: 1

**天真方法:**解决这个问题最简单的方法是使用变量 **i** 遍历范围**【1，N】**，翻转所有索引为 **i** 的[倍数](https://www.geeksforgeeks.org/print-first-m-multiples-of-n-without-using-any-loop-in-python/)的数组元素。最后，打印阵列中存在的 **1** 的总数。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to count total number of 1s in
// array by performing given operations
int cntOnesArrWithGivenOp(int arr[], int N)
{
    // Stores count of 1s in the array
    // by performing the operations
    int cntOnes = 0;

    // Iterate over the range [1, N]
    for (int i = 1; i <= N; i++) {

        // Flip all array elements whose
        // index is multiple of i
        for (int j = i - 1; j < N;
             j += i) {

            // Update arr[i]
            arr[j] = !(arr[j]);
        }
    }

    // Traverse the array
    for (int i = 0; i < N; i++) {

        // If current element is 1
        if (arr[i] == 1) {

            // Update cntOnes
            cntOnes += 1;
        }
    }

    return cntOnes;
}

// Driver Code
int main()
{

    int arr[] = { 0, 0, 0, 0, 0 };

    int N = sizeof(arr)
            / sizeof(arr[0]);

    cout << cntOnesArrWithGivenOp(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
class GFG
{

    // Function to count total number of 1s in
    // array by performing given operations
    static int cntOnesArrWithGivenOp(int arr[], int N)
    {

        // Stores count of 1s in the array
        // by performing the operations
        int cntOnes = 0;

        // Iterate over the range [1, N]
        for (int i = 1; i <= N; i++)
        {

            // Flip all array elements whose
            // index is multiple of i
            for (int j = i - 1; j < N; j += i)
            {

                // Update arr[i]
                arr[j] = arr[j] == 0 ? 1 : 0;
            }
        }

        // Traverse the array
        for (int i = 0; i < N; i++)
        {

            // If current element is 1
            if (arr[i] == 1)
            {

                // Update cntOnes
                cntOnes += 1;
            }
        }
        return cntOnes;
    }

    // Driver Code
    public static void main(String[] args)
    {
        int arr[] = { 0, 0, 0, 0, 0 };
        int N = arr.length;
        System.out.print(cntOnesArrWithGivenOp(arr, N));
    }
}

// This code is contributed by shikhasingrajput
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to count total number of 1s in
# array by performing given operations
def cntOnesArrWithGivenOp(arr, N):

    # Stores count of 1s in the array
    # by performing the operations
    cntOnes = 0

    # Iterate over the range [1, N]
    for i in range(1, N + 1):

        # Flip all array elements whose
        # index is multiple of i
        for j in range(i - 1, N, i):

            # Update arr[i]
            arr[j] = 1 if arr[j] == 0 else 0

    # Traverse the array
    for i in range(N):

        # If current element is 1
        if (arr[i] == 1):

            # Update cntOnes
            cntOnes += 1

    return cntOnes

# Driver Code
if __name__ == '__main__':

    arr = [ 0, 0, 0, 0, 0 ]
    N = len(arr)

    print(cntOnesArrWithGivenOp(arr, N))

# This code is contributed by 29AjayKumar
```

## C#

```
// C# program to implement
// the above approach
using System;
class GFG
{

    // Function to count total number of 1s in
    // array by performing given operations
    static int cntOnesArrWithGivenOp(int []arr, int N)
    {

        // Stores count of 1s in the array
        // by performing the operations
        int cntOnes = 0;

        // Iterate over the range [1, N]
        for (int i = 1; i <= N; i++)
        {

            // Flip all array elements whose
            // index is multiple of i
            for (int j = i - 1; j < N; j += i)
            {

                // Update arr[i]
                arr[j] = arr[j] == 0 ? 1 : 0;
            }
        }

        // Traverse the array
        for (int i = 0; i < N; i++)
        {

            // If current element is 1
            if (arr[i] == 1)
            {

                // Update cntOnes
                cntOnes += 1;
            }
        }
        return cntOnes;
    }

    // Driver Code
    public static void Main(String[] args)
    {
        int []arr = { 0, 0, 0, 0, 0 };
        int N = arr.Length;
        Console.Write(cntOnesArrWithGivenOp(arr, N));
    }
}

// This code contributed by shikhasingrajput
```

## java 描述语言

```
<script>

// javascript program for the above approach

    // Function to count total number of 1s in
    // array by performing given operations
    function cntOnesArrWithGivenOp(arr, N)
    {

        // Stores count of 1s in the array
        // by performing the operations
        let cntOnes = 0;

        // Iterate over the range [1, N]
        for (let i = 1; i <= N; i++)
        {

            // Flip all array elements whose
            // index is multiple of i
            for (let j = i - 1; j < N; j += i)
            {

                // Update arr[i]
                arr[j] = arr[j] == 0 ? 1 : 0;
            }
        }

        // Traverse the array
        for (let i = 0; i < N; i++)
        {

            // If current element is 1
            if (arr[i] == 1)
            {

                // Update cntOnes
                cntOnes += 1;
            }
        }
        return cntOnes;
    }

// Driver Code

        let arr = [ 0, 0, 0, 0, 0 ];
        let N = arr.length;
        document.write(cntOnesArrWithGivenOp(arr, N));

</script>
```

**Output:** 

```
2
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*

**高效途径:**优化上述途径，思路基于只有[完美方块](https://www.geeksforgeeks.org/check-if-given-number-is-perfect-square-in-cpp/)包含奇数个[因子](https://www.geeksforgeeks.org/efficient-program-print-number-factors-n-numbers/)的事实。按照以下步骤解决问题:

*   初始化一个变量，比如**cntone**，通过执行这些操作来存储数组中 **1** 的计数。
*   更新**[**【sqrt(n)**](https://www.geeksforgeeks.org/sqrt-sqrtl-sqrtf-cpp/)**
*   **最后，打印**cntone**的值。**

**下面是上述方法的实现:**

## **C++**

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to count total number of 1s in
// array by performing the given operations
int cntOnesArrWithGivenOp(int arr[], int N)
{

    // Stores count of 1s in the array
    // by performing the operations
    int cntOnes = 0;

    // Update cntOnes
    cntOnes = sqrt(N);

    return cntOnes;
}

// Driver Code
int main()
{

    int arr[] = { 0, 0, 0, 0, 0 };

    int N = sizeof(arr)
            / sizeof(arr[0]);

    cout << cntOnesArrWithGivenOp(arr, N);

    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java program to implement
// the above approach
import java.util.*;
class GFG
{

  // Function to count total number of 1s in
  // array by performing the given operations
  static int cntOnesArrWithGivenOp(int arr[], int N)
  {

    // Stores count of 1s in the array
    // by performing the operations
    int cntOnes = 0;

    // Update cntOnes
    cntOnes = (int)Math.sqrt(N);
    return cntOnes;
  }

  // Driver code
  public static void main(String[] args)
  {
    int arr[] = { 0, 0, 0, 0, 0 };
    int N = arr.length;
    System.out.println(cntOnesArrWithGivenOp(arr, N));
  }
}

// This code is contributed by susmitakundugoaldanga
```

## **蟒蛇 3**

```
# Python3 program to implement
# the above approach

# Function to count total number of 1s in
# array by performing the given operations
def cntOnesArrWithGivenOp(arr, N) :

    # Stores count of 1s in the array
    # by performing the operations
    cntOnes = 0;

    # Update cntOnes
    cntOnes = int(N ** (1/2));
    return cntOnes;

# Driver Code
if __name__ == "__main__" :
    arr = [ 0, 0, 0, 0, 0 ];
    N = len(arr);
    print(cntOnesArrWithGivenOp(arr, N));

    # This code is contributed by AnkThon
```

## **C#**

```
// C# program to implement
// the above approach
using System;
class GFG
{

  // Function to count total number of 1s in
  // array by performing the given operations
  static int cntOnesArrWithGivenOp(int []arr, int N)
  {

    // Stores count of 1s in the array
    // by performing the operations
    int cntOnes = 0;

    // Update cntOnes
    cntOnes = (int)Math.Sqrt(N);
    return cntOnes;
  }

  // Driver code
  public static void Main(String[] args)
  {
    int []arr = { 0, 0, 0, 0, 0 };
    int N = arr.Length;
    Console.WriteLine(cntOnesArrWithGivenOp(arr, N));
  }
}

// This code is contributed by shikhasingrajput
```

## **java 描述语言**

```
<script>
// javascript program to implement
// the above approach

    // Function to count total number of 1s in
    // array by performing the given operations
    function cntOnesArrWithGivenOp(arr , N) {

        // Stores count of 1s in the array
        // by performing the operations
        var cntOnes = 0;

        // Update cntOnes
        cntOnes = parseInt( Math.sqrt(N));
        return cntOnes;
    }

    // Driver code

        var arr = [ 0, 0, 0, 0, 0 ];
        var N = arr.length;
        document.write(cntOnesArrWithGivenOp(arr, N));

// This code contributed by Rajput-Ji
</script>
```

****Output:** 

```
2
```** 

*****时间复杂度:**O(log<sub>2</sub>(N))*
***辅助空间:** O(1)***
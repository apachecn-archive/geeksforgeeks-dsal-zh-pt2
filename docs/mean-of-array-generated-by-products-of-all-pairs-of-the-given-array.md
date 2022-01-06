# 给定数组的所有对的乘积生成的数组的平均值

> 原文:[https://www . geeksforgeeks . org/给定数组的所有对的乘积生成的数组平均值/](https://www.geeksforgeeks.org/mean-of-array-generated-by-products-of-all-pairs-of-the-given-array/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，任务是找出由给定数组的无序对的乘积形成的数组的[平均值。](https://www.geeksforgeeks.org/program-for-mean-and-median-of-an-unsorted-array/)

**示例:**

> **输入:** arr[] = {2，5，7}
> **输出:** 19.67
> **说明:**
> 数组 arr[]的无序对的乘积为 2 * 5 = 10，2 * 7 = 14，5 * 7 = 35。
> 因此，成对乘积的结果数组是{10，14，35}。
> 成对乘积阵列的平均值为 59/3 = 19.67
> 
> **输入:** arr[] = {1，2，4，8}
> **输出:** 11.67
> **解释:**
> *数组 arr[]无序对的乘积为 1 * 2 = 2，1 * 4 = 4，1 * 8 = 8，2 * 4 = 8，2 * 8 = 16，4 * 8 = 32。*
> *因此，成对乘积的结果数组是{2，4，8，8，16，32}。*
> *对积数组的平均值为 70/6，即 11.67*

**天真法:**解决问题最简单的方法是[生成所有可能的数组对](https://www.geeksforgeeks.org/find-all-pairs-possible-from-the-given-array/) **pairProductArray[]** 即数组无序对的乘积形成的数组 **arr[]** 。然后，找到 **pairProductArray[]** 的[均值。按照以下步骤解决问题:](https://www.geeksforgeeks.org/program-average-array-iterative-recursive/)

*   生成所有可能的数组对 **arr[]** ，并将它们的产品存储在 **pairProductArray[]** 中。
*   初始化一个变量 **sum** 来存储**pairProductArray【】**的元素之和。
*   将变量**和**除以 pairProductArray【】的**大小，得到所需的平均值。**
*   最后，打印**和**的值作为合成平均值。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the mean of pair
// product array of arr[]
float pairProductMean(int arr[], int N)
{
    // Store product of pairs
    vector<int> pairArray;

    // Generate all unordered pairs
    for (int i = 0; i < N; i++) {
        for (int j = i + 1; j < N; j++) {

            int pairProduct
                = arr[i] * arr[j];

            // Store product of pairs
            pairArray.push_back(pairProduct);
        }
    }

    // Size of pairArray
    int length = pairArray.size();

    // Store sum of pairArray
    float sum = 0;
    for (int i = 0; i < length; i++)
        sum += pairArray[i];

    // Stores the mean of pairArray[]
    float mean;

    // Find mean of pairArray[]
    if (length != 0)
        mean = sum / length;
    else
        mean = 0;

    // Return the resultant mean
    return mean;
}

// Driver Code
int main()
{
    // Given array arr[]
    int arr[] = { 1, 2, 4, 8 };

    int N = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    cout << fixed << setprecision(2)
         << pairProductMean(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the
// above approach
import java.util.*;
class GFG{

// Function to find the mean
// of pair product array of arr[]
static double  pairProductMean(int arr[],
                               int N)
{
  // Store product of pairs
  Vector<Integer> pairArray =
         new Vector<>();

  // Generate all unordered pairs
  for (int i = 0; i < N; i++)
  {
    for (int j = i + 1; j < N; j++)
    {
      int pairProduct = arr[i] *
                        arr[j];

      // Store product of pairs
      pairArray.add(pairProduct);
    }
  }

  // Size of pairArray
  int length = pairArray.size();

  // Store sum of pairArray
  float sum = 0;
  for (int i = 0; i < length; i++)
    sum += pairArray.get(i);

  // Stores the mean of
  // pairArray[]
  float mean;

  // Find mean of pairArray[]
  if (length != 0)
    mean = sum / length;
  else
    mean = 0;

  // Return the resultant mean
  return mean;
}

// Driver Code
public static void main(String[] args)
{
  // Given array arr[]
  int arr[] = {1, 2, 4, 8};

  int N = arr.length;

  // Function Call

  System.out.format("%.2f",
                    pairProductMean(arr, N));
}
}

// This code is contributed by shikhasingrajput
```

## 蟒蛇 3

```
# Python3 program for the
# above approach

# Function to find the mean
# of pair product array of arr
def pairProductMean(arr, N):

    # Store product of pairs
    pairArray = [];

    # Generate all unordered
    # pairs
    for i in range(N):
        for j in range(i + 1, N):
            pairProduct = arr[i] * arr[j];

            # Store product of pairs
            pairArray.append(pairProduct);

    # Size of pairArray
    length = len(pairArray);

    # Store sum of pairArray
    sum = 0;
    for i in range(length):
        sum += pairArray[i];

    # Stores the mean of
    # pairArray
    mean = 0;

    # Find mean of pairArray
    if (length != 0):
        mean = sum / length;
    else:
        mean = 0;

    # Return the resultant
    # mean
    return mean;

# Driver Code
if __name__ == '__main__':

    # Given array arr
    arr = [1, 2, 4, 8];

    N = len(arr);

    # Function Call
    print("{0:.2f}".format(
            pairProductMean(arr, N)))

# This code is contributed by Rajput-Ji
```

## C#

```
// C# program for the
// above approach
using System;
using System.Collections.Generic;
class GFG{

// Function to find the mean
// of pair product array of []arr
static double  pairProductMean(int []arr,
                               int N)
{
  // Store product of pairs
  List<int> pairArray =
         new List<int>();

  // Generate all unordered pairs
  for (int i = 0; i < N; i++)
  {
    for (int j = i + 1; j < N; j++)
    {
      int pairProduct = arr[i] *
                        arr[j];

      // Store product of pairs
      pairArray.Add(pairProduct);
    }
  }

  // Size of pairArray
  int length = pairArray.Count;

  // Store sum of pairArray
  float sum = 0;
  for (int i = 0; i < length; i++)
    sum += pairArray[i];

  // Stores the mean of
  // pairArray[]
  float mean;

  // Find mean of pairArray[]
  if (length != 0)
    mean = sum / length;
  else
    mean = 0;

  // Return the resultant mean
  return mean;
}

// Driver Code
public static void Main(String[] args)
{
  // Given array []arr
  int []arr = {1, 2, 4, 8};

  int N = arr.Length;

  // Function Call
  Console.WriteLine("{0:F2}",
                    pairProductMean(arr,
                                    N));
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript program for the
// above approach

    // Function to find the mean
    // of pair product array of arr
    function pairProductMean(arr , N)
    {
        // Store product of pairs
        var pairArray = [];

        // Generate all unordered pairs
        for (i = 0; i < N; i++) {
            for (j = i + 1; j < N; j++) {
                var pairProduct = arr[i] * arr[j];

                // Store product of pairs
                pairArray.push(pairProduct);
            }
        }

        // Size of pairArray
        var length = pairArray.length;

        // Store sum of pairArray
        var sum = 0;
        for (i = 0; i < length; i++)
            sum += pairArray[i];

        // Stores the mean of
        // pairArray
        var mean;

        // Find mean of pairArray
        if (length != 0)
            mean = sum / length;
        else
            mean = 0;

        // Return the resultant mean
        return mean;
    }

    // Driver Code

        // Given array arr
        var arr = [ 1, 2, 4, 8 ];

        var N = arr.length;

        // Function Call

        document.write(pairProductMean(arr, N).toFixed(2));

// This code contributed by gauravrajput1

</script>
```

**Output**

```
11.67
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(N <sup>2</sup> )*

**有效方法:**想法是利用每个元素 **arr[i]** 与位于元素 **arr[i]** 右侧的每个元素 **arr[j]** 相乘的事实，更正式地说，位于索引 **i** 处的元素与位于索引 **j** 处的所有元素相乘，使得 **j > i** 。按照以下步骤解决问题:

*   为给定数组 **arr[]** 创建一个[后缀和数组](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/) **后缀和[]** 。
*   初始化变量 **res** 以存储数组 **arr[]** 的乘积对的[和。](https://www.geeksforgeeks.org/sum-product-pairs-array-elements/)
*   迭代数组 **arr[]** ，对于每个位置 **i** 用**arr[I]*后缀 SumArray[i+1]** 递增 **res** 。
*   将变量 **res** 除以**N *(N–1)/2**，这是可能产品的数量。
*   最后，打印 **res** 的值作为合成平均值。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the mean of pair
// product array of arr[]
float pairProductMean(int arr[], int N)
{
    // Initializing suffix sum array
    int suffixSumArray[N];
    suffixSumArray[N - 1] = arr[N - 1];

    // Build suffix sum array
    for (int i = N - 2; i >= 0; i--) {
        suffixSumArray[i]
            = suffixSumArray[i + 1]
              + arr[i];
    }

    // Size of pairProductArray
    int length = (N * (N - 1)) / 2;

    // Stores sum of pairProductArray
    float res = 0;

    for (int i = 0; i < N - 1; i++) {
        res += arr[i]
               * suffixSumArray[i + 1];
    }

    // Store the mean
    float mean;

    // Find mean of pairProductArray
    if (length != 0)
        mean = res / length;
    else
        mean = 0;

    // Return the resultant mean
    return mean;
}

// Driver Code
int main()
{
    // Given array arr[]
    int arr[] = { 1, 2, 4, 8 };
    int N = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    cout << fixed << setprecision(2)
         << pairProductMean(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.util.*;

class GFG{

// Function to find the mean of pair
// product array of arr[]
static float pairProductMean(int arr[], int N)
{

    // Initializing suffix sum array
    int suffixSumArray[] = new int[N];
    suffixSumArray[N - 1] = arr[N - 1];

    // Build suffix sum array
    for(int i = N - 2; i >= 0; i--)
    {
        suffixSumArray[i] = suffixSumArray[i + 1] +
                                       arr[i];
    }

    // Size of pairProductArray
    int length = (N * (N - 1)) / 2;

    // Stores sum of pairProductArray
    float res = 0;

    for(int i = 0; i < N - 1; i++)
    {
        res += arr[i] *
               suffixSumArray[i + 1];
    }

    // Store the mean
    float mean;

    // Find mean of pairProductArray
    if (length != 0)
        mean = res / length;
    else
        mean = 0;

    // Return the resultant mean
    return mean;
}

// Driver Code
public static void main (String[] args)
{

    // Given array arr[]
    int arr[] = { 1, 2, 4, 8 };
    int N = arr.length;

    // Function call
    System.out.format("%.2f",
                      pairProductMean(arr, N));
}
}

// This code is contributed by sanjoy_62
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the mean of pair
# product array of arr[]
def pairProductMean(arr, N):

    # Initializing suffix sum array
    suffixSumArray = [0] * N
    suffixSumArray[N - 1] = arr[N - 1]

    # Build suffix sum array
    for i in range(N - 2, -1, -1):
        suffixSumArray[i] = suffixSumArray[i + 1] + arr[i]

    # Size of pairProductArray
    length = (N * (N - 1)) // 2

    # Stores sum of pairProductArray
    res = 0

    for i in range(N - 1):
        res += arr[i] * suffixSumArray[i + 1]

    # Store the mean
    mean = 0

    # Find mean of pairProductArray
    if (length != 0):
        mean = res / length
    else:
        mean = 0

    # Return the resultant mean
    return mean

# Driver Code
if __name__ == '__main__':

    # Given array arr[]
    arr = [ 1, 2, 4, 8 ]
    N = len(arr)

    # Function Call
    print(round(pairProductMean(arr, N), 2))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to find the mean of pair
// product array of arr[]
static double pairProductMean(int[] arr, int N)
{

    // Initializing suffix sum array
    int[] suffixSumArray = new int[N];
    suffixSumArray[N - 1] = arr[N - 1];

    // Build suffix sum array
    for(int i = N - 2; i >= 0; i--)
    {
        suffixSumArray[i] = suffixSumArray[i + 1] +
                                       arr[i];
    }

    // Size of pairProductArray
    int length = (N * (N - 1)) / 2;

    // Stores sum of pairProductArray
    double res = 0;

    for(int i = 0; i < N - 1; i++)
    {
        res += arr[i] *
               suffixSumArray[i + 1];
    }

    // Store the mean
    double mean;

    // Find mean of pairProductArray
    if (length != 0)
        mean = res / length;
    else
        mean = 0;

    // Return the resultant mean
    return mean;
}

// Driver code
public static void Main()
{

    // Given array arr[]
    int[] arr = { 1, 2, 4, 8 };
    int N = arr.Length;

    // Function call
    Console.WriteLine(string.Format("{0:0.00}",
                      pairProductMean(arr, N)));
}
}

// This code is contributed by code_hunt
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to find the mean of pair
// product array of arr[]
function pairProductMean(arr, N)
{
    // Initializing suffix sum array
    var suffixSumArray = Array(N);
    suffixSumArray[N - 1] = arr[N - 1];

    // Build suffix sum array
    for (var i = N - 2; i >= 0; i--) {
        suffixSumArray[i]
            = suffixSumArray[i + 1]
              + arr[i];
    }

    // Size of pairProductArray
    var length = (N * (N - 1)) / 2;

    // Stores sum of pairProductArray
    var res = 0;

    for (var i = 0; i < N - 1; i++) {
        res += arr[i]
               * suffixSumArray[i + 1];
    }

    // Store the mean
    var mean;

    // Find mean of pairProductArray
    if (length != 0)
        mean = res / length;
    else
        mean = 0;

    // Return the resultant mean
    return mean;
}

// Driver Code
// Given array arr[]
var arr = [ 1, 2, 4, 8 ];
var N = arr.length;
// Function Call
document.write( pairProductMean(arr, N).toFixed(2));

</script>
```

**Output**

```
11.67
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)
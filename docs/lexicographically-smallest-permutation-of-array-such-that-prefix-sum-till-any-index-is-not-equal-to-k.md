# 数组的字典最小排列，直到任何索引的前缀和不等于 K

> 原文:[https://www . geeksforgeeks . org/按字典顺序排列的最小数组排列-这样-前缀-和-直到-任意索引-不等于-k/](https://www.geeksforgeeks.org/lexicographically-smallest-permutation-of-array-such-that-prefix-sum-till-any-index-is-not-equal-to-k/)

给定一个由 **N** 个不同正整数和一个整数 **K、**组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]、**，任务是[找到数组](https://www.geeksforgeeks.org/lexicographically-smallest-permutation-distinct-elements-using-minimum-replacements/)的字典最小排列，使得输出数组的任何前缀的元素之和不等于 **K** 。如果不存在这样的排列，则打印“ **-1** ”。否则，打印输出数组。

**示例:**

> **输入:** arr[] = {2，6，4，5，3，1}，K = 15
> **输出:** 1 2 3 4 6 5
> **解释:**
> 给定数组的字典最小排列是，{1，2，3，4，6，5}没有等于 15 的前缀和。
> 
> **输入:** arr[]={3，1，4，6}，K = 12
> **输出:** 1 3 4 6
> **解释:**
> 给定数组的字典最小排列是，{1，3，4，6}没有等于 12 的前缀和。

**处理方法:**首先[按升序](https://www.geeksforgeeks.org/c-program-to-sort-an-array-in-ascending-order/)对数组进行排序，然后将和等于 **K** 的前缀的最后一个元素与下一个元素进行交换，就可以解决这个问题。按照以下步骤解决此问题:

*   如果数组的[和等于 **K** ，那么打印“ **-1** ”，因为不可能找到满足条件的数组的任何排列。](https://www.geeksforgeeks.org/program-find-sum-elements-given-array/)
*   [按升序对数组进行排序。](https://www.geeksforgeeks.org/c-program-to-sort-an-array-in-ascending-order/)
*   初始化一个变量，比如说**假定**为 **0** 来存储前缀的总和。
*   [使用变量 **i** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，N-2】**，并执行以下步骤:
    *   通过**arr【I】**增加**设定**。
    *   如果**假定**等于 **K，**则[交换](https://www.geeksforgeeks.org/swap-two-variables-in-one-line-in-c-c-python-php-and-java/)**arr【I】**和**arr【I+1】**，然后[断开](https://www.geeksforgeeks.org/break-statement-cc/)。
*   最后，完成以上步骤后，打印数组的元素， **arr[]** 。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the output array
// satisfying given conditions
void findpermutation(int arr[], int N, int K)
{
    int sum = 0;

    // Traverse the array arr[]
    for (int i = 0; i < N; i++) {
        sum = sum + arr[i];
    }

    // If sum is equal to K
    if (sum == K) {
        cout << -1 << endl;
    }
    else {
        // Sort array in ascending order
        sort(arr, arr + N);

        // Stores the sum of a prefix
        int preSum = 0;

        // Traverse the array arr[]
        for (int i = 0; i < N; i++) {
            // Update the preSum
            preSum = preSum + arr[i];
            // If preSum is equal to K
            if (preSum == K) {
                // Swap
                swap(arr[i], arr[i + 1]);
                break;
            }
        }

        // Print the array arr[]
        for (int i = 0; i < N; i++) {
            cout << arr[i] << " ";
        }

        cout << endl;
    }
}

// Driver code
int main()
{
    int arr[] = { 2, 6, 4, 5, 3, 1 };
    int N = sizeof(arr) / sizeof(arr[0]);
    int K = 15;

    findpermutation(arr, N, K);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to find the output array
// satisfying given conditions
static void findpermutation(int arr[], int N, int K)
{
    int sum = 0;

    // Traverse the array arr[]
    for(int i = 0; i < N; i++)
    {
        sum = sum + arr[i];
    }

    // If sum is equal to K
    if (sum == K)
    {
        System.out.println(-1);
    }
    else
    {

        // Sort array in ascending order
        Arrays.sort(arr);

        // Stores the sum of a prefix
        int preSum = 0;

        // Traverse the array arr[]
        for(int i = 0; i < N; i++)
        {

            // Update the preSum
            preSum = preSum + arr[i];

            // If preSum is equal to K
            if (preSum == K)
            {

                // Swap
                swap(arr, i, i + 1);
                break;
            }
        }

        // Print the array arr[]
        for(int i = 0; i < N; i++)
        {
            System.out.print(arr[i] + " ");
        }
        System.out.println( );
    }
}

static int[] swap(int []arr, int i, int j)
{
    int temp = arr[i];
    arr[i] = arr[j];
    arr[j] = temp;
    return arr;
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 2, 6, 4, 5, 3, 1 };
    int N = arr.length;
    int K = 15;

    findpermutation(arr, N, K);
}
}

// This code is contributed by shivanisinghss2110
```

## 蟒蛇 3

```
# Pyhton3 program for the above approach

# Function to find the output array
# satisfying given conditions
def findpermutation(arr, N, K):

    sum = 0

    # Traverse the array arr[]
    for i in range(0, N):
        sum = sum + arr[i]

    # If sum is equal to K
    if (sum == K):
        print("-1")
    else:

        # Sort array in ascending order
        arr.sort()

        # Stores the sum of a prefix
        preSum = 0

        # Traverse the array arr[]
        for i in range(0, N):

            # Update the preSum
            preSum = preSum + arr[i]

            # If preSum is equal to K
            if (preSum == K):

                #  Swap
                temp = arr[i]
                arr[i] = arr[i + 1]
                arr[i + 1] = temp

        # Print the array arr[]
        for i in range(0, N):
            print(arr[i], end = " ")

# Driver code
arr = [ 2, 6, 4, 5, 3, 1 ]
N = len(arr)
K = 15

findpermutation(arr, N, K)

# This code is contributed by amreshkumar3
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to find the output array
// satisfying given conditions
static void findpermutation(int []arr, int N, int K)
{
    int sum = 0;

    // Traverse the array arr[]
    for(int i = 0; i < N; i++)
    {
        sum = sum + arr[i];
    }

    // If sum is equal to K
    if (sum == K)
    {
         Console.WriteLine(-1);
    }
    else
    {

        // Sort array in ascending order
        Array.Sort(arr);

        // Stores the sum of a prefix
        int preSum = 0;

        // Traverse the array arr[]
        for(int i = 0; i < N; i++)
        {

            // Update the preSum
            preSum = preSum + arr[i];

            // If preSum is equal to K
            if (preSum == K)
            {

                // Swap
                swap(arr, i, i + 1);
                break;
            }
        }

        // Print the array arr[]
        for(int i = 0; i < N; i++)
        {
             Console.WriteLine(arr[i] + " ");
        }
         Console.WriteLine( );
    }
}

static int[] swap(int []arr, int i, int j)
{
    int temp = arr[i];
    arr[i] = arr[j];
    arr[j] = temp;
    return arr;
}

// Driver code
static void Main()
{
    int []arr= { 2, 6, 4, 5, 3, 1 };
    int N = arr.Length;
    int K = 15;

    findpermutation(arr, N, K);
}
}

// This code is contributed by SoumikMondal
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to find the output array
// satisfying given conditions
function findpermutation(arr, N, K)
{
    var sum = 0;

    var i;
    // Traverse the array arr[]
    for (i = 0; i < N; i++) {
        sum = sum + arr[i];
    }

    // If sum is equal to K
    if (sum == K) {
        document.write(-1);
     }
    else {
        // Sort array in ascending order
        arr = arr.sort(function(a, b) {
          return a - b;
         });

        // Stores the sum of a prefix
        var preSum = 0;

        // Traverse the array arr[]
        for (i = 0; i < N; i++) {
            // Update the preSum
            preSum = preSum + arr[i];
            // If preSum is equal to K
            if (preSum == K) {
                // Swap
                var temp  = arr[i];
                arr[i] = arr[i+1];
                arr[i+1] = temp;
                break;
            }
        }

        // Print the array arr[]
        for (i = 0; i < N; i++) {
             document.write(arr[i] + " ");
        }

        document.write("<br>")
    }
}

// Driver code
    arr = [2, 6, 4, 5, 3, 1];
    N = arr.length;
    K = 15;

    findpermutation(arr, N, K);

</script>
```

**Output**

```
1 2 3 4 6 5 
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)
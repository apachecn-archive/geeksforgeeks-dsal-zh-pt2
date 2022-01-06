# 通过最多 K 次重复将数组元素除以 2 来最大化数组中 1 的数量

> 原文:[https://www . geeksforgeeks . org/按最多 k 次 2 次重复划分数组元素来最大化数组中的 1 个数/](https://www.geeksforgeeks.org/maximize-count-of-1s-in-an-array-by-repeated-division-of-array-elements-by-2-at-most-k-times/)

给定一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**和一个整数 **K** ，通过将任意元素最多重复除以 2**K**次，找到可以减少到 **1** 的最大数组元素数的任务。
***注:**为奇数阵元，取其*[*ceil*](https://www.geeksforgeeks.org/ceil-floor-functions-cpp/)*值之除。*

**示例:**

> ***输入:** arr[] = {5，8，4，7}，K = 5*
> ***输出:** 2*
> ***说明:***
> *5 需要 3 次运算(5→3→2→1)。*
> 8 需要 3 次操作(8 *→4→2→1* )。
> 4 需要 2 次操作( *4→2→1* )。
> 7 需要 3 次运算(7 *→4→2→1* )
> 因此，在 5 次运算中，最大可化为 1 的数组元素个数为 2，可以是(4，5)、(4，8)也可以是(4，7)。
> 
> ***输入:*** *arr[] = {5，8，5，7}，K = 5*
> *输出:* 1

**方法:**为了最大化元素的数量，想法是[按照升序](https://www.geeksforgeeks.org/c-program-to-sort-an-array-in-ascending-order/)对数组进行排序，并从第一个索引开始减少元素，并按照减少第 **i <sup>th</sup>** 元素所需的操作数量减少 **K** 。按照以下步骤解决问题:

*   初始化一个变量，比如 **cnt** ，来存储所需的元素数量。
*   [按递增顺序排列数组**arr[]**](https://www.geeksforgeeks.org/c-program-to-sort-an-array-in-ascending-order/)。
*   [使用变量 **i** 遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)、 **arr[]** ，并执行以下步骤:
    *   存储将 **arr[i]** 减少到 **1** 所需的操作数为**opr = ceil(**[**log2(arr[I])**](https://www.geeksforgeeks.org/log2-function-in-c-with-examples/)**)**。
    *   将 **K** 减少 **opr** 。
    *   如果 **K** 的值小于 **0** ，[脱离回路](https://www.geeksforgeeks.org/break-statement-cc/)。否则，将 **cnt** 增加 **1** 。
*   完成上述步骤后，打印 **cnt** 的值作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to count the maximum number of
// array elements that can be reduced to 1
// by repeatedly dividing array elements by 2
void findMaxNumbers(int arr[], int n, int k)
{
    // Sort the array in ascending order
    sort(arr, arr + n);

    // Store the count of array elements
    int cnt = 0;

    // Traverse the array
    for (int i = 0; i < n; i++) {

        // Store the number of operations
        // required to reduce arr[i] to 1
        int opr = ceil(log2(arr[i]));

        // Decrement k by opr
        k -= opr;

        // If k becomes less than 0,
        // then break out of the loop
        if (k < 0) {
            break;
        }

        // Increment cnt by 1
        cnt++;
    }

    // Print the answer
    cout << cnt;
}

// Driver Code
int main()
{
    int arr[] = { 5, 8, 4, 7 };
    int N = sizeof(arr) / sizeof(arr[0]);
    int K = 5;

    findMaxNumbers(arr, N, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
public class GFG
{

// Function to count the maximum number of
// array elements that can be reduced to 1
// by repeatedly dividing array elements by 2
static void findMaxNumbers(int arr[], int n, int k)
{

    // Sort the array in ascending order
    Arrays.sort(arr);

    // Store the count of array elements
    int cnt = 0;

    // Traverse the array
    for (int i = 0; i < n; i++)
    {

        // Store the number of operations
        // required to reduce arr[i] to 1
        int opr = (int)Math.ceil((Math.log(arr[i]) / Math.log(2)));

        // Decrement k by opr
        k -= opr;

        // If k becomes less than 0,
        // then break out of the loop
        if (k < 0) {
            break;
        }

        // Increment cnt by 1
        cnt++;
    }

    // Print the answer
    System.out.println(cnt);
}

// Driver Code
public static void main(String args[])
{
    int arr[] = { 5, 8, 4, 7 };
    int N = arr.length;
    int K = 5;
    findMaxNumbers(arr, N, K);
}
}

// This code is contributed by jana_sayantan.
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach
import math

# Function to count the maximum number of
# array elements that can be reduced to 1
# by repeatedly dividing array elements by 2
def findMaxNumbers(arr, n, k) :

    # Sort the array in ascending order
    arr.sort()

    # Store the count of array elements
    cnt = 0

    # Traverse the array
    for i in range(n):

        # Store the number of operations
        # required to reduce arr[i] to 1
        opr = math.ceil(math.log2(arr[i]))

        # Decrement k by opr
        k -= opr

        # If k becomes less than 0,
        # then break out of the loop
        if (k < 0) :
            break

        # Increment cnt by 1
        cnt += 1

    # Print the answer
    print(cnt)

# Driver Code
arr = [ 5, 8, 4, 7 ]
N = len(arr)
K = 5

findMaxNumbers(arr, N, K)

# This code is contributed by splevel62.
```

## C#

```
// C# program for the above approach
using System;
public class GFG
{

// Function to count the maximum number of
// array elements that can be reduced to 1
// by repeatedly dividing array elements by 2
static void findMaxNumbers(int[] arr, int n, int k)
{

    // Sort the array in ascending order
    Array.Sort(arr);

    // Store the count of array elements
    int cnt = 0;

    // Traverse the array
    for (int i = 0; i < n; i++)
    {

        // Store the number of operations
        // required to reduce arr[i] to 1
        int opr = (int)Math.Ceiling((Math.Log(arr[i]) / Math.Log(2)));

        // Decrement k by opr
        k -= opr;

        // If k becomes less than 0,
        // then break out of the loop
        if (k < 0) {
            break;
        }

        // Increment cnt by 1
        cnt++;
    }

    // Print the answer
    Console.Write(cnt);
}

// Driver Code
public static void Main(String[] args)
{
    int[] arr = { 5, 8, 4, 7 };
    int N = arr.Length;
    int K = 5;
    findMaxNumbers(arr, N, K);
}
}

// This code is contributed by susmitakundugoaldanga.
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to count the maximum number of
// array elements that can be reduced to 1
// by repeatedly dividing array elements by 2
function findMaxNumbers( arr, n, k)
{
    // Sort the array in ascending order
    arr.sort();

    // Store the count of array elements
    let cnt = 0;

    // Traverse the array
    for (let i = 0; i < n; i++) {

        // Store the number of operations
        // required to reduce arr[i] to 1
        let opr = Math.ceil(Math.log2(arr[i]));

        // Decrement k by opr
        k -= opr;

        // If k becomes less than 0,
        // then break out of the loop
        if (k < 0) {
            break;
        }

        // Increment cnt by 1
        cnt++;
    }

    // Print the answer
    document.write(cnt);
}

// Driver Code

let arr = [ 5, 8, 4, 7 ];
let N = arr.length;
let K = 5;

findMaxNumbers(arr, N, K);

</script>
```

**Output:** 

```
2
```

***时间复杂度:** O(N*log N)*
***辅助空间:** O(1)*
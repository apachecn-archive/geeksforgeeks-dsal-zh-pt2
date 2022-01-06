# 最大化元素最小且子集大小至少为 X 的乘积的子集的数量

> 原文:[https://www . geeksforgeeks . org/最大化子集计数-具有最小元素乘积和最小大小的子集-至少-x/](https://www.geeksforgeeks.org/maximize-count-of-subsets-having-product-of-smallest-element-and-size-of-the-subset-at-least-x/)

给定一个由 **N** 个整数和一个整数 **X** 组成的数组 **arr[]** ，任务是计算给定数组中可能的子集的最大数量，该数组具有

> 子集的最小元素*子集的大小≥ X

**示例:**

> **输入:** arr[] = {7，11，2，9，5}，X = 10
> **输出:** 2
> **解释:**
> 可能的解决方案之一是{7，9}和{11，5}。
> 在子集{7，9}中最小的元素(= 7)，子集的大小(= 2)。
> 因此，子集的最小元素与子集大小的乘积等于 14 ( > 10)。
> 在子集{11，5}中最小的元素(= 5)，子集的大小(= 2)。
> 因此，子集的最小元素*子集大小的乘积等于 10
> 因此，所需的输出为 2
> 
> **输入:** arr[] = {2，4，2，3}，X = 8
> T3】输出: 1

**进场:**使用[贪婪进场](https://www.geeksforgeeks.org/greedy-algorithms/)可以解决问题。其思想是[按照降序](https://www.geeksforgeeks.org/how-to-sort-an-array-in-descending-order-using-stl-in-c/)对数组进行排序，然后逐个遍历元素来检查所需的条件。
按照以下步骤解决问题。

1.  [按降序排列数组](https://www.geeksforgeeks.org/arrays-sort-in-java-with-examples/)。
2.  初始化变量**计数器**、 **sz** 来存储可能子集的计数和当前子集的大小。
3.  迭代给定的数组，检查 **arr[i] * sz ≥ X** 是否存在。如果发现为真，重置 **sz** 并将**计数器**增加 1。
4.  最后，完成数组遍历后，打印**计数器**作为所需答案。

下面是上述方法的实现:

## C++

```
// C++ Program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Comparator function to return
// the greater of two numbers
bool comp(int a, int b)
{
    return a > b;
}

// Function to return the maximum count
// of subsets possible which
// satisfy the above condition
int maxSubset(int arr[], int N, int X)
{

    // Sort the array in
    // descending order
    sort(arr, arr + N, comp);

    // Stores the count of subsets
    int counter = 0;

    // Stores the size of
    // the current subset
    int sz = 0;

    for (int i = 0; i < N; i++)
    {
        sz++;

        // Check for the necessary
        // conditions
        if (arr[i] * sz >= X) {
            counter++;
            sz = 0;
        }
    }
    return counter;
}

// Driver Code
int main()
{
    int arr[] = { 7, 11, 2, 9, 5 };
    int N = sizeof(arr) / sizeof(arr[0]);
    int X = 10;
    cout << maxSubset(arr, N, X);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;

class GFG{

// Function to return the maximum count
// of subsets possible which
// satisfy the above condition
static int maxSubset(Integer arr[], int N,
                                    int X)
{

    // Sort the array in
    // descending order
    Arrays.sort(arr, Collections.reverseOrder());

    // Stores the count of subsets
    int counter = 0;

    // Stores the size of
    // the current subset
    int sz = 0;

    for(int i = 0; i < N; i++)
    {
        sz++;

        // Check for the necessary
        // conditions
        if (arr[i] * sz >= X)
        {
            counter++;
            sz = 0;
        }
    }
    return counter;
}

// Driver Code
public static void main(String[] args)
{
    Integer arr[] = { 7, 11, 2, 9, 5 };
    int N = arr.length;
    int X = 10;

    System.out.print(maxSubset(arr, N, X));
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 Program to implement
# the above approach

# Function to return the maximum count
# of subsets possible which
# satisfy the above condition
def maxSubset(arr, N, X):

    # Sort the array in
    # descending order
    arr.sort(reverse = True)

    # Stores the count of subsets
    counter = 0

    # Stores the size of
    # the current subset
    sz = 0

    for i in range(N):
        sz += 1

        # Check for the necessary
        # conditions
        if(arr[i] * sz >= X):
            counter += 1
            sz = 0

    return counter

# Driver Code

# Given array
arr = [ 7, 11, 2, 9, 5 ]
N = len(arr)
X = 10

# Function call
print(maxSubset(arr, N, X))

# This code is contributed by Shivam Singh
```

## C#

```
// C# program to implement
// the above approach
using System;
using System.Linq;

class GFG{

// Function to return the maximum count
// of subsets possible which
// satisfy the above condition
static int maxSubset(int []arr, int N,
                                int X)
{

    // Sort the array in
    // descending order
    Array.Sort(arr);
    Array.Reverse(arr);

    // Stores the count of subsets
    int counter = 0;

    // Stores the size of
    // the current subset
    int sz = 0;

    for(int i = 0; i < N; i++)
    {
        sz++;

        // Check for the necessary
        // conditions
        if (arr[i] * sz >= X)
        {
            counter++;
            sz = 0;
        }
    }
    return counter;
}

// Driver Code
public static void Main(String[] args)
{
    int []arr = { 7, 11, 2, 9, 5 };
    int N = arr.Length;
    int X = 10;

    Console.Write(maxSubset(arr, N, X));
}
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>
// Javascript Program to implement
// the above approach

// Comparator function to return
// the greater of two numbers
function comp(a, b)
{
    return a > b;
}

// Function to return the maximum count
// of subsets possible which
// satisfy the above condition
function maxSubset(arr, N, X)
{

    // Sort the array in
    // descending order
    arr = arr.sort((a, b)=>b-a);

    // Stores the count of subsets
    let counter = 0;

    // Stores the size of
    // the current subset
    let sz = 0;

    for (let i = 0; i < N; i++)
    {
        sz++;

        // Check for the necessary
        // conditions
        if (arr[i] * sz >= X) {
            counter++;
            sz = 0;
        }
    }
    return counter;
}

// Driver Code
    let arr = [ 7, 11, 2, 9, 5 ];
    let N = arr.length;
    let X = 10;
    document.write(maxSubset(arr, N, X));

// This code is contributed by Saurabh Jaiswal
    </script>
```

**Output:** 

```
2
```

***时间复杂度:** O(NLog(N))*
***辅助空间:** O(1)*
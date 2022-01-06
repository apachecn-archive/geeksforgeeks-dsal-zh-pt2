# 通过对相邻索引重复加减 arr[I–1]–( I–1)使数组严格递增

> 原文:[https://www . geeksforgeeks . org/制作数组-通过对相邻索引重复加减 arri-1-i-1 进行严格递增/](https://www.geeksforgeeks.org/make-an-array-strictly-increasing-by-repeatedly-subtracting-and-adding-arri-1-i-1-to-adjacent-indices/)

给定一个由 **N** 正整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**，任务是检查给定数组**arr【】**是否可以严格递增，使得对于范围**【1，N–1】**中的任何索引 **i** ，如果**(arr[I–1]–(I–1))**至少为**0**，则将其添加到**如果可以使数组严格递增，则打印**是**。否则，打印**否**。**

**示例:**

> **输入:** arr[] = {1，5，2，7，6}
> **输出:**是
> **说明:**
> 考虑以下操作:
> 
> 1.  选择索引 **1** ，arr[I–1]–(I–1)的值为 1，至少为 0。将 1 加到 arr[1]并从 arr[0]中减去它，会将数组修改为{0，6，2，7，6}。
> 2.  选择索引 **2** ，arr[I–1]–(I–1)的值为 5，至少为 0。将 arr[2]加 5 并从 arr[1]中减去它，会将数组修改为{0，1，7，7，6}。
> 3.  选择索引 **3** ，arr[I–1]–(I–1)的值为 5，至少为 0。将 6 加到 arr[3]并从 arr[2]中减去它，将数组修改为{0，1，2，12，6}。
> 4.  选择索引 **4** ，arr[I–1]–(I–1)的值为 9，至少为 0。将 9 加到 arr[4]并从 arr[3]中减去，将数组修改为{0，1，2，3，15}。
> 
> 经过以上操作，数组变得严格递增。
> 
> **输入:** arr[] = {0，1，0}
> **输出:**否

**方法:**给定的问题可以用[贪婪方法](https://www.geeksforgeeks.org/greedy-algorithms/)解决。按照以下步骤解决问题

*   [在范围**【1，N–1】**内使用变量 **i** 遍历给定数组](https://www.geeksforgeeks.org/iterating-arrays-java/)，并执行以下步骤:
    *   如果**arr[I–1]**至少为**(I–1)**，则执行以下步骤:
        *   将**arr[I]–arr[I–1]**的值存储在一个变量中，比如 **P** 。
        *   将**arr[I–1]**更新为**arr[I–1]–P**。
        *   将 **arr[i]** 更新为 **arr[i] + P** 。
*   完成以上步骤后，如果[数组**arr【】**排序为](https://www.geeksforgeeks.org/program-check-array-sorted-not-iterative-recursive/)，则打印**“是”**。否则，打印**“否”**

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to check if an array
// can be made strictly increasing
void check(int arr[], int n)
{
    // Traverse the given array arr[]
    for (int i = 1; i < n; i++) {

        if (arr[i - 1] >= (i - 1)) {

            // Update the value of p,
            // arr[i], and arr[i - 1]
            int p = arr[i - 1] - (i - 1);
            arr[i] += p;
            arr[i - 1] -= p;
        }
    }

    // Traverse the given array
    for (int i = 1; i < n; i++) {

        // Check if the array arr[] is
        // strictly increasing or not
        if (arr[i] <= arr[i - 1]) {

            cout << "No";
            return;
        }
    }

    // Otherwise, array is increasing
    // order, print Yes
    cout << "Yes";
}

// Driver Code
int main()
{
    int arr[] = { 1, 5, 2, 7, 6 };
    int N = sizeof(arr) / sizeof(arr[0]);
    check(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;

class GFG{

// Function to check if an array
// can be made strictly increasing
static void check(int arr[], int n)
{

    // Traverse the given array arr[]
    for(int i = 1; i < n; i++)
    {
        if (arr[i - 1] >= (i - 1))
        {

            // Update the value of p,
            // arr[i], and arr[i - 1]
            int p = arr[i - 1] - (i - 1);
            arr[i] += p;
            arr[i - 1] -= p;
        }
    }

    // Traverse the given array
    for(int i = 1; i < n; i++)
    {

        // Check if the array arr[] is
        // strictly increasing or not
        if (arr[i] <= arr[i - 1])
        {
            System.out.println("No");
            return;
        }
    }

    // Otherwise, array is increasing
    // order, print Yes
    System.out.println("Yes");
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 1, 5, 2, 7, 6 };
    int N = arr.length;

    check(arr, N);
}
}

// This code is contributed by Dharanendra L V.
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to check if an array
# can be made strictly increasing
def check(arr, n):
    # Traverse the given array arr[]
    for i in range(1, n):

        if (arr[i - 1] >= (i - 1)):

            # Update the value of p,
            # arr[i], and arr[i - 1]
            p = arr[i - 1] - (i - 1)
            arr[i] += p
            arr[i - 1] -= p

    # Traverse the given array
    for i in range(1, n):
        # Check if the array arr[] is
        # strictly increasing or not
        if (arr[i] <= arr[i - 1]):

            print ("No")
            return

    # Otherwise, array is increasing
    # order, prYes
    print ("Yes")

# Driver Code
if __name__ == '__main__':
    arr = [1, 5, 2, 7, 6]
    N = len(arr)
    check(arr, N)

# This code is contributed by mohit kumar 29.
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to check if an array
// can be made strictly increasing
static void check(int []arr, int n)
{

    // Traverse the given array arr[]
    for(int i = 1; i < n; i++)
    {
        if (arr[i - 1] >= (i - 1))
        {

            // Update the value of p,
            // arr[i], and arr[i - 1]
            int p = arr[i - 1] - (i - 1);
            arr[i] += p;
            arr[i - 1] -= p;
        }
    }

    // Traverse the given array
    for(int i = 1; i < n; i++)
    {

        // Check if the array arr[] is
        // strictly increasing or not
        if (arr[i] <= arr[i - 1])
        {
            Console.Write("No");
            return;
        }
    }

    // Otherwise, array is increasing
    // order, print Yes
    Console.Write("Yes");
}

// Driver Code
public static void Main()
{
    int []arr = { 1, 5, 2, 7, 6 };
    int N = arr.Length;
    check(arr, N);
}
}

// This code is contributed by SURENDRA_GANGWAR.
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to check if an array
// can be made strictly increasing
function check(arr, n)
{

    // Traverse the given array arr
    for(var i = 1; i < n; i++)
    {
        if (arr[i - 1] >= (i - 1))
        {

            // Update the value of p,
            // arr[i], and arr[i - 1]
            var p = arr[i - 1] - (i - 1);
            arr[i] += p;
            arr[i - 1] -= p;
        }
    }

    // Traverse the given array
    for(var i = 1; i < n; i++)
    {

        // Check if the array arr is
        // strictly increasing or not
        if (arr[i] <= arr[i - 1])
        {
            document.write("No");
            return;
        }
    }

    // Otherwise, array is increasing
    // order, print Yes
    document.write("Yes");
}

// Driver Code
var arr = [ 1, 5, 2, 7, 6 ];
var N = arr.length;

check(arr, N);

// This code is contributed by 29AjayKumar

</script>
```

**Output:** 

```
Yes
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)
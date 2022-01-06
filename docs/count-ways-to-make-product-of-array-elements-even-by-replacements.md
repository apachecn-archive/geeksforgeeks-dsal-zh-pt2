# 计算数组元素乘积的方法，甚至通过替换

> 原文:[https://www . geeksforgeeks . org/count-制造数组元素乘积的方法-偶数替换/](https://www.geeksforgeeks.org/count-ways-to-make-product-of-array-elements-even-by-replacements/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】**，任务是计算通过多次替换数组元素使数组元素乘积相等的方法的数量。由于计数可能很大，打印计数[模 10 <sup>9</sup> +7](https://www.geeksforgeeks.org/modulo-1097-1000000007/) 。

**示例:**

> **输入:** arr[] = {1，3}
> **输出:** 3
> **解释:**
> 操作 1:用 2 替换 arr[0]。因此，arr[]修改为{2，3}。产品= 6。
> 操作 2:用 10 替换 arr[0]。因此，arr[]修改为{1，10}，乘积= 10。
> 操作 3:用 2 替换 arr[0]和 arr[1]。因此，arr[]修改为{2，2}，乘积= 4。
> 因此，存在 3 种可能的方式。
> 
> **输入:**arr[]= { 3 }
> T3】输出: 1

**进场:**思路是用[贪婪进场](https://www.geeksforgeeks.org/greedy-algorithms/)解决这个问题。
按照以下步骤解决问题:

*   为了使阵列 **的[乘积为偶数](https://www.geeksforgeeks.org/program-for-product-of-array/)**，必须至少存在一个偶数阵列元素。
*   [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)。对于每个数组元素，都会出现以下两种情况:
    *   如果数组只由一个**单个**元素组成，那么只有一个**单个**方式存在才能使数组的乘积相等。
    *   否则，**2<sup>N</sup>–1**方式。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to count ways to make
// product of given array even.
void makeProductEven(int arr[], int N)
{
    int m = 1000000007, ans = 1;

    // Calculate 2 ^ N
    for (int i = 0; i < N; i++)
    {
        ans = (ans * 2) % m;
    }

    // Print the answer
    cout << ans - 1;
}

// Driver Code
int main()
{

    // Given array
    int arr[] = { 1, 3 };

    // Size of the array
    int N = sizeof(arr) / sizeof(arr[0]);
    makeProductEven(arr, N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for above approach
/*package whatever //do not write package name here */
import java.io.*;
class GFG
{

  // Method to count ways to make
  // product of given array even.
  static void makeProductEven(int arr[], int N)
  {
    int m = 1000000007, ans = 1;

    // Calculate 2 ^ N
    for (int i = 0; i < N; i++)
    {
      ans = (ans * 2) % m;
    }

    // Print the answer
    System.out.println(ans - 1);
  }
  public static void main(String[] args)
  {

    // Given array
    int arr[] = { 1, 3 };

    // Size of the array
    int N = arr.length;
    makeProductEven(arr, N);
  }
}

// This code is contributed by shubham agrawal
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to count ways to make
# product of given array even.
def makeProductEven(arr, N) :
    m = 1000000007; ans = 1;

    # Calculate 2 ^ N
    for i in range(N) :
        ans = (ans * 2) % m;

    # Print the answer
    print(ans - 1);

# Driver Code
if __name__ == "__main__" :

    # Given array
    arr = [ 1, 3 ];

    # Size of the array
    N = len(arr);

    makeProductEven(arr, N);

    # This code is contributed by AnkThon
```

## C#

```
// C# program for above approach
/*package whatever //do not write package name here */
using System;
public class GFG
{

  // Method to count ways to make
  // product of given array even.
  static void makeProductEven(int []arr, int N)
  {
    int m = 1000000007, ans = 1;

    // Calculate 2 ^ N
    for (int i = 0; i < N; i++)
    {
      ans = (ans * 2) % m;
    }

    // Print the answer
    Console.WriteLine(ans - 1);
  }

  // Driver code
  public static void Main(String[] args)
  {

    // Given array
    int []arr = { 1, 3 };

    // Size of the array
    int N = arr.Length;
    makeProductEven(arr, N);
  }
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to count ways to make
// product of given array even.
function makeProductEven(arr, N)
{
    var m = 1000000007, ans = 1;

    // Calculate 2 ^ N
    for (var i = 0; i < N; i++)
    {
        ans = (ans * 2) % m;
    }

    // Print the answer
    document.write( ans - 1);
}

// Driver Code
// Given array
var arr = [ 1, 3 ];
// Size of the array
var N = arr.length;
makeProductEven(arr, N);

</script>
```

**Output**

```
3
```

**时间复杂度:** O(N)

**辅助空间:** O(1)
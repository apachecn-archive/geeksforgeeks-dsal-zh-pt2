# 最大化给定数组中两对之间的余数差

> 原文:[https://www . geeksforgeeks . org/maximum-余数-给定数组中两对的差值/](https://www.geeksforgeeks.org/maximize-remainder-difference-between-two-pairs-in-given-array/)

给定大小为 **N、**的[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** ，任务是找到 4 个索引 **i、j、k、l** ，使得 **0 < = i、j、k、l < N** 且**arr[I]% arr[j]–arr[k]% arr[l]**的值最大。打印最大差异。如果不存在，则打印 **-1。**

**示例:**

> **输入:** N=8，arr[] = {1，2，4，6，8，3，5，7}
> **输出:** 7
> **解释:**选择元素 1，2，7，8 和 2% 1–7% 8 给出可能的最大结果。
> 
> **输入:** N=3，arr[] = {1，50，101}
> **输出:** -1
> **解释:**既然只有 3 个元素，所以没有可能的答案。

**天真的方法:**蛮力的想法是检查所有可能的组合，然后找到最大差异。
***时间复杂度:**O(N<sup>4</sup>)*
***辅助空间:** O(1)*

**高效途径:**这个想法是基于这样的观察:在[对数组进行升序排序](https://www.geeksforgeeks.org/sort-c-stl/)时，从左侧选择第一对，即最小 2 值，从右侧选择第二对，即最大 2 值给出答案。此外， **arr[i+1]%arr[i]** 始终小于等于 **arr[i]%arr[i+1]。**所以，最小化第一对值，最大化第二对值。按照以下步骤解决问题:

*   如果阵列的[大小小于 **4、**，则返回 **-1。**](https://www.geeksforgeeks.org/arraysize-c-stl/)
*   [按升序排列数组**arr[]**](https://www.geeksforgeeks.org/sort-c-stl/)。
*   将变量**第一个**初始化为 **arr[1]%arr[0]** ，将**第二个**初始化为 **arr[N-2]%arr[N-1]。**
*   执行上述步骤后，打印**秒-先**的值作为答案。

下面是上述方法的实现。

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the required
// maximum difference
void maxProductDifference(vector<int>& arr)
{

    // Base Case
    if (arr.size() < 4) {
        cout << "-1\n";
        return;
    }

    // Sort the array
    sort(arr.begin(), arr.end());

    // First pair
    int first = arr[1] % arr[0];

    // Second pair
    int second = arr[arr.size() - 2]
                 % arr[arr.size() - 1];

    // Print the result
    cout << second - first;

    return;
}

// Driver Code
int main()
{
    vector<int> arr = { 1, 2, 4, 6, 8, 3, 5, 7 };

    maxProductDifference(arr);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.util.Arrays;

class GFG
{

    // Function to find the required
    // maximum difference
    static void maxProductDifference(int[] arr)
    {

        // Base Case
        if (arr.length < 4) {
            System.out.println("-1");
            return;
        }

        // Sort the array
        Arrays.sort(arr);

        // First pair
        int first = arr[1] % arr[0];

        // Second pair
        int second
            = arr[arr.length - 2] % arr[arr.length - 1];

        // Print the result
        System.out.println(second - first);

        return;
    }

    // Driver Code
    public static void main(String[] args)
    {
        int[] arr = { 1, 2, 4, 6, 8, 3, 5, 7 };

        maxProductDifference(arr);
    }
}

// This code is contributed by Potta Lokesh
```

## 蟒蛇 3

```
# python program for the above approach

# Function to find the required
# maximum difference

def maxProductDifference(arr):

    # Base Case
    if (len(arr) < 4):
        print("-1")
        return

        # Sort the array

    arr.sort()

    # First pair
    first = arr[1] % arr[0]

    # Second pair

    second = arr[len(arr) - 2] % arr[len(arr) - 1]

    # Print the result
    print(second - first)

# Driver Code
if __name__ == "__main__":

    arr = [1, 2, 4, 6, 8, 3, 5, 7]

    maxProductDifference(arr)

    # This code is contributed by rakeshsahni
```

## C#

```
// C# program for the above approach
using System;

public class GFG
{

    // Function to find the required
    // maximum difference
    static void maxProductDifference(int[] arr)
    {

        // Base Case
        if (arr.Length < 4) {
            Console.WriteLine("-1");
            return;
        }

        // Sort the array
        Array.Sort(arr);

        // First pair
        int first = arr[1] % arr[0];

        // Second pair
        int second
            = arr[arr.Length - 2] % arr[arr.Length - 1];

        // Print the result
        Console.WriteLine(second - first);

        return;
    }

    // Driver Code
    public static void Main(String[] args)
    {
        int[] arr = { 1, 2, 4, 6, 8, 3, 5, 7 };

        maxProductDifference(arr);
    }
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to find the required
// maximum difference
function maxProductDifference(arr)
{

  // Base Case
  if (arr.length < 4) {
    document.write("-1<br>");
    return;
  }

  // Sort the array
  arr.sort();

  // First pair
  let first = arr[1] % arr[0];

  // Second pair
  let second = arr[arr.length - 2] % arr[arr.length - 1];

  // Print the result
  document.write(second - first);

  return;
}

// Driver Code
let arr = [1, 2, 4, 6, 8, 3, 5, 7];
maxProductDifference(arr);

// This code is contributed by gfgking.
</script>
```

**Output:** 

```
7
```

***时间复杂度:** O(N*log(N))*
***辅助空间:** O(1)*
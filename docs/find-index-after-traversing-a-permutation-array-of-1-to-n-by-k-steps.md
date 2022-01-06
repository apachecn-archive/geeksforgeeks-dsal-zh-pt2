# 通过 K 步遍历 1 到 N 的排列数组后找到索引

> 原文:[https://www . geeksforgeeks . org/遍历 1 到 n 乘 k 步排列数组后查找索引/](https://www.geeksforgeeks.org/find-index-after-traversing-a-permutation-array-of-1-to-n-by-k-steps/)

给定一个整数 **K** 和一个长度为 **N** 的索引数组**arr【】**,其中包含范围为【1，N】的元素，任务是从索引 1 开始通过 **K** 步遍历数组后找到索引。
**遍历索引数组:**在遍历索引数组时，下一个要访问的索引是当前索引处的值。
**举例:**

> **输入:** arr[] = {3，2，4，1}，K = 5
> **输出:** 4
> **解释:**
> 遍历索引从索引 1 开始:
> 1 =>3 =>4 =>1 =>3 =>4
> 最后，在 K 次遍历之后，索引为 4
> **输入:** arr[] = {6，5

**方法:**问题中的关键观察是，在遍历索引数组 N 次后，它会重复自己。因此，我们可以找到![K \% N  ](img/43a65993f4494c9aa57ca77ebdd687f8.png "Rendered by QuickLaTeX.com")的值，然后在![K \% N  ](img/43a65993f4494c9aa57ca77ebdd687f8.png "Rendered by QuickLaTeX.com")遍历后最终找到索引。
以下是上述方法的实施:

## C++

```
// C++ implementation to find the
// index after traversing the index
// array K times

#include<bits/stdc++.h>
using namespace std;

// Function to find the index after
// traversing the index array K times
int findIndexAfterKTrav(vector<int> arr,
                        int n, int k){
    k = k % n;
    int indi = 1;

    // Loop to traverse the index
    // array K times
    while (k){
        indi = arr[indi-1];
        k--;
    }

    return arr[indi-1];
}

// Driver Code
int main() {
    int n = 4, k = 5;
    vector<int> arr{3, 2, 4, 1};

    // Function Call
    cout << findIndexAfterKTrav(arr, n, k);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find the
// index after traversing the index
// array K times
class GFG{

// Function to find the index after
// traversing the index array K times
public static int findIndexAfterKTrav(int[] arr,
                                      int n, int k)
{
    k = k % n;
    int indi = 1;

    // Loop to traverse the index
    // array K times
    while (k > 0)
    {
        indi = arr[indi - 1];
        k--;
    }
    return arr[indi - 1];
}

// Driver code
public static void main(String[] args)
{
    int n = 4, k = 5;
    int[] arr = { 3, 2, 4, 1 };

    // Function Call
    System.out.print(findIndexAfterKTrav(arr, n, k));
}
}

// This code is contributed by divyeshrabadiya07
```

## 蟒蛇 3

```
# Python3 implementation to find the
# index after traversing the index
# array K times

# Function to find the index after
# traversing the index array K times
def findIndexAfterKTrav(arr, n, k):

    k = k % n;
    indi = 1;

    # Loop to traverse the index
    # array K times
    while (k > 0):
        indi = arr[indi - 1];
        k -= 1;

    return arr[indi - 1];

# Driver code
if __name__ == '__main__':

    n = 4;
    k = 5;
    arr = [ 3, 2, 4, 1 ];

    # Function Call
    print(findIndexAfterKTrav(arr, n, k));

# This code is contributed by Princi Singh
```

## C#

```
// C# implementation to find the
// index after traversing the index
// array K times
using System;

class GFG{

// Function to find the index after
// traversing the index array K times
public static int findIndexAfterKTrav(int[] arr,
                                      int n, int k)
{
    k = k % n;
    int indi = 1;

    // Loop to traverse the index
    // array K times
    while (k > 0)
    {
        indi = arr[indi - 1];
        k--;
    }
    return arr[indi - 1];
}

// Driver code
public static void Main(String[] args)
{
    int n = 4, k = 5;
    int[] arr = { 3, 2, 4, 1 };

    // Function Call
    Console.Write(findIndexAfterKTrav(arr, n, k));
}
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>

// Javascript implementation to find the
// index after traversing the index
// array K times

// Function to find the index after
// traversing the index array K times
function findIndexAfterKTrav(arr, n, k)
{
    k = k % n;
    var indi = 1;

    // Loop to traverse the index
    // array K times
    while (k){
        indi = arr[indi-1];
        k--;
    }

    return arr[indi-1];
}

// Driver Code
var n = 4, k = 5;
var arr = [3, 2, 4, 1];

// Function Call
document.write( findIndexAfterKTrav(arr, n, k));

// This code is contributed by itsok.
</script>
```

**Output:** 

```
4
```
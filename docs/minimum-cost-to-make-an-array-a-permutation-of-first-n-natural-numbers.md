# 使数组成为前 N 个自然数排列的最小成本

> 原文:[https://www . geeksforgeeks . org/将第一个 n 个自然数排列成数组的最小成本/](https://www.geeksforgeeks.org/minimum-cost-to-make-an-array-a-permutation-of-first-n-natural-numbers/)

给定一个大小为 **N** 的正整数数组 **arr** ，任务是找到使这个数组成为前 N 个自然数的排列的最小代价，其中将一个元素递增或递减 1 的代价是 1。
**例:**

> **输入:** arr[] = {1，1，7，4}
> **输出:** 5
> **解释:**
> 对 1 进行一次递增运算
> 对 7 进行四次递减运算
> 结果数组= {1，2，3，4}
> **输入:** arr[] = {1，2，3，4，5}
> **输出:** 0

**进场:**

1.  按升序排列数组元素
2.  遍历排序后的数组:
    *   检查索引为(0 ≤ i < N) 的**处的元素是否等于 **i + 1** 。**
    *   如果不是，那就让它相等，并记下两者之间的差额作为这次手术的费用。
3.  遍历完成后，打印所执行操作的总成本。

以下是上述方法的实现:

## C++

```
// C++ program to calculate minimum cost
// to make an Array a permutation
// of first N natural numbers

#include <bits/stdc++.h>
using namespace std;

// Function to calculate minimum cost
// for making permutation of size N
int make_permutation(int arr[], int n)
{
    // sorting the array in ascending order
    sort(arr, arr + n);

    // To store the required answer
    int ans = 0;

    // Traverse the whole array
    for (int i = 0; i < n; i++)
        ans += abs(i + 1 - arr[i]);

    // Return the required answer
    return ans;
}

// Driver code
int main()
{
    int arr[] = { 5, 3, 8, 1, 1 };
    int n = sizeof(arr) / sizeof(arr[0]);

    // Function call
    cout << make_permutation(arr, n);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to calculate minimum cost
// to make an Array a permutation
// of first N natural numbers
import java.util.*;

class GFG{

// Function to calculate minimum cost
// for making permutation of size N
static int make_permutation(int arr[], int n)
{
    // sorting the array in ascending order
    Arrays.sort(arr);

    // To store the required answer
    int ans = 0;

    // Traverse the whole array
    for (int i = 0; i < n; i++)
        ans += Math.abs(i + 1 - arr[i]);

    // Return the required answer
    return ans;
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 5, 3, 8, 1, 1 };
    int n = arr.length;

    // Function call
    System.out.print(make_permutation(arr, n));
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program to calculate minimum cost
# to make an Array a permutation
# of first N natural numbers

# Function to calculate minimum cost
# for making permutation of size N
def make_permutation(arr,  n) :

    # sorting the array in ascending order
    arr.sort();

    # To store the required answer
    ans = 0;

    # Traverse the whole array
    for i in range(n) :
        ans += abs(i + 1 - arr[i]);

    # Return the required answer
    return ans;

# Driver code
if __name__ == "__main__" :

    arr = [ 5, 3, 8, 1, 1 ];
    n = len(arr);

    # Function call
    print(make_permutation(arr, n));

    # This code is contributed by Yash_R
```

## C#

```
// C# program to calculate minimum cost
// to make an Array a permutation
// of first N natural numbers
using System;

class GFG{

    // Function to calculate minimum cost
    // for making permutation of size N
    static int make_permutation(int []arr, int n)
    {
        // sorting the array in ascending order
        Array.Sort(arr);

        // To store the required answer
        int ans = 0;

        // Traverse the whole array
        for (int i = 0; i < n; i++)
            ans += Math.Abs(i + 1 - arr[i]);

        // Return the required answer
        return ans;
    }

    // Driver code
    public static void Main(string[] args)
    {
        int []arr = { 5, 3, 8, 1, 1 };
        int n = arr.Length;

        // Function call
        Console.WriteLine(make_permutation(arr, n));
    }
}

// This code is contributed by Yash_R
```

## java 描述语言

```
<script>
// Java Script program to calculate minimum cost
// to make an Array a permutation
// of first N natural numbers

// Function to calculate minimum cost
// for making permutation of size N
function make_permutation(arr,n)
{
    // sorting the array in ascending order
    arr.sort();

    // To store the required answer
    let ans = 0;

    // Traverse the whole array
    for (let i = 0; i < n; i++)
        ans += Math.abs(i + 1 - arr[i]);

    // Return the required answer
    return ans;
}

// Driver code

    let arr = [ 5, 3, 8, 1, 1 ];
    let n = arr.length;

    // Function call
    document.write(make_permutation(arr, n));
// contributed by sravan kumar
</script>
```

**Output:** 

```
5
```
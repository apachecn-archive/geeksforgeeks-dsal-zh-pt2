# 清空数组的最小成本，其中移除元素的成本是 2^(removed_count) * arr[i]

> 原文:[https://www . geesforgeks . org/最小成本到空数组-其中移除元素的成本是-2removed_count-arri/](https://www.geeksforgeeks.org/minimum-cost-to-empty-array-where-cost-of-removing-an-element-is-2removed_count-arri/)

给定一个数组 **arr[]，**任务是找到从数组中移除所有元素的最小成本，其中移除一个元素的成本是 **2^j * arr[i]。**这里，j 是已经移除的元素数量。

**示例:**

> **输入:** arr[] = {3，1，3，2}
> **输出:** 25
> **说明:**
> 先移除 3。成本= 2^(0)*3 = 3
> 然后移除 3。成本= 2^(1)*3 = 6
> 然后移除 2。成本= 2^(2)*2 = 8
> 最后，去掉 1。成本= 2^(3)*1 = 8
> 总成本= 3 + 6 + 8 + 8 = 25
> 
> **输入:** arr[] = {1，2}
> **输出:** 4
> **说明:**
> 先移除 2。成本= 2^(0)*2 = 2
> 然后去掉 1。成本= 2^(1)*1 = 2
> 总成本= 2 + 2 = 4

**方法:**思路是用一个[贪婪的编程范式](https://www.geeksforgeeks.org/greedy-algorithms/)来解决这个问题。
我们必须最小化表达式(2^j * arr[i])。这可以通过以下方式实现:

*   按降序排列数组。
*   将幂(2，I)与每个元素 I 相乘，从 0 开始到数组的大小。

因此，从数组中移除元素的总成本如下所示:

![\text{Total Cost = }arr[0]*2^{0} + arr[1] * 2^{1} + .... arr[n]*2^{n}  ](img/4421b304c28e84e93e5c7084065d3fa5.png "Rendered by QuickLaTeX.com")

当数组按降序排列时。

下面是上述方法的实现:

## C++

```
// C++ implementation to find the
// minimum cost of removing all
// elements from the array

#include <bits/stdc++.h>
using namespace std;

#define ll long long int
// Function to find the minimum
// cost of removing elements from
// the array
int removeElements(ll arr[], int n)
{

    // Sorting in Increasing order
    sort(arr, arr + n, greater<int>());
    ll ans = 0;

    // Loop to find the minimum
    // cost of removing elements
    for (int i = 0; i < n; i++) {
        ans += arr[i] * pow(2, i);
    }

    return ans;
}

// Driver Code
int main()
{
    int n = 4;
    ll arr[n] = { 3, 1, 2, 3 };

    // Function Call
    cout << removeElements(arr, n);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find the
// minimum cost of removing all
// elements from the array
import java.util.*;

class GFG{

// Reverse array in decreasing order
static long[] reverse(long a[])
{
    int i, n = a.length;
    long t;

    for(i = 0; i < n / 2; i++)
    {
        t = a[i];
        a[i] = a[n - i - 1];
        a[n - i - 1] = t;
    }
    return a;
}

// Function to find the minimum
// cost of removing elements from
// the array
static long removeElements(long arr[],
                           int n)
{

    // Sorting in Increasing order
    Arrays.sort(arr);
    arr = reverse(arr);

    long ans = 0;

    // Loop to find the minimum
    // cost of removing elements
    for(int i = 0; i < n; i++)
    {
        ans += arr[i] * Math.pow(2, i);
    }
    return ans;
}

// Driver Code
public static void main(String[] args)
{
    int n = 4;
    long arr[] = { 3, 1, 2, 3 };

    // Function call
    System.out.print(removeElements(arr, n));
}
}

// This code is contributed by amal kumar choubey
```

## 蟒蛇 3

```
# Python3 implementation to find the
# minimum cost of removing all
# elements from the array

# Function to find the minimum
# cost of removing elements from
# the array
def removeElements(arr, n):

    # Sorting in Increasing order
    arr.sort(reverse = True)
    ans = 0

    # Loop to find the minimum
    # cost of removing elements
    for i in range(n):
        ans += arr[i] * pow(2, i)

    return ans

# Driver Code
if __name__ == "__main__":

    n = 4
    arr = [ 3, 1, 2, 3 ]

    # Function call
    print(removeElements(arr, n))

# This code is contributed by chitranayal
```

## C#

```
// C# implementation to find the
// minimum cost of removing all
// elements from the array
using System;

class GFG{

// Reverse array in decreasing order
static long[] reverse(long []a)
{
    int i, n = a.Length;
    long t;

    for(i = 0; i < n / 2; i++)
    {
        t = a[i];
        a[i] = a[n - i - 1];
        a[n - i - 1] = t;
    }
    return a;
}

// Function to find the minimum
// cost of removing elements from
// the array
static long removeElements(long []arr,
                           int n)
{

    // Sorting in Increasing order
    Array.Sort(arr);
    arr = reverse(arr);

    long ans = 0;

    // Loop to find the minimum
    // cost of removing elements
    for(int i = 0; i < n; i++)
    {
        ans += (long)(arr[i] * Math.Pow(2, i));
    }
    return ans;
}

// Driver Code
public static void Main(String[] args)
{
    int n = 4;
    long []arr = { 3, 1, 2, 3 };

    // Function call
    Console.Write(removeElements(arr, n));
}
}

// This code is contributed by amal kumar choubey
```

## java 描述语言

```
<script>
      // JavaScript implementation to find the
      // minimum cost of removing all
      // elements from the array
      // Function to find the minimum
      // cost of removing elements from
      // the array
      function removeElements(arr, n) {
        // Sorting in Increasing order
        arr.sort((a, b) => b - a);

        var ans = 0;

        // Loop to find the minimum
        // cost of removing elements
        for (var i = 0; i < n; i++) {
          ans += arr[i] * Math.pow(2, i);
        }
        return ans;
      }

      // Driver Code
      var n = 4;
      var arr = [3, 1, 2, 3];

      // Function call
      document.write(removeElements(arr, n));
</script>
```

**Output**

```
25
```

***时间复杂度** : O(N * log N)*
***辅助空间** : O(1)*
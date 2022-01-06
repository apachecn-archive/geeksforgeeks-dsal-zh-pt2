# 将所有奇数元素变为偶数后，将差异最小化

> 原文:[https://www . geesforgeks . org/将所有奇数元素变为偶数后最小化差异/](https://www.geeksforgeeks.org/minimize-difference-after-changing-all-odd-elements-to-even/)

给定一个 **N** 正整数的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** 。我们必须对给定数组中的每个奇数元素执行一次运算，即在给定数组中将每个奇数元素乘以 2，任务是在执行给定运算后，找到数组中任意两个元素之间的[最小差](https://www.geeksforgeeks.org/find-minimum-difference-pair/)。
**举例:**

> **输入:** arr[] = {2，8，15，29，40}
> **输出:** 1
> **解释:**
> 将第三个元素 15 乘以 2，这样它将变成 30。
> 现在你有 30 和 29，所以最小差会变成 1。
> **输入:** arr[] = { 3，8，13，30，50 }
> **输出:** 2
> **解释:**
> 将 3 乘以 2，这样就变成了 6。
> 现在你有 6 和 8，所以最小差会变成 2。

**进场:**

1.  通过将给定数组中的每个奇数乘以 2，将其转换为偶数。
2.  按递增顺序对给定数组进行排序。
3.  找出上面排序的数组中任意两个连续元素之间的最小差异。
4.  上面计算的差值是执行给定操作后数组中任意两个元素之间的最小差值。

以下是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;
#define ll long long

// Function to minimize the difference
// between two elements of array
void minDiff(vector<ll> a, int n)
{

    // Find all the element which are
    // possible by multiplying
    // 2 to odd numbers
    for (int i = 0; i < n; i++) {
        if (a[i] % 2 == 1)
            a.push_back(a[i] * 2);
    }

    // Sort the array
    sort(a.begin(), a.end());

    ll mindifference = a[1] - a[0];

    // Find the minimum difference
    // Iterate and find which adjacent
    // elements have the minimum difference
    for (int i = 1; i < a.size(); i++) {

        mindifference = min(mindifference,
                            a[i] - a[i - 1]);
    }

    // Print the minimum difference
    cout << mindifference << endl;
}

// Driver Code
int main()
{
    // Given array
    vector<ll> arr = { 3, 8, 13, 30, 50 };

    int n = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    minDiff(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
class GFG{

// Function to minimize the difference
// between two elements of array
public static void minDiff(long[] a, int n)
{

    // Find all the element which are
    // possible by multiplying
    // 2 to odd numbers
    for(int i = 0; i < n; i++)
    {
       if (a[i] % 2 == 1)
           a[i] *= 2;
    }

    // Sort the array
    Arrays.sort(a);

    long mindifference = a[1] - a[0];

    // Find the minimum difference
    // Iterate and find which adjacent
    // elements have the minimum difference
    for(int i = 1; i < a.length; i++)
    {
       mindifference = Math.min(mindifference,
                                a[i] - a[i - 1]);
    }

    // Print the minimum difference
    System.out.println(mindifference);
}

// Driver Code
public static void main(String []args)
{

    // Given array
    long [] arr = { 3, 8, 13, 30, 50 };

    int n = arr.length;

    // Function call
    minDiff(arr, n);
}
}

// This code is contributed by jrishabh99
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to minimize the difference
# between two elements of array
def minDiff(a,n):

    # Find all the element which are
    # possible by multiplying
    # 2 to odd numbers
    for i in range(n):
        if (a[i] % 2 == 1):
            a.append(a[i] * 2)

    # Sort the array
    a = sorted(a)

    mindifference = a[1] - a[0]

    # Find the minimum difference
    # Iterate and find which adjacent
    # elements have the minimum difference
    for i in range(1, len(a)):

        mindifference = min(mindifference,
                            a[i] - a[i - 1])

    # Print the minimum difference
    print(mindifference)

# Driver Code
if __name__ == '__main__':
    arr = [3, 8, 13, 30, 50]

    n = len(arr)

    # Function Call
    minDiff(arr, n)

# This code is contributed by Mohit Kumar
```

## C#

```
// C# program for the above approach
using System;
class GFG{

// Function to minimize the difference
// between two elements of array
public static void minDiff(long[] a, int n)
{

    // Find all the element which are
    // possible by multiplying
    // 2 to odd numbers
    for(int i = 0; i < n; i++)
    {
        if (a[i] % 2 == 1)
            a[i] *= 2;
    }

    // Sort the array
    Array.Sort(a);

    long mindifference = a[1] - a[0];

    // Find the minimum difference
    // Iterate and find which adjacent
    // elements have the minimum difference
    for(int i = 1; i < a.Length; i++)
    {
        mindifference = Math.Min(mindifference,
                                 a[i] - a[i - 1]);
    }

    // Print the minimum difference
    Console.Write(mindifference);
}

// Driver Code
public static void Main()
{

    // Given array
    long []arr = { 3, 8, 13, 30, 50 };

    int n = arr.Length;

    // Function call
    minDiff(arr, n);
}
}

// This code is contributed by Code_Mech
```

## java 描述语言

```
<script>

// Javascript implementation of the above approach

// Function to minimize the difference
// between two elements of array
function minDiff(a, n)
{

    // Find all the element which are
    // possible by multiplying
    // 2 to odd numbers
    for(let i = 0; i < n; i++)
    {
       if (a[i] % 2 == 1)
           a[i] *= 2;
    }

    // Sort the array
    a.sort((a, b) => a - b);

    let mindifference = a[1] - a[0];

    // Find the minimum difference
    // Iterate and find which adjacent
    // elements have the minimum difference
    for(let i = 1; i < a.length; i++)
    {
       mindifference = Math.min(mindifference,
                                a[i] - a[i - 1]);
    }

    // Print the minimum difference
     document.write(mindifference);
}

  // Driver Code

    // Given array
    let arr = [ 3, 8, 13, 30, 50 ];

    let n = arr.length;

    // Function call
    minDiff(arr, n);

</script>
```

**Output:** 

```
2
```

**时间复杂度:***O(N * log<sub>2</sub>N)*
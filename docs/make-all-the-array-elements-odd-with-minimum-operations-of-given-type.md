# 用给定类型的最小运算使所有数组元素为奇数

> 原文:[https://www . geesforgeks . org/make-all-the-array-elements-奇数-具有给定类型的最小操作/](https://www.geeksforgeeks.org/make-all-the-array-elements-odd-with-minimum-operations-of-given-type/)

给定一个由偶数组成的数组 **arr[]** 。每次移动时，您可以从数组中选择任意偶数 **X** ，并将所有出现的 **X** 除以 **2** 。任务是找到所需的最小移动次数，以便数组中的所有元素都变成奇数。

**示例:**

> **输入:** arr[] = {40，6，40，20}
> **输出:** 4
> 移动 1:选择 40 并将 40 的所有出现
> 除以 2 得到{20，6，20，20}
> 移动 2:选择 20 并将 20 的所有出现
> 除以 2 得到{10，6，10，10}
> 移动 3:选择 10 并将所有出现
> 分开
> 移动 4:选择 6 除以 2 得到{5，3，5，5}。
> 
> **输入:** arr[] = {2，4，16，8}
> 输出: 4

**进场:**这个问题可以用[贪婪进场](https://www.geeksforgeeks.org/greedy-algorithms/)解决。一举一动，取阵中**剩余最大的偶数**除以 2。取最大值是因为在除以 2 之后，它有可能等于数组中的其他元素，从而最大限度地减少了总运算量。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the count of
// minimum operations required
int minOperations(int arr[], int n)
{

    // Insert all the elements in a set
    set<int> s;
    for (int i = 0; i < n; i++) {
        s.insert(arr[i]);
    }

    // To store the number of moves
    int moves = 0;

    // While the set is not empty
    while (s.empty() == 0) {

        // The last element of the set
        int z = *(s.rbegin());

        // If the number is even
        if (z % 2 == 0) {
            moves++;
            s.insert(z / 2);
        }

        // Remove the element from the set
        s.erase(z);
    }

    return moves;
}

// Driver code
int main()
{
    int arr[] = { 40, 6, 40, 20 };
    int n = sizeof(arr) / sizeof(int);

    cout << minOperations(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.io.*;
import java.util.*;

class GFG
{
    // Function to return the count of
    // minimum operations required
    static int minOperations(int arr[], int n)
    {

        // Insert all the elements in a set
        TreeSet<Integer> s = new TreeSet<Integer>();
        for (int i = 0; i < n; i++)
        {
            s.add(arr[i]);
        }

        // To store the number of moves
        int moves = 0;

        // While the set is not empty
        while (s.size() != 0)
        {

            // The last element of the set
            Integer z = s.last();

            // If the number is even
            if (z % 2 == 0)
            {
                moves++;
                s.add(z / 2);
            }

            // Remove the element from the set
            s.remove(z);
        }

        return moves;
    }

    // Driver code
    public static void main (String[] args)
    {
        int arr[] = { 40, 6, 40, 20 };
        int n = arr.length;

        System.out.println(minOperations(arr, n));

    }
}

// This code is contributed by ApurvaRaj
```

## 蟒蛇 3

```
# Python3 implementation of the approach
from collections import OrderedDict as mpp

# Function to return the count of
# minimum operations required
def minOperations(arr, n):

    # Insert all the elements in a set
    s = mpp()
    for i in range(n):
        s[arr[i]] = 1

    # To store the number of moves
    moves = 0

    # While the set is not empty
    while (len(s) > 0):

        # The last element of the set
        z = sorted(list(s.keys()))[-1]

        # If the number is even
        if (z % 2 == 0):
            moves += 1
            s[z / 2] = 1

        # Remove the element from the set
        del s[z]

    return moves

# Driver code

arr = [40, 6, 40, 20]
n = len(arr)

print(minOperations(arr, n))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;

class GFG
{
    // Function to return the count of
    // minimum operations required
    static int minOperations(int []arr, int n)
    {

        // Insert all the elements in a set
        SortedSet<int> s = new SortedSet<int>();
        for (int i = 0; i < n; i++)
        {
            s.Add(arr[i]);
        }

        // To store the number of moves
        int moves = 0;

        // While the set is not empty
        while (s.Count != 0)
        {

            // The last element of the set
            int z = s.Max;

            // If the number is even
            if (z % 2 == 0)
            {
                moves++;
                s.Add(z / 2);
            }

            // Remove the element from the set
            s.Remove(z);
        }

        return moves;
    }

    // Driver code
    public static void Main(String[] args)
    {
        int []arr = { 40, 6, 40, 20 };
        int n = arr.Length;

        Console.WriteLine(minOperations(arr, n));
    }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to find all the distinct
// remainders when n is divided by
// all the elements from
// the range [1, n + 1]
function findRemainders(n)
{

    // Set will be used to store
    // the remainders in order
    // to eliminate duplicates
    var vc = new Set();

    // Find the remainders
    for(var i = 1; i <= Math.ceil(Math.sqrt(n)); i++)
        vc.add(parseInt(n / i));
    for(var i = parseInt(n / Math.ceil(Math.sqrt(n))) - 1;
            i >= 0; i--)
        vc.add(i);

    // Print the contents of the set
    [...vc].sort((a, b) => a - b).forEach(it => {
        document.write(it + " ");
    });
}

// Driver code
var n = 5;

findRemainders(n);

// This code is contributed by famously

</script>
```

**Output:** 

```
4
```
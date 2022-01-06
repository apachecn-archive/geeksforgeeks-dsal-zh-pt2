# 使任意两个数组元素相等的最小按位异或运算

> 原文:[https://www . geeksforgeeks . org/最小位异或运算使任意两个数组元素相等/](https://www.geeksforgeeks.org/minimum-bitwise-xor-operations-to-make-any-two-array-elements-equal/)

给定大小为 **N** 的整数数组 arr[]和一个整数 **K** 。可以在任意数组元素和 **K** 之间执行任意次数的按位异或运算。任务是打印使数组的任意两个元素相等所需的最小操作数。如果在执行上述操作后不可能使数组的任何两个元素相等，则 print -1。
**举例:**

> **输入:** arr[] = {1，9，4，3}，K = 3
> **输出:** -1
> **解释:**不可能使任何两个元素相等
> **输入:** arr[] = {13，13，21，15}，K = 13
> **输出:** 0
> **解释:**已经存在两个相同的元素

**方法:**关键的观察是，如果有可能做出所需的数组，那么答案将是 0、1 或 2。永远不会超过 2。

> 因为，如果(x ^ k) = y
> 那么，执行(y ^ k)将再次给出 x

1.  如果数组中已经有相等的元素，答案将是 **0** 。
2.  答案为 **1** ，我们将创建一个新的数组**b【】**,该数组保存 **b[i] = (a[i] ^ K)** ，
    现在，对于每个 **a[i]** 我们将检查是否有任何索引 **j** ,以便 **i！= j** 和 **a[i] = b[j]** 。
    如果是，则答案为 **1** 。
3.  答案为 **2** ，我们将在新数组**b【】**中检查一个索引 **i** ，如果有索引 **j** 这样的话 **i！= j** 和 **b[i] = b[j]** 。
    如果是，则答案为 **2** 。
4.  如果不满足上述任一条件，则答案为 **-1** 。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the count of
// minimum operations required
int minOperations(int a[], int n, int K)
{
    unordered_map<int, bool> map;
    for (int i = 0; i < n; i++) {

        // Check if the initial array
        // already contains an equal pair
        if (map[a[i]])
            return 0;
        map[a[i]] = true;
    }

    // Create new array with XOR operations
    int b[n];
    for (int i = 0; i < n; i++)
        b[i] = a[i] ^ K;

    // Clear the map
    map.clear();

    // Check if the solution
    // is a single operation
    for (int i = 0; i < n; i++) {

        // If Bitwise XOR operation between
        // 'k' and a[i] gives
        // a number other than a[i]
        if (a[i] != b[i])
            map[b[i]] = true;
    }

    // Check if any of the a[i]
    // gets equal to any other element
    // of the array after the operation
    for (int i = 0; i < n; i++)

        // Single operation
        // will be enough
        if (map[a[i]])
            return 1;

    // Clear the map
    map.clear();

    // Check if the solution
    // is two operations
    for (int i = 0; i < n; i++) {

        // Check if the array 'b'
        // contains duplicates
        if (map[b[i]])
            return 2;

        map[b[i]] = true;
    }

    // Otherwise it is impossible to
    // create such an array with
    // Bitwise XOR operations
    return -1;
}

// Driver code
int main()
{

    int K = 3;
    int a[] = { 1, 9, 4, 3 };
    int n = sizeof(a) / sizeof(a[0]);

    // Function call to compute the result
    cout << minOperations(a, n, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.HashMap;

class GFG
{
    // Function to return the count of
    // minimum operations required
    static int minOperations(int[] a, int n, int k)
    {
        HashMap<Integer,
                Boolean> map = new HashMap<>();
        for (int i = 0; i < n; i++)
        {

            // Check if the initial array
            // already contains an equal pair
            if (map.containsKey(a[i]) &&
                map.get(a[i]))
                return 0;
            map.put(a[i], true);
        }

        // Create new array with XOR operations
        int[] b = new int[n];
        for (int i = 0; i < n; i++)
            b[i] = a[i] ^ k;

        // Clear the map
        map.clear();

        // Check if the solution
        // is a single operation
        for (int i = 0; i < n; i++)
        {

            // If Bitwise XOR operation between
            // 'k' and a[i] gives
            // a number other than a[i]
            if (a[i] != b[i])
                map.put(b[i], true);
        }

        // Check if any of the a[i]
        // gets equal to any other element
        // of the array after the operation
        for (int i = 0; i < n; i++)

            // Single operation
            // will be enough
            if (map.containsKey(a[i]) &&
                map.get(a[i]))
                return 1;

        // Clear the map
        map.clear();

        // Check if the solution
        // is two operations
        for (int i = 0; i < n; i++)
        {

            // Check if the array 'b'
            // contains duplicates
            if (map.containsKey(b[i]) &&
                map.get(b[i]))
                return 2;

            map.put(b[i], true);
        }

        // Otherwise it is impossible to
        // create such an array with
        // Bitwise XOR operations
        return -1;
    }

    // Driver Code
    public static void main(String[] args)
    {
        int K = 3;
        int[] a = { 1, 9, 4, 3 };
        int n = a.length;
        System.out.println(minOperations(a, n, K));
    }
}

// This code is contributed by
// Vivek Kumar Singh
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the count of
# minimum operations required
def minOperations(a, n, K) :

    map = dict.fromkeys(a, False);
    for i in range(n) :

        # Check if the initial array
        # already contains an equal pair
        if (map[a[i]]) :
            return 0;
        map[a[i]] = True;

    # Create new array with XOR operations
    b = [0] * n;
    for i in range(n) :
        b[i] = a[i] ^ K;

    # Clear the map
    map.clear();

    # Check if the solution
    # is a single operation
    for i in range(n) :

        # If Bitwise XOR operation between
        # 'k' and a[i] gives
        # a number other than a[i]
        if (a[i] != b[i]) :
            map[b[i]] = True;

    # Check if any of the a[i]
    # gets equal to any other element
    # of the array after the operation
    for i in range(n) :

        # Single operation
        # will be enough
        if a[i] in map :
            return 1;

    # Clear the map
    map.clear();

    # Check if the solution
    # is two operations
    for i in range(n) :

        # Check if the array 'b'
        # contains duplicates
        if b[i] in map :
            return 2;

        map[b[i]] = True;

    # Otherwise it is impossible to
    # create such an array with
    # Bitwise XOR operations
    return -1;

# Driver code
if __name__ == "__main__" :

    K = 3;
    a = [ 1, 9, 4, 3 ];
    n = len(a);

    # Function call to compute the result
    print(minOperations(a, n, K));

# This code is contributed by AnkitRai01
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
    public static int minOperations(int[] a,
                                    int n, int K)
    {

        Dictionary<int, Boolean> map =
                new Dictionary<int, Boolean>();

        for (int i = 0; i < n; i++)
        {

            // Check if the initial array
            // already contains an equal pair
            if (map.ContainsKey(a[i]))
                return 0;

            map.Add(a[i], true);
        }

        // Create new array with XOR operations
        int[] b = new int[n];
        for (int i = 0; i < n; i++)
            b[i] = a[i] ^ K;

        // Clear the map
        map.Clear();

        // Check if the solution
        // is a single operation
        for (int i = 0; i < n; i++)
        {

            // If Bitwise OR operation between
            // 'k' and a[i] gives
            // a number other than a[i]
            if (a[i] != b[i])
                map.Add(b[i], true);
        }

        // Check if any of the a[i]
        // gets equal to any other element
        // of the array after the operation
        for (int i = 0; i < n; i++)
        {

            // Single operation
            // will be enough
            if (map.ContainsKey(a[i]))
                return 1;
        }

        // Clear the map
        map.Clear();

        // Check if the solution
        // is two operations
        for (int i = 0; i < n; i++)
        {

            // Check if the array 'b'
            // contains duplicates
            if (map.ContainsKey(b[i]))
                return 2;
            map.Add(b[i], true);
        }

        // Otherwise it is impossible to
        // create such an array with
        // Bitwise OR operations
        return -1;
    }

    // Driver code
    public static void Main(String[] args)
    {
        int K = 3;
        int[] a = { 1, 9, 4, 3 };
        int n = a.Length;
        Console.WriteLine(minOperations(a, n, K));
    }
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to return the count of
// minimum operations required
function minOperations(a, n, K)
{
    var map = new Map();
    for (var i = 0; i < n; i++) {

        // Check if the initial array
        // already contains an equal pair
        if (map[a[i]])
            return 0;
        map[a[i]] = true;
    }

    // Create new array with XOR operations
    var b = Array(n);
    for (var i = 0; i < n; i++)
        b[i] = a[i] ^ K;

    // Clear the map
    map = new Map();

    // Check if the solution
    // is a single operation
    for (var i = 0; i < n; i++) {

        // If Bitwise XOR operation between
        // 'k' and a[i] gives
        // a number other than a[i]
        if (a[i] != b[i])
            map[b[i]] = true;
    }

    // Check if any of the a[i]
    // gets equal to any other element
    // of the array after the operation
    for (var i = 0; i < n; i++)

        // Single operation
        // will be enough
        if (map[a[i]])
            return 1;

    // Clear the map
    map = new Map();

    // Check if the solution
    // is two operations
    for (var i = 0; i < n; i++) {

        // Check if the array 'b'
        // contains duplicates
        if (map[b[i]])
            return 2;

        map[b[i]] = true;
    }

    // Otherwise it is impossible to
    // create such an array with
    // Bitwise XOR operations
    return -1;
}

// Driver code
var K = 3;
var a = [ 1, 9, 4, 3 ];
var n = a.length;
// Function call to compute the result
document.write( minOperations(a, n, K));

</script>   
```

**Output:** 

```
-1
```
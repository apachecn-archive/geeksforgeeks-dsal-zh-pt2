# 使任意两个数组元素相等的最小按位或运算

> 原文:[https://www . geesforgeks . org/最小位或运算使任意两个数组元素相等/](https://www.geeksforgeeks.org/minimum-bitwise-or-operations-to-make-any-two-array-elements-equal/)

给定一个整数数组 **arr[]** 和一个整数 **K** ，我们可以在任意数组元素和 **K** 之间执行任意次数的按位或运算。任务是打印使数组的任意两个元素相等所需的最小操作数。如果在执行上述操作后无法使数组的任何两个元素相等，则打印 **-1** 。
**举例:**

> **输入:** arr[] = {1，9，4，3}，K = 3
> **输出:** 1
> 我们可以用 x 对 a[0]进行 OR 运算，使其为 3，等于 a[3]
> **输入:** arr[] = {13，26，21，15}，K = 13
> **输出:** -1

**方法:**关键的观察是，如果有可能做出想要的阵列，那么答案将是 **0** 、 **1** 或 **2** 。绝对不会超过 **2** 。

> 因为，如果 **(x | k) = y**
> 那么，无论你执行 **(y | k)**
> 多少次，它总会给出 **y** 作为结果。

*   如果数组中已经有相等的元素，答案将是 **0** 。
*   答案为 **1** ，我们将创建一个新的数组 **b[]** ，该数组保存 **b[i] = (a[i] | K)** ，
    现在，对于每个 **a[i]** 我们将检查是否有任何索引 **j** 以使 **i！= j** 和 **a[i] = b[j]** 。
    如果是，则答案为 **1** 。
*   答案为 **2** ，我们将在新数组**b【】**
    中检查一个索引 **i** ，如果有任何索引 **j** 这样的话 **i！= j** 和 **b[i] = b[j]** 。
    如果是，则答案为 **2** 。
*   如果不满足上述任一条件，则答案为 **-1** 。

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

    // Create new array with OR operations
    int b[n];
    for (int i = 0; i < n; i++)
        b[i] = a[i] | K;

    // Clear the map
    map.clear();

    // Check if the solution
    // is a single operation
    for (int i = 0; i < n; i++) {

        // If Bitwise OR operation between
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
    // Bitwise OR operations
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
    public static int minOperations(int[] a, int n, int K)
    {

        HashMap<Integer, Boolean> map = new HashMap<>();

        for (int i = 0; i < n; i++)
        {

            // Check if the initial array
            // already contains an equal pair
            if (map.containsKey(a[i]))
                return 0;

            map.put(a[i], true);
        }

        // Create new array with OR operations
        int[] b = new int[n];
        for (int i = 0; i < n; i++)
            b[i] = a[i] | K;

        // Clear the map
        map.clear();

        // Check if the solution
        // is a single operation
        for (int i = 0; i < n; i++)
        {

            // If Bitwise OR operation between
            // 'k' and a[i] gives
            // a number other than a[i]
            if (a[i] != b[i])
                map.put(b[i], true);
        }

        // Check if any of the a[i]
        // gets equal to any other element
        // of the array after the operation
        for (int i = 0; i < n; i++)
        {

            // Single operation
            // will be enough
            if (map.containsKey(a[i]))
                return 1;
        }

        // Clear the map
        map.clear();

        // Check if the solution
        // is two operations
        for (int i = 0; i < n; i++)
        {

            // Check if the array 'b'
            // contains duplicates
            if (map.containsKey(b[i]))
                return 2;
            map.put(b[i], true);
        }

        // Otherwise it is impossible to
        // create such an array with
        // Bitwise OR operations
        return -1;
    }

    // Driver code
    public static void main(String[] args)
    {
        int K = 3;
        int[] a = { 1, 9, 4, 3 };
        int n = a.length;
        System.out.println(minOperations(a, n, K));
    }
}

// This code is contributed by
// sanjeev2552
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the count of
# minimum operations required
def minOperations(a, n, K) :

    map = dict.fromkeys(a,0) ;

    for i in range(n) :

        # Check if the initial array
        # already contains an equal pair
        if (map[a[i]]) :
            return 0;

        map[a[i]] = True;

    # Create new array with OR operations
    b = [0]*n;

    for i in range(n) :
        b[i] = a[i] | K;

    # Clear the map
    map.clear();

    # Check if the solution
    # is a single operation
    for i in range(n) :

        # If Bitwise OR operation between
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
        if a[i] not in map :
            pass

        elif (map[a[i]]) :
            return 1;

    # Clear the map
    map.clear();

    # Check if the solution
    # is two operations
    for i in range(n) :

        # Check if the array 'b'
        # contains duplicates
        if (map[b[i]]) :
            return 2;

        map[b[i]] = true;

    # Otherwise it is impossible to
    # create such an array with
    # Bitwise OR operations
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

        Dictionary<int,
                   Boolean> map = new Dictionary<int,
                                                 Boolean>();

        for (int i = 0; i < n; i++)
        {

            // Check if the initial array
            // already contains an equal pair
            if (map.ContainsKey(a[i]))
                return 0;

            map.Add(a[i], true);
        }

        // Create new array with OR operations
        int[] b = new int[n];
        for (int i = 0; i < n; i++)
            b[i] = a[i] | K;

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

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// JavaScript implementation of the approach

// Function to return the count of
// minimum operations required
function minOperations(a, n, K) {
    let map = new Map();
    for (let i = 0; i < n; i++) {

        // Check if the initial array
        // already contains an equal pair
        if (map.has(a[i]))
            return 0;
        map.set(a[i], true);
    }

    // Create new array with OR operations
    let b = new Array(n);
    for (let i = 0; i < n; i++)
        b[i] = a[i] | K;

    // Clear the map
    map.clear();

    // Check if the solution
    // is a single operation
    for (let i = 0; i < n; i++) {

        // If Bitwise OR operation between
        // 'k' and a[i] gives
        // a number other than a[i]
        if (a[i] != b[i])
            map.set(b[i], true);
    }

    // Check if any of the a[i]
    // gets equal to any other element
    // of the array after the operation
    for (let i = 0; i < n; i++)

        // Single operation
        // will be enough
        if (map.has(a[i]))
            return 1;

    // Clear the map
    map.clear();

    // Check if the solution
    // is two operations
    for (let i = 0; i < n; i++) {

        // Check if the array 'b'
        // contains duplicates
        if (map.has(b[i]))
            return 2;

        map.set(b[i], true);
    }

    // Otherwise it is impossible to
    // create such an array with
    // Bitwise OR operations
    return -1;
}

// Driver code

let K = 3;
let a = [1, 9, 4, 3];
let n = a.length;

// Function call to compute the result
document.write(minOperations(a, n, K));

// This code is contributed by gfgking

</script>
```

**Output:** 

```
1
```

时间复杂度:0(n)

辅助空间:O(n)
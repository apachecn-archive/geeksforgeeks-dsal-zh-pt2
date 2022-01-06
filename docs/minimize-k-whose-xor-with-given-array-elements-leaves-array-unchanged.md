# 最小化 K，其与给定数组元素的异或保持数组不变

> 原文:[https://www . geesforgeks . org/minimum-k-what-xor-with-given-array-elements-leaks-array-unchanged/](https://www.geeksforgeeks.org/minimize-k-whose-xor-with-given-array-elements-leaves-array-unchanged/)

给定一个由 **N** 元素组成的[数组](https://www.geeksforgeeks.org/array-data-structure/)，任务是找到 **K** 的最小值，使得 **K** 与所有数组元素的[按位异或](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)产生相同的元素集。如果无法找到 **K** 的任何值，则打印**-1”**。

**示例:**

> **输入:** arr[] = { 1，0，2，3}
> **输出:** 1
> **解释:**
> 对于 K = 1，
> 1 xor 1 = 0
> 1 xor 0 = 1
> 1 xor 2 = 3
> 1 xor 3 = 2
> 因此，K = 1 是保持数组不变的最小可能正值。
> 
> **输入:** arr[] = { 7，1，2，3，8}
> **输出:** -1

**天真方法:**天真方法是迭代范围**【1，1024】**内 **K** 的所有可能值，检查 **K** 与数组中所有元素的按位异或是否给出相同的数组元素。如果对于 **K** 的任何最小值，按位异或产生相同的数组，然后打印 **K** 的值，否则打印 **"-1"** 。
***时间复杂度:**O(K * N<sup>2</sup>)*
***辅助空间:** O(1)*

**高效方法:**上述方法可以通过使用额外的空间进行优化。以下是步骤:

1.  将所有元素插入[集合](https://www.geeksforgeeks.org/set-in-cpp-stl/)。
2.  迭代**【0，1024】**范围内 **K** 的所有可能值。
3.  对于集合中的每个元素，求其与 **K** 的按位异或。
4.  第一个值 **K** 与元素插入按位异或后生成的所有元素与给定集合的元素相同，然后打印 **K** 的值。
5.  如果没有得到这样的 **K** ，打印**-1”**。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum
// value of K in given range
int min_value(int arr[], int N)
{
    int x, X, K;

    // Declare a set
    set<int> S;

    for (int i = 0; i < N; i++) {
        S.insert(arr[i]);
    }

    // Initialize count variable
    int count = 0;

    // Iterate in range [1, 1024]
    for (int i = 1; i <= 1024; i++) {

        // counter set as 0
        count = 0;

        // Iterating through the Set
        for (auto it = S.begin(); it != S.end(); it++)

        // Check if the XOR
        // calculated is present
        // in the Set
        {

            X = ((i | *it) - (i & *it));

            // If the value of Bitwise XOR
            // inside the given set then
            // increment count
            if (S.find(X) != S.end()) {
                count++;
            }
        }

        // Check if the value of count is
        // equal to the size of set
        if (count == S.size()) {
            K = i;

            // Return minimum value of K
            return K;
        }
    }

    // If no such K is found
    return -1;
}

// Driver Code
int main()
{
    // Given array
    int arr[] = { 1, 0, 3, 3, 0, 2 };

    int N = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    cout << min_value(arr, N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG {

    // Function to find the minimum
    // value of K in given range
    static int min_value(int arr[], int N)
    {
        int x, X, K;

        // Declare a set
        HashSet<Integer> S = new HashSet<Integer>();

        for (int i = 0; i < N; i++) {
            S.add(arr[i]);
        }

        // Initialize count variable
        int count = 0;

        // Iterate in range [1, 1024]
        for (int i = 1; i <= 1024; i++) {

            // counter set as 0
            count = 0;

            // Iterating through the Set
            for (int it : S) {

                // Check if the XOR
                // calculated is present
                // in the Set
                X = ((i | it) - (i & it));

                // If the value of Bitwise XOR
                // inside the given set then
                // increment count
                if (S.contains(X)) {
                    count++;
                }
            }

            // Check if the value of count is
            // equal to the size of set
            if (count == S.size()) {
                K = i;

                // Return minimum value of K
                return K;
            }
        }

        // If no such K is found
        return -1;
    }

    // Driver Code
    public static void main(String[] args)
    {

        // Given array
        int arr[] = { 1, 0, 3, 3, 0, 2 };

        int N = arr.length;

        // Function Call
        System.out.print(min_value(arr, N));
    }
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the minimum
# value of K in given range

def min_value(arr, N):

    x, X, K = 0, 0, 0

    # Declare a set
    S = set()

    for i in range(N):
        S.add(arr[i])

    # Initialize count variable
    count = 0

    # Iterate in range [1, 1024]
    for i in range(1, 1024):

        # counter set as 0
        count = 0

        # Iterating through the Set
        for it in S:

            # Check if the XOR
            # calculated is present
            # in the Set
            X = ((i | it) - (i & it))

            # If the value of Bitwise XOR
            # inside the given set then
            # increment count
            if X in S:
                count += 1

        # Check if the value of count is
        # equal to the size of set
        if (count == len(S)):
            K = i

            # Return minimum value of K
            return K

    # If no such K is found
    return -1

# Driver Code

# Given array
arr = [1, 0, 3, 3, 0, 2]

N = len(arr)

# Function Call
print(min_value(arr, N))

# This code is contributed by shubhamsingh10
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG {

    // Function to find the minimum
    // value of K in given range
    static int min_value(int[] arr, int N)
    {
        // int x;
        int X, K;

        // Declare a set
        HashSet<int> S = new HashSet<int>();

        for (int i = 0; i < N; i++) {
            S.Add(arr[i]);
        }

        // Initialize count variable
        int count = 0;

        // Iterate in range [1, 1024]
        for (int i = 1; i <= 1024; i++) {

            // counter set as 0
            count = 0;

            // Iterating through the Set
            foreach(int it in S)
            {

                // Check if the XOR
                // calculated is present
                // in the Set
                X = ((i | it) - (i & it));

                // If the value of Bitwise XOR
                // inside the given set then
                // increment count
                if (S.Contains(X)) {
                    count++;
                }
            }

            // Check if the value of count is
            // equal to the size of set
            if (count == S.Count) {
                K = i;

                // Return minimum value of K
                return K;
            }
        }

        // If no such K is found
        return -1;
    }

    // Driver code
    static void Main()
    {

        // Given array
        int[] arr = { 1, 0, 3, 3, 0, 2 };

        int N = arr.Length;

        // Function call
        Console.Write(min_value(arr, N));
    }
}

// This code is contributed by divyeshrabadiya07
```

## java 描述语言

```
<script>
// Javascript implementation for the above approach

    // Function to find the minimum
    // value of K in given range
    function min_value(arr, N)
    {
        let x, X, K;

        // Declare a set
        let S = [];

        for (let i = 0; i < N; i++) {
            S.push(arr[i]);
        }

        // Initialize count variable
        let count = 0;

        // Iterate in range [1, 1024]
        for (let i = 1; i <= 1024; i++) {

            // counter set as 0
            count = 0;

            // Iterating through the Set
            for (let it in S) {

                // Check if the XOR
                // calculated is present
                // in the Set
                X = ((i | it) - (i & it));

                // If the value of Bitwise XOR
                // inside the given set then
                // increment count
                for (let j in S) {
                if (S[j]==X) {
                    count++;
                }
                }
            }

            // Check if the value of count is
            // equal to the size of set
            if (count == S.length) {
                K = i;

                // Return minimum value of K
                return K;
            }
        }

        // If no such K is found
        return -1;
    }

    // Driver Code

    // Given array
        let arr = [ 1, 0, 3, 3, 0, 2 ];

        let N = arr.length;

        // Function Call
        document.write(min_value(arr, N));

</script>
```

**Output:** 

```
1
```

***时间复杂度:**O(K * N * log<sub>2</sub>N)*
***辅助空间:** O(1)*
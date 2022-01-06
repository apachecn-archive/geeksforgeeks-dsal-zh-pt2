# 给定数组中所有对(I，j)的最大 LCM

> 原文:[https://www . geeksforgeeks . org/maximum-LCM-in-all-pairs-I-j-from-the-the-给定-array/](https://www.geeksforgeeks.org/maximum-lcm-among-all-pairs-i-j-from-the-given-array/)

给定一个数组 **arr[]** ，任务是当数组的元素成对出现时找到最大值 [LCM](https://www.geeksforgeeks.org/lcm-gq/) 。

**示例:**

> **输入:** arr[] = {17，3，8，6}
> **输出:** 136
> **解释:**
> 各自带 LCM 的对是:
> {8，17}有 LCM 136，
> {3，17}有 LCM 51，
> {6，17}有 LCM 102，
> {3，8}有 LCM 24，
> {3
> 其中最大= 136。
> 
> **输入:**数组[] = {1，8，12，9}
> **输出:** 72
> **说明:**
> 72 是给定数组所有对中 LCM 最高的。

**天真方法:**使用两个循环[生成数组中所有可能的元素对](https://www.geeksforgeeks.org/print-all-possible-combinations-of-r-elements-in-a-given-array-of-size-n/)和[计算它们的 LCM](https://www.geeksforgeeks.org/program-to-find-lcm-of-two-numbers/) 。每当我们获得更高的值时，就更新 LCM。
***时间复杂度:** O(N <sup>2</sup> )*

下面是上述方法的实现:

## C++

```
// C++ implementation to find the maximum
// LCM of pairs in an array

#include <bits/stdc++.h>
using namespace std;

// Function comparing all LCM pairs
int maxLcmOfPairs(int arr[], int n)
{
    // To store the highest LCM
    int maxLCM = -1;

    // To generate all pairs from array
    for (int i = 0; i < n; i++) {
        for (int j = i + 1; j < n; j++) {

            // Find LCM of the pair
            // Update the maxLCM if this is
            // greater than its existing value
            maxLCM
                = max(maxLCM, (arr[i] * arr[j])
                                  / __gcd(arr[i], arr[j]));
        }
    }

    // Return the highest value of LCM
    return maxLCM;
}

// Driver code
int main()
{
    int arr[] = { 17, 3, 8, 6 };
    int n = sizeof(arr) / sizeof(arr[0]);

    cout << maxLcmOfPairs(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find the maximum
// LCM of pairs in an array
import java.util.*;
class GFG {

    // Function comparing all LCM pairs
    static int maxLcmOfPairs(int arr[], int n)
    {
        // To store the highest LCM
        int maxLCM = -1;

        // To generate all pairs from array
        for (int i = 0; i < n; i++) {
            for (int j = i + 1; j < n; j++) {

                // Find LCM of the pair
                // Update the maxLCM if this is
                // greater than its existing value
                maxLCM = Math.max(
                    maxLCM, (arr[i] * arr[j])
                                / __gcd(arr[i], arr[j]));
            }
        }

        // Return the highest value of LCM
        return maxLCM;
    }

    static int __gcd(int a, int b)
    {
        return b == 0 ? a : __gcd(b, a % b);
    }

    // Driver code
    public static void main(String[] args)
    {
        int arr[] = { 17, 3, 8, 6 };
        int n = arr.length;

        System.out.print(maxLcmOfPairs(arr, n));
    }
}

// This code is contributed by sapnasingh4991
```

## 蟒蛇 3

```
# Python3 implementation to find the
# maximum LCM of pairs in an array
from math import gcd

# Function comparing all LCM pairs

def maxLcmOfPairs(arr, n):

    # To store the highest LCM
    maxLCM = -1

    # To generate all pairs from array
    for i in range(n):
        for j in range(i + 1, n, 1):

            # Find LCM of the pair
            # Update the maxLCM if this is
            # greater than its existing value
            maxLCM = max(maxLCM, (arr[i] * arr[j]) //
                         gcd(arr[i], arr[j]))

    # Return the highest value of LCM
    return maxLCM

# Driver code
if __name__ == '__main__':

    arr = [17, 3, 8, 6]
    n = len(arr)

    print(maxLcmOfPairs(arr, n))

# This code is contributed by hupendraSingh
```

## C#

```
// C# implementation to find the maximum
// LCM of pairs in an array
using System;
class GFG {

    // Function comparing all LCM pairs
    static int maxLcmOfPairs(int[] arr, int n)
    {
        // To store the highest LCM
        int maxLCM = -1;

        // To generate all pairs from array
        for (int i = 0; i < n; i++) {
            for (int j = i + 1; j < n; j++) {

                // Find LCM of the pair
                // Update the maxLCM if this is
                // greater than its existing value
                maxLCM = Math.Max(
                    maxLCM, (arr[i] * arr[j])
                                / __gcd(arr[i], arr[j]));
            }
        }

        // Return the highest value of LCM
        return maxLCM;
    }

    static int __gcd(int a, int b)
    {
        return b == 0 ? a : __gcd(b, a % b);
    }

    // Driver code
    public static void Main()
    {
        int[] arr = { 17, 3, 8, 6 };
        int n = arr.Length;

        Console.Write(maxLcmOfPairs(arr, n));
    }
}

// This code is contributed by Code_Mech
```

## java 描述语言

```
<script>
// javascript implementation to find the maximum
// LCM of pairs in an array

    // Function comparing all LCM pairs
    function maxLcmOfPairs(arr , n)
    {

        // To store the highest LCM
        var maxLCM = -1;

        // To generate all pairs from array
        for (i = 0; i < n; i++)
        {
            for (j = i + 1; j < n; j++)
            {

                // Find LCM of the pair
                // Update the maxLCM if this is
                // greater than its existing value
                maxLCM = Math.max(maxLCM, (arr[i] * arr[j]) / __gcd(arr[i], arr[j]));
            }
        }

        // Return the highest value of LCM
        return maxLCM;
    }

    function __gcd(a , b) {
        return b == 0 ? a : __gcd(b, a % b);
    }

    // Driver code
        var arr = [ 17, 3, 8, 6 ];
        var n = arr.length;
        document.write(maxLcmOfPairs(arr, n));

// This code is contributed by umadevi9616
</script>
```

**Output**

```
136
```

**另一种方法:**
我们可以用 [**贪心法**](https://www.geeksforgeeks.org/greedy-algorithms/) 。为了应用贪婪的方法，我们必须[对给定的数组](https://www.geeksforgeeks.org/array-data-structure/array-sorting/)进行排序，然后比较数组元素对的 LCM，最后计算 LCM 的最大值。

下面是上述方法的实现:

## C++

```
// C++ implementation to find the maximum
// LCM of pairs in an array

#include <bits/stdc++.h>
using namespace std;

// Function for the highest value of LCM pairs
int greedyLCM(int arr[], int n)
{
    // Sort the given array
    sort(arr, arr + n);

    // Compute the highest LCM
    int maxLCM = arr[n - 1];

    for (int i = n - 1; i >= 0; i--) {
        if (arr[i] * arr[i] < maxLCM)
            break;

        for (int j = i - 1; j >= 0; j--) {

            if (arr[i] * arr[j] < maxLCM)
                break;

            else

                // Find LCM of the pair
                // Update the maxLCM if this is
                // greater than its existing value
                maxLCM = max(maxLCM,
                             (arr[i] * arr[j])
                                 / __gcd(arr[i], arr[j]));
        }
    }

    // return the maximum lcm
    return maxLCM;
}

// Driver code
int main()
{
    int arr[] = { 17, 3, 8, 6 };
    int n = sizeof(arr) / sizeof(arr[0]);

    cout << greedyLCM(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find the
// maximum LCM of pairs in an array
import java.util.*;

class GFG {

    // Function for the highest value
    // of LCM pairs
    static int greedyLCM(int arr[], int n)
    {

        // Sort the given array
        Arrays.sort(arr);

        // Compute the highest LCM
        int maxLCM = arr[n - 1];

        for (int i = n - 1; i >= 0; i--) {
            if (arr[i] * arr[i] < maxLCM)
                break;

            for (int j = i - 1; j >= 0; j--) {
                if (arr[i] * arr[j] < maxLCM)
                    break;
                else

                    // Find LCM of the pair
                    // Update the maxLCM if this is
                    // greater than its existing value
                    maxLCM = Math.max(
                        maxLCM,
                        (arr[i] * arr[j])
                            / __gcd(arr[i], arr[j]));
            }
        }

        // Return the maximum lcm
        return maxLCM;
    }

    static int __gcd(int a, int b)
    {
        return b == 0 ? a : __gcd(b, a % b);
    }

    // Driver code
    public static void main(String[] args)
    {
        int arr[] = { 17, 3, 8, 6 };
        int n = arr.length;

        System.out.print(greedyLCM(arr, n));
    }
}

// This code is contributed by Amit Katiyar
```

## 蟒蛇 3

```
# Python3 implementation to
# find the maximum LCM of
# pairs in an array
from math import gcd

# Function for the highest
# value of LCM pairs

def greedyLCM(arr, n):

    # Sort the given array
    arr.sort()

    # Compute the highest LCM
    maxLCM = arr[n - 1]

    for i in range(n - 1, -1, -1):
        if (arr[i] * arr[i] < maxLCM):
            break

        for j in range(i - 1, -1, -1):
            if (arr[i] * arr[j] < maxLCM):
                break

            else:
                # Find LCM of the pair
                # Update the maxLCM if this is
                # greater than its existing value
                maxLCM = max(maxLCM,
                             (arr[i] * arr[j]) //
                             gcd(arr[i], arr[j]))

    # Return the maximum lcm
    return maxLCM

# Driver code
arr = [17, 3, 8, 6]
n = len(arr)

print(greedyLCM(arr, n))

# This code is contributed by divyeshrabadiya07
```

## C#

```
// C# implementation to find the
// maximum LCM of pairs in an array
using System;

class GFG {

    // Function for the highest value
    // of LCM pairs
    static int greedyLCM(int[] arr, int n)
    {

        // Sort the given array
        Array.Sort(arr);

        // Compute the highest LCM
        int maxLCM = arr[n - 1];

        for (int i = n - 1; i >= 0; i--) {
            if (arr[i] * arr[i] < maxLCM)
                break;

            for (int j = i - 1; j >= 0; j--) {
                if (arr[i] * arr[j] < maxLCM)
                    break;
                else

                    // Find LCM of the pair
                    // Update the maxLCM if this is
                    // greater than its existing value
                    maxLCM = Math.Max(
                        maxLCM,
                        (arr[i] * arr[j])
                            / __gcd(arr[i], arr[j]));
            }
        }

        // Return the maximum lcm
        return maxLCM;
    }

    static int __gcd(int a, int b)
    {
        return b == 0 ? a : __gcd(b, a % b);
    }

    // Driver code
    public static void Main(String[] args)
    {
        int[] arr = { 17, 3, 8, 6 };
        int n = arr.Length;

        Console.Write(greedyLCM(arr, n));
    }
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>

// Javascript implementation to find the
// maximum LCM of pairs in an array

// Function for the highest value
// of LCM pairs
function greedyLCM(arr, n)
{

    // Sort the given array
    arr.sort(function(a, b){return a - b});

    // Compute the highest LCM
    let maxLCM = arr[n - 1];

    for(let i = n - 1; i >= 0; i--)
    {
        if (arr[i] * arr[i] < maxLCM)
            break;

        for(let j = i - 1; j >= 0; j--)
        {
            if (arr[i] * arr[j] < maxLCM)
                break;
            else

                // Find LCM of the pair
                // Update the maxLCM if this is
                // greater than its existing value
                maxLCM = Math.max(maxLCM,
                    parseInt((arr[i] * arr[j]) /
                        __gcd(arr[i], arr[j]), 10));
        }
    }

    // Return the maximum lcm
    return maxLCM;
}

function __gcd(a, b)
{
    return b == 0 ? a : __gcd(b, a % b);
}

// Driver code
let arr = [ 17, 3, 8, 6 ];
let n = arr.length;

document.write(greedyLCM(arr, n));

// This code is contributed by mukesh07

</script>
```

**Output**

```
136
```

***时间复杂度:**T3】O(N<sup>2</sup>*
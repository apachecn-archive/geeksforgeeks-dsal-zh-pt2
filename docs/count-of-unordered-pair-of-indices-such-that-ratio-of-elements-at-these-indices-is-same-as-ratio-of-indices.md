# 无序索引对的计数，使得这些索引处的元素比率与索引比率

相同

> 原文:[https://www . geeksforgeeks . org/无序索引对的计数-这些索引处的元素比率与索引比率相同/](https://www.geeksforgeeks.org/count-of-unordered-pair-of-indices-such-that-ratio-of-elements-at-these-indices-is-same-as-ratio-of-indices/)

给定 N 个整数的数组 arr[]，任务是找到数组中无序对(I，j)的数量，使得这些索引处的元素比率与索引比率相同( **arr[j]/arr[i] = j/i** )。

示例:

> **输入:** arr[] = {4，5，12，10，6}
> **输出:** 2
> **解释:**符合给定条件的对是:
> 
> 1.  (1，3) as arr[3] / arr[1] = 12/4 = 3 = 3/1
> 2.  (2，4) as arr[4] / arr[2] = 10/5 = 2 = 4/2
> 
> **输入:** arr[] = {5，-2，4，20，25，-6 }
> T3】输出: 3

**天真的** **方法**:给定的问题可以通过迭代给定数组中所有无序的对(I，j)来解决，同时跟踪符合条件 arr[j] / arr[i] = j / i 的对的数量

下面是上述方法的实现:

## C++

```
// C++ program of the above approach
#include <bits/stdc++.h>
using namespace std;

// Function of find the count of unordered
// pairs (i, j) in the array such that
// arr[j] / arr[i] = j / i.
int countPairs(int arr[], int n)
{
    // Stores the count of valid pairs
    int count = 0;

    // Iterating over all possible pairs
    for (int i = 0; i < n - 1; i++) {
        for (int j = i + 1; j < n; j++) {

            // Check if the pair is valid
            if ((arr[j] % arr[i] == 0)
                && (j + 1) % (i + 1) == 0
                && (arr[j] / arr[i]
                    == (j + 1) / (i + 1))) {
                count++;
            }
        }
    }

    // Return answer
    return count;
}

// Driver Code
int main()
{
    int arr[] = { 5, -2, 4, 20, 25, -6 };
    int n = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    cout << countPairs(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program of the above approach
import java.util.*;

class GFG
{

// Function of find the count of unordered
// pairs (i, j) in the array such that
// arr[j] / arr[i] = j / i.
static int countPairs(int arr[], int n)
{

    // Stores the count of valid pairs
    int count = 0;

    // Iterating over all possible pairs
    for (int i = 0; i < n - 1; i++) {
        for (int j = i + 1; j < n; j++) {

            // Check if the pair is valid
            if ((arr[j] % arr[i] == 0)
                && (j + 1) % (i + 1) == 0
                && (arr[j] / arr[i]
                    == (j + 1) / (i + 1))) {
                count++;
            }
        }
    }

    // Return answer
    return count;
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 5, -2, 4, 20, 25, -6 };
    int n = arr.length;

    // Function Call
    System.out.print(countPairs(arr, n));
}
}

// This code is contributed by shikhasingrajput
```

## 蟒蛇 3

```
# Python 3 program of the above approach

# Function of find the count of unordered
# pairs (i, j) in the array such that
# arr[j] / arr[i] = j / i.
def countPairs(arr, n):

    # Stores the count of valid pairs
    count = 0

    # Iterating over all possible pairs
    for i in range(n - 1):
        for j in range(i + 1, n):

            # Check if the pair is valid
            if ((arr[j] % arr[i] == 0)
                and (j + 1) % (i + 1) == 0
                and (arr[j] // arr[i]
                     == (j + 1) // (i + 1))):
                count += 1

    # Return answer
    return count

# Driver Code
if __name__ == "__main__":

    arr = [5, -2, 4, 20, 25, -6]
    n = len(arr)

    # Function Call
    print(countPairs(arr, n))

    # This code is contributed by ukasp.
```

## C#

```
// C# program for the above approach
using System;

public class GFG
{

// Function of find the count of unordered
// pairs (i, j) in the array such that
// arr[j] / arr[i] = j / i.
static int countPairs(int[] arr, int n)
{

    // Stores the count of valid pairs
    int count = 0;

    // Iterating over all possible pairs
    for (int i = 0; i < n - 1; i++) {
        for (int j = i + 1; j < n; j++) {

            // Check if the pair is valid
            if ((arr[j] % arr[i] == 0)
                && (j + 1) % (i + 1) == 0
                && (arr[j] / arr[i]
                    == (j + 1) / (i + 1))) {
                count++;
            }
        }
    }

    // Return answer
    return count;
}   

    // Driver Code
    public static void Main (string[] args)
    {
        int[] arr = { 5, -2, 4, 20, 25, -6 };
        int n = arr.Length;

        // Function Call
        Console.WriteLine(countPairs(arr, n));
    }
}

// This code is contributed by avijitmondal1998.
```

## java 描述语言

```
<script>
        // JavaScript Program to implement
        // the above approach

        // Function of find the count of unordered
        // pairs (i, j) in the array such that
        // arr[j] / arr[i] = j / i.
        function countPairs(arr, n)
        {

            // Stores the count of valid pairs
            let count = 0;

            // Iterating over all possible pairs
            for (let i = 0; i < n - 1; i++) {
                for (let j = i + 1; j < n; j++) {

                    // Check if the pair is valid
                    if ((arr[j] % arr[i] == 0)
                        && (j + 1) % (i + 1) == 0
                        && (arr[j] / arr[i]
                            == (j + 1) / (i + 1))) {
                        count++;
                    }
                }
            }

            // Return answer
            return count;
        }

        // Driver Code

        let arr = [5, -2, 4, 20, 25, -6];
        let n = arr.length;
        // Function Call
        document.write(countPairs(arr, n));

     // This code is contributed by Potta Lokesh

    </script>
```

**Output**

```
3
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*

**高效方法:**上述方法可以通过观察 **y / x** 对于任意一对 **(x，y)** 可以达到的最大值为 **N** 来优化。另外， **y** 必须能被 **x** 整除。因此，对于范围**【1，N】**中的 **x** ，迭代范围**【1，N】**中的所有 **y** ，使得 **y** 可被 **x** 整除，并记录对的数量 **(x，y)** ，使得 **arr[y] / arr[x] = y / x** 。这可以使用厄拉多塞的[筛来完成。

以下是上述方法的实施:](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)

## C++

```
// C++ program of the above approach
#include <bits/stdc++.h>
using namespace std;

// Function of find the count of unordered
// pairs (i, j) in the array such that
// arr[j] / arr[i] = j / i.
int countPairs(int arr[], int n)
{
    // Stores the count of valid pairs
    int count = 0;

    // Iterating over all values of
    // x in range [1, N].
    for (int x = 1; x <= n; x++) {

        // Iterating over all values
        // of y that are divisible by
        // x in the range [1, N].
        for (int y = 2 * x; y <= n; y += x) {

            // Check if the pair is valid
            if ((arr[y - 1] % arr[x - 1] == 0)
                && (arr[y - 1] / arr[x - 1]
                    == y / x)) {
                count++;
            }
        }
    }

    // Return answer
    return count;
}

// Driver Code
int main()
{
    int arr[] = { 5, -2, 4, 20, 25, -6 };
    int n = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    cout << countPairs(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program of the above approach
class GFG{

// Function of find the count of unordered
// pairs (i, j) in the array such that
// arr[j] / arr[i] = j / i.
static int countPairs(int arr[], int n)
{

    // Stores the count of valid pairs
    int count = 0;

    // Iterating over all values of
    // x in range [1, N].
    for (int x = 1; x <= n; x++) {

        // Iterating over all values
        // of y that are divisible by
        // x in the range [1, N].
        for (int y = 2 * x; y <= n; y += x) {

            // Check if the pair is valid
            if ((arr[y - 1] % arr[x - 1] == 0)
                && (arr[y - 1] / arr[x - 1]
                    == y / x)) {
                count++;
            }
        }
    }

    // Return answer
    return count;
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 5, -2, 4, 20, 25, -6 };
    int n = arr.length;

    // Function Call
    System.out.print(countPairs(arr, n));
}
}

// This code is contributed by shikhasingrajput
```

## 蟒蛇 3

```
# Python 3 program of the above approach

# Function of find the count of unordered
# pairs (i, j) in the array such that
# arr[j] / arr[i] = j / i.
def countPairs(arr, n):

    # Stores the count of valid pairs
    count = 0

    # Iterating over all values of
    # x in range [1, N].
    for x in range(1, n + 1, 1):

        # Iterating over all values
        # of y that are divisible by
        # x in the range [1, N].
        for y in range(2 * x, n + 1, x):

            # Check if the pair is valid
            if ((arr[y - 1] % arr[x - 1] == 0) and (arr[y - 1] // arr[x - 1] == y // x)):
                count += 1

    # Return answer
    return count

# Driver Code
if __name__ == '__main__':
    arr = [5, -2, 4, 20, 25, -6]
    n = len(arr)

    # Function Call
    print(countPairs(arr, n))

    # This code is contributed by SURENDRA_GANGWAR.
```

## C#

```
// C# program of the above approach
using System;
class GFG {

    // Function of find the count of unordered
    // pairs (i, j) in the array such that
    // arr[j] / arr[i] = j / i.
    static int countPairs(int[] arr, int n)
    {

        // Stores the count of valid pairs
        int count = 0;

        // Iterating over all values of
        // x in range [1, N].
        for (int x = 1; x <= n; x++) {

            // Iterating over all values
            // of y that are divisible by
            // x in the range [1, N].
            for (int y = 2 * x; y <= n; y += x) {

                // Check if the pair is valid
                if ((arr[y - 1] % arr[x - 1] == 0)
                    && (arr[y - 1] / arr[x - 1] == y / x)) {
                    count++;
                }
            }
        }

        // Return answer
        return count;
    }

    // Driver Code
    public static void Main()
    {
        int[] arr = { 5, -2, 4, 20, 25, -6 };
        int n = arr.Length;

        // Function Call
        Console.WriteLine(countPairs(arr, n));
    }
}

// This code is contributed by ukasp.
```

## java 描述语言

```
<script>
// javascript program of the above approach

// Function of find the count of unordered
// pairs (i, j) in the array such that
// arr[j] / arr[i] = j / i.
function countPairs(arr , n)
{

    // Stores the count of valid pairs
    var count = 0;

    // Iterating over all values of
    // x in range [1, N].
    for (var x = 1; x <= n; x++) {

        // Iterating over all values
        // of y that are divisible by
        // x in the range [1, N].
        for (var y = 2 * x; y <= n; y += x) {

            // Check if the pair is valid
            if ((arr[y - 1] % arr[x - 1] == 0)
                && (arr[y - 1] / arr[x - 1]
                    == y / x)) {
                count++;
            }
        }
    }

    // Return answer
    return count;
}

// Driver Code
var arr = [ 5, -2, 4, 20, 25, -6 ];
var n = arr.length;

// Function Call
document.write(countPairs(arr, n));

// This code is contributed by shikhasingrajput
</script>
```

**Output**

```
3
```

***时间复杂度:** O(N*log N)*
***辅助空间:** O(1)*
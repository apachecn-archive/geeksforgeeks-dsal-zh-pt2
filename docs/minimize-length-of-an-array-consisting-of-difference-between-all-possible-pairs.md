# 最小化由所有可能对之间的差异组成的数组的长度

> 原文:[https://www . geesforgeks . org/最小化由所有可能对之间的差异组成的数组长度/](https://www.geeksforgeeks.org/minimize-length-of-an-array-consisting-of-difference-between-all-possible-pairs/)

给定一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** ，任务是找到需要插入到数组中的元素的最小数量，使得数组中存在所有可能对的绝对差。

**示例:**

> **输入:** arr[] = { 3，5 }
> **输出:** 3
> **解释:**
> 在数组中插入 2 会将 arr[]修改为{ 2，3，5 }
> 在数组中插入 1 会将 arr[]修改为{ 1，2，3，5 }
> 在数组中插入 4 会将 arr[]修改为{ 1，2，3，4，5 }
> 由于数组中所有可能的对的绝对差异都存在于数组中，因此需要的输出为
> 
> **输入:** arr[] = { 2，4 }
> **输出:** 0
> **解释:**
> 由于数组中已经存在所有可能的对数组的绝对差，因此需要的输出为 0。

**天真方法:**解决这个问题最简单的方法是从数组中找出每一个可能的对的绝对差，[检查得到的差是否存在于数组中](https://www.geeksforgeeks.org/check-if-a-value-is-present-in-an-array-in-java/)。如果不存在，则插入获得的差值。否则，打印插入数组的元素数。

***时间复杂度:** O(N * X)，其中 X 是数组中最大的元素。*
***辅助空间:** O(X)*

**高效方法:**上述方法可以基于以下观察进行优化:

> 因为数组中必须存在所有可能的最终数组对的绝对差。
> 所以最终的数组必须是 X，2 * X，3 * X，4 * X，…
> 
> 从最后一个数组的上述序列中，可以观察到 X 的值一定是给定数组的 GCD。

按照以下步骤解决问题:

*   [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)[计算给定数组](https://www.geeksforgeeks.org/gcd-two-array-numbers/)的 GCD，说 **X** 。
*   找到数组中最大的[元素，说 **Max** 。](https://www.geeksforgeeks.org/c-program-find-largest-element-array/)
*   通过插入所有可能对的绝对差，数组中元素的总数为**(最大)/ X** 。
*   因此，插入数组的元素总数等于**((Max/X)–N)**。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the GCD of an array
int findGcd(int arr[], int N)
{

    // Stores GCD of an array
    int gcd = arr[0];

    // Traverse the array
    for (int i = 1; i < N; i++) {

        // Update gcd
        gcd = __gcd(gcd, arr[i]);
    }
    return gcd;
}

// Function to find minimum count of elements
// inserted into the array such that absolute
// difference of pairs present in the array
void findMax(int arr[], int N)
{

    // Stores gcd of the array
    int gcd = findGcd(arr, N);

    // Stores the largest element
    // in the array
    int Max = INT_MIN;

    // Traverse the array
    for (int i = 0; i < N; i++) {

        // Update Max
        Max = max(Max, arr[i]);
    }

    // Stores minimum count of elements inserted
    // into the array such that absolute difference
    // of pairs present in the array
    int ans = (Max / gcd) - N;

    cout << ans;
}

// Driver Code
int main()
{

    // Given array
    int arr[] = { 3, 5 };

    // Size of the array
    int N = (sizeof(arr) / (sizeof(arr[0])));

    // Function Call
    findMax(arr, N);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
class GFG
{

// Recursive function to return gcd of a and b
static int gcdd(int a, int b)
{
    // Everything divides 0
    if (a == 0)
       return b;
    if (b == 0)
       return a;

    // base case
    if (a == b)
        return a;

    // a is greater
    if (a > b)
        return gcdd(a - b, b);
    return gcdd(a, b - a);
}

// Function to find the GCD of an array
static int findGcd(int arr[], int N)
{

    // Stores GCD of an array
    int gcd = arr[0];

    // Traverse the array
    for (int i = 1; i < N; i++)
    {

        // Update gcd
        gcd = gcdd(gcd, arr[i]);
    }
    return gcd;
}

// Function to find minimum count of elements
// inserted into the array such that absolute
// difference of pairs present in the array
static void findMax(int arr[], int N)
{

    // Stores gcd of the array
    int gcd = findGcd(arr, N);

    // Stores the largest elemetn
    // in the array
    int Max = Integer.MIN_VALUE;

    // Traverse the array
    for (int i = 0; i < N; i++)
    {

        // Update Max
        Max = Math.max(Max, arr[i]);
    }

    // Stores minimum count of elements inserted
    // into the array such that absolute difference
    // of pairs present in the array
    int ans = (Max / gcd) - N;
    System.out.println(ans);
}

// Driver code
public static void main(String[] args)
{

    // Given array
    int arr[] = { 3, 5 };

    // Size of the array
    int N = arr.length;

    // Function Call
    findMax(arr, N);
}
}

// This code is contributed by susmitakundugoaldanga.
```

## 蟒蛇 3

```
# Python3 program for the above approach
import math
import sys

# Function to find the GCD of an array
def findGcd(arr, N):

    # Stores GCD of an array
    gcd = arr[0]

    # Traverse the array
    for i in range(1, N):

        # Update gcd
        gcd = math.gcd(gcd, arr[i])

    return gcd

# Function to find minimum count of elements
# inserted into the array such that absolute
# difference of pairs present in the array
def findMax(arr, N):

    # Stores gcd of the array
    gcd = findGcd(arr, N)

    # Stores the largest elemetn
    # in the array
    Max = -sys.maxsize - 1

    # Traverse the array
    for i in range(N):

        # Update Max
        Max = max(Max, arr[i])

    # Stores minimum count of elements inserted
    # into the array such that absolute difference
    # of pairs present in the array
    ans = (Max // gcd) - N

    print(ans)

# Driver Code
if __name__ == "__main__":

    # Given array
    arr = [3, 5]

    # Size of the array
    N = len(arr)

    # Function Call
    findMax(arr, N)

# This code is contributed by chitranayal
```

## C#

```
// C# program for the above approach
using System;

class GFG
{

    // Recursive function to return gcd of a and b
    static int gcdd(int a, int b)
    {

        // Everything divides 0
        if (a == 0)
            return b;
        if (b == 0)
            return a;

        // base case
        if (a == b)
            return a;

        // a is greater
        if (a > b)
            return gcdd(a - b, b);
        return gcdd(a, b - a);
    }

    // Function to find the GCD of an array
    static int findGcd(int[] arr, int N)
    {

        // Stores GCD of an array
        int gcd = arr[0];

        // Traverse the array
        for (int i = 1; i < N; i++)
        {

            // Update gcd
            gcd = gcdd(gcd, arr[i]);
        }
        return gcd;
    }

    // Function to find minimum count of elements
    // inserted into the array such that absolute
    // difference of pairs present in the array
    static void findMax(int[] arr, int N)
    {

        // Stores gcd of the array
        int gcd = findGcd(arr, N);

        // Stores the largest elemetn
        // in the array
        int Max = Int32.MinValue;

        // Traverse the array
        for (int i = 0; i < N; i++)
        {

            // Update Max
            Max = Math.Max(Max, arr[i]);
        }

        // Stores minimum count of elements inserted
        // into the array such that absolute difference
        // of pairs present in the array
        int ans = (Max / gcd) - N;
        Console.WriteLine(ans);
    }

    // Driver code
    static public void Main()
    {

        // Given array
        int[] arr = new int[] { 3, 5 };

        // Size of the array
        int N = arr.Length;

        // Function Call
        findMax(arr, N);
    }
}

// This code is contributed by Dharanendra L V.
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Recursive function to return gcd of a and b
function gcdd(a, b)
{

    // Everything divides 0
    if (a == 0)
        return b;
    if (b == 0)
        return a;

    // Base case
    if (a == b)
        return a;

    // a is greater
    if (a > b)
        return gcdd(a - b, b);

    return gcdd(a, b - a);
}

// Function to find the GCD of an array
function findGcd(arr, N)
{

    // Stores GCD of an array
    var gcd = arr[0];

    // Traverse the array
    for(i = 1; i < N; i++)
    {

        // Update gcd
        gcd = gcdd(gcd, arr[i]);
    }
    return gcd;
}

// Function to find minimum count of elements
// inserted into the array such that absolute
// difference of pairs present in the array
function findMax(arr, N)
{

    // Stores gcd of the array
    var gcd = findGcd(arr, N);

    // Stores the largest elemetn
    // in the array
    var Max = Number.MIN_VALUE;

    // Traverse the array
    for(i = 0; i < N; i++)
    {

        // Update Max
        Max = Math.max(Max, arr[i]);
    }

    // Stores minimum count of elements inserted
    // into the array such that absolute difference
    // of pairs present in the array
    var ans = (Max / gcd) - N;
    document.write(ans);
}

// Driver code

// Given array
var arr = [ 3, 5 ];

// Size of the array
var N = arr.length;

// Function Call
findMax(arr, N);

// This code is contributed by umadevi9616

</script>
```

**Output:** 

```
3
```

***时间复杂度:** O(N * Log(X))，其中 X 是数组中最大的元素。*
**辅助空间:** O(1)
# 通过移除数组中的最大 K 值来清空数组

> 原文:[https://www . geeksforgeeks . org/通过从数组中移除最大 k 值来清空数组/](https://www.geeksforgeeks.org/empty-an-array-by-removing-maximum-of-k-value-from-it/)

给定大小为 N 且值为 K 的数组 arr，任务是通过从中移除最大值 K 来清空该数组。如果数组为空，则打印移除的值，否则为-1。
**例:**

> **输入:** arr[] = {2，2}，K = 5
> **输出:** 4
> **解释:**
> 从 K (=5)中移除 arr[1] (=2)后，K = 5–2 = 3
> 从 K (=3)中移除 arr[2] (=2)后，K = 3–2 = 1
> 由于数组已清空，K 仍为> 0
> 因此移除的值= 2+2 = 4【T0 2，2}，K = 10
> **输出:** -1
> **说明:**
> 从 K (=10)中移除 arr[1] (=5)后，K = 10–5 = 5
> 从 K (=5)中移除 arr[2] (=3)后，K = 5–3 = 2
> 从 K (=2)中移除 arr[3] (=2)后，K = 2–2 = 0
> () K = 0–2 =-2
> 由于数组已经清空，K 为< 0
> 因此对于这个 K
> 数组不能清空，因此输出为-1

**进场:**

*   给定的问题可以观察为[找到数组](https://www.geeksforgeeks.org/program-find-sum-elements-given-array/) arr 的总和，并从 k
    中移除该总和
*   如果这个和小于或等于 K，那么数组可以被清空，输出将是数组的和。

*   否则输出将为-1。

以下是上述方法的实现:

## C++

```
// C++ program to empty an Array
// by removing a maximum of K value from it

#include <bits/stdc++.h>
using namespace std;

// Function to Empty an Array by removing
// maximum of K value from it
void emptyArray(long long int n,
                long long int k,
                long long int arr[])
{
    long long int sum = 0, i;

    // Find the total sum of the array
    for (i = 0; i < n; i++)
        sum += arr[i];

    // Find if sum is less than or equal to K
    if (sum <= k)
        cout << sum << "\n";
    else
        cout << -1 << "\n";
}

// Driver code
int main()
{

    long long int n = 2, k = 5;
    long long int arr[] = { 2, 2 };

    emptyArray(n, k, arr);

    n = 4, k = 10;
    long long int arr1[] = { 5, 3, 2, 2 };

    emptyArray(n, k, arr1);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to empty an Array
// by removing a maximum of K value from it
class GFG
{

    // Function to Empty an Array by removing
    // maximum of K value from it
    static void emptyArray(int n, int k, int arr[])
    {
        int sum = 0, i;

        // Find the total sum of the array
        for (i = 0; i < n; i++)
            sum += arr[i];

        // Find if sum is less than or equal to K
        if (sum <= k)
            System.out.println(sum);
        else
            System.out.println(-1);
    }

    // Driver code
    public static void main (String[] args)
    {
        int n = 2;
        int k = 5;
        int arr[] = { 2, 2 };

        emptyArray(n, k, arr);

        n = 4; k = 10;
        int arr1[] = { 5, 3, 2, 2 };

        emptyArray(n, k, arr1);
    }
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python program to empty an Array
# by removing a maximum of K value from it

# Function to Empty an Array by removing
# maximum of K value from it
def emptyArray(n, k, arr) :

    sum = 0;

    # Find the total sum of the array
    for i in range(n) :
        sum += arr[i];

    # Find if sum is less than or equal to K
    if (sum <= k) :
        print(sum);
    else :
        print(-1);

# Driver code
if __name__ == "__main__" :

    n = 2; k = 5;
    arr = [ 2, 2 ];

    emptyArray(n, k, arr);

    n = 4; k = 10;
    arr1 = [ 5, 3, 2, 2 ];

    emptyArray(n, k, arr1);

# This code is contributed by AnkitRai01
```

## C#

```
// C# program to empty an Array
// by removing a maximum of K value from it
using System;

class GFG
{

    // Function to Empty an Array by removing
    // maximum of K value from it
    static void emptyArray(int n, int k, int []arr)
    {
        int sum = 0, i;

        // Find the total sum of the array
        for (i = 0; i < n; i++)
            sum += arr[i];

        // Find if sum is less than or equal to K
        if (sum <= k)
            Console.WriteLine(sum);
        else
            Console.WriteLine(-1);
    }

    // Driver code
    public static void Main(String[] args)
    {
        int n = 2;
        int k = 5;
        int []arr = { 2, 2 };

        emptyArray(n, k, arr);

        n = 4; k = 10;
        int []arr1 = { 5, 3, 2, 2 };

        emptyArray(n, k, arr1);
    }
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// JavaScript program to empty an Array
// by removing a maximum of K value from it

// Function to Empty an Array by removing
// maximum of K value from it
function emptyArray(n, k, arr)
{
    var sum = 0, i;

    // Find the total sum of the array
    for (i = 0; i < n; i++)
        sum += arr[i];

    // Find if sum is less than or equal to K
    if (sum <= k)
        document.write( sum + "<br>");
    else
        document.write( -1 );
}

// Driver code

var n = 2, k = 5;
var arr = [2, 2];
emptyArray(n, k, arr);
var n = 4, k = 10;
var arr1 = [5, 3, 2, 2];
emptyArray(n, k, arr1);

</script>
```

**Output:** 

```
4
-1
```
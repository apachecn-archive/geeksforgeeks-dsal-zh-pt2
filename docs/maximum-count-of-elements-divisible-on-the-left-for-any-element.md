# 任何元素左侧可分割元素的最大数量

> 原文:[https://www . geesforgeks . org/元素最大计数-任何元素可在左边整除/](https://www.geeksforgeeks.org/maximum-count-of-elements-divisible-on-the-left-for-any-element/)

给定一个由 **N** 元素组成的数组 **arr[]** 。元素 arr[i]的良好值是有效索引 j < i 的数量，使得 arr[j]可被 arr[i]整除。
**例:**

> **输入:** arr[] = {9，6，2，3}
> **输出:** 2
> 9 左侧没有任何元素。
> 6 不分割左侧任何元素。
> 2 除 6。
> 3 除 6 和 9。
> **输入:** arr[] = {8，1，28，4，2，6，7}
> **输出:** 3

**天真的做法:**对于每个元素，在它的左边找到能被它整除的数的个数，打印这些值的最大值。
以下是上述办法的实施情况:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the maximum count
// of required elements
int findMax(int arr[], int n)
{
    int res = 0;
    int i, j;

    // For every element in the array starting
    // from the second element
    for(i = 0; i < n ; i++)
    {

        // Check all the elements on the left
        // of current element which are divisible
        // by the current element
        int count = 0;
        for(j = 0; j < i; j++)
        {
            if (arr[j] % arr[i] == 0)
                count += 1;
        }
        res = max(count, res);
    }
    return res;
}

// Driver code
int main()
{
    int arr[] = { 8, 1, 28, 4, 2, 6, 7 };
    int n = sizeof(arr) / sizeof(int);

    cout << findMax(arr, n);

    return 0;
}

// This code is contributed by Rajput-Ji
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

// Function to return the maximum count
// of required elements
static int findMax(int arr[], int n)
{
    int res = 0;
    int i, j;

    // For every element in the array starting
    // from the second element
    for(i = 0; i < n ; i++)
    {

        // Check all the elements on the left
        // of current element which are divisible
        // by the current element
        int count = 0;
        for(j = 0; j < i; j++)
        {
            if (arr[j] % arr[i] == 0)
                count += 1;
        }
        res = Math.max(count, res);
    }
    return res;
}

// Driver Code
public static void main (String[] args)
{
    int arr[] = {8, 1, 28, 4, 2, 6, 7};
    int n = arr.length;
    System.out.println(findMax(arr, n));
}
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the maximum count
# of required elements
def findMax(arr, n):
    res = 0

    # For every element in the array starting
    # from the second element
    for i in range(1, n):

        # Check all the elements on the left
        # of current element which are divisible
        # by the current element
        count = 0
        for j in range(0, i):
            if arr[j] % arr[i] == 0:
                count += 1
        res = max(count, res)
    return res

# Driver code
arr = [8, 1, 28, 4, 2, 6, 7]
n = len(arr)
print(findMax(arr, n))
```

## C#

```
// C# implementation of the above approach
using System;

class GFG
{

// Function to return the maximum count
// of required elements
static int findMax(int []arr, int n)
{
    int res = 0;
    int i, j;

    // For every element in the array 
    // starting from the second element
    for(i = 0; i < n ; i++)
    {

        // Check all the elements on the left
        // of current element which are divisible
        // by the current element
        int count = 0;
        for(j = 0; j < i; j++)
        {
            if (arr[j] % arr[i] == 0)
                count += 1;
        }
        res = Math.Max(count, res);
    }
    return res;
}

// Driver Code
public static void Main (String[] args)
{
    int []arr = {8, 1, 28, 4, 2, 6, 7};
    int n = arr.Length;
    Console.WriteLine(findMax(arr, n));
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// JavaScript implementation of the approach

// Function to return the maximum count
// of required elements
function findMax(arr, n)
{
    var res = 0;
    var i, j;

    // For every element in the array starting
    // from the second element
    for(i = 0; i < n ; i++)
    {

        // Check all the elements on the left
        // of current element which are divisible
        // by the current element
        var count = 0;
        for(j = 0; j < i; j++)
        {
            if (arr[j] % arr[i] == 0)
                count += 1;
        }
        res = Math.max(count, res);
    }
    return res;
}

// Driver code
var arr = [8, 1, 28, 4, 2, 6, 7];
var n = arr.length;
document.write( findMax(arr, n));

</script>
```

**Output:** 

```
3
```

**时间复杂度:** O(N <sup>2</sup> )
**高效方法:**可以观察到，对于任何元素对 **(arr[i]，arr[j])** 其中 **i < j** 和 **(arr[i] % arr[j]) = 0** ，如果其左边可被 **arr[i]** 整除的元素数为 **X** 因此，对于每一个可以被它右边的任何其他元素整除的元素，不需要计算它左边可以被它整除的元素的数量，这将提高整个程序的时间复杂度，但是应该注意的是，对于没有元素可以被任何其他元素整除的输入(例如，当所有元素都是质数时)，最坏的时间复杂度仍然是 **O(N <sup>2</sup> )** 。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the maximum count
// of required elements
int findMax(int arr[], int n)
{

    // divisible[i] will store true
    // if arr[i] is divisible by
    // any element on its right
    bool divisible[n] = { false };

    // To store the maximum required count
    int res = 0;

    // For every element of the array
    for (int i = n - 1; i > 0; i--) {

        // If the current element is
        // divisible by any element
        // on its right
        if (divisible[i])
            continue;

        // Find the count of element
        // on the left which are divisible
        // by the current element
        int cnt = 0;
        for (int j = 0; j < i; j++) {

            // If arr[j] is divisible then
            // set divisible[j] to true
            if ((arr[j] % arr[i]) == 0) {
                divisible[j] = true;
                cnt++;
            }
        }

        // Update the maximum required count
        res = max(res, cnt);
    }

    return res;
}

// Driver code
int main()
{
    int arr[] = { 8, 1, 28, 4, 2, 6, 7 };
    int n = sizeof(arr) / sizeof(int);

    cout << findMax(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

// Function to return the maximum count
// of required elements
static int findMax(int arr[], int n)
{

    // divisible[i] will store true
    // if arr[i] is divisible by
    // any element on its right
    boolean []divisible = new boolean[n];

    // To store the maximum required count
    int res = 0;

    // For every element of the array
    for (int i = n - 1; i > 0; i--)
    {

        // If the current element is
        // divisible by any element
        // on its right
        if (divisible[i])
            continue;

        // Find the count of element
        // on the left which are divisible
        // by the current element
        int cnt = 0;
        for (int j = 0; j < i; j++)
        {

            // If arr[j] is divisible then
            // set divisible[j] to true
            if ((arr[j] % arr[i]) == 0)
            {
                divisible[j] = true;
                cnt++;
            }
        }

        // Update the maximum required count
        res = Math.max(res, cnt);
    }
    return res;
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 8, 1, 28, 4, 2, 6, 7 };
    int n = arr.length;

    System.out.println(findMax(arr, n));
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the maximum count
# of required elements
def findMax(arr, n) :

    # divisible[i] will store true
    # if arr[i] is divisible by
    # any element on its right
    divisible = [ False ] * n;

    # To store the maximum required count
    res = 0;

    # For every element of the array
    for i in range(n - 1, -1, -1) :

        # If the current element is
        # divisible by any element
        # on its right
        if (divisible[i]) :
            continue;

        # Find the count of element
        # on the left which are divisible
        # by the current element
        cnt = 0;
        for j in range(i) :

            # If arr[j] is divisible then
            # set divisible[j] to true
            if ((arr[j] % arr[i]) == 0) :
                divisible[j] = True;
                cnt += 1;

        # Update the maximum required count
        res = max(res, cnt);

    return res;

# Driver code
if __name__ == "__main__" :

    arr = [ 8, 1, 28, 4, 2, 6, 7 ];
    n = len(arr);

    print(findMax(arr, n));

# This code is contributed by kanugargng
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to return the maximum count
// of required elements
static int findMax(int []arr, int n)
{

    // divisible[i] will store true
    // if arr[i] is divisible by
    // any element on its right
    bool []divisible = new bool[n];

    // To store the maximum required count
    int res = 0;

    // For every element of the array
    for (int i = n - 1; i > 0; i--)
    {

        // If the current element is
        // divisible by any element
        // on its right
        if (divisible[i])
            continue;

        // Find the count of element
        // on the left which are divisible
        // by the current element
        int cnt = 0;
        for (int j = 0; j < i; j++)
        {

            // If arr[j] is divisible then
            // set divisible[j] to true
            if ((arr[j] % arr[i]) == 0)
            {
                divisible[j] = true;
                cnt++;
            }
        }

        // Update the maximum required count
        res = Math.Max(res, cnt);
    }
    return res;
}

// Driver code
public static void Main(String[] args)
{
    int []arr = { 8, 1, 28, 4, 2, 6, 7 };
    int n = arr.Length;

    Console.WriteLine(findMax(arr, n));
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// JavaScript implementation of the approach

// Function to return the maximum count
// of required elements
function findMax(arr, n)
{

    // divisible[i] will store true
    // if arr[i] is divisible by
    // any element on its right
    var divisible = Array(n).fill(false);

    // To store the maximum required count
    var res = 0;

    // For every element of the array
    for (var i = n - 1; i > 0; i--) {

        // If the current element is
        // divisible by any element
        // on its right
        if (divisible[i])
            continue;

        // Find the count of element
        // on the left which are divisible
        // by the current element
        var cnt = 0;
        for (var j = 0; j < i; j++) {

            // If arr[j] is divisible then
            // set divisible[j] to true
            if ((arr[j] % arr[i]) == 0) {
                divisible[j] = true;
                cnt++;
            }
        }

        // Update the maximum required count
        res = Math.max(res, cnt);
    }

    return res;
}

// Driver code
var arr = [8, 1, 28, 4, 2, 6, 7];
var n = arr.length;
document.write( findMax(arr, n));

</script>
```

**Output:** 

```
3
```
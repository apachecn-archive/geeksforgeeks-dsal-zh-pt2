# 最小化所需的奖励计数，使得较小的值在相邻对中获得较少的奖励

> 原文:[https://www . geeksforgeeks . org/最大限度地减少所需奖品的数量，使得价值较小的元素获得的奖品少于相邻的价值较大的元素/](https://www.geeksforgeeks.org/minimize-the-number-of-prizes-required-such-that-elements-with-smaller-value-gets-less-prizes-than-adjacent-greater-ones/)

给定一个长度为 **N** 的数组 **arr[]** ，任务是找到所需的最小奖品数量，这样如果两个元素相邻，则具有较小值的元素获得的奖品数量少于其相邻的具有较大值的元素。
**注:**每个元素至少获得一次奖励。

**示例:**

> **输入:** arr[] = {1，2，2，3}
> **输出:** 6
> **说明:**
> 索引{0}处的元素将获得{1}奖励。
> 索引{1}处的元素将获得{2}份奖品。
> 索引{2}处的元素将获得{1}份奖品。
> 索引{3}处的元素将获得{2}份奖品。
> 那么，满足
> 上述条件所需的奖品总数为 6 个
> 
> **输入:** arr[] = {3，2，2，1}
> **输出:** 6
> **说明:**
> 索引{0}处的元素将获得{2}奖励。
> 索引{1}处的元素将获得{1}份奖品。
> 索引{2}处的元素将获得{2}份奖品。
> 索引{3}处的元素将获得{1}份奖品。
> 那么，满足
> 上述条件所需的奖品总数为 6 个

**天真方法:**遍历数组的元素，对于数组的每个元素，在元素的左边找到连续的较小元素，在索引的右边找到连续的较小元素。

> 索引 I 处的奖励=最大值(左边连续的较小元素，右边连续的较小元素，1)

下面是上述方法的实现:

## C++

```
// C++ implementation to find the
// minimum prizes required such
// that adjacent smaller elements
// gets less number of prizes

#include <bits/stdc++.h>

using namespace std;

// Function to find the minimum
// number of required such that
// adjacent smaller elements gets
// less number of prizes
int findMinPrizes(int arr[], int n)
{
    int totalPrizes = 0, j, x, y;

    // Loop to iterate over every
    // elements of the array
    for (int i = 0; i < n; i++) {
        x = 1;
        j = i;

        // Loop to find the consecutive
        // smaller elements at left
        while (j > 0 && arr[j] > arr[j - 1]) {
            x++;
            j--;
        }
        j = i;
        y = 1;

        // Loop to find the consecutive
        // smaller elements at right
        while (j < n - 1 && arr[j] > arr[j + 1]) {
            y++;
            j++;
        }

        totalPrizes += max({ x, y });
    }
    cout << totalPrizes << endl;

    return 0;
}

// Driver Code
int main()
{
    int arr[] = { 1, 2, 2, 3 };
    int n = sizeof(arr) / sizeof(arr[0]);

    findMinPrizes(arr, n);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find the
// minimum prizes required such
// that adjacent smaller elements
// gets less number of prizes
import java.util.*;
class GFG{

// Function to find the minimum
// number of required such that
// adjacent smaller elements gets
// less number of prizes
static int findMinPrizes(int arr[], int n)
{
    int totalPrizes = 0, j, x, y;

    // Loop to iterate over every
    // elements of the array
    for (int i = 0; i < n; i++)
    {
        x = 1;
        j = i;

        // Loop to find the consecutive
        // smaller elements at left
        while (j > 0 && arr[j] > arr[j - 1])
        {
            x++;
            j--;
        }
        j = i;
        y = 1;

        // Loop to find the consecutive
        // smaller elements at right
        while (j < n - 1 && arr[j] > arr[j + 1])
        {
            y++;
            j++;
        }

        totalPrizes += Math.max(x, y );
    }
    System.out.print(totalPrizes + "\n");

    return 0;
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 1, 2, 2, 3 };
    int n = arr.length;

    findMinPrizes(arr, n);
}
}

// This code is contributed by gauravrajput1
```

## 蟒蛇 3

```
# Python3 implementation to find the
# minimum prizes required such
# that adjacent smaller elements
# gets less number of prizes

# Function to find the minimum
# number of required such that
# adjacent smaller elements gets
# less number of prizes
def findMinPrizes(arr, n):

    totalPrizes = 0

    # Loop to iterate over every
    # elements of the array
    for i in range(n):
        x = 1
        j = i

        # Loop to find the consecutive
        # smaller elements at left
        while (j > 0 and arr[j] > arr[j - 1]):
            x += 1
            j -= 1

        j = i
        y = 1

        # Loop to find the consecutive
        # smaller elements at right
        while (j < n - 1 and arr[j] >
                             arr[j + 1]):
            y += 1
            j += 1

        totalPrizes += max(x, y)

    print(totalPrizes)

# Driver code
arr = [ 1, 2, 2, 3 ]
n = len(arr)

findMinPrizes(arr, n)

# This code is contributed by stutipathak31jan
```

## C#

```
// C# implementation to find the
// minimum prizes required such
// that adjacent smaller elements
// gets less number of prizes
using System;

class GFG{

// Function to find the minimum
// number of required such that
// adjacent smaller elements gets
// less number of prizes
static int findMinPrizes(int []arr, int n)
{
    int totalPrizes = 0, j, x, y;

    // Loop to iterate over every
    // elements of the array
    for(int i = 0; i < n; i++)
    {
        x = 1;
        j = i;

        // Loop to find the consecutive
        // smaller elements at left
        while (j > 0 && arr[j] > arr[j - 1])
        {
            x++;
            j--;
        }
        j = i;
        y = 1;

        // Loop to find the consecutive
        // smaller elements at right
        while (j < n - 1 &&
          arr[j] > arr[j + 1])
        {
            y++;
            j++;
        }
        totalPrizes += Math.Max(x, y);
    }
    Console.Write(totalPrizes + "\n");

    return 0;
}

// Driver Code
public static void Main(String[] args)
{
    int []arr = { 1, 2, 2, 3 };
    int n = arr.Length;

    findMinPrizes(arr, n);
}
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>

    // Javascript implementation to find the
    // minimum prizes required such
    // that adjacent smaller elements
    // gets less number of prizes 

    // Function to find the minimum
    // number of required such that
    // adjacent smaller elements gets
    // less number of prizes
    function findMinPrizes(arr, n)
    {
        let totalPrizes = 0, j, x, y;

        // Loop to iterate over every
        // elements of the array
        for (let i = 0; i < n; i++) {
            x = 1;
            j = i;

            // Loop to find the consecutive
            // smaller elements at left
            while (j > 0 && arr[j] > arr[j - 1]) {
                x++;
                j--;
            }
            j = i;
            y = 1;

            // Loop to find the consecutive
            // smaller elements at right
            while (j < n - 1 && arr[j] > arr[j + 1]) {
                y++;
                j++;
            }

            totalPrizes += Math.max( x, y );
        }
        document.write(totalPrizes);

        return 0;
    }

    let arr = [ 1, 2, 2, 3 ];
    let n = arr.length;
    findMinPrizes(arr, n);

    // This code is contributed by divyesh072019.
</script>
```

**Output:** 

```
6
```

**性能分析:**

*   **时间复杂度:** *O(N <sup>2</sup> )*
*   **辅助空间:** *O(1)*

**有效方法:**想法是为数组的每个元素预先计算左右连续较小元素的[计数。这意味着，如果左边的元素较小，那么该元素左边的所有较小元素也将小于当前元素。即](https://www.geeksforgeeks.org/find-the-nearest-smaller-numbers-on-left-side-in-an-array/)

```
if (arr[i-1] < arr[i])
    smallerLeft[i] = smallerLeft[i-1] + 1
```

类似地，可以使用以下事实来计算连续的较小元素:如果右边的元素大于当前元素，那么右边的连续的较大元素也将大于当前元素。即

```
if (arr[i] < arr[i+1])
    smallerRight[i] = smallerRight[i+1] + 1
```

下面是上述方法的实现:

## C++

```
// C++ implementation to find the
// minimum prizes required such
// that adjacent smaller elements
// gets less number of prizes

#include <bits/stdc++.h>

using namespace std;

// Function to find the minimum
// number of required such that
// adjacent smaller elements gets
// less number of prizes
int minPrizes(int arr[], int n)
{
    int dpLeft[n];

    dpLeft[0] = 1;

    // Loop to compute the smaller
    // elements at the left
    for (int i = 1; i < n; i++) {

        if (arr[i] > arr[i - 1]) {

            dpLeft[i] = dpLeft[i - 1] + 1;
        }
        else {

            dpLeft[i] = 1;
        }
    }

    int dpRight[n];

    dpRight[n - 1] = 1;

    // Loop to find the smaller
    // elements at the right
    for (int i = n - 2; i >= 0; i--) {

        if (arr[i] > arr[i + 1]) {

            dpRight[i] = dpRight[i + 1] + 1;
        }
        else {

            dpRight[i] = 1;
        }
    }

    int totalPrizes = 0;

    // Loop to find the minimum
    // prizes required
    for (int i = 0; i < n; i++) {

        totalPrizes += max(dpLeft[i],
                           dpRight[i]);
    }
    cout << totalPrizes << endl;

    return 0;
}

// Driver Code
int main()
{
    int arr[] = { 1, 2, 2, 3 };
    int n = sizeof(arr) / sizeof(arr[0]);

    minPrizes(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find the
// minimum prizes required such
// that adjacent smaller elements
// gets less number of prizes
import java.util.*;

class GFG{

// Function to find the minimum
// number of required such that
// adjacent smaller elements gets
// less number of prizes
static int minPrizes(int arr[], int n)
{
    int []dpLeft = new int[n];

    dpLeft[0] = 1;

    // Loop to compute the smaller
    // elements at the left
    for(int i = 1; i < n; i++)
    {
        if (arr[i] > arr[i - 1])
        {
            dpLeft[i] = dpLeft[i - 1] + 1;
        }
        else
        {
            dpLeft[i] = 1;
        }
    }

    int []dpRight = new int[n];

    dpRight[n - 1] = 1;

    // Loop to find the smaller
    // elements at the right
    for(int i = n - 2; i >= 0; i--)
    {
        if (arr[i] > arr[i + 1])
        {
            dpRight[i] = dpRight[i + 1] + 1;
        }
        else
        {
            dpRight[i] = 1;
        }
    }

    int totalPrizes = 0;

    // Loop to find the minimum
    // prizes required
    for(int i = 0; i < n; i++)
    {
        totalPrizes += Math.max(dpLeft[i],
                               dpRight[i]);
    }
    System.out.print(totalPrizes + "\n");
    return 0;
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 1, 2, 2, 3 };
    int n = arr.length;

    minPrizes(arr, n);
}
}

// This code is contributed by Amit Katiyar
```

## 蟒蛇 3

```
# Python3 implementation to find the
# minimum prizes required such
# that adjacent smaller elements
# gets less number of prizes

# Function to find the minimum
# number of required such that
# adjacent smaller elements gets
# less number of prizes
def minPrizes(arr, n):

    dpLeft = [0] * n
    dpLeft[0] = 1

    # Loop to compute the smaller
    # elements at the left
    for i in range(n):
        if arr[i] > arr[i - 1]:
            dpLeft[i] = dpLeft[i - 1] + 1

        else:
            dpLeft[i] = 1

    dpRight = [0] * n
    dpRight[-1] = 1

    # Loop to find the smaller
    # elements at the right
    for i in range(n - 2, -1, -1):
        if arr[i] > arr[i + 1]:
            dpRight[i] = dpRight[i + 1] + 1

        else:
            dpRight[i] = 1

    totalPrizes = 0

    # Loop to find the minimum
    # prizes required
    for i in range(n):
        totalPrizes += max(dpLeft[i],
                           dpRight[i])

    print(totalPrizes)

# Driver code
arr = [ 1, 2, 2, 3 ]
n = len(arr)

minPrizes(arr, n)

# This code is contributed by stutipathak31jan
```

## C#

```
// C# implementation to find the
// minimum prizes required such
// that adjacent smaller elements
// gets less number of prizes
using System;

class GFG{

// Function to find the minimum
// number of required such that
// adjacent smaller elements gets
// less number of prizes
static int minPrizes(int []arr, int n)
{
    int []dpLeft = new int[n];

    dpLeft[0] = 1;

    // Loop to compute the smaller
    // elements at the left
    for(int i = 1; i < n; i++)
    {
        if (arr[i] > arr[i - 1])
        {
            dpLeft[i] = dpLeft[i - 1] + 1;
        }
        else
        {
            dpLeft[i] = 1;
        }
    }

    int []dpRight = new int[n];

    dpRight[n - 1] = 1;

    // Loop to find the smaller
    // elements at the right
    for(int i = n - 2; i >= 0; i--)
    {
        if (arr[i] > arr[i + 1])
        {
            dpRight[i] = dpRight[i + 1] + 1;
        }
        else
        {
            dpRight[i] = 1;
        }
    }

    int totalPrizes = 0;

    // Loop to find the minimum
    // prizes required
    for(int i = 0; i < n; i++)
    {
        totalPrizes += Math.Max(dpLeft[i],
                               dpRight[i]);
    }
    Console.Write(totalPrizes + "\n");
    return 0;
}

// Driver Code
public static void Main(String[] args)
{
    int []arr = { 1, 2, 2, 3 };
    int n = arr.Length;

    minPrizes(arr, n);
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// Javascript implementation to find the
// minimum prizes required such
// that adjacent smaller elements
// gets less number of prizes

// Function to find the minimum
// number of required such that
// adjacent smaller elements gets
// less number of prizes
function minPrizes(arr, n)
{
    let dpLeft = new Array(n);

    dpLeft[0] = 1;

    // Loop to compute the smaller
    // elements at the left
    for(let i = 1; i < n; i++)
    {
        if (arr[i] > arr[i - 1])
        {
            dpLeft[i] = dpLeft[i - 1] + 1;
        }
        else
        {
            dpLeft[i] = 1;
        }
    }

    let dpRight = new Array(n);

    dpRight[n - 1] = 1;

    // Loop to find the smaller
    // elements at the right
    for(let i = n - 2; i >= 0; i--)
    {
        if (arr[i] > arr[i + 1])
        {
            dpRight[i] = dpRight[i + 1] + 1;
        }
        else
        {
            dpRight[i] = 1;
        }
    }

    let totalPrizes = 0;

    // Loop to find the minimum
    // prizes required
    for(let i = 0; i < n; i++)
    {
        totalPrizes += Math.max(dpLeft[i],
                               dpRight[i]);
    }
    document.write(totalPrizes + "</br>");
    return 0;
}

// Driver code
let arr = [ 1, 2, 2, 3 ];
let n = arr.length;

minPrizes(arr, n);

// This code is contributed by suresh07

</script>
```

**Output:** 

```
6
```

**性能分析:**

*   **时间复杂度:** *O(N)*
*   **辅助空间:**T2【O(N)
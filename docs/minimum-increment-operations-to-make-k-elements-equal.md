# 使 K 个元素相等的最小增量操作

> 原文:[https://www . geesforgeks . org/minimum-increment-operations-to-make-k-elements-equal/](https://www.geeksforgeeks.org/minimum-increment-operations-to-make-k-elements-equal/)

给定一个由 **N** 元素组成的数组**arr【】**和一个整数 **K** ，任务是通过只执行增量操作使数组中的任何 **K** 元素相等，即在一次操作中，任何元素都可以增加 1。找出使任何 **K** 元素相等所需的最小操作次数。
**举例:**

> **输入:** arr[] = {3，1，9，100}，K = 3
> **输出:**14
> 6 次加 1 8 次，共
> 14 次运算，使 3 个元素等于 9。
> **输入:** arr[] = {5，3，10，5}，K = 2
> **输出:** 0
> 不需要操作，因为第一个和最后一个
> 元素已经相等。

**天真的做法:**

1.  按升序对数组进行排序。
2.  现在选择 **K** 元素并使它们相等。
3.  选择**I<sup>th</sup>T3【值】作为最大值，并使所有小于它的元素等于**I<sup>th</sup>T7】元素。****
4.  计算使所有 **i** 元素的 **K** 元素等于 **i <sup>第</sup>T5】元素所需的操作次数。**
5.  答案是所有可能性中最小的一个。

这种方法的时间复杂度将是 **O(n*K + nlogn)** 。
**高效方法:**考虑到使**1<sup>ST</sup>****K**元素等于**K**元素所需的操作，可以在恒定时间内使用[滑动窗口技术](https://www.geeksforgeeks.org/window-sliding-technique/)修改天真方法以计算使 **K** 元素等于**I<sup>th</sup>T10】元素比 **O(K)** 快所需的最小操作
让 **C** 成为使**【l，l+K–1】**范围内的元素等于**(l+K–1)<sup>第</sup>** 元素所需的操作或成本。现在要找到范围**【l+1，l+K】**的成本，可以使用范围**【l，l+K–1】**的解决方案。
让 **C'** 成为**【l+1，l+K】**范围的成本。** 

1.  由于我们将**l<sup>th</sup>T3【元素】增加到**(l+K–1)<sup>th</sup>**元素， **C** 包含成本元素(l+K–1)–元素(l)，但 **C'** 不需要包含此成本。
    所以，**C’= C –(元素(l+k–1)–元素(l))**** 
2.  现在**C’**代表使**【l+1，l+K–1】**范围内所有元素等于**(l+K–1)<sup>第</sup>** 个元素的成本。
    由于我们需要使所有元素等于 **(l + K) <sup>第</sup>** 个元素而不是**(l + K–1)<sup>第</sup>** 个元素，因此我们可以将这些**K–1**个元素递增到 **(l + K) <sup>第</sup>** 个元素，从而使**C ' = C '+(K–1)*(元素(l+K)**

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the minimum number of
// increment operations required to make
// any k elements of the array equal
int minOperations(vector<int> ar, int k)
{
    // Sort the array in increasing order
    sort(ar.begin(), ar.end());

    // Calculate the number of operations
    // needed to make 1st k elements equal to
    // the kth element i.e. the 1st window
    int opsNeeded = 0;
    for (int i = 0; i < k; i++) {
        opsNeeded += ar[k - 1] - ar[i];
    }

    // Answer will be the minimum of all
    // possible k sized windows
    int ans = opsNeeded;

    // Find the operations needed to make
    // k elements equal to ith element
    for (int i = k; i < ar.size(); i++) {

        // Slide the window to the right and
        // subtract increments spent on leftmost
        // element of the previous window
        opsNeeded = opsNeeded - (ar[i - 1] - ar[i - k]);

        // Add increments needed to make the 1st k-1
        // elements of this window equal to the
        // kth element of the current window
        opsNeeded += (k - 1) * (ar[i] - ar[i - 1]);
        ans = min(ans, opsNeeded);
    }
    return ans;
}

// Driver code
int main()
{
    vector<int> arr = { 3, 1, 9, 100 };
    int n = arr.size();
    int k = 3;

    cout << minOperations(arr, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.Arrays;

class geeksforgeeks {

// Function to return the minimum number of
// increment operations required to make
// any k elements of the array equal
static int minOperations(int ar[], int k)
{
    // Sort the array in increasing order
    Arrays.sort(ar);

    // Calculate the number of operations
    // needed to make 1st k elements equal to
    // the kth element i.e. the 1st window
    int opsNeeded = 0;
    for (int i = 0; i < k; i++) {
        opsNeeded += ar[k - 1] - ar[i];
    }

    // Answer will be the minimum of all
    // possible k sized windows
    int ans = opsNeeded;

    // Find the operations needed to make
    // k elements equal to ith element
    for (int i = k; i < ar.length; i++) {

        // Slide the window to the right and
        // subtract increments spent on leftmost
        // element of the previous window
        opsNeeded = opsNeeded - (ar[i - 1] - ar[i - k]);

        // Add increments needed to make the 1st k-1
        // elements of this window equal to the
        // kth element of the current window
        opsNeeded += (k - 1) * (ar[i] - ar[i - 1]);
        ans = Math.min(ans, opsNeeded);
    }
    return ans;
}

// Driver code
public static void main(String[] args)
{
    int[] arr = { 3, 1, 9, 100 };
    int n = arr.length;
    int k = 3;

    System.out.printf("%d",minOperations(arr, k));
}
}

// This code is contributed by Atul_kumar_Shrivastava
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the minimum number of
# increment operations required to make
# any k elements of the array equal
def minOperations(ar, k):

    # Sort the array in increasing order
    ar = sorted(ar)

    # Calculate the number of operations
    # needed to make 1st k elements equal to
    # the kth element i.e. the 1st window
    opsNeeded = 0
    for i in range(k):
        opsNeeded += ar[k - 1] - ar[i]

    # Answer will be the minimum of all
    # possible k sized windows
    ans = opsNeeded

    # Find the operations needed to make
    # k elements equal to ith element
    for i in range(k, len(ar)):

        # Slide the window to the right and
        # subtract increments spent on leftmost
        # element of the previous window
        opsNeeded = opsNeeded - (ar[i - 1] - ar[i - k])

        # Add increments needed to make the 1st k-1
        # elements of this window equal to the
        # kth element of the current window
        opsNeeded += (k - 1) * (ar[i] - ar[i - 1])
        ans = min(ans, opsNeeded)

    return ans

# Driver code
arr = [3, 1, 9, 100]
n = len(arr)
k = 3

print(minOperations(arr, k))

# This code is contributed by Mohit Kumar
```

## C#

```
// C# implementation of the approach
using System;

class geeksforgeeks {

// Function to return the minimum number of
// increment operations required to make
// any k elements of the array equal
static int minOperations(int[] ar, int k)
{
    // Sort the array in increasing order
    Array.Sort(ar);

    // Calculate the number of operations
    // needed to make 1st k elements equal to
    // the kth element i.e. the 1st window
    int opsNeeded = 0;
    for (int i = 0; i < k; i++) {
        opsNeeded += ar[k - 1] - ar[i];
    }

    // Answer will be the minimum of all
    // possible k sized windows
    int ans = opsNeeded;

    // Find the operations needed to make
    // k elements equal to ith element
    for (int i = k; i < ar.Length; i++) {

        // Slide the window to the right and
        // subtract increments spent on leftmost
        // element of the previous window
        opsNeeded = opsNeeded - (ar[i - 1] - ar[i - k]);

        // Add increments needed to make the 1st k-1
        // elements of this window equal to the
        // kth element of the current window
        opsNeeded += (k - 1) * (ar[i] - ar[i - 1]);
        ans = Math.Min(ans, opsNeeded);
    }
    return ans;
}

// Driver code
public static void Main()
{
    int[] arr = { 3, 1, 9, 100 };
    int n = arr.Length;
    int k = 3;

    Console.Write(minOperations(arr, k));
}
}

// This code is contributed by AbhiThakur
```

## java 描述语言

```
<script>

// JavaScript implementation of the approach

// Function to return the minimum number of
// increment operations required to make
// any k elements of the array equal
function minOperations(ar,k)
{
    // Sort the array in increasing order
    ar.sort(function(a,b){return a-b});

    // Calculate the number of operations
    // needed to make 1st k elements equal to
    // the kth element i.e. the 1st window
    let opsNeeded = 0;
    for (let i = 0; i < k; i++) {
        opsNeeded += ar[k - 1] - ar[i];
    }

    // Answer will be the minimum of all
    // possible k sized windows
    let ans = opsNeeded;

    // Find the operations needed to make
    // k elements equal to ith element
    for (let i = k; i < ar.length; i++) {

        // Slide the window to the right and
        // subtract increments spent on leftmost
        // element of the previous window
        opsNeeded = opsNeeded - (ar[i - 1] - ar[i - k]);

        // Add increments needed to make the 1st k-1
        // elements of this window equal to the
        // kth element of the current window
        opsNeeded += (k - 1) * (ar[i] - ar[i - 1]);
        ans = Math.min(ans, opsNeeded);
    }
    return ans;
}

// Driver code
let arr=[3, 1, 9, 100 ];
let n = arr.length;
let k = 3;
document.write(minOperations(arr, k));

// This code is contributed by patel2127

</script>
```

**Output:** 

```
14
```

**时间复杂度:** O(nlogn)
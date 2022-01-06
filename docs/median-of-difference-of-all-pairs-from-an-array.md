# 一个数组中所有对的差值的中值

> 原文:[https://www . geesforgeks . org/数组中所有对的差异中位数/](https://www.geeksforgeeks.org/median-of-difference-of-all-pairs-from-an-array/)

给定一个长度为 **N** 的数组 **arr[]** ，任务是找到所有数组元素对的差值的中值。

**示例:**

> **输入:** arr[] = {1，2，3，4}
> **输出:** 1
> **解释:**
> 给定数组中所有对的差为{ 2–1，3–2，4–3，3–1，4–2，4–1 } = { 1，1，2，2，3}。
> 由于数组包含 6 个元素，中值是差数组索引 3 处的元素。
> 所以，答案是 1。
> **输入:** arr[] = {1，3，5}
> **输出:** 2
> **说明:**差阵为{2，2，4}。因此，中位数是 2。

**天真方法:**任务是[从给定数组](https://www.geeksforgeeks.org/find-all-pairs-possible-from-the-given-array/)中生成所有可能的对，并计算数组中每对的差值 **arr[]** 并将它们存储在数组 **diff[]** 中。排序 **diff[]** 找到中间元素。
***时间复杂度:**O(N<sup>2</sup>* log(N<sup>2</sup>)*
***辅助空间:** O(N <sup>2</sup> )*

**高效方式:**上述方式可以使用[二分搜索法](https://www.geeksforgeeks.org/binary-search/)和[排序](https://www.geeksforgeeks.org/sorting-algorithms/)进行优化。按照以下步骤解决问题:

*   给定数组排序。
*   初始化**低=0** 和**高=arr[N-1]-arr[0]** 。
*   计算中间等于**(低+高)/ 2** 。
*   计算小于**中间**的差异数。如果超过差阵的中值指数，**【上限(N *(N–1)/2)】**，则更新**高**为**中-1**。否则，将**低**更新为**中+ 1** 。
*   重复以上步骤，直到**低**和**高**相等。

下面是上面的实现方法:

## C++

```
// C++ Program to implement
// the above approach
#include <bits/stdc++.h>
#define ll long long
using namespace std;

// Function check if mid can be median
// index of the difference array
bool possible(ll mid, vector<ll>& a)
{

    // Size of the array
    ll n = a.size();

    // Total possible no of pair
    // possible
    ll total = (n * (n - 1)) / 2;

    // The index of the element in the
    // difference of all pairs
    // from the array
    ll need = (total + 1) / 2;

    ll count = 0;
    ll start = 0, end = 1;

    // Count the number of pairs
    // having difference <= mid
    while (end < n) {

        if (a[end] - a[start] <= mid) {
            end++;
        }
        else {
            count += (end - start - 1);
            start++;
        }
    }

    // If the difference between end
    // and first element is less then
    // or equal to mid
    if (end == n && start < end
        && a[end - 1] - a[start] <= mid) {

        ll t = end - start - 1;

        count += (t * (t + 1) / 2);
    }

    // Checking for the no of element less than
    // or equal to mid is greater than median or
    // not
    if (count >= need)
        return true;
    else
        return false;
}

// Function to calculate the median
// of differences of all pairs
// from the array
ll findMedian(vector<ll>& a)
{

    // Size of the array
    ll n = a.size();

    // Initialising the low and high
    ll low = 0, high = a[n - 1] - a[0];

    // Binary search
    while (low <= high) {

        // Calculate mid
        ll mid = (low + high) / 2;

        // If mid can be the median
        // of the array
        if (possible(mid, a))
            high = mid - 1;
        else
            low = mid + 1;
    }

    // Returning the median of the
    // differences of pairs from
    // the array
    return high + 1;
}

// Driver Code
int main()
{

    vector<ll> a = { 1, 7, 5, 2 };

    sort(a.begin(), a.end());

    cout << findMedian(a) << endl;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;

class GFG{

// Function check if mid can be median
// index of the difference array
static boolean possible(long mid, int[] a)
{

    // Size of the array
    long n = a.length;

    // Total possible no of pair
    // possible
    long total = (n * (n - 1)) / 2;

    // The index of the element in the
    // difference of all pairs
    // from the array
    long need = (total + 1) / 2;

    long count = 0;
    long start = 0, end = 1;

    // Count the number of pairs
    // having difference <= mid
    while (end < n)
    {
        if (a[(int)end] - a[(int)start] <= mid)
        {
            end++;
        }
        else
        {
            count += (end - start - 1);
            start++;
        }
    }

    // If the difference between end
    // and first element is less then
    // or equal to mid
    if (end == n && start < end &&
        a[(int)end - 1] - a[(int)start] <= mid)
    {
        long t = end - start - 1;
        count += (t * (t + 1) / 2);
    }

    // Checking for the no of element less than
    // or equal to mid is greater than median or
    // not
    if (count >= need)
        return true;
    else
        return false;
}

// Function to calculate the median
// of differences of all pairs
// from the array
static long findMedian(int[] a)
{

    // Size of the array
    long n = a.length;

    // Initialising the low and high
    long low = 0, high = a[(int)n - 1] - a[0];

    // Binary search
    while (low <= high)
    {

        // Calculate mid
        long mid = (low + high) / 2;

        // If mid can be the median
        // of the array
        if (possible(mid, a))
            high = mid - 1;
        else
            low = mid + 1;
    }

    // Returning the median of the
    // differences of pairs from
    // the array
    return high + 1;

}

// Driver code
public static void main (String[] args)
{
    int[] a = { 1, 7, 5, 2 };

    Arrays.sort(a);

    System.out.println(findMedian(a));
}
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function check if mid can be median
# index of the difference array
def possible(mid, a):

    # Size of the array
    n = len(a);

    # Total possible no of pair
    # possible
    total = (n * (n - 1)) // 2;

    # The index of the element in the
    # difference of all pairs
    # from the array
    need = (total + 1) // 2;

    count = 0;
    start = 0; end = 1;

    # Count the number of pairs
    # having difference <= mid
    while (end < n):
        if (a[end] - a[start] <= mid):
            end += 1;

        else:
            count += (end - start - 1);
            start += 1;

    # If the difference between end
    # and first element is less then
    # or equal to mid
    if (end == n and start < end and
      a[end - 1] - a[start] <= mid):
        t = end - start - 1;

        count += (t * (t + 1) // 2);

    # Checking for the no of element
    # less than or equal to mid is
    # greater than median or not
    if (count >= need):
        return True;
    else:
        return False;

# Function to calculate the median
# of differences of all pairs
# from the array
def findMedian(a):

    # Size of the array
    n = len(a);

    # Initialising the low and high
    low = 0; high = a[n - 1] - a[0];

    # Binary search
    while (low <= high):

        # Calculate mid
        mid = (low + high) // 2;

        # If mid can be the median
        # of the array
        if (possible(mid, a)):
            high = mid - 1;
        else :
            low = mid + 1;

    # Returning the median of the
    # differences of pairs from
    # the array
    return high + 1;

# Driver Code
if __name__ == "__main__" :

    a = [ 1, 7, 5, 2 ];

    a.sort()

    print(findMedian(a));

# This code is contributed by AnkitRai01
```

## C#

```
// C# program to implement
// the above approach
using System;

class GFG{

// Function check if mid can be median
// index of the difference array
static bool possible(long mid, int[] a)
{

    // Size of the array
    long n = a.Length;

    // Total possible no of pair
    // possible
    long total = (n * (n - 1)) / 2;

    // The index of the element in the
    // difference of all pairs
    // from the array
    long need = (total + 1) / 2;

    long count = 0;
    long start = 0, end = 1;

    // Count the number of pairs
    // having difference <= mid
    while (end < n)
    {
        if (a[(int)end] - a[(int)start] <= mid)
        {
            end++;
        }
        else
        {
            count += (end - start - 1);
            start++;
        }
    }

    // If the difference between end
    // and first element is less then
    // or equal to mid
    if (end == n && start < end &&
          a[(int)end - 1] - a[(int)start] <= mid)
    {
        long t = end - start - 1;
        count += (t * (t + 1) / 2);
    }

    // Checking for the no of element less than
    // or equal to mid is greater than median or
    // not
    if (count >= need)
        return true;
    else
        return false;
}

// Function to calculate the median
// of differences of all pairs
// from the array
static long findMedian(int[] a)
{

    // Size of the array
    long n = a.Length;

    // Initialising the low and high
    long low = 0, high = a[(int)n - 1] - a[0];

    // Binary search
    while (low <= high)
    {

        // Calculate mid
        long mid = (low + high) / 2;

        // If mid can be the median
        // of the array
        if (possible(mid, a))
            high = mid - 1;
        else
            low = mid + 1;
    }

    // Returning the median of the
    // differences of pairs from
    // the array
    return high + 1;
}

// Driver code
public static void Main (string[] args)
{
    int[] a = { 1, 7, 5, 2 };

    Array.Sort(a);

    Console.Write(findMedian(a));
}
}

// This code is contributed by rutvik_56
```

## java 描述语言

```
<script>

// Javascript Program to implement
// the above approach

// Function check if mid can be median
// index of the difference array
function possible(mid, a)
{

    // Size of the array
    let n = a.length;

    // Total possible no of pair
    // possible
    let total = parseInt((n * (n - 1)) / 2);

    // The index of the element in the
    // difference of all pairs
    // from the array
    let need = parseInt((total + 1) / 2);

    let count = 0;
    let start = 0, end = 1;

    // Count the number of pairs
    // having difference <= mid
    while (end < n) {

        if (a[end] - a[start] <= mid) {
            end++;
        }
        else {
            count += (end - start - 1);
            start++;
        }
    }

    // If the difference between end
    // and first element is less then
    // or equal to mid
    if (end == n && start < end
        && a[end - 1] - a[start] <= mid) {

        let t = end - start - 1;

        count += parseInt(t * (t + 1) / 2);
    }

    // Checking for the no of element less than
    // or equal to mid is greater than median or
    // not
    if (count >= need)
        return true;
    else
        return false;
}

// Function to calculate the median
// of differences of all pairs
// from the array
function findMedian(a)
{

    // Size of the array
    let n = a.length;

    // Initialising the low and high
    let low = 0, high = a[n - 1] - a[0];

    // Binary search
    while (low <= high) {

        // Calculate mid
        let mid = (low + high) / 2;

        // If mid can be the median
        // of the array
        if (possible(mid, a))
            high = mid - 1;
        else
            low = mid + 1;
    }

    // Returning the median of the
    // differences of pairs from
    // the array
    return high + 1;
}

// Driver Code

    let a = [ 1, 7, 5, 2 ];

    a.sort();

    document.write(findMedian(a));

</script>
```

**输出:**

```
3
```

***时间复杂度:** O(N*log(M))，其中 N 为元素个数，M 为数组元素对之间的最大差值。*
***辅助空间:** O(1)*
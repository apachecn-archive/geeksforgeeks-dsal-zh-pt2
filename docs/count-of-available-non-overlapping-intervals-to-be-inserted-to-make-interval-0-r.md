# 要插入的可用非重叠间隔的计数，以形成间隔[0，R]

> 原文:[https://www . geeksforgeeks . org/可用计数-非重叠-要插入的间隔-制作间隔-0-r/](https://www.geeksforgeeks.org/count-of-available-non-overlapping-intervals-to-be-inserted-to-make-interval-0-r/)

给定一个整数 **R** ，表示范围**【0，R】**和两个数组**开始[]** 和**结束[]** ，大小为 **N** ，表示范围【0，R】中的开始和结束间隔。任务是计算需要插入到数组中的可用非重叠间隔的数量，以便在合并数组中的各个范围时**开始[]** 和**结束[]** ，合并的间隔变为[0，R]。

**示例:**

> **输入:** R = 10，N = 3，开始[] = {2，5，8}，结束[] = {3，9，10}
> **输出:** 2
> **解释:**
> 范围{[2，3]，[5，10]}由数组给出。为了使合并的间隔变为[0，R]，应该插入并合并范围[0，2]和[3，5]。因此，需要在数组中插入两个范围。
> 
> **输入:** R = 8，N = 2，开始[] = {2，6}，结束[] = {3，7}
> **输出:** 3
> **解释:**
> 范围{[2，3]，[6，7]}由数组给出。为了使合并的间隔变为[0，R]，应该插入并合并范围[0，2]，[3，6]和[7，8]。因此，需要在数组中插入三个范围。

**做法:**思路是用[排序](https://www.geeksforgeeks.org/sorting-algorithms/)解决问题。

*   最初，给定的两个数组都被排序，以便使用的间隔聚集在一起。
*   现在，数组以排序的方式迭代(即，一个指针指向**开始**的开始，另一个指针指向**结束**的开始。
*   如果当前开始元素较小，则表示正在查看新的时间间隔，如果当前结束索引较小，则表示正在退出当前时间间隔。
*   在此过程中，存储当前活动间隔的计数。如果在任何时候当前活动计数为 0，则有一个可用的时间间隔。因此，可用时间间隔的计数会增加。
*   这样，两个数组都被迭代。

下面是上述方法的实现:

## C++

```
// C++ implementation of the above approach

#include <iostream>
using namespace std;

// The following two functions
// are used to sort the array.
// QuickSort is being implemented in
// the following functions

// Function to find the pivot index
int partition(int arr[], int l, int h)
{
    int pivot = arr[l];
    int i = l + 1;
    int j = h;

    while (i <= j) {

        while (i <= h
               && arr[i] < pivot) {
            i++;
        }

        while (j > l
               && arr[j] > pivot) {
            j--;
        }

        if (i < j) {

            int temp = arr[i];
            arr[i] = arr[j];
            arr[j] = temp;
            i++;
            j--;
        }
        else
            i++;
    }

    arr[l] = arr[j];
    arr[j] = pivot;
    return j;
}

// Function to implement Quick Sort
void sortArray(int arr[], int l, int h)
{
    if (l >= h)
        return;

    // Pivot is pointing to pivot index
    // before which every element
    // is smaller and after pivot,
    // every element is greater
    int pivot = partition(arr, l, h);

    // Sort the array before pivot element
    sortArray(arr, l, pivot - 1);

    // Sort the array after pivot element
    sortArray(arr, pivot + 1, h);
}

// Function to count the available intervals
// from the given range of numbers
int findMaxIntervals(int start[], int end[],
                     int n, int R)
{
    int ans = 0;
    int prev = 0;
    int currActive = 0;
    int i = 0;
    int j = 0;

    // If range starts after 0
    // then an interval is available
    // from 0 to start[0]
    if (start[0] > 0)
        ans++;

    while (i < n && j < n) {
        // When a new interval starts
        if (start[i] < end[j]) {

            // Since index variable i is being
            // incremented, the current active
            // interval will also get incremented
            i++;
            currActive++;
        }

        // When the current interval ends
        else if (start[i] > end[j]) {

            // Since index variable j is being
            // decremented, the currect active
            // interval will also get decremented
            j++;
            currActive--;
        }

        // When start and end both are same
        // there is no change in currActive
        else {
            i++;
            j++;
        }
        if (currActive == 0) {
            ans++;
        }
    }

    // If the end of interval
    // is before the range
    // so interval is available
    // at the end
    if (end[n - 1] < R)
        ans++;
    return ans;
}

// Driver code
int main()
{
    int R, N;
    R = 10;
    N = 3;
    int start[N] = { 2, 5, 8 };
    int end[N] = { 3, 9, 10 };

    // Sort the start array
    sortArray(start, 0, N - 1);

    // Sort the end array
    sortArray(end, 0, N - 1);

    // Calling the function
    cout << findMaxIntervals(
        start, end, N, R);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
import java.util.*;
class GFG{

// The following two functions
// are used to sort the array.
// QuickSort is being implemented in
// the following functions

// Function to find the pivot index
static int partition(int arr[], int l, int h)
{
    int pivot = arr[l];
    int i = l + 1;
    int j = h;

    while (i <= j)
    {
        while (i <= h && arr[i] < pivot)
        {
            i++;
        }

        while (j > l && arr[j] > pivot)
        {
            j--;
        }

        if (i < j)
        {
            int temp = arr[i];
            arr[i] = arr[j];
            arr[j] = temp;
            i++;
            j--;
        }
        else
            i++;
    }

    arr[l] = arr[j];
    arr[j] = pivot;
    return j;
}

// Function to implement Quick Sort
static void sortArray(int arr[], int l, int h)
{
    if (l >= h)
        return;

    // Pivot is pointing to pivot index
    // before which every element
    // is smaller and after pivot,
    // every element is greater
    int pivot = partition(arr, l, h);

    // Sort the array before pivot element
    sortArray(arr, l, pivot - 1);

    // Sort the array after pivot element
    sortArray(arr, pivot + 1, h);
}

// Function to count the available intervals
// from the given range of numbers
static int findMaxIntervals(int start[],
                            int end[],
                            int n, int R)
{
    int ans = 0;
    int prev = 0;
    int currActive = 0;
    int i = 0;
    int j = 0;

    // If range starts after 0
    // then an interval is available
    // from 0 to start[0]
    if (start[0] > 0)
        ans++;

    while (i < n && j < n)
    {
        // When a new interval starts
        if (start[i] < end[j])
        {

            // Since index variable i is being
            // incremented, the current active
            // interval will also get incremented
            i++;
            currActive++;
        }

        // When the current interval ends
        else if (start[i] > end[j])
        {

            // Since index variable j is being
            // decremented, the currect active
            // interval will also get decremented
            j++;
            currActive--;
        }

        // When start and end both are same
        // there is no change in currActive
        else
        {
            i++;
            j++;
        }
        if (currActive == 0)
        {
            ans++;
        }
    }

    // If the end of interval
    // is before the range
    // so interval is available
    // at the end
    if (end[n - 1] < R)
        ans++;
    return ans;
}

// Driver code
public static void main(String args[])
{
    int R, N;
    R = 10;
    N = 3;
    int start[] = new int[]{ 2, 5, 8 };
    int end[] = new int[]{ 3, 9, 10 };

    // Sort the start array
    sortArray(start, 0, N - 1);

    // Sort the end array
    sortArray(end, 0, N - 1);

    // Calling the function
    System.out.print(findMaxIntervals(start, end, N, R));
}
}

// This code is contributed by Code_Mech
```

## 蟒蛇 3

```
# Python3 implementation of the above approach

# The following two functions
# are used to sort the array.
# QuickSort is being implemented in
# the following functions

# Function to find the pivot index
def partition(arr, l, h):

    pivot = arr[l]
    i = l + 1
    j = h

    while (i <= j):
        while (i <= h and arr[i] < pivot):
            i += 1

        while (j > l and arr[j] > pivot):
            j -= 1

        if (i < j):
            temp = arr[i]
            arr[i] = arr[j]
            arr[j] = temp
            i += 1
            j -= 1
        else:
            i += 1

    arr[l] = arr[j]
    arr[j] = pivot
    return j

# Function to implement Quick Sort
def sortArray(arr, l, h):

    if (l >= h):
        return

    # Pivot is pointing to pivot index
    # before which every element
    # is smaller and after pivot,
    # every element is greater
    pivot = partition(arr, l, h)

    # Sort the array before pivot element
    sortArray(arr, l, pivot - 1)

    # Sort the array after pivot element
    sortArray(arr, pivot + 1, h)

# Function to count the available intervals
# from the given range of numbers
def findMaxIntervals(start, end, n, R):

    ans = 0
    prev = 0
    currActive = 0
    i = 0
    j = 0

    # If range starts after 0
    # then an interval is available
    # from 0 to start[0]
    if (start[0] > 0):
        ans += 1

    while (i < n and j < n):

        # When a new interval starts
        if (start[i] < end[j]):

            # Since index variable i is being
            # incremented, the current active
            # interval will also get incremented
            i += 1
            currActive += 1

        # When the current interval ends
        elif (start[i] > end[j]):

            # Since index variable j is being
            # decremented, the currect active
            # interval will also get decremented
            j += 1
            currActive -= 1

        # When start and end both are same
        # there is no change in currActive
        else:
            i += 1
            j += 1
        if (currActive == 0):
            ans += 1

    # If the end of interval
    # is before the range
    # so interval is available
    # at the end
    if (end[n - 1] < R):
        ans += 1
    return ans

# Driver code
if __name__ == '__main__':

    R = 10
    N = 3
    start = [ 2, 5, 8 ]
    end = [ 3, 9, 10 ]

    # Sort the start array
    sortArray(start, 0, N - 1)

    # Sort the end array
    sortArray(end, 0, N - 1)

    # Calling the function
    print(findMaxIntervals(start, end, N, R))

# This code is contributed by Surendra_Gangwar
```

## C#

```
// C# implementation of the above approach
using System;
class GFG{

// The following two functions
// are used to sort the array.
// QuickSort is being implemented in
// the following functions

// Function to find the pivot index
static int partition(int []arr, int l, int h)
{
    int pivot = arr[l];
    int i = l + 1;
    int j = h;

    while (i <= j)
    {
        while (i <= h && arr[i] < pivot)
        {
            i++;
        }

        while (j > l && arr[j] > pivot)
        {
            j--;
        }

        if (i < j)
        {
            int temp = arr[i];
            arr[i] = arr[j];
            arr[j] = temp;
            i++;
            j--;
        }
        else
            i++;
    }

    arr[l] = arr[j];
    arr[j] = pivot;
    return j;
}

// Function to implement Quick Sort
static void sortArray(int []arr, int l, int h)
{
    if (l >= h)
        return;

    // Pivot is pointing to pivot index
    // before which every element
    // is smaller and after pivot,
    // every element is greater
    int pivot = partition(arr, l, h);

    // Sort the array before pivot element
    sortArray(arr, l, pivot - 1);

    // Sort the array after pivot element
    sortArray(arr, pivot + 1, h);
}

// Function to count the available intervals
// from the given range of numbers
static int findMaxIntervals(int []start,
                            int []end,
                            int n, int R)
{
    int ans = 0;
    int prev = 0;
    int currActive = 0;
    int i = 0;
    int j = 0;

    // If range starts after 0
    // then an interval is available
    // from 0 to start[0]
    if (start[0] > 0)
        ans++;

    while (i < n && j < n)
    {
        // When a new interval starts
        if (start[i] < end[j])
        {

            // Since index variable i is being
            // incremented, the current active
            // interval will also get incremented
            i++;
            currActive++;
        }

        // When the current interval ends
        else if (start[i] > end[j])
        {

            // Since index variable j is being
            // decremented, the currect active
            // interval will also get decremented
            j++;
            currActive--;
        }

        // When start and end both are same
        // there is no change in currActive
        else
        {
            i++;
            j++;
        }
        if (currActive == 0)
        {
            ans++;
        }
    }

    // If the end of interval
    // is before the range
    // so interval is available
    // at the end
    if (end[n - 1] < R)
        ans++;
    return ans;
}

// Driver code
public static void Main()
{
    int R, N;
    R = 10;
    N = 3;
    int []start = new int[]{ 2, 5, 8 };
    int []end = new int[]{ 3, 9, 10 };

    // Sort the start array
    sortArray(start, 0, N - 1);

    // Sort the end array
    sortArray(end, 0, N - 1);

    // Calling the function
    Console.Write(findMaxIntervals(start, end, N, R));
}
}

// This code is contributed by Code_Mech
```

## java 描述语言

```
<script>

// Javascript implementation of the above approach

// The following two functions
// are used to sort the array.
// QuickSort is being implemented in
// the following functions

// Function to find the pivot index
function partition(arr, l, h)
{
    let pivot = arr[l];
    let i = l + 1;
    let j = h;

    while (i <= j)
    {
        while (i <= h && arr[i] < pivot)
        {
            i++;
        }

        while (j > l && arr[j] > pivot)
        {
            j--;
        }

        if (i < j)
        {
            let temp = arr[i];
            arr[i] = arr[j];
            arr[j] = temp;
            i++;
            j--;
        }
        else
            i++;
    }

    arr[l] = arr[j];
    arr[j] = pivot;
    return j;
}

// Function to implement Quick Sort
function sortArray(arr, l, h)
{
    if (l >= h)
        return;

    // Pivot is pointing to pivot index
    // before which every element
    // is smaller and after pivot,
    // every element is greater
    let pivot = partition(arr, l, h);

    // Sort the array before pivot element
    sortArray(arr, l, pivot - 1);

    // Sort the array after pivot element
    sortArray(arr, pivot + 1, h);
}

// Function to count the available intervals
// from the given range of numbers
function findMaxIntervals(start,
                            end, n, R)
{
    let ans = 0;
    let prev = 0;
    let currActive = 0;
    let i = 0;
    let j = 0;

    // If range starts after 0
    // then an interval is available
    // from 0 to start[0]
    if (start[0] > 0)
        ans++;

    while (i < n && j < n)
    {
        // When a new interval starts
        if (start[i] < end[j])
        {

            // Since index variable i is being
            // incremented, the current active
            // interval will also get incremented
            i++;
            currActive++;
        }

        // When the current interval ends
        else if (start[i] > end[j])
        {

            // Since index variable j is being
            // decremented, the currect active
            // interval will also get decremented
            j++;
            currActive--;
        }

        // When start and end both are same
        // there is no change in currActive
        else
        {
            i++;
            j++;
        }
        if (currActive == 0)
        {
            ans++;
        }
    }

    // If the end of interval
    // is before the range
    // so interval is available
    // at the end
    if (end[n - 1] < R)
        ans++;
    return ans;
}

// Driver Code

    let R, N;
    R = 10;
    N = 3;
    let start = [ 2, 5, 8 ];
    let end = [ 3, 9, 10 ];

    // Sort the start array
    sortArray(start, 0, N - 1);

    // Sort the end array
    sortArray(end, 0, N - 1);

    // Calling the function
       document.write(findMaxIntervals(start, end, N, R));

</script>
```

**Output:** 

```
2
```
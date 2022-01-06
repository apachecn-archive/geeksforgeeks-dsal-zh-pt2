# 在双离子数组中找到一个元素

> 原文:[https://www.geeksforgeeks.org/find-element-bitonic-array/](https://www.geeksforgeeks.org/find-element-bitonic-array/)

给定 n 个不同元素的双音素序列，编写一个程序，在 O(log n)时间内在双音素序列中找到给定的元素 x。双调和数列是先严格递增后严格递减的数列。

**示例:**

```
Input :  arr[] = {-3, 9, 18, 20, 17, 5, 1};
         key = 20
Output : Found at index 3

Input :  arr[] = {5, 6, 7, 8, 9, 10, 3, 2, 1};
         key = 30
Output : Not Found
```

一个**简单的解决方法**就是做一个[线性搜索](https://www.geeksforgeeks.org/linear-search/)。这个解决方案的时间复杂度是 0(n)。
安**高效解决方案**基于[二分搜索法](https://www.geeksforgeeks.org/binary-search/)。其思想是找到双调和点 k，它是给定序列的最大元素的索引。如果要搜索的元素大于最大元素返回值-1，则搜索两部分的元素。下面是如何做到这一点的逐步算法。

1.  找到给定数组中的双调和点，即给定双调和数组中的最大元素。这可以通过修改二分搜索法算法在对数(n)时间内完成。如何做到这一点，可以参考[这篇](https://www.geeksforgeeks.org/find-the-maximum-element-in-an-array-which-is-first-increasing-and-then-decreasing/)的帖子。
2.  如果要搜索的元素等于位点的元素，则打印位点的索引。
3.  如果要搜索的元素大于在一个比特点的元素，那么该元素在数组中不存在。
4.  如果要搜索的元素少于一个比特点上的元素，那么使用二分搜索法在数组的两半中搜索该元素。

下面是上述想法的实现:

## C++

```
// CPP code to search key in bitonic array
#include <iostream>

using namespace std;

// Function for binary search in ascending part
int ascendingBinarySearch(int arr[], int low,
                        int high, int key)
{
    while (low <= high)
    {
        int mid = low + (high - low) / 2;
        if (arr[mid] == key)
            return mid;
        if (arr[mid] > key)
            high = mid - 1;
        else
            low = mid + 1;
    }
    return -1;
}

// Function for binary search in
// descending part of array
int descendingBinarySearch(int arr[], int low,
                        int high, int key)
{
    while (low <= high)
    {
        int mid = low + (high - low) / 2;
        if (arr[mid] == key)
            return mid;
        if (arr[mid] < key)
            high = mid - 1;
        else
            low = mid + 1;
    }
    return -1;
}

// finding bitonic point
int findBitonicPoint(int arr[], int n,
                    int l, int r)
{
    int mid;
    int bitonicPoint = 0;
    mid = (r + l) / 2;
    if (arr[mid] > arr[mid - 1]
        && arr[mid] > arr[mid + 1])
    {
        return mid;
    }

    else if (arr[mid] > arr[mid - 1]
            && arr[mid] < arr[mid + 1])
    {
        bitonicPoint = findBitonicPoint(arr, n, mid, r);
    }

    else if (arr[mid] < arr[mid - 1]
            && arr[mid] > arr[mid + 1])
    {
        bitonicPoint = findBitonicPoint(arr, n, l, mid);
    }
    return bitonicPoint;
}

// Function to search key in
// bitonic array
int searchBitonic(int arr[], int n,
                int key, int index)
{
    if (key > arr[index])
        return -1;

    else if (key == arr[index])
        return index;

    else {
        int temp
            = ascendingBinarySearch(arr,
                                    0, index - 1,
                                    key);
        if (temp != -1) {
            return temp;
        }

        // Search in right of k
        return descendingBinarySearch(arr,
                                    index + 1,
                                    n - 1,
                                    key);
    }
}

// Driver code
int main()
{
    int arr[] = { -8, 1, 2, 3, 4, 5, -2, -3 };
    int key = 1;
    int n, l, r;
    n = sizeof(arr) / sizeof(arr[0]);
    l = 0;
    r = n - 1;
    int index;

    // Function call
    index = findBitonicPoint(arr, n, l, r);

    int x = searchBitonic(arr, n, key, index);

    if (x == -1)
        cout << "Element Not Found" << endl;
    else
        cout << "Element Found at index " << x << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to search key in bitonic array
public class GFG {

    // Function for binary search
    // in ascending part
    static int ascendingBinarySearch(int arr[],
                                    int low,
                                    int high,
                                    int key)
    {
        while (low <= high)
        {
            int mid = low + (high - low) / 2;
            if (arr[mid] == key)
            {
                return mid;
            }
            if (arr[mid] > key)
            {
                high = mid - 1;
            }
            else
            {
                low = mid + 1;
            }
        }
        return -1;
    }

    // Function for binary search in
    // descending part of array
    static int descendingBinarySearch(int arr[],
                                    int low,
                                    int high,
                                    int key)
    {
        while (low <= high)
        {
            int mid = low + (high - low) / 2;
            if (arr[mid] == key)
            {
                return mid;
            }
            if (arr[mid] < key)
            {
                high = mid - 1;
            }
            else
            {
                low = mid + 1;
            }
        }
        return -1;
    }

    // finding bitonic point
    static int findBitonicPoint(int arr[],
                                int n,
                                int l,
                                int r)
    {
        int mid;
        int bitonicPoint = 0;
        mid = (r + l) / 2;
        if (arr[mid] > arr[mid - 1]
            && arr[mid] > arr[mid + 1])
        {
            return mid;
        }
        else {
            if (arr[mid] > arr[mid - 1]
                && arr[mid] < arr[mid + 1])
            {
                bitonicPoint = findBitonicPoint(arr, n, mid, r);
            }
            else {
                if (arr[mid] < arr[mid - 1]
                    && arr[mid] > arr[mid + 1])
                {
                    bitonicPoint = findBitonicPoint(arr, n, l, mid);
                }
            }
        }
        return bitonicPoint;
    }

    // Function to search key in bitonic array
    static int searchBitonic(int arr[], int n,
                            int key, int index)
    {
        if (key > arr[index])
        {
            return -1;
        }
        else if (key == arr[index])
        {
            return index;
        }
        else {
            int temp = ascendingBinarySearch(
                arr, 0, index - 1, key);
            if (temp != -1)
            {
                return temp;
            }

            // Search in right of k
            return descendingBinarySearch(arr, index + 1,
                                        n - 1, key);
        }
    }

    // Driver code
    public static void main(String args[])
    {
        int arr[] = { -8, 1, 2, 3, 4, 5, -2, -3 };
        int key = 5;
        int n, l, r;
        n = arr.length;
        l = 0;
        r = n - 1;
        int index;
        index = findBitonicPoint(arr, n, l, r);

        int x = searchBitonic(arr, n, key, index);

        if (x == -1) {
            System.out.println("Element Not Found");
        }
        else {
            System.out.println("Element Found at index "
                            + x);
        }
    }
}

/*This code is contributed by 29AjayKumar*/
```

## 蟒蛇 3

```
# Python code to search key in bitonic array

# Function for binary search in ascending part
def ascendingBinarySearch(arr, low, high, key):

    while low <= high:
        mid = low + (high - low) // 2

        if arr[mid] == key:
            return mid

        if arr[mid] > key:
            high = mid - 1
        else:
            low = mid + 1

    return -1

# Function for binary search in descending part of array
def descendingBinarySearch(arr, low, high, key):

    while low <= high:
        mid = low + (high - low) // 2

        if arr[mid] == key:
            return mid

        if arr[mid] < key:
            high = mid - 1
        else:
            low = mid + 1

    return -1

# Find bitonic point
def findBitonicPoint(arr, n, l, r):

    bitonicPoint = 0
    mid = (r + l) // 2

    if arr[mid] > arr[mid-1] and arr[mid] > arr[mid+1]:
        return mid

    elif arr[mid] > arr[mid-1] and arr[mid] < arr[mid+1]:
        bitonicPoint = findBitonicPoint(arr, n, mid, r)
    else:
        bitonicPoint = finsBitonicPoint(arr, n, l, mid)

    return bitonicPoint

# Function to search key in bitonic array
def searchBitonic(arr, n, key, index):

    if key > arr[index]:
        return -1
    elif key == arr[index]:
        return index
    else:
        temp = ascendingBinarySearch(arr, 0, index-1, key)
        if temp != -1:
            return temp

        # search in right of k
        return descendingBinarySearch(arr, index+1, n-1, key)

# Driver code
def main():
    arr = [-8, 1, 2, 3, 4, 5, -2, -3]
    key = 1
    n = len(arr)
    l = 0
    r = n - 1

    # Function call
    index = findBitonicPoint(arr, n, l, r)

    x = searchBitonic(arr, n, key, index)

    if x == -1:
        print("Element Not Found")
    else:
        print("Element Found at index", x)

main()

# This code is contributed by stutipathak31jan
```

## C#

```
// C# code to search key in bitonic array
using System;

class GFG {
    // Function for binary search in ascending part
    static int ascendingBinarySearch(int[] arr, int low,
                                    int high, int key)
    {
        while (low <= high)
        {
            int mid = low + (high - low) / 2;
            if (arr[mid] == key)
            {
                return mid;
            }
            if (arr[mid] > key)
            {
                high = mid - 1;
            }
            else {
                low = mid + 1;
            }
        }
        return -1;
    }

    // Function for binary search in descending part of
    // array
    static int descendingBinarySearch(int[] arr, int low,
                                    int high, int key)
    {
        while (low <= high)
        {
            int mid = low + (high - low) / 2;
            if (arr[mid] == key)
            {
                return mid;
            }
            if (arr[mid] < key)
            {
                high = mid - 1;
            }
            else
            {
                low = mid + 1;
            }
        }
        return -1;
    }

    // finding bitonic point
    static int findBitonicPoint(int[] arr, int n, int l,
                                int r)
    {
        int mid;
        int bitonicPoint = 0;
        mid = (r + l) / 2;
        if (arr[mid] > arr[mid - 1]
            && arr[mid] > arr[mid + 1])
        {
            return mid;
        }
        else
        {
            if (arr[mid] > arr[mid - 1]
                && arr[mid] < arr[mid + 1]) {
                bitonicPoint = findBitonicPoint(arr, n, mid, r);
            }
            else
            {
                if (arr[mid] < arr[mid - 1]
                    && arr[mid] > arr[mid + 1]) {
                    bitonicPoint = findBitonicPoint(arr, n, l, mid);
                }
            }
        }
        return bitonicPoint;
    }

    // Function to search key in bitonic array
    static int searchBitonic(int[] arr, int n, int key,
                            int index)
    {
        if (key > arr[index])
        {
            return -1;
        }
        else if (key == arr[index])
        {
            return index;
        }
        else {
            int temp = ascendingBinarySearch(
                arr, 0, index - 1, key);
            if (temp != -1) {
                return temp;
            }

            // Search in right of k
            return descendingBinarySearch(arr, index + 1,
                                        n - 1, key);
        }
    }

    // Driver Code
    static public void Main()
    {
        int[] arr = { -8, 1, 2, 3, 4, 5, -2, -3 };
        int key = 1;
        int n, l, r;
        n = arr.Length;
        l = 0;
        r = n - 1;
        int index;
        index = findBitonicPoint(arr, n, l, r);

        int x = searchBitonic(arr, n, key, index);

        if (x == -1) {
            Console.WriteLine("Element Not Found");
        }
        else {
            Console.WriteLine("Element Found at index "
                            + x);
        }
    }
}

// This code is contributed by ajit
```

## java 描述语言

```
<script>

// JavaScript code to search key in bitonic array

// Function for binary search in ascending part
function ascendingBinarySearch(arr, low, high, key) {
    while (low <= high) {
        let mid = Math.floor(low + (high - low) / 2);
        if (arr[mid] == key)
            return mid;
        if (arr[mid] > key)
            high = mid - 1;
        else
            low = mid + 1;
    }
    return -1;
}

// Function for binary search in
// descending part of array
function descendingBinarySearch(arr, low, high, key) {
    while (low <= high) {
        let mid = Math.floor(low + (high - low) / 2);
        if (arr[mid] == key)
            return mid;
        if (arr[mid] < key)
            high = mid - 1;
        else
            low = mid + 1;
    }
    return -1;
}

// finding bitonic point
function findBitonicPoint(arr, n, l, r) {
    let mid;
    let bitonicPoint = 0;
    mid = Math.floor((r + l) / 2);
    if (arr[mid] > arr[mid - 1]
        && arr[mid] > arr[mid + 1]) {
        return mid;
    }

    else if (arr[mid] > arr[mid - 1]
        && arr[mid] < arr[mid + 1]) {
        bitonicPoint = findBitonicPoint(arr, n, mid, r);
    }

    else if (arr[mid] < arr[mid - 1]
        && arr[mid] > arr[mid + 1]) {
        bitonicPoint = findBitonicPoint(arr, n, l, mid);
    }
    return bitonicPoint;
}

// Function to search key in
// bitonic array
function searchBitonic(arr, n, key, index) {
    if (key > arr[index])
        return -1;

    else if (key == arr[index])
        return index;

    else {
        let temp
            = ascendingBinarySearch(arr,
                0, index - 1,
                key);
        if (temp != -1) {
            return temp;
        }

        // Search in right of k
        return descendingBinarySearch(arr,
            index + 1,
            n - 1,
            key);
    }
}

// Driver code

let arr = [-8, 1, 2, 3, 4, 5, -2, -3];
let key = 1;
let n, l, r;
n = arr.length;
l = 0;
r = n - 1;
let index;

// Function call
index = findBitonicPoint(arr, n, l, r);

let x = searchBitonic(arr, n, key, index);

if (x == -1)
    document.write("Element Not Found" + "<br>");
else
    document.write("Element Found at index " + x + "<br>");

</script>
```

**Output**

```
Element Found at index 1
```

**时间复杂度**:O(log n)
T3】辅助空间 : O(1)

本文由 **Vaishali Goyal** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。
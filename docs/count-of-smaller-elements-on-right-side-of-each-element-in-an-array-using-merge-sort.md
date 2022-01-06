# 使用合并排序对数组中每个元素右侧的较小元素进行计数

> 原文:[https://www . geesforgeks . org/数组中每个元素右侧的较小元素计数-使用-合并-排序/](https://www.geeksforgeeks.org/count-of-smaller-elements-on-right-side-of-each-element-in-an-array-using-merge-sort/)

给定一个由 **N** 个整数组成的数组 **arr[]** ，任务是计算数组中每个元素右侧较小元素的数量

**示例:**

> **输入:** arr[] = {6，3，7，2}
> **输出:** 2，1，1，0
> **解释:**
> 6 = 2[3，2]
> 后的较小元素 3 = 1[2]
> 7 = 1[2]
> 后的较小元素 2 = 0
> 
> **输入:** arr[] = {6，19，111，13}
> **输出:** 0，1，1，0
> **解释:**
> 6 = 0 后的较小元素
> 19 = 1[13]
> 111 = 1[13]
> 13 = 0 后的较小元素

**方法:**
在合并两个数组时使用[合并排序](https://www.geeksforgeeks.org/merge-sort/)的思想。当较高的索引元素小于较低的索引元素时，表示较高的索引元素小于该较低索引之后的所有元素，因为左侧部分已经排序。因此，将所需计数的较低索引元素之后的所有元素相加。

下面是上述方法的实现

## C++

```
// C++ program to find the count of
// smaller elements on right side of
// each element in an Array
// using Merge sort
#include <bits/stdc++.h>
using namespace std;

const int N = 100001;
int ans[N];

// Utility function that merge the array
// and count smaller element on right side
void merge(pair<int, int> a[], int start,
                int mid, int end)
{
    pair<int, int> f[mid - start + 1],
                   s[end - mid];

    int n = mid - start + 1;
    int m = end - mid;

    for(int i = start; i <= mid; i++)
        f[i - start] = a[i];
    for(int i = mid + 1; i <= end; i++)
        s[i - mid - 1] = a[i];

    int i = 0, j = 0, k = start;
    int cnt = 0;

    // Loop to store the count of smaller
    // Elements on right side when both
    // Array have some elements
    while(i < n && j < m)
    {
        if (f[i].second <= s[j].second)
        {
            ans[f[i].first] += cnt;
            a[k++] = f[i++];
        }
        else
        {
            cnt++;
            a[k++] = s[j++];
        }
    }

    // Loop to store the count of smaller
    // elements in right side when only
    // left array have some element
    while(i < n)
    {
        ans[f[i].first] += cnt;
        a[k++] = f[i++];
    }

    // Loop to store the count of smaller
    // elements in right side when only
    // right array have some element
    while(j < m)
    {
        a[k++] = s[j++];
    }
}

// Function to invoke merge sort.
void mergesort(pair<int, int> item[],
                    int low, int high)
{
    if (low >= high)
        return;

    int mid = (low + high) / 2;
    mergesort(item, low, mid);
    mergesort(item, mid + 1, high);
    merge(item, low, mid, high);
}

// Utility function that prints
// out an array on a line
void print(int arr[], int n)
{
    for(int i = 0; i < n; i++)
        cout << arr[i] << " ";
}

// Driver code.
int main()
{
    int arr[] = { 10, 9, 5, 2, 7,
                   6, 11, 0, 2 };

    int n = sizeof(arr) / sizeof(int);
    pair<int, int> a[n];
    memset(ans, 0, sizeof(ans));

    for(int i = 0; i < n; i++)
    {
        a[i].second = arr[i];
        a[i].first = i;
    }

    mergesort(a, 0, n - 1);
    print(ans, n);

    return 0;
}

// This code is contributed by rishabhtyagi2306
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the count of smaller elements
// on right side of each element in an Array
// using Merge sort

import java.util.*;

public class GFG {

    // Class for storing the index
    // and Value pairs
    class Item {

        int val;
        int index;

        public Item(int val, int index)
        {
            this.val = val;
            this.index = index;
        }
    }

    // Function to count the number of
    // smaller elements on right side
    public ArrayList<Integer> countSmall(int[] A)
    {

        int len = A.length;
        Item[] items = new Item[len];

        for (int i = 0; i < len; i++) {
            items[i] = new Item(A[i], i);
        }

        int[] count = new int[len];
        mergeSort(items, 0, len - 1, count);
        ArrayList<Integer> res = new ArrayList<>();

        for (int i : count) {
            res.add(i);
        }
        return res;
    }

    // Function for Merge Sort
    private void mergeSort(Item[] items,
                           int low, int high,
                           int[] count)
    {

        if (low >= high) {
            return;
        }

        int mid = low + (high - low) / 2;
        mergeSort(items, low, mid, count);
        mergeSort(items, mid + 1, high, count);
        merge(items, low, mid, mid + 1, high, count);
    }

    // Utility function that merge the array
    // and count smaller element on right side
    private void merge(Item[] items, int low,
                       int lowEnd, int high,
                       int highEnd, int[] count)
    {
        int m = highEnd - low + 1;
        Item[] sorted = new Item[m];
        int rightCounter = 0;
        int lowPtr = low, highPtr = high;
        int index = 0;

        // Loop to store the count of smaller
        // Elements on right side when both
        // Array have some elements
        while (lowPtr <= lowEnd && highPtr <= highEnd) {
            if (items[lowPtr].val > items[highPtr].val) {
                rightCounter++;
                sorted[index++] = items[highPtr++];
            }
            else {
                count[items[lowPtr].index] += rightCounter;
                sorted[index++] = items[lowPtr++];
            }
        }

        // Loop to store the count of smaller
        // elements in right side when only
        // left array have some element
        while (lowPtr <= lowEnd) {
            count[items[lowPtr].index] += rightCounter;
            sorted[index++] = items[lowPtr++];
        }

        // Loop to store the count of smaller
        // elements in right side when only
        // right array have some element
        while (highPtr <= highEnd) {
            sorted[index++] = items[highPtr++];
        }

        System.arraycopy(sorted, 0, items, low, m);
    }

    // Utility function that prints
    // out an array on a line
    void printArray(ArrayList<Integer> countList)
    {

        for (Integer i : countList)
            System.out.print(i + " ");

        System.out.println("");
    }

    // Driver Code
    public static void main(String[] args)
    {
        GFG cntSmall = new GFG();
        int arr[] = { 10, 9, 5, 2, 7, 6, 11, 0, 2 };
        int n = arr.length;
        ArrayList<Integer> countList
            = cntSmall.countSmall(arr);
        cntSmall.printArray(countList);
    }
}
```

## 蟒蛇 3

```
# Python3 program to find the count of
# smaller elements on right side of
# each element in an Array
# using Merge sort
N = 100001
ans = [0] * N

# Utility function that merge the array
# and count smaller element on right side
def merge(a, start, mid, end):

    f = [0] * (mid - start + 1)
    s = [0] * (end - mid)

    n = mid - start + 1
    m = end - mid

    for i in range(start, mid + 1):
        f[i - start] = a[i]
    for i in range ( mid + 1, end + 1):
        s[i - mid - 1] = a[i]

    i = 0
    j = 0
    k = start
    cnt = 0

    # Loop to store the count of smaller
    # Elements on right side when both
    # Array have some elements
    while (i < n and j < m):
        if (f[i][1] <= s[j][1]):
            ans[f[i][0]] += cnt
            a[k] = f[i]
            k += 1
            i += 1

        else:
            cnt += 1
            a[k] = s[j]
            k += 1
            j += 1

    # Loop to store the count of smaller
    # elements in right side when only
    # left array have some element
    while (i < n):
        ans[f[i][0]] += cnt
        a[k] = f[i];
        k += 1
        i += 1

    # Loop to store the count of smaller
    # elements in right side when only
    # right array have some element
    while (j < m):
        a[k] = s[j]
        k += 1
        j += 1

# Function to invoke merge sort.
def mergesort(item, low, high):

    if (low >= high):
        return

    mid = (low + high) // 2
    mergesort(item, low, mid)
    mergesort(item, mid + 1, high)
    merge(item, low, mid, high)

# Utility function that prints
# out an array on a line
def print_(arr, n):

    for i in range(n):
        print(arr[i], end = " ")

# Driver code.
if __name__ == "__main__":

    arr = [ 10, 9, 5, 2, 7,
            6, 11, 0, 2 ]

    n = len(arr)
    a = [[0 for x in range(2)]
            for y in range(n)]

    for i in range(n):
        a[i][1] = arr[i]
        a[i][0] = i

    mergesort(a, 0, n - 1)
    print_(ans, n)

# This code is contributed by chitranayal
```

## C#

```
// C# program to find the count of smaller elements
// on right side of each element in an Array
// using Merge sort
using System;
using System.Collections.Generic;

class GFG
{

    // Class for storing the index
    // and Value pairs
    public class Item
    {

        public int val;
        public int index;

        public Item(int val, int index)
        {
            this.val = val;
            this.index = index;
        }
    }

    // Function to count the number of
    // smaller elements on right side
    public List<int> countSmall(int[] A)
    {

        int len = A.Length;
        Item[] items = new Item[len];

        for (int i = 0; i < len; i++)
        {
            items[i] = new Item(A[i], i);
        }

        int[] count = new int[len];
        mergeSort(items, 0, len - 1, count);
        List<int> res = new List<int>();

        foreach (int i in count)
        {
            res.Add(i);
        }
        return res;
    }

    // Function for Merge Sort
    private void mergeSort(Item[] items,
                        int low, int high,
                        int[] count)
    {

        if (low >= high)
        {
            return;
        }

        int mid = low + (high - low) / 2;
        mergeSort(items, low, mid, count);
        mergeSort(items, mid + 1, high, count);
        merge(items, low, mid, mid + 1, high, count);
    }

    // Utility function that merge the array
    // and count smaller element on right side
    private void merge(Item[] items, int low,
                    int lowEnd, int high,
                    int highEnd, int[] count)
    {
        int m = highEnd - low + 1;
        Item[] sorted = new Item[m];
        int rightCounter = 0;
        int lowPtr = low, highPtr = high;
        int index = 0;

        // Loop to store the count of smaller
        // Elements on right side when both
        // Array have some elements
        while (lowPtr <= lowEnd && highPtr <= highEnd)
        {
            if (items[lowPtr].val > items[highPtr].val)
            {
                rightCounter++;
                sorted[index++] = items[highPtr++];
            }
            else
            {
                count[items[lowPtr].index] += rightCounter;
                sorted[index++] = items[lowPtr++];
            }
        }

        // Loop to store the count of smaller
        // elements in right side when only
        // left array have some element
        while (lowPtr <= lowEnd)
        {
            count[items[lowPtr].index] += rightCounter;
            sorted[index++] = items[lowPtr++];
        }

        // Loop to store the count of smaller
        // elements in right side when only
        // right array have some element
        while (highPtr <= highEnd)
        {
            sorted[index++] = items[highPtr++];
        }

        Array.Copy(sorted, 0, items, low, m);
    }

    // Utility function that prints
    // out an array on a line
    void printArray(List<int> countList)
    {

        foreach (int i in countList)
            Console.Write(i + " ");

        Console.WriteLine("");
    }

    // Driver Code
    public static void Main(String[] args)
    {
        GFG cntSmall = new GFG();
        int []arr = { 10, 9, 5, 2, 7, 6, 11, 0, 2 };
        int n = arr.Length;
        List<int> countList
            = cntSmall.countSmall(arr);
        cntSmall.printArray(countList);
    }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript program to find the count of
// smaller elements on right side of each
// element in an Array using Merge sort
let N = 100001;
let ans = new Array(N);

// Utility function that merge the array
// and count smaller element on right side
function merge(a, start, mid, end)
{
    let f = new Array((mid - start + 1));
    let s = new Array(end - mid);
    let n = mid - start + 1;
    let m = end - mid;

    for(let i = start; i <= mid; i++)
        f[i - start] = a[i];
    for(let i = mid + 1; i <= end; i++)
        s[i - mid - 1] = a[i];

    let i = 0, j = 0, k = start;
    let cnt = 0;

    // Loop to store the count of smaller
    // Elements on right side when both
    // Array have some elements
    while(i < n && j < m)
    {
        if (f[i][1] <= s[j][1])
        {
            ans[f[i][0]] += cnt;
            a[k++] = f[i++];
        }
        else
        {
            cnt++;
            a[k++] = s[j++];
        }
    }

    // Loop to store the count of smaller
    // elements in right side when only
    // left array have some element
    while(i < n)
    {
        ans[f[i][0]] += cnt;
        a[k++] = f[i++];
    }

    // Loop to store the count of smaller
    // elements in right side when only
    // right array have some element
    while(j < m)
    {
        a[k++] = s[j++];
    }      
}

// Function to invoke merge sort.
function mergesort(item, low, high)
{
    if (low >= high)
        return;

    let mid = Math.floor((low + high) / 2);
    mergesort(item, low, mid);
    mergesort(item, mid + 1, high);
    merge(item, low, mid, high);
}

// Utility function that prints
// out an array on a line
function print(arr, n)
{
    for(let i = 0; i < n; i++)
        document.write(arr[i] + " ");
}

// Driver Code
let arr = [ 10, 9, 5, 2, 7, 6, 11, 0, 2 ];
let n = arr.length;
let a = new Array(n);
for(let i = 0; i < a.length; i++)
{
    a[i] = new Array(2);
}
for(let i = 0; i < ans.length; i++)
{
    ans[i] = 0;
}

for(let i = 0; i < n; i++)
{
    a[i][1] = arr[i];
    a[i][0] = i;
}
mergesort(a, 0, n - 1);
print(ans, n);

// This code is contributed by rag2127

</script>
```

**Output**

```
7 6 3 1 3 2 2 0 0
```

**时间复杂度:** O(N log N)
**相关文章:** [计算右侧较小元素](https://www.geeksforgeeks.org/count-smaller-elements-on-right-side/)
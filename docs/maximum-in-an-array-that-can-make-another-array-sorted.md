# 一个数组中可以使另一个数组排序的最大值

> 原文:[https://www . geeksforgeeks . org/最大数组中可以生成另一个数组排序的/](https://www.geeksforgeeks.org/maximum-in-an-array-that-can-make-another-array-sorted/)

给定两个数组，其中一个数组几乎被排序，一个元素位于错误的位置，使得数组未排序，任务是用第二个数组中的最大元素交换该元素，该元素可用于使第一个数组被排序。
**例:**

> 输入:arr1 = {1，3，7，4，10}，
> arr2 = {2，1，5，8，9}
> 输出:1 3 7 9 10
> 用 9 交换 4。
> 输入:arr1 = {20，1，23}，
> arr2 = {50，26，7}
> 输出:不可能

**进场:**
1。获取使数组未排序的元素的索引。
2。从第二个数组中获取满足错误索引元素相邻条件的最大元素，即
(i)最大元素> = arr【错误索引-1】
(ii)最大元素< = arr【错误索引+1】如果存在错误索引+1

## C++

```
// C++ program to make array sorted
#include <bits/stdc++.h>
using namespace std;

// Function to check whether there is any
// swappable element present to make the first
// array sorted
bool swapElement(int arr1[], int arr2[], int n)
{

    // wrongIdx is the index of the element
    // which is making the first array unsorted
    int wrongIdx = 0;
    for (int i = 1; i < n; i++) {
        if (arr1[i] < arr1[i - 1])
            wrongIdx = i;

    int maximum = INT_MIN;
    int maxIdx = -1;
    bool res = false;

    // Find the maximum element which satisfies the
    // the above mentioned neighboring conditions
    for (int i = 0; i < n; i++) {
        if (arr2[i] > maximum && arr2[i] >= arr1[wrongIdx - 1]) {
            if (wrongIdx + 1 <= n - 1 &&
                arr2[i] <= arr1[wrongIdx + 1]) {
                maximum = arr2[i];
                maxIdx = i;
                res = true;
            }
        }
    }

    // if res is true then swap the element
    // and make the first array sorted
    if (res)
        swap(arr1[wrongIdx], arr2[maxIdx]);

    return res;
}

// Function to print the sorted array if elements
// are swapped.
void getSortedArray(int arr1[], int arr2[], int n)
{
    if (swapElement(arr1, arr2, n))
        for (int i = 0; i < n; i++)
            cout << arr1[i] << " ";
    else
        cout << "Not Possible" << endl;
}

// Drivers code
int main()
{

    int arr1[] = { 1, 3, 7, 4, 10 };
    int arr2[] = { 2, 1, 6, 8, 9 };

    int n = sizeof(arr1) / sizeof(arr1[0]);

    getSortedArray(arr1, arr2, n);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to make array sorted

class GFG
{

// Function to check whether there
// is any swappable element present
// to make the first array sorted
static boolean swapElement(int[] arr1,
                           int[] arr2, int n)
{

    // wrongIdx is the index of the
    // element which is making the
    // first array unsorted
    int wrongIdx = 0;
    for (int i = 1; i < n; i++)
    {
        if (arr1[i] < arr1[i - 1])
        {
            wrongIdx = i;
        }
    }
    int maximum = Integer.MIN_VALUE;
    int maxIdx = -1;
    boolean res = false;

    // Find the maximum element which
    // satisfies the above mentioned
    // neighboring conditions
    for (int i = 0; i < n; i++)
    {
        if (arr2[i] > maximum &&
            arr2[i] >= arr1[wrongIdx - 1])
        {
            if (wrongIdx + 1 <= n - 1 &&
                arr2[i] <= arr1[wrongIdx + 1])
            {
                maximum = arr2[i];
                maxIdx = i;
                res = true;
            }
        }
    }

    // if res is true then swap
    // the element and make the
    // first array sorted
    if (res)
    {
        swap(arr1, wrongIdx, arr2, maxIdx);
    }

    return res;
}

static void swap(int[] a, int wrongIdx,
                 int[] b, int maxIdx)
{
    int c = a[wrongIdx];
    a[wrongIdx] = b[maxIdx];
    b[maxIdx] = c;
}

// Function to print the sorted
// array if elements are swapped.
static void getSortedArray(int arr1[], 
                           int arr2[], int n)
{
    if (swapElement(arr1, arr2, n))
    {
        for (int i = 0; i < n; i++)
        {
            System.out.print(arr1[i] + " ");
        }
    }
    else
    {
        System.out.println("Not Possible");
    }
}

// Driver code
public static void main(String[] args)
{
    int arr1[] = {1, 3, 7, 4, 10};
    int arr2[] = {2, 1, 6, 8, 9};

    int n = arr1.length;

    getSortedArray(arr1, arr2, n);
}
}

// This code contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to make array sorted
import sys

# Function to check whether there is any
# swappable element present to make the
# first array sorted
def swapElement(arr1, arr2, n) :

    # wrongIdx is the index of the element
    # which is making the first array unsorted
    wrongIdx = 0;
    for i in range(1, n) :
        if (arr1[i] < arr1[i - 1]) :
            wrongIdx = i

    maximum = -(sys.maxsize - 1)
    maxIdx = -1
    res = False

    # Find the maximum element which satisfies 
    # the above mentioned neighboring conditions
    for i in range(n) :
        if (arr2[i] > maximum and
            arr2[i] >= arr1[wrongIdx - 1]) :
            if (wrongIdx + 1 <= n - 1 and
                arr2[i] <= arr1[wrongIdx + 1]) :
                maximum = arr2[i]
                maxIdx = i
                res = True

    # if res is true then swap the element
    # and make the first array sorted
    if (res) :
        (arr1[wrongIdx],
         arr2[maxIdx]) = (arr2[maxIdx],
                          arr1[wrongIdx])

    return res

# Function to print the sorted array
# if elements are swapped.
def getSortedArray(arr1, arr2, n) :

    if (swapElement(arr1, arr2, n)) :

        for i in range(n) :
            print(arr1[i], end = " ")
    else :
        print("Not Possible")

# Driver code
if __name__ == "__main__" :

    arr1 = [ 1, 3, 7, 4, 10 ]
    arr2 = [ 2, 1, 6, 8, 9 ]

    n = len(arr1)

    getSortedArray(arr1, arr2, n)

# This code is contributed by Ryuga
```

## C#

```
// C# program to make array sorted
using System;

class GFG
{

// Function to check whether there
// is any swappable element present
// to make the first array sorted
static bool swapElement(int[] arr1,
                        int[] arr2, int n)
{

    // wrongIdx is the index of the
    // element which is making the
    // first array unsorted
    int wrongIdx = 0;
    for (int i = 1; i < n; i++)
    {
        if (arr1[i] < arr1[i - 1])
        {
            wrongIdx = i;
        }
    }
    int maximum = int.MinValue;
    int maxIdx = -1;
    bool res = false;

    // Find the maximum element which
    // satisfies the above mentioned
    // neighboring conditions
    for (int i = 0; i < n; i++)
    {
        if (arr2[i] > maximum && arr2[i] >= arr1[wrongIdx - 1])
        {
            if (wrongIdx + 1 <= n - 1 &&
                     arr2[i] <= arr1[wrongIdx + 1])
            {
                maximum = arr2[i];
                maxIdx = i;
                res = true;
            }
        }
    }

    // if res is true then swap the element
    // and make the first array sorted
    if (res)
    {
        swap(arr1, wrongIdx, arr2, maxIdx);
    }

    return res;
}

static void swap(int[] a, int wrongIdx,
                 int[] b, int maxIdx)
{
    int c = a[wrongIdx];
    a[wrongIdx] = b[maxIdx];
    b[maxIdx] = c;
}

// Function to print the sorted array
// if elements are swapped.
static void getSortedArray(int []arr1,
                           int []arr2, int n)
{
    if (swapElement(arr1, arr2, n))
    {
        for (int i = 0; i < n; i++)
        {
            Console.Write(arr1[i] + " ");
        }
    }
    else
    {
        Console.Write("Not Possible");
    }
}

// Driver Code
public static void Main()
{
    int []arr1 = {1, 3, 7, 4, 10};
    int []arr2 = {2, 1, 6, 8, 9};

    int n = arr1.Length;

    getSortedArray(arr1, arr2, n);
}
}

// This code is contributed
// by PrinciRaj1992
```

## java 描述语言

```
<script>
    // Javascript program to make array sorted

    // Function to check whether there
    // is any swappable element present
    // to make the first array sorted
    function swapElement(arr1, arr2, n)
    {

        // wrongIdx is the index of the
        // element which is making the
        // first array unsorted
        let wrongIdx = 0;
        for (let i = 1; i < n; i++)
        {
            if (arr1[i] < arr1[i - 1])
            {
                wrongIdx = i;
            }
        }
        let maximum = Number.MIN_VALUE;
        let maxIdx = -1;
        let res = false;

        // Find the maximum element which
        // satisfies the above mentioned
        // neighboring conditions
        for (let i = 0; i < n; i++)
        {
            if (arr2[i] > maximum && arr2[i] >= arr1[wrongIdx - 1])
            {
                if (wrongIdx + 1 <= n - 1 &&
                         arr2[i] <= arr1[wrongIdx + 1])
                {
                    maximum = arr2[i];
                    maxIdx = i;
                    res = true;
                }
            }
        }

        // if res is true then swap the element
        // and make the first array sorted
        if (res)
        {
            swap(arr1, wrongIdx, arr2, maxIdx);
        }

        return res;
    }

    function swap(a, wrongIdx, b, maxIdx)
    {
        let c = a[wrongIdx];
        a[wrongIdx] = b[maxIdx];
        b[maxIdx] = c;
    }

    // Function to print the sorted array
    // if elements are swapped.
    function getSortedArray(arr1, arr2, n)
    {
        if (swapElement(arr1, arr2, n))
        {
            for (let i = 0; i < n; i++)
            {
                document.write(arr1[i] + " ");
            }
        }
        else
        {
            document.write("Not Possible");
        }
    }

    let arr1 = [1, 3, 7, 4, 10];
    let arr2 = [2, 1, 6, 8, 9];

    let n = arr1.length;

    getSortedArray(arr1, arr2, n);

    // This code is contributed by decode2207.
</script>
```

**Output:** 

```
1 3 7 9 10
```
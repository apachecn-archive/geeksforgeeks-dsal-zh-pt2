# 合并排序与 O(1)额外空间合并和 O(n lg n)时间【仅限无符号整数】

> 原文:[https://www . geesforgeks . org/merge-sort-with-O1-extra-space-merge-on-LG-n-time/](https://www.geeksforgeeks.org/merge-sort-with-o1-extra-space-merge-and-on-lg-n-time/)

我们已经讨论了[合并排序](https://www.geeksforgeeks.org/merge-sort/)。如何修改算法，使合并在 O(1)个额外空间工作，算法在 O(n Log n)个时间内仍然工作。我们可以假设输入值只是整数。

**示例:**

```
Input : 5 4 3 2 1
Output : 1 2 3 4 5

Input : 999 612 589 856 56 945 243
Output : 56 243 589 612 856 945 999
```

对于整数类型，合并排序可以使用一些模数和除法的数学技巧就地进行。这意味着在一个索引中存储两个元素值，并且可以使用模数和除法提取。

首先，我们必须找到一个大于数组所有元素的值。现在我们可以把初始值存储为模，第二个值存储为除。假设我们想将 **arr[i]** 和 **arr[j]** 都存储在索引 I(表示在 arr[i]中)。首先我们必须找到一个大于 arr[i]和 arr[j]的**‘maxval’**。现在我们可以存储为**arr[I]= arr[I]+arr[j]* maxval**。现在 **arr[i]%maxval** 将给出 arr[i]的初始值， **arr[i]/maxval** 将给出 arr[j]的值。下面是合并排序的实现。

**进场:** *(欧几里德除法)*

> 被除数=除数*商+余数

> 例:5/3 = q:1，r:2 应用欧几里德:3*1+2 =>5(被除数)
> 
> 除数= maxele(数组中的绝对 max 元素)+1(这样我们总是得到非零余数)
> 商= min(第一，第二)
> 余数=原始元素
> 
> 注意:(获取当前元素时，假设当前容器已经有编码元素，因此使用%除数)
> 第一个= arr[i] %除数
> 第二个= arr[j] %除数
> 
> 编码元素=余数+商*除数

**合并中可能出现的问题:**

1.如果当前数字是整数。MAX 然后通常大于当前元素的新编码值将导致整数溢出和数据损坏(在 python 中，数字大小没有限制，因此不会出现此问题)。

2.不处理负数(例如，当用另一个-ve 数字(选择最小的)编码一个-ve 数字(当前)时，符号不能被保留，因为两个数字都有-ve 符号。此外，在计算被除数=除数*商+余数(除数= maxele，商=最小，余数=原始)时，必须使用绝对值，并且必须恢复符号，但由于符号保留问题，它可能无法工作。

3.仅适用于无符号整数，如通常非负的索引。

4.AUX = O(n)在最坏的情况下，假设在 python 这样的语言中，字/整数大小没有限制，当输入数组元素几乎为 integer 时。MAX，那么编码值将可能需要 2x 位空间来表示新的数字，2x 位空间整体上可以变成+1x 数组大小，这几乎就像创建一个 AUX 数组，但以间接的方式。

5.mod 和除法运算是最昂贵的，因此降低了整体性能(在某种程度上)。

## C++

```
// C++ program to sort an array using merge sort such
// that merge operation takes O(1) extra space.
#include <bits/stdc++.h>
using namespace std;
void merge(int arr[], int beg, int mid, int end, int maxele)
{
    int i = beg;
    int j = mid + 1;
    int k = beg;
    while (i <= mid && j <= end) {
        if (arr[i] % maxele <= arr[j] % maxele) {
            arr[k] = arr[k] + (arr[i] % maxele) * maxele;
            k++;
            i++;
        }
        else {
            arr[k] = arr[k] + (arr[j] % maxele) * maxele;
            k++;
            j++;
        }
    }
    while (i <= mid) {
        arr[k] = arr[k] + (arr[i] % maxele) * maxele;
        k++;
        i++;
    }
    while (j <= end) {
        arr[k] = arr[k] + (arr[j] % maxele) * maxele;
        k++;
        j++;
    }

    // Obtaining actual values
    for (int i = beg; i <= end; i++)
        arr[i] = arr[i] / maxele;
}

// Recursive merge sort with extra parameter, naxele
void mergeSortRec(int arr[], int beg, int end, int maxele)
{
    if (beg < end) {
        int mid = (beg + end) / 2;
        mergeSortRec(arr, beg, mid, maxele);
        mergeSortRec(arr, mid + 1, end, maxele);
        merge(arr, beg, mid, end, maxele);
    }
}

// This functions finds max element and calls recursive
// merge sort.
void mergeSort(int arr[], int n)
{
   int maxele = *max_element(arr, arr+n) + 1;
   mergeSortRec(arr, 0, n-1, maxele);
}

int main()
{
    int arr[] = { 999, 612, 589, 856, 56, 945, 243 };
    int n = sizeof(arr) / sizeof(arr[0]);

    mergeSort(arr, n);

    cout << "Sorted array \n";
    for (int i = 0; i < n; i++)
        cout << arr[i] << " ";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to sort an array
// using merge sort such that
// merge operation takes O(1)
// extra space.
import java.util.Arrays;

class GFG
{

    static void merge(int[] arr, int beg,
                        int mid, int end,
                        int maxele)
    {
        int i = beg;
        int j = mid + 1;
        int k = beg;
        while (i <= mid && j <= end)
        {
            if (arr[i] % maxele <=
                arr[j] % maxele)
            {
                arr[k] = arr[k] + (arr[i]
                        % maxele) * maxele;
                k++;
                i++;
            }
            else
            {
                arr[k] = arr[k] +
                        (arr[j] % maxele)
                        * maxele;
                k++;
                j++;
            }
        }
        while (i <= mid)
        {
            arr[k] = arr[k] + (arr[i]
                    % maxele) * maxele;
            k++;
            i++;
        }
        while (j <= end)
        {
            arr[k] = arr[k] + (arr[j]
                    % maxele) * maxele;
            k++;
            j++;
        }

        // Obtaining actual values
        for (i = beg; i <= end; i++)
        {
            arr[i] = arr[i] / maxele;
        }
    }

    // Recursive merge sort
    // with extra parameter, naxele
    static void mergeSortRec(int[] arr, int beg,
            int end, int maxele)
    {
        if (beg < end)
        {
            int mid = (beg + end) / 2;
            mergeSortRec(arr, beg,
                        mid, maxele);
            mergeSortRec(arr, mid + 1,
                        end, maxele);
            merge(arr, beg, mid,
                    end, maxele);
        }
    }

    // This functions finds
    // max element and calls
    // recursive merge sort.
    static void mergeSort(int[] arr, int n)
    {
        int maxele = Arrays.stream(arr).max().getAsInt() + 1;
        mergeSortRec(arr, 0, n - 1, maxele);
    }

    // Driver code
    public static void main(String[] args)
    {

        int[] arr = {999, 612, 589,
                    856, 56, 945, 243};
        int n = arr.length;

        mergeSort(arr, n);

        System.out.println("Sorted array ");
        for (int i = 0; i < n; i++)
        {
            System.out.print(arr[i] + " ");
        }
    }
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to sort an array using
# merge sort such that merge operation
# takes O(1) extra space.
def merge(arr, beg, mid, end, maxele):

    i = beg
    j = mid + 1
    k = beg

    while (i <= mid and j <= end):
        if (arr[i] % maxele <= arr[j] % maxele):
            arr[k] = arr[k] + (arr[i] %
                    maxele) * maxele
            k += 1
            i += 1
        else:
            arr[k] = arr[k] + (arr[j] %
                    maxele) * maxele
            k += 1
            j += 1

    while (i <= mid):
        arr[k] = arr[k] + (arr[i] %
                maxele) * maxele
        k += 1
        i += 1
    while (j <= end):
        arr[k] = arr[k] + (arr[j] %
                maxele) * maxele
        k += 1
        j += 1

    # Obtaining actual values
    for i in range(beg, end + 1):
        arr[i] = arr[i] // maxele

# Recursive merge sort with extra
# parameter, naxele
def mergeSortRec(arr, beg, end, maxele):

    if (beg < end):
        mid = (beg + end) // 2
        mergeSortRec(arr, beg, mid, maxele)
        mergeSortRec(arr, mid + 1, end, maxele)
        merge(arr, beg, mid, end, maxele)

# This functions finds max element and
# calls recursive merge sort.
def mergeSort(arr, n):

   maxele = max(arr) + 1
   mergeSortRec(arr, 0, n - 1, maxele)

# Driver Code
if __name__ == '__main__':

    arr = [ 999, 612, 589, 856, 56, 945, 243 ]
    n =  len(arr)
    mergeSort(arr, n)

    print("Sorted array")

    for i in range(n):
        print(arr[i], end = " ")

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program to sort an array
// using merge sort such that
// merge operation takes O(1)
// extra space.
using System;
using System.Linq;

class GFG
{
static void merge(int []arr, int beg,
                  int mid, int end,
                  int maxele)
{
    int i = beg;
    int j = mid + 1;
    int k = beg;
    while (i <= mid && j <= end)
    {
        if (arr[i] %
            maxele <= arr[j] % maxele)
        {
            arr[k] = arr[k] + (arr[i] %
                     maxele) * maxele;
            k++;
            i++;
        }
        else
        {
            arr[k] = arr[k] +
                    (arr[j] % maxele) *
                              maxele;
            k++;
            j++;
        }
    }
    while (i <= mid)
    {
        arr[k] = arr[k] + (arr[i] %
                 maxele) * maxele;
        k++;
        i++;
    }
    while (j <= end)
    {
        arr[k] = arr[k] + (arr[j] %
                 maxele) * maxele;
        k++;
        j++;
    }

    // Obtaining actual values
    for ( i = beg; i <= end; i++)
        arr[i] = arr[i] / maxele;
}

// Recursive merge sort
// with extra parameter, naxele
static void mergeSortRec(int []arr, int beg,
                         int end, int maxele)
{
    if (beg < end)
    {
        int mid = (beg + end) / 2;
        mergeSortRec(arr, beg,
                     mid, maxele);
        mergeSortRec(arr, mid + 1,
                     end, maxele);
        merge(arr, beg, mid,
              end, maxele);
    }
}

// This functions finds
// max element and calls
// recursive merge sort.
static void mergeSort(int []arr, int n)
{
    int maxele = arr.Max() + 1;
    mergeSortRec(arr, 0, n - 1, maxele);
}

//Driver code
public static void Main ()
{
    int []arr = {999, 612, 589,
                 856, 56, 945, 243};
    int n = arr.Length;

    mergeSort(arr, n);

    Console.WriteLine("Sorted array ");
    for (int i = 0; i < n; i++)
        Console.Write( arr[i] + " ");
}
}

// This code is contributed
// by inder_verma.
```

## java 描述语言

```
<script>
// Javascript program to sort an array
// using merge sort such that
// merge operation takes O(1)
// extra space.   

    function merge(arr,beg,mid,end,maxele)
    {
        let i = beg;
        let j = mid + 1;
        let k = beg;
        while (i <= mid && j <= end)
        {
            if (arr[i] % maxele <=
                arr[j] % maxele)
            {
                arr[k] = arr[k] + (arr[i]
                        % maxele) * maxele;
                k++;
                i++;
            }
            else
            {
                arr[k] = arr[k] +
                        (arr[j] % maxele)
                        * maxele;
                k++;
                j++;
            }
        }
        while (i <= mid)
        {
            arr[k] = arr[k] + (arr[i]
                    % maxele) * maxele;
            k++;
            i++;
        }
        while (j <= end)
        {
            arr[k] = arr[k] + (arr[j]
                    % maxele) * maxele;
            k++;
            j++;
        }

        // Obtaining actual values
        for (i = beg; i <= end; i++)
        {
            arr[i] = Math.floor(arr[i] / maxele);
        }
    }

    // Recursive merge sort
    // with extra parameter, naxele
    function mergeSortRec(arr,beg,end,maxele)
    {
        if (beg < end)
        {
            let mid = Math.floor((beg + end) / 2);
            mergeSortRec(arr, beg,
                        mid, maxele);
            mergeSortRec(arr, mid + 1,
                        end, maxele);
            merge(arr, beg, mid,
                    end, maxele);
        }
    }

    // This functions finds
    // max element and calls
    // recursive merge sort.
    function  mergeSort(arr,n)
    {
        let maxele = Math.max(...arr) + 1;
        mergeSortRec(arr, 0, n - 1, maxele);

    }

    // Driver code
    let arr=[999, 612, 589,
                    856, 56, 945, 243];

    let n = arr.length;
    mergeSort(arr, n);

    document.write("Sorted array <br>");
    for (let i = 0; i < n; i++)
        {
            document.write(arr[i] + " ");
        }

// This code is contributed by patel2127
</script>
```

**Output:** 

```
Sorted array 
56 243 589 612 856 945 999
```
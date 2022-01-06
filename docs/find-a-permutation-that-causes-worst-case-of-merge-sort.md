# 找出导致合并排序最坏情况的排列

> 原文:[https://www . geeksforgeeks . org/find-a-排列-原因-最差情况-合并-排序/](https://www.geeksforgeeks.org/find-a-permutation-that-causes-worst-case-of-merge-sort/)

给定一组元素，找出这些元素的哪个排列会导致合并排序的最坏情况。
渐近地，合并排序总是需要 O(n Log n)个时间，但是需要更多比较的情况在实践中一般需要更多的时间。我们基本上需要找到输入元素的排列，当使用典型的合并排序算法进行排序时，这将导致最大数量的比较。

**示例:**

```
Consider the below set of elements 
{1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 
 13, 14, 15, 16}

Below permutation of the set causes 153
comparisons.
{1, 9, 5, 13, 3, 11, 7, 15, 2, 10, 6, 
 14, 4, 12, 8, 16}

And an already sorted permutation causes
30 comparisons. 

See this for a program that counts 
comparisons and shows above results.
```

现在如何获得输入集合并排序的最坏情况输入？

让我们尝试以自下而上的方式构建数组
让排序后的数组为{1，2，3，4，5，6，7，8}。

为了生成合并排序的最坏情况，导致上述排序数组的合并操作应该导致最大的比较。为此，合并操作中涉及的左右子数组应该存储排序数组的替换元素。即左子阵列应该是{1，3，5，7}，右子阵列应该是{2，4，6，8}。现在数组的每个元素都将被比较至少一次，这将导致最大的比较。我们对左右子阵列也应用相同的逻辑。对于阵列{1，3，5，7}，最差的情况是当其左右子阵列分别为{1，5}和{3，7}时，而对于阵列{2，4，6，8}，最差的情况发生在{2，4}和{6，8}时。

**完整算法–**
**生成 orstCase(arr[])**

1.  左右创建两个辅助数组，并在其中存储备用数组元素。
2.  调用左侧子数组的 generatewordstcase:generatewordstcase(左侧)
3.  调用右子数组的 generatewordstcase:generatewordstcase(右)
4.  将左右子阵列的所有元素复制回原始阵列。

下面是这个想法的实现

## C++

```
// C++ program to generate Worst Case
// of Merge Sort
#include <bits/stdc++.h>
using namespace std;

// Function to print an array
void printArray(int A[], int size)
{
    for(int i = 0; i < size; i++)
    {
        cout << A[i] << " ";
    }
    cout << endl;
}

// Function to join left and right subarray
int join(int arr[], int left[], int right[],
         int l, int m, int r)
{
    int i;
    for(i = 0; i <= m - l; i++)
        arr[i] = left[i];

    for(int j = 0; j < r - m; j++)
    {
        arr[i + j] = right[j];
    }
}

// Function to store alternate elements in
// left and right subarray
int split(int arr[], int left[], int right[],
          int l, int m, int r)
{
    for(int i = 0; i <= m - l; i++)
        left[i] = arr[i * 2];

    for(int i = 0; i < r - m; i++)
        right[i] = arr[i * 2 + 1];
}

// Function to generate Worst Case
// of Merge Sort
int generateWorstCase(int arr[], int l,
                      int r)
{
    if (l < r)
    {
        int m = l + (r - l) / 2;

        // Create two auxiliary arrays
        int left[m - l + 1];
        int right[r - m];

        // Store alternate array elements
        // in left and right subarray
        split(arr, left, right, l, m, r);

        // Recurse first and second halves
        generateWorstCase(left, l, m);
        generateWorstCase(right, m + 1, r);

        // Join left and right subarray
        join(arr, left, right, l, m, r);
    }
}

// Driver code
int main()
{

    // Sorted array
    int arr[] = { 1, 2, 3, 4, 5, 6, 7, 8, 9,
                  10, 11, 12, 13, 14, 15, 16 };

    int n = sizeof(arr) / sizeof(arr[0]);

    cout << "Sorted array is \n";
    printArray(arr, n);

    // Generate Worst Case of Merge Sort
    generateWorstCase(arr, 0, n - 1);

    cout << "\nInput array that will result "
         << "in worst case of merge sort is \n";

    printArray(arr, n);

    return 0;
}

// This code is contributed by Mayank Tyagi
```

## C

```
// C program to generate Worst Case of Merge Sort
#include <stdlib.h>
#include <stdio.h>

// Function to print an array
void printArray(int A[], int size)
{
    for (int i = 0; i < size; i++)
        printf("%d ", A[i]);

    printf("\n");
}

// Function to join left and right subarray
int join(int arr[], int left[], int right[],
        int l, int m, int r)
{
    int i; // Used in second loop
    for (i = 0; i <= m - l; i++)
        arr[i] = left[i];

    for (int j = 0; j < r - m; j++)
        arr[i + j] = right[j];
}

// Function to store alternate elements in left
// and right subarray
int split(int arr[], int left[], int right[],
        int l, int m, int r)
{
    for (int i = 0; i <= m - l; i++)
        left[i] = arr[i * 2];

    for (int i = 0; i < r - m; i++)
        right[i] = arr[i * 2 + 1];
}

// Function to generate Worst Case of Merge Sort
int generateWorstCase(int arr[], int l, int r)
{
    if (l < r)
    {
        int m = l + (r - l) / 2;

        // create two auxiliary arrays
        int left[m - l + 1];
        int right[r - m];

        // Store alternate array elements in left
        // and right subarray
        split(arr, left, right, l, m, r);

        // Recurse first and second halves
        generateWorstCase(left, l, m);
        generateWorstCase(right, m + 1, r);

        // join left and right subarray
        join(arr, left, right, l, m, r);
    }
}

// Driver code
int main()
{
    // Sorted array
    int arr[] = { 1, 2, 3, 4, 5, 6, 7, 8, 9,
                10, 11, 12, 13, 14, 15, 16 };
    int n = sizeof(arr) / sizeof(arr[0]);

    printf("Sorted array is \n");
    printArray(arr, n);

    // generate Worst Case of Merge Sort
    generateWorstCase(arr, 0, n - 1);

    printf("\nInput array that will result in "
            "worst case of merge sort is \n");
    printArray(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to generate Worst Case of Merge Sort

import java.util.Arrays;

class GFG
{
    // Function to join left and right subarray
    static void join(int arr[], int left[], int right[],
                    int l, int m, int r)
    {
        int i;
        for (i = 0; i <= m - l; i++)
            arr[i] = left[i];

        for (int j = 0; j < r - m; j++)
            arr[i + j] = right[j];
    }

    // Function to store alternate elements in left
    // and right subarray
    static void split(int arr[], int left[], int right[],
                     int l, int m, int r)
    {
        for (int i = 0; i <= m - l; i++)
            left[i] = arr[i * 2];

        for (int i = 0; i < r - m; i++)
            right[i] = arr[i * 2 + 1];
    }

    // Function to generate Worst Case of Merge Sort
    static void generateWorstCase(int arr[], int l, int r)
    {
        if (l < r)
        {
            int m = l + (r - l) / 2;

            // create two auxiliary arrays
            int[] left = new int[m - l + 1];
            int[] right = new int[r - m];

            // Store alternate array elements in left
            // and right subarray
            split(arr, left, right, l, m, r);

            // Recurse first and second halves
            generateWorstCase(left, l, m);
            generateWorstCase(right, m + 1, r);

            // join left and right subarray
            join(arr, left, right, l, m, r);
        }
    }

    // driver program
    public static void main (String[] args)
    {
        // sorted array
        int arr[] = { 1, 2, 3, 4, 5, 6, 7, 8, 9,
                      10, 11, 12, 13, 14, 15, 16 };
        int n = arr.length;
        System.out.println("Sorted array is");
        System.out.println(Arrays.toString(arr));

        // generate Worst Case of Merge Sort
        generateWorstCase(arr, 0, n - 1);

        System.out.println("\nInput array that will result in \n"+
             "worst case of merge sort is \n");

        System.out.println(Arrays.toString(arr));
    }
}

// Contributed by Pramod Kumar
```

## C#

```
// C# program to generate Worst Case of
// Merge Sort
using System;

class GFG {

    // Function to join left and right subarray
    static void join(int []arr, int []left,
              int []right, int l, int m, int r)
    {
        int i;
        for (i = 0; i <= m - l; i++)
            arr[i] = left[i];

        for (int j = 0; j < r - m; j++)
            arr[i + j] = right[j];
    }

    // Function to store alternate elements in
    // left and right subarray
    static void split(int []arr, int []left,
            int []right, int l, int m, int r)
    {
        for (int i = 0; i <= m - l; i++)
            left[i] = arr[i * 2];

        for (int i = 0; i < r - m; i++)
            right[i] = arr[i * 2 + 1];
    }

    // Function to generate Worst Case of
    // Merge Sort
    static void generateWorstCase(int []arr,
                                int l, int r)
    {
        if (l < r)
        {
            int m = l + (r - l) / 2;

            // create two auxiliary arrays
            int[] left = new int[m - l + 1];
            int[] right = new int[r - m];

            // Store alternate array elements
            // in left and right subarray
            split(arr, left, right, l, m, r);

            // Recurse first and second halves
            generateWorstCase(left, l, m);
            generateWorstCase(right, m + 1, r);

            // join left and right subarray
            join(arr, left, right, l, m, r);
        }
    }

    // driver program
    public static void Main ()
    {

        // sorted array
        int []arr = { 1, 2, 3, 4, 5, 6, 7, 8, 9,
                    10, 11, 12, 13, 14, 15, 16 };

        int n = arr.Length;
        Console.Write("Sorted array is\n");

        for(int i = 0; i < n; i++)
            Console.Write(arr[i] + " ");

        // generate Worst Case of Merge Sort
        generateWorstCase(arr, 0, n - 1);

        Console.Write("\nInput array that will "
                  + "result in \n worst case of"
                         + " merge sort is \n");

        for(int i = 0; i < n; i++)
            Console.Write(arr[i] + " ");
    }
}

// This code is contributed by Smitha
```

## java 描述语言

```
<script>
    // javascript program to generate Worst Case
    // of Merge Sort

    // Function to print an array
    function printArray(A,size)
    {
        for(let i = 0; i < size; i++)
        {
            document.write(A[i] + " ");
        }

    }

    // Function to join left and right subarray
    function join(arr,left,right,l,m,r)
    {
        let i;
        for(i = 0; i <= m - l; i++)
            arr[i] = left[i];

        for(let j = 0; j < r - m; j++)
        {
            arr[i + j] = right[j];
        }
    }

    // Function to store alternate elements in
    // left and right subarray
      function split(arr,left,right,l,m,r)
    {
        for(let i = 0; i <= m - l; i++)
            left[i] = arr[i * 2];

        for(let i = 0; i < r - m; i++)
            right[i] = arr[i * 2 + 1];
    }

    // Function to generate Worst Case
    // of Merge Sort
    function generateWorstCase(arr,l,r)
    {
        if (l < r)
        {
            let m = l + parseInt((r - l) / 2, 10);

            // Create two auxiliary arrays
            let left = new Array(m - l + 1);
            let right = new Array(r - m);
            left.fill(0);
            right.fill(0);

            // Store alternate array elements
            // in left and right subarray
            split(arr, left, right, l, m, r);

            // Recurse first and second halves
            generateWorstCase(left, l, m);
            generateWorstCase(right, m + 1, r);

            // Join left and right subarray
            join(arr, left, right, l, m, r);
        }
    }

    let arr = [1, 2, 3, 4, 5, 6, 7, 8, 9,
                10, 11, 12, 13, 14, 15, 16 ];   
    let n = arr.length;
    document.write("Sorted array is" + "</br>");
    printArray(arr, n);

    // Generate Worst Case of Merge Sort
    generateWorstCase(arr, 0, n - 1);

    document.write("</br>" + "Input array that will result "
    + "in worst case of merge sort is" + "</br>");

    printArray(arr, n);

    // This code is contributed by vaibhavrabadiya117.
</script>
```

**输出:**

```
Sorted array is 
1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 

Input array that will result in worst 
case of merge sort is 
1 9 5 13 3 11 7 15 2 10 6 14 4 12 8 16 
```

参考资料–[叠加溢出](http://stackoverflow.com/questions/24594112/when-will-the-worst-case-of-merge-sort-occur/24594419#24594419)
本文由**阿迪亚·戈埃尔**供稿。如果您发现任何不正确的地方，请写评论，或者您想分享更多关于上面讨论的主题的信息
# 对名称或字符串数组进行排序的程序

> 原文:[https://www . geesforgeks . org/c-program-sort-array-name-strings/](https://www.geeksforgeeks.org/c-program-sort-array-names-strings/)

给定一个字符串数组，其中所有字符都是相同的大小写，编写一个 C 函数按字母顺序对它们进行排序。

想法是在 C 中使用 [qsort()，编写一个比较函数，使用 strcmp()比较两个字符串。](https://www.geeksforgeeks.org/comparator-function-of-qsort-in-c/)

```
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

// Defining comparator function as per the requirement
static int myCompare(const void* a, const void* b)
{

    // setting up rules for comparison
    return strcmp(*(const char**)a, *(const char**)b);
}

// Function to sort the array
void sort(const char* arr[], int n)
{
    // calling qsort function to sort the array
    // with the help of Comparator
    qsort(arr, n, sizeof(const char*), myCompare);
}

int main()
{

    // Get the array of names to be sorted
    const char* arr[]
        = { "geeksforgeeks", "geeksquiz", "clanguage" };

    int n = sizeof(arr) / sizeof(arr[0]);
    int i;

    // Print the given names
    printf("Given array is\n");
    for (i = 0; i < n; i++)
        printf("%d: %s \n", i, arr[i]);

    // Sort the given names
    sort(arr, n);

    // Print the sorted names
    printf("\nSorted array is\n");
    for (i = 0; i < n; i++)
        printf("%d: %s \n", i, arr[i]);

    return 0;
}
```

**Output:**

```
Given array is
0: geeksforgeeks 
1: geeksquiz 
2: clanguage 

Sorted array is
0: clanguage 
1: geeksforgeeks 
2: geeksquiz

```

如果您发现任何不正确的地方，或者您想分享关于上面讨论的主题的更多信息，请写评论
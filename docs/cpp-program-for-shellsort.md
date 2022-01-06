# 外壳排序的 C++程序

> 原文:[https://www.geeksforgeeks.org/cpp-program-for-shellsort/](https://www.geeksforgeeks.org/cpp-program-for-shellsort/)

在 shellSort 中，我们对数组 h 进行排序，得到一个大的 h 值。我们不断减少 h 的值，直到它变成 1。如果第 h 个元素的所有子列表都被排序，那么这个数组被称为 h 排序的。

```
// C++ implementation of Shell Sort
#include <iostream>

/* function to sort arr using shellSort */
void shellSort(int arr[], int n)
{
    // Start with a big gap, then reduce the gap
    for (int gap = n / 2; gap > 0; gap /= 2) {
        // Do a gapped insertion sort for this gap size.
        // The first gap elements arr[0..gap-1] are already in gapped order
        // keep adding one more element until the entire array is
        // gap sorted
        for (int i = gap; i < n; i += 1) {
            // add arr[i] to the elements that have been gap sorted
            // save arr[i] in temp and make a hole at position i
            int temp = arr[i];

            // shift earlier gap-sorted elements up until the correct
            // location for arr[i] is found
            int j;
            for (j = i; j >= gap && arr[j - gap] > temp; j -= gap)
                arr[j] = arr[j - gap];

            // put temp (the original arr[i]) in its correct location
            arr[j] = temp;
        }
    }
}

void printArray(int arr[], int n)
{
    for (int i = 0; i < n; i++)
        std::cout << arr[i] << " ";
    std::cout << "\n";
}

int main()
{
    int arr[] = { 12, 34, 54, 2, 3 };
    int n = sizeof(arr) / sizeof(arr[0]);

    std::cout << "Array before sorting: \n";
    printArray(arr, n);

    shellSort(arr, n);

    std::cout << "Array after sorting: \n";
    printArray(arr, n);
}
```

**Output:**

```
Array before sorting: 
12 34 54 2 3 
Array after sorting: 
2 3 12 34 54

```

更多详情请参考[外壳排序](https://www.geeksforgeeks.org/shellsort/)完整文章！
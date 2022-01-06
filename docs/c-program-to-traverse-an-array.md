# 遍历数组的 C 程序

> 原文:[https://www . geesforgeks . org/c-程序遍历数组/](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)

给定一个大小为 **N** 的整数数组，任务是遍历并打印[数组](https://www.geeksforgeeks.org/arrays-in-c-cpp/)中的元素。
**例:**

> **输入:** arr[] = {2，-1，5，6，0，-3}
> **输出:** 2 -1 5 6 0 -3
> 
> **输入:** arr[] = {4，0，-2，-9，-7，1}
> 输出: 4 0 -2 -9 -7 1

**进场:-**

1.从 **0** 到 **N-1** 开始循环，这里 **N** 就是阵的大小。

```
for(i = 0; i < N; i++)
```

2.在的帮助下访问数组的每个元素

```
arr[index]
```

3.打印元素。

```
printf("%d ", arr[i])
```

下面是上述方法的实现:

## C

```
// C program to traverse the array

#include <stdio.h>

// Function to traverse and print the array
void printArray(int* arr, int n)
{
    int i;

    printf("Array: ");
    for (i = 0; i < n; i++) {
        printf("%d ", arr[i]);
    }
    printf("\n");
}

// Driver program
int main()
{
    int arr[] = { 2, -1, 5, 6, 0, -3 };
    int n = sizeof(arr) / sizeof(arr[0]);

    printArray(arr, n);

    return 0;
}
```

**Output:** 

```
Array: 2 -1 5 6 0 -3
```

***时间复杂度:** O(n)*

***辅助空间:** O(1)*
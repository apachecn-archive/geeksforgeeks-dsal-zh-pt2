# 用于 Gnome 排序的 C++程序

> 原文:[https://www.geeksforgeeks.org/cpp-program-for-gnome-sort/](https://www.geeksforgeeks.org/cpp-program-for-gnome-sort/)

**算法步骤**

1.  如果你在数组的开始，那么转到右边的元素(从 arr[0]到 arr[1])。
2.  如果当前数组元素大于或等于前一个数组元素，则向右移动一步

```
                   if (arr[i] >= arr[i-1])
                      i++;

```

3.  如果当前数组元素小于前一个数组元素，则交换这两个元素并向后退一步

```
                       if (arr[i] < arr[i-1])
                       {
                           swap(arr[i], arr[i-1]);
                           i--;
                       }

```

4.  重复步骤 2)和 3)，直到“I”到达数组的末尾(即“n-1”)
5.  如果到达数组的末尾，则停止并对数组进行排序。

```
// A C++ Program to implement Gnome Sort
#include <iostream>
using namespace std;

// A function to sort the algorithm using gnome sort
void gnomeSort(int arr[], int n)
{
    int index = 0;

    while (index < n) {
        if (index == 0)
            index++;
        if (arr[index] >= arr[index - 1])
            index++;
        else {
            swap(arr[index], arr[index - 1]);
            index--;
        }
    }
    return;
}

// A utility function ot print an array of size n
void printArray(int arr[], int n)
{
    cout << "Sorted sequence after Gnome sort: ";
    for (int i = 0; i < n; i++)
        cout << arr[i] << " ";
    cout << "\n";
}

// Driver program to test above functions.
int main()
{
    int arr[] = { 34, 2, 10, -9 };
    int n = sizeof(arr) / sizeof(arr[0]);

    gnomeSort(arr, n);
    printArray(arr, n);

    return (0);
}
```

**Output:**

```
Sorted sequence after Gnome sort: -9 2 10 34

```

详情请参考 [Gnome Sort](https://www.geeksforgeeks.org/gnome-sort-a-stupid-one/) 上的完整文章！
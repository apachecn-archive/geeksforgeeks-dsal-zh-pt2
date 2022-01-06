# 循环旋转一个数组的 C++程序

> 原文:[https://www . geesforgeks . org/CPP-逐个程序地循环旋转一个数组/](https://www.geeksforgeeks.org/cpp-program-for-program-to-cyclically-rotate-an-array-by-one/)

给定一个数组，将该数组顺时针旋转 1。

**示例:**

```
Input:  arr[] = {1, 2, 3, 4, 5}
Output: arr[] = {5, 1, 2, 3, 4}
```

以下是步骤。
1)将最后一个元素存储在一个变量中，比如 x。
2)将所有元素向前移动一个位置。
3)将数组的第一个元素替换为 x。

## C++

```
// C++ code for program 
// to cyclically rotate
// an array by one
# include <iostream>
using namespace std;

void rotate(int arr[], int n)
{
    int x = arr[n - 1], i;
    for (i = n - 1; i > 0; i--)
    arr[i] = arr[i - 1]; 
    arr[0] = x;
}

// Driver code
int main() 
{
    int arr[] = {1, 2, 3, 4, 5}, i;
    int n = sizeof(arr) / 
            sizeof(arr[0]);

    cout << "Given array is 
";
    for (i = 0; i < n; i++)
        cout << arr[i] << ' ';

    rotate(arr, n);

    cout << "
Rotated array is
";
    for (i = 0; i < n; i++)
        cout << arr[i] << ' ';

    return 0;
}

// This code is contributed by jit_t
```

**Output**

```
Given array is 
1 2 3 4 5 

Rotated array is
5 1 2 3 4 
```
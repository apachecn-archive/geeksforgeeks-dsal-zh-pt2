# 寻找数组中最大元素的 C++程序

> 原文:[https://www . geesforgeks . org/CPP-逐个程序查找数组中最大的元素/](https://www.geeksforgeeks.org/cpp-program-for-program-to-find-largest-element-in-an-array/)

给定一个数组，找出其中最大的元素。
**例:**

```
Input : arr[] = {10, 20, 4}
Output : 20

Input : arr[] = {20, 10, 20, 4, 100}
Output : 100
```

解决方法是将 max 初始化为第一个元素，然后从第二个元素开始遍历给定的数组，直到结束。对于每个遍历的元素，将其与 max 进行比较，如果大于 max，则更新 max。

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ program to find maximum
// in arr[] of size n 
#include <bits/stdc++.h>
using namespace std;

int largest(int arr[], int n)
{
    int i;

    // Initialize maximum element
    int max = arr[0];

    // Traverse array elements 
    // from second and compare
    // every element with current max 
    for (i = 1; i < n; i++)
        if (arr[i] > max)
            max = arr[i];

    return max;
}

// Driver Code
int main()
{
    int arr[] = {10, 324, 45, 90, 9808};
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << "Largest in given array is " 
         << largest(arr, n);
    return 0;
}

// This Code is contributed 
// by Shivi_Aggarwal
```

**输出:**

```
Largest in given array is 9808
```

**使用库函数:**
我们在 C++ 中使用 [std::max_element。](https://www.geeksforgeeks.org/stdmax_element-in-cpp/) 

## C++

```
// C++ program to find maximum in arr[] of size n 
#include <bits/stdc++.h>
using namespace std;

// returns maximum in arr[] of size n
int largest(int arr[], int n)
{
    return *max_element(arr, arr+n);
}

int main()
{
    int arr[] = {10, 324, 45, 90, 9808};
    int n = sizeof(arr)/sizeof(arr[0]);
    cout << largest(arr, n);
    return 0;
}
```

**输出:**

```
9808
```

上述解的时间复杂度为![Theta(n)    ](img/05b79e35d5fd4b07c3708f8cc9c15ccb.png "Rendered by QuickLaTeX.com")。

更多详情请参考[程序寻找数组中最大元素](https://www.geeksforgeeks.org/c-program-find-largest-element-array/)的完整文章！
# 走狗排序的 C++程序

> 原文:[https://www.geeksforgeeks.org/cpp-program-for-stooge-sort/](https://www.geeksforgeeks.org/cpp-program-for-stooge-sort/)

Stooge 排序是一种递归排序算法。其定义如下(用于升序排序)。

```
Step 1 : If value at index 0 is greater than
         value at last index, swap them.
Step 2:  Recursively,
       a) Stooge sort the initial 2/3rd of the array.
       b) Stooge sort the last 2/3rd of the array.
       c) Stooge sort the initial 2/3rd again to confirm.

```

## C++

```
// C++ code to implement stooge sort
#include <iostream>
using namespace std;

// Function to implement stooge sort
void stoogesort(int arr[],int l, int h)
{
    if (l >= h)
      return;

    // If first element is smaller than last,
    // swap them
    if (arr[l] > arr[h])
       swap(arr[l], arr[h]);

    // If there are more than 2 elements in
    // the array
    if(h-l+1>2)
    {
        int t = (h-l+1)/3;

        // Recursively sort first 2/3 elements
        stoogesort(arr, l, h-t);

        // Recursively sort last 2/3 elements
        stoogesort(arr, l+t, h);

        // Recursively sort first 2/3 elements
        // again to confirm
        stoogesort(arr, l, h-t);
    }
}

// Driver Code
int main()
{
    int arr[] = {2, 4, 5, 3, 1};
    int n = sizeof(arr)/sizeof(arr[0]);

    // Calling Stooge Sort function to sort
    // the array
    stoogesort(arr, 0, n-1);

    // Display the sorted array
    for (int i=0; i<n; i++)
        cout << arr[i] << " ";

    return 0;
}
```

**输出:**

```
1 2 3 4 5 

```

更多详情请参考[走狗排序](https://www.geeksforgeeks.org/stooge-sort/)整篇文章！
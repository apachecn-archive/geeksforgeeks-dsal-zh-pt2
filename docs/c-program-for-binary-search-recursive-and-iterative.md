# 二分搜索法的 C 程序(递归和迭代)

> 原文:[https://www . geesforgeks . org/c-program-for-binary-search-recursive-and-iterative/](https://www.geeksforgeeks.org/c-program-for-binary-search-recursive-and-iterative/)

经过一次比较，我们基本上忽略了一半的元素。

1.  将 x 与中间元素进行比较。
2.  如果 x 与中间元素匹配，我们返回中间索引。
3.  否则如果 x 大于中间元素，那么 x 只能位于中间元素之后的右半子阵列中。所以我们重复右半部分。
4.  否则(x 较小)在左半部分重复出现。

**递归:**

## C/C++

```
#include <stdio.h>

// A recursive binary search function. It returns location of x in
// given array arr[l..r] is present, otherwise -1
int binarySearch(int arr[], int l, int r, int x)
{
   if (r >= l)
   {
        int mid = l + (r - l)/2;

        // If the element is present at the middle itself
        if (arr[mid] == x)  return mid;

        // If element is smaller than mid, then it can only be present
        // in left subarray
        if (arr[mid] > x) return binarySearch(arr, l, mid-1, x);

        // Else the element can only be present in right subarray
        return binarySearch(arr, mid+1, r, x);
   }

   // We reach here when element is not present in array
   return -1;
}

int main(void)
{
   int arr[] = {2, 3, 4, 10, 40};
   int n = sizeof(arr)/ sizeof(arr[0]);
   int x = 10;
   int result = binarySearch(arr, 0, n-1, x);
   (result == -1)? printf("Element is not present in array")
                 : printf("Element is present at index %d", result);
   return 0;
}
```

**迭代**T2】

## C/C++

```
#include <stdio.h>

// A iterative binary search function. It returns location of x in
// given array arr[l..r] if present, otherwise -1
int binarySearch(int arr[], int l, int r, int x)
{
  while (l <= r)
  {
    int m = l + (r-l)/2;

    // Check if x is present at mid
    if (arr[m] == x) 
        return m;  

    // If x greater, ignore left half  
    if (arr[m] < x) 
        l = m + 1; 

    // If x is smaller, ignore right half 
    else 
         r = m - 1; 
  }

  // if we reach here, then element was not present
  return -1; 
}

int main(void)
{
   int arr[] = {2, 3, 4, 10, 40};
   int n = sizeof(arr)/ sizeof(arr[0]);
   int x = 10;
   int result = binarySearch(arr, 0, n-1, x);
   (result == -1)? printf("Element is not present in array")
                 : printf("Element is present at index %d", result);
   return 0;
}
```

更多详情请参考[二分搜索法](https://www.geeksforgeeks.org/binary-search/)整篇文章！
# 用于 BogoSort 或排列排序的 C++程序

> 原文:[https://www . geesforgeks . org/CPP-program-for-bogo sort-or-arrange-sort/](https://www.geeksforgeeks.org/cpp-program-for-bogosort-or-permutation-sort/)

BogoSort 也称为排列排序、愚蠢排序、缓慢排序、猎枪排序或猴子排序，是一种基于生成和测试范式的特别无效的算法。该算法连续生成输入的排列，直到找到一个排序的。( [Wiki](https://en.wikipedia.org/wiki/Bogosort) )
例如，如果使用 bogosort 对一副牌进行排序，它将包括检查该副牌是否有序，如果没有，则将该副牌抛向空中，随机捡起牌，并重复该过程直到该副牌被排序。

**伪代码:**

```
while not Sorted(list) do
    shuffle (list)
done
```

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ implementation of Bogo Sort
#include <bits/stdc++.h>
using namespace std;

// To check if array is sorted or not
bool isSorted(int a[], int n)
{
    while (--n > 1)
        if (a[n] < a[n - 1])
            return false;
    return true;
}

// To generate permutation of the array
void shuffle(int a[], int n)
{
    for (int i = 0; i < n; i++)
        swap(a[i], a[rand() % n]);
}

// Sorts array a[0..n-1] using Bogo sort
void bogosort(int a[], int n)
{
    // if array is not sorted then shuffle
    // the array again
    while (!isSorted(a, n))
        shuffle(a, n);
}

// prints the array
void printArray(int a[], int n)
{
    for (int i = 0; i < n; i++)
        printf("%d ", a[i]);
    printf("\n");
}

// Driver code
int main()
{
    int a[] = { 3, 2, 5, 1, 0, 4 };
    int n = sizeof a / sizeof a[0];
    bogosort(a, n);
    printf("Sorted array :\n");
    printArray(a, n);
    return 0;
}
```

**Output:** 

```
Sorted array :
0 1 2 3 4 5
```

更多详情请参考 [BogoSort 或排列排序](https://www.geeksforgeeks.org/bogosort-permutation-sort/)整篇文章！
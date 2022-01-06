# C/C++程序求出现奇数次的次数

> 原文:[https://www . geeksforgeeks . org/c-program-for-find-number-occurrent-奇数次/](https://www.geeksforgeeks.org/c-program-for-find-the-number-occurring-odd-number-of-times/)

给定一个由出现偶数次的正整数组成的数组 **arr[]** ，除了出现奇数次的一个数。任务是找出这个奇数次出现的次数。

**示例:**

```
Input : arr = {1, 2, 3, 2, 3, 1, 3}
Output : 3

Input : arr = {5, 7, 2, 7, 5, 2, 5}
Output : 5
```

**天真的方法:**一个简单的解决方案是运行两个嵌套循环。外部循环逐个选取所有元素，内部循环计算外部循环选取的元素的出现次数。

## C++

```
// C++ program to find the element
// occurring odd number of times
#include <bits/stdc++.h>
using namespace std;

// Function to find the element
// occurring odd number of times
int getOddOccurrence(int arr[], int arr_size)
{
    for (int i = 0; i < arr_size; i++) {

        int count = 0;

        for (int j = 0; j < arr_size; j++) {
            if (arr[i] == arr[j])
                count++;
        }
        if (count % 2 != 0)
            return arr[i];
    }
    return -1;
}

// driver code
int main()
{
    int arr[] = { 2, 3, 5, 4, 5, 2,
                  4, 3, 5, 2, 4, 4, 2 };
    int n = sizeof(arr) / sizeof(arr[0]);

    // Function calling
    cout << getOddOccurrence(arr, n);

    return 0;
}
```

## C

```
// C program to find the element
// occurring odd number of times
#include <stdio.h>

// Function to find the element
// occurring odd number of times
int getOddOccurrence(int arr[], int arr_size)
{
    for(int i = 0; i < arr_size; i++)
    {
        int count = 0;

        for(int j = 0; j < arr_size; j++)
        {
            if (arr[i] == arr[j])
                count++;
        }
        if (count % 2 != 0)
            return arr[i];
    }
    return -1;
}

// Driver code
int main()
{
    int arr[] = { 2, 3, 5, 4, 5, 2,
                  4, 3, 5, 2, 4, 4, 2 };
    int n = sizeof(arr) / sizeof(arr[0]);

    // Function calling
    printf("%d",getOddOccurrence(arr, n));

    return 0;
}

// This code is contributed by rbbansal
```

**Output:** 

```
5
```
# C++程序在排序的二进制数组中计数 1

> 原文:[https://www . geeksforgeeks . org/c-程序到计数-1 进制排序-二进制数组/](https://www.geeksforgeeks.org/c-program-to-count-1s-in-a-sorted-binary-array/)

给定一个按非递增顺序排序的二进制数组，计算其中 1 的个数。

**示例:**

```
Input: arr[] = {1, 1, 0, 0, 0, 0, 0}
Output: 2

Input: arr[] = {1, 1, 1, 1, 1, 1, 1}
Output: 7

Input: arr[] = {0, 0, 0, 0, 0, 0, 0}
Output: 0
```

一个简单的解决方案是线性遍历数组。简单解的时间复杂度为 O(n)。我们可以使用[二分搜索法](https://www.geeksforgeeks.org/binary-search/)找到以 O(Logn)为单位的时间计数。想法是使用二分搜索法查找 1 的最后一次出现。一旦我们找到索引的最后一次出现，我们返回索引+ 1 作为计数。
以下是上述想法的实现。

## C++

// C++ program to count one’s in a boolean array#include <bits stdc="">using namespace std;</bits>

/*返回 arr 中 1 的计数[低..高】。数组是
假设按非递增顺序排序*/
int countOnes(bool arr[]，int low，int high)
{
if(high>= low)
{
//得到中间索引
int mid = low+(high–low)/2；

//检查中间索引处的元素是否为最后 1
if((mid = = high | | arr[mid+1]= = 0)&&(arr[mid]= = 1))
返回 mid+1；

//如果元素不是最后一个 1，右侧重复出现
if (arr[mid] == 1)
返回 countOnes(arr，(mid + 1)，高)；

//否则左侧重复
返回 countOnes(arr，low，(mid-1))；
}
返回 0；
}

/*驱动程序代码*/
int main()
{
bool arr[]= { 1，1，1，0，0，0 }；
int n = sizeof(arr)/sizeof(arr[0])；
cout < <“给定数组中 1 的计数为”< < countOnes(arr，0，n-1)；返回 0；}[tabbyending]

**Output**

```
Count of 1's in given array is 4
```

上述解决方案的时间复杂度为 O(Logn)

空间复杂度 o(log n)(函数调用栈)

迭代求解的相同方法是
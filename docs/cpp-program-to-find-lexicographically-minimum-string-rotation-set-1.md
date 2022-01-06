# C++程序查找字典最小字符串旋转|集合 1

> 原文:[https://www . geesforgeks . org/CPP-program-to-find-按字典顺序-最小字符串-旋转-set-1/](https://www.geeksforgeeks.org/cpp-program-to-find-lexicographically-minimum-string-rotation-set-1/)

编写代码来查找循环数组中的字典序最小值，例如，对于 BCABDADAB 数组，字典序最小值是 ABBCABDAD。
来源:谷歌笔试
更多示例:

```
Input:  GEEKSQUIZ
Output: EEKSQUIZG

Input:  GFG
Output: FGG

Input:  GEEKSFORGEEKS
Output: EEKSFORGEEKSG
```

下面是一个简单的解决方案。让给定的字符串为“str”
1)将“str”与其自身连接起来，并存储在一个临时字符串中，比如“concat”。
2)创建一个字符串数组来存储“字符串”的所有旋转。让数组为“arr”。
3)通过在索引 0、1、2 处获取“concat”的子串，找到“str”的所有旋转..n-1。将这些旋转存储在 arr[]中
4)排序 arr[]并返回 arr[0]。

以下是上述解决方案的实现。

## C++

```
// A simple C++ program to find lexicographically minimum rotation
// of a given string
#include <iostream>
#include <algorithm>
using namespace std;

// This functionr return lexicographically minimum
// rotation of str
string minLexRotation(string str)
{
    // Find length of given string
    int n = str.length();

    // Create an array of strings to store all rotations
    string arr[n];

    // Create a concatenation of string with itself
    string concat = str + str;

    // One by one store all rotations of str in array.
    // A rotation is obtained by getting a substring of concat
    for (int i = 0; i < n; i++)
        arr[i] = concat.substr(i, n);

    // Sort all rotations
    sort(arr, arr+n);

    // Return the first rotation from the sorted array
    return arr[0];
}

// Driver program to test above function
int main()
{
    cout << minLexRotation("GEEKSFORGEEKS") << endl;
    cout << minLexRotation("GEEKSQUIZ") << endl;
    cout << minLexRotation("BCABDADAB") << endl;
}
```

**输出:**

```
EEKSFORGEEKSG
EEKSQUIZG
ABBCABDAD
```

在假设我们使用了一个 O(nLogn)排序算法的情况下，上述解的时间复杂度为 O(n <sup>2</sup> Logn)。
详情请参考[字典最小字符串旋转|第 1 集](https://www.geeksforgeeks.org/lexicographically-minimum-string-rotation/)的完整文章！
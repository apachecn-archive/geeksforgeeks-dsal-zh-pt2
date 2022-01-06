# 给定字符串数组中回文字符串的计数

> 原文:[https://www . geeksforgeeks . org/给定字符串数组中的回文字符串计数/](https://www.geeksforgeeks.org/count-of-palindrome-strings-in-given-array-of-strings/)

给定一个大小为 **N** 的字符串数组 **arr[]** ，其中每个字符串仅由小写英文字母组成。任务是返回数组中所有回文字符串的计数。

**示例:**

> **输入:**arr[]= {“ABC”、“car”、“ada”、“racecar”、“cool”}
> **输出:** 2
> **说明:**“ada”和“racecar”是两个回文串。
> 
> **输入:**arr[]= {“def”、“ABA”}
> **输出:** 1
> **说明:**“ABA”是唯一的回文串。

**进场:**解决方案基于 [**贪婪进场**](https://www.geeksforgeeks.org/greedy-algorithms/) 。检查数组中的每一个字符串是否是回文，并记录计数。按照以下步骤解决问题:

*   将计数变量 ans 初始化为 0。
*   使用变量 I 迭代范围[0，N]，如果 arr[i]是回文，则递增 ans 的值。
*   执行上述步骤后，打印 ans 的值作为答案。

下面是上述方法的实现。

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check if given string
// is Palindrome or not
bool isPalindrome(string& s)
{
    // Copy string s char into string a
    string a = s;
    reverse(s.begin(), s.end());

    // Chek if two string are equal or not
    return s == a;
}

// Function to return count 
// of Palindrome string
int PalindromicStrings(string arr[], int N)
{
    int ans = 0;

    // Loop to find palindrome string
    for (int i = 0; i < N; i++) {

        // Cheking if given string is
        // palindrome or not
        if (isPalindrome(arr[i])) {

            // Update answer varibale
            ans++;
        }
    }
    return ans;
}

// Driver Code
int main()
{

    string arr[]
        = { "abc", "car", "ada", 
           "racecar", "cool" };
    int N = sizeof(arr) / sizeof(arr[0]);

    // Print required answer
    cout << PalindromicStrings(arr, N);

    return 0;
}
```

**Output**

```
2
```

***时间复杂度:*** O(N * W)其中 W 是琴弦的平均长度
***辅助空间:*** O(1)
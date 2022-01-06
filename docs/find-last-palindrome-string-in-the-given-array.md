# 查找给定数组中的最后一个回文字符串

> 原文:[https://www . geesforgeks . org/find-last-回文-给定数组中的字符串/](https://www.geeksforgeeks.org/find-last-palindrome-string-in-the-given-array/)

给定一组大小为 **N** 的字符串 **arr[]** ，其中每个字符串仅由小写英文字母组成。任务是返回数组中最后一个[回文串](https://www.geeksforgeeks.org/string-palindrome/)。

**注意:**保证始终有一个回文串存在。

**示例:**

> **输入:**arr[]= {“ABC”、“car”、“ada”、“racecar”、“cool”}
> **输出:**【racecar】
> **解释:**最后一个回文的字符串是“race car”。
> 注意“ada”也是回文，但不是 Last。
> 
> **输入:**【arr[]**= { " def "，" aba"}
> **输出:**【ABA】**

****进场:**解决方案基于贪婪进场。检查数组中从最后一个开始的每一个字符串是否是**回文**，并跟踪最后一个回文字符串。按照以下步骤解决问题:**

*   **将字符串变量**和**初始化为空字符串。**
*   **[使用变量 **i** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/) **(N，0)**，并执行以下任务:

    *   如果 **arr[i]** 是回文，则将 **ans** 的值设置为 **arr[i]** 。** 
*   **执行上述步骤后，打印**和**的值作为答案。**

**下面是上述方法的实现:**

## **C++**

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

// Function to return last Palindrome string
string LastPalindrome(string arr[], int N)
{

    // Loop to find the last palindrome string
    for (int i = N - 1; i >= 0; i--) {

        // Cheking if given string is
        // palindrome or not
        if (isPalindrome(arr[i])) {

            // Return the answer
            return arr[i];
        }
    }
}

// Driver Code
int main()
{

    string arr[]
        = { "abc", "car", "ada", "racecar",
            "cool" };
    int N = sizeof(arr) / sizeof(arr[0]);

    // Print required answer
    cout << LastPalindrome(arr, N);

    return 0;
}
```

****Output:**

```
racecar

```** 

*****时间复杂度:** O(N*W)其中 W 是 arr[]*
***中任意字符串的最大大小辅助空间:** O(1)***
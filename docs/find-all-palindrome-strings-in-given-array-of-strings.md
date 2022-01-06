# 查找给定字符串数组中的所有回文字符串

> 原文:[https://www . geeksforgeeks . org/find-all-回文-字符串在给定的字符串数组中/](https://www.geeksforgeeks.org/find-all-palindrome-strings-in-given-array-of-strings/)

给定一个大小为 **N** 的字符串数组 **arr[]** ，其中每个字符串仅由小写英文字母组成。任务是找到数组中的所有回文字符串。如果给定数组中没有回文，则打印-1。

**示例:**

> **输入:**arr[]= {“ABC”、“car”、“ada”、“racecar”、“cool”}
> **输出:**“ada”、“race car”
> **解释:**这两个是给定数组中唯一的回文字符串
> 
> **输入:**arr[]= {“def”，“ab”}
> **输出:** -1
> **解释:**给定数组中不存在回文串。

**进场:**解决方案基于 [**贪婪进场**](https://www.geeksforgeeks.org/greedy-algorithms/) 。检查数组中的每个字符串是否是回文，并跟踪所有的回文字符串。按照以下步骤解决问题:

*   初始化字符串**和**的向量。
*   使用变量 **i** 迭代范围**【0，N】**，如果**arr【I】**是回文，则将其添加到 **ans** 中。
*   执行上述步骤后，将出现在**和**中的字符串打印为结果字符串。

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

// Function to return all Palindrome string
vector<string> PalindromicStrings(string arr[], 
                                  int N)
{
    vector<string> ans;

    // Loop to find palindrome string
    for (int i = 0; i < N; i++) {

        // Cheking if given string is
        // palindrome or not
        if (isPalindrome(arr[i])) {

            // Update answer varibale
            ans.push_back(arr[i]);
        }
    }
    return ans;
}

// Driver Code
int main()
{

    string arr[]
        = { "abc", "car", "ada", "racecar", "cool" };
    int N = sizeof(arr) / sizeof(arr[0]);

    // Print required answer
    vector<string> s = PalindromicStrings(arr, N);
    if(s.size() == 0)
        cout << "-1";
    for(string st: s)
        cout << st << " ";

    return 0;
}
```

**Output**

```
ada racecar 
```

***时间复杂度:*** O(N * W)其中 W 是琴弦的平均长度
***辅助空间:*** O(N * W)
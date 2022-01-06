# 尽量减少字符串中唯一字符的数量

> 原文:[https://www . geesforgeks . org/minimum-number-unique-characters-string/](https://www.geeksforgeeks.org/minimize-number-unique-characters-string/)

给定两个字符串 A 和 B。通过用 B[i]交换 A[i]或保持不变来最小化字符串 A 中唯一字符的数量。交换次数可以大于或等于 0。请注意，A[i]只能与 b 中的相同索引元素交换。请打印最少数量的唯一字符。约束:0

示例:

```
Input : A = ababa
        B = babab
Output : 1
Swapping all b's in string A, with
a's in string B results in string
A having all characters as a. 

Input : A = abaaa
        B = bbabb
Output : 2
Initially string A has 2 unique
characters. Swapping at any index 
does not change this count.

```

 [### 推荐:请首先在 IDE 上尝试您的方法，然后查看解决方案。](https://ide.geeksforgeeks.org) 

**方法:**使用[回溯](https://www.geeksforgeeks.org/backtracking-algorithms/)可以解决问题。创建一个映射，其中键是 A[i]，值是对应字符的计数。地图的大小显示了不同字符的数量，因为只有那些出现在字符串 A 中的元素才作为关键字出现在地图中。在每个指数位置，都有两种选择:要么用 B[i]交换 A[i]，要么保持 A[i]不变。从索引 0 开始，对每个索引执行以下操作:

1.  保持 A[i]不变，在映射中将 A[i]的计数增加 1，并递归调用下一个索引。
2.  通过将 A[i]的计数减少 1 进行回溯，用 B[i]交换 A[i]，在映射中将 A[i]的计数增加 1，并再次递归调用下一个索引。

保留一个变量 ans 来存储不同字符的整体最小值。在上述两种情况下，当遍历整个字符串时，比较 ans 中不同字符的当前数量和总体最小值，并相应地更新 ans。

**实施:**

```
// CPP program to minimize number of
// unique characters in a string.

#include <bits/stdc++.h>
using namespace std;

// Utility function to find minimum
// number of unique characters in string.
void minCountUtil(string A, string B,
                  unordered_map<char, int>& ele,
                  int& ans, int ind)
{

    // If entire string is traversed, then
    // compare current number of distinct
    // characters in A with overall minimum.
    if (ind == A.length()) {
        ans = min(ans, (int)ele.size());
        return;
    }

    // swap A[i] with B[i], increase count of
    // corresponding character in map and call
    // recursively for next index.
    swap(A[ind], B[ind]);
    ele[A[ind]]++;
    minCountUtil(A, B, ele, ans, ind + 1);

    // Backtrack (Undo the changes done)
    ele[A[ind]]--;

    // If count of character is reduced to zero,
    // then that character is not present in A.
    // So remove that character from map.
    if (ele[A[ind]] == 0) 
        ele.erase(A[ind]);

    // Restore A to original form.
    // (Backtracking step)
    swap(A[ind], B[ind]);

    // Increase count of A[i] in map and
    // call recursively for next index.
    ele[A[ind]]++;
    minCountUtil(A, B, ele, ans, ind + 1);

    // Restore the changes done
    // (Backtracking step)
    ele[A[ind]]--;
    if (ele[A[ind]] == 0) 
        ele.erase(A[ind]);    
}

// Function to find minimum number of
// distinct characters in string.
int minCount(string A, string B)
{
    // Variable to store minimum number
    // of distinct character.
    // Initialize it with length of A
    // as maximum possible value is
    // length of A.
    int ans = A.length();

    // Map to store count of distinct
    // characters in A. To keep
    // complexity of insert operation
    // constant unordered_map is used.
    unordered_map<char, int> ele;

    // Call utility function to find
    // minimum number of unique
    // characters.
    minCountUtil(A, B, ele, ans, 0);

    return ans;
}

int main()
{
    string A = "abaaa";
    string B = "bbabb";

    cout << minCount(A, B);
    return 0;
}
```

**Output:**

```
2

```

**时间复杂度:**O(2<sup>n</sup>)
T5】辅助空间: O(n)
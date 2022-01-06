# 可由四位数字构成的最大可能时间|(递归方法)

> 原文:[https://www . geeksforgeeks . org/最大可能时间由四位数组成-递归方法/](https://www.geeksforgeeks.org/maximum-possible-time-that-can-be-formed-from-four-digits-recursive-approach/)

给定一个具有 4 个整数的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** 。任务是返回**最大** 24 小时时间，该时间可以使用数组中的数字来形成。注意 24 小时格式的**最小**时间为 **00:00** ，**最大**为 **23:59** 。如果无法形成有效时间，则返回空字符串。
**示例:**

> **输入** : arr[] = {1，2，3，4}
> **输出** : 23:41
> **解释** : 23:41 是 24 小时格式的最大可能时间
> 
> **输入** : arr[] = {5，5，6，6}
> **输出**:
> **解释**:给定的数字不能形成有效时间

**HashMap 方法:-** 解决这个问题的一种方法已经讨论过了

**递归方式**:任务也可以使用[递归](https://www.geeksforgeeks.org/recursion/)解决。尝试使用递归生成所有可能的[排列](https://www.geeksforgeeks.org/write-a-c-program-to-print-all-permutations-of-a-given-string/)，然后在**排序**所有排列后，丢弃**无效的**排列并返回具有最大**可能值的排列。如果不存在有效的排列，返回一个空的**字符串。有效排列的条件。****

*   **小时**的第一个**数字必须在**【0，2】**范围内。**
*   如果选择**第一个**数字作为 **2** 否则**【0，9】**，则**小时数**第二个**数字必须在**【0，3】**范围内。**
*   **分钟**的第一个**数字必须在**【0，5】**范围内，第二个**数字必须在**分钟**范围内**【0，9】**

下面是上述代码的实现:

## C++

```
// C++ implementation of the above approach
#include <bits/stdc++.h>
using namespace std;

// Stores all the permutations
vector<string> res;

// Function to generate valid permutations
void getMax(int idx, vector<int>& nums, string per)
{
    // All the digits are used
    if (idx == nums.size()) {

        // If first digit is
        // not 0, 1 or 2 then it is
        // invalid, return
        if (per[0] != '0'
            && per[0] != '1'
            && per[0] != '2')
            return;

        // Second digit must be less than 7
        if (per[2] >= '6')
            return;

        // If first digit is 2
        // then second digit must be
        // smaller than 5
        if (per[0] == '2'
            and per[1] >= '4')
            return;

        // Push the vali
        // d permutation in result
        res.push_back(per);
        return;
    }

    for (int i = idx; i < nums.size(); i++) {

        // add num to res
        per += nums[i] + '0';

        // swap and solve
        // for further permutation
        swap(nums[idx], nums[i]);

        // Recur
        getMax(idx + 1, nums, per);

        // Backtrack
        per.pop_back();

        swap(nums[i], nums[idx]);
    }
}

// Function to return maximum time
// possible in 24-hour format
string getMaxtime(vector<int>& arr)
{
    string per = "";
    getMax(0, arr, per);

    // No valid permutation
    // can be generated
    if (res.empty())
        return "";

    // Sort all valid permutations
    sort(res.begin(), res.end());

    // Largest valid permutation
    string ans = res[res.size() - 1];

    // Resultant string
    string result
        = ans.substr(0, 2)
          + ":"
          + ans.substr(2, 2);
    return result;
}

// Driver Code
int main()
{
    vector<int> arr = { 1, 2, 3, 4 };
    int n = sizeof(arr) / sizeof(int);
    cout << (getMaxtime(arr));
    return 0;
}
```

**Output**

```
23:41
```

***时间复杂度*** **:** O(N！*日志(N！))
***辅助空间*** **:** O(N)
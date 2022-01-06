# 最小递增子序列数

> 原文:[https://www . geeksforgeeks . org/最小递增子序列数/](https://www.geeksforgeeks.org/minimum-number-of-increasing-subsequences/)

给定一个 N 大小的整数数组，你要把它分成最小数量的“严格递增子序列”
例如:让序列为{1，3，2，4}，那么答案就是 2。在这种情况下，第一个递增顺序是{1，3，4}，第二个递增顺序是{2}。
示例:

> 输入:arr[] = {1 3 2 4}
> 输出:2
> 有两个递增的子序列{1，3，4}和{2}
> 输入:arr[] = {4 3 2 1}
> 输出:4
> 输入:arr[] = {1 2 3 4}
> 输出:1
> 输入:arr[] = {1 6 2 4 3}
> 输出:3

如果我们关注这个例子，我们可以看到增加子序列的最小数量等于[最长减少子序列](https://www.geeksforgeeks.org/longest-decreasing-subsequence/)的长度，其中来自最长减少子序列的每个元素代表一个增加子序列，因此它可以在 N*Log(N)时间复杂度中找到，就像[最长增加子序列](https://www.geeksforgeeks.org/longest-monotonically-increasing-subsequence-size-n-log-n/)通过将所有元素乘以-1 一样。
我们对所有元素进行迭代器，并将其存储在排序数组( [multiset](https://www.geeksforgeeks.org/multiset-in-cpp-stl/) ) S 到目前为止找到的每个递增子序列中的最后一个元素，对于每个元素 X，我们在 S 中选择小于 X 的最大元素-使用二分搜索法-并用 X 替换它，这意味着我们将当前元素添加到以 X 结尾的递增子序列中，否则， 如果 S 中没有小于 X 的元素，我们就把它插入 S 中，形成一个新的递增子序列，以此类推，直到最后一个元素，最后一个元素的答案将是 S 的大小

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ program to count the Minimum number of
// increasing subsequences
#include <bits/stdc++.h>
using namespace std;

int MinimumNumIncreasingSubsequences(int arr[], int n)
{
    multiset<int> last;

    // last element in each  increasing subsequence
    // found so far
    for (int i = 0; i < n; i++) {

        // here our current element is arr[i]
        multiset<int>::iterator it = last.lower_bound(arr[i]);

        // iterator to the first element larger
        // than or equal to arr[i]
        if (it == last.begin())

            // if all the elements in last larger
            // than or to arr[i] then insert it into last
            last.insert(arr[i]);

        else {
            it--;

            // the largest element smaller than arr[i] is the number
            // before *it which is it--
            last.erase(it); // erase the largest element smaller than arr[i]
            last.insert(arr[i]); // and replace it with arr[i]
        }
    }
    return last.size(); // our answer is the size of last
}

// Driver program
int main()
{
    int arr[] = { 8, 4, 1, 2, 9 };
    int n = sizeof(arr) / sizeof(int);
    cout << "Minimum number of increasing subsequences are : "
         << MinimumNumIncreasingSubsequences(arr, n);
    return 0;
}
```

**Output**

```
Minimum number of increasing subsequences are : 3
```
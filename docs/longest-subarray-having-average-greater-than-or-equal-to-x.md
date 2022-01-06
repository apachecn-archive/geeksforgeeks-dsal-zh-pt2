# 平均值大于或等于 x 的最长子阵列

> 原文:[https://www . geeksforgeeks . org/最长子阵列平均值大于或等于 x/](https://www.geeksforgeeks.org/longest-subarray-having-average-greater-than-or-equal-to-x/)

给定一个整数数组和一个整数 x。求整数平均值大于或等于 x 的最大尺寸子数组的长度

示例:

```
Input : arr[] = {-2, 1, 6, -3}, x = 3
Output : 2
Longest subarray is {1, 6} having average
3.5 greater than x = 3.

Input : arr[] = {2, -3, 3, 2, 1}, x = 2
Output : 3
Longest subarray is {3, 2, 1} having 
average 2 equal to x = 2.

```

 [### 推荐:请首先在 IDE 上尝试您的方法，然后查看解决方案。](https://ide.geeksforgeeks.org) 

一个**简单的**解就是逐个考虑每个子阵，求其平均值。如果平均值大于或等于 x，则将子阵列的长度与目前发现的最大长度进行比较。这个解的时间复杂度为 O(n <sup>2</sup> )。

一个有效的解决方案是使用二分搜索法和前缀和。假设所需的最长子阵列是..j]而它的长度是 l = j-i+1。因此，数学上可以写成:

> (页:1)-什么(j)]/l)≥x
> = =>(arr[I-什么 j]/l)-x≥0
> = =>(arr[I-什么(j))x * l)/≥0…(1)

等式(1)相当于从子阵列的每个元素中减去 x，然后取结果子阵列的平均值。因此，从数组的每个元素中减去 x，就可以得到最终的子数组。让更新后的子阵列为 arr1。等式(1)可以进一步简化为:

> S7-1200 可编程控制器-什么 j)]/≥0
> = =>σ(arr 1[I-什么(j))0…(2)

等式(2)只是总和大于或等于零的最长子阵列。求和大于或等于零的最长子阵列可以通过以下文章中讨论的方法找到:
[求和大于 k 的最长子阵列](https://www.geeksforgeeks.org/largest-subarray-having-sum-greater-than-k/)。

分步算法是:
1。从数组的每个元素中减去 x。
2。使用前缀和和二分搜索法查找更新数组中总和大于或等于零的最长子数组。

以下是上述方法的实现:

## C++

```
// CPP program to find Longest subarray
// having average greater than or equal
// to x.
#include <bits/stdc++.h>

using namespace std;

// Comparison function used to sort preSum vector.
bool compare(const pair<int, int>& a, const pair<int, int>& b)
{
    if (a.first == b.first)
        return a.second < b.second;

    return a.first < b.first;
}

// Function to find index in preSum vector upto which
// all prefix sum values are less than or equal to val.
int findInd(vector<pair<int, int> >& preSum, int n, int val)
{

    // Starting and ending index of search space.
    int l = 0;
    int h = n - 1;
    int mid;

    // To store required index value.
    int ans = -1;

    // If middle value is less than or equal to
    // val then index can lie in mid+1..n
    // else it lies in 0..mid-1.
    while (l <= h) {
        mid = (l + h) / 2;
        if (preSum[mid].first <= val) {
            ans = mid;
            l = mid + 1;
        }
        else
            h = mid - 1;
    }

    return ans;
}

// Function to find Longest subarray having average
// greater than or equal to x.
int LongestSub(int arr[], int n, int x)
{
    int i;

    // Update array by subtracting x from
    // each element.
    for (i = 0; i < n; i++)
        arr[i] -= x;

    // Length of Longest subarray.
    int maxlen = 0;

    // Vector to store pair of prefix sum
    // and corresponding ending index value.
    vector<pair<int, int> > preSum;

    // To store current value of prefix sum.
    int sum = 0;

    // To store minimum index value in range
    // 0..i of preSum vector.
    int minInd[n];

    // Insert values in preSum vector.
    for (i = 0; i < n; i++) {
        sum = sum + arr[i];
        preSum.push_back({ sum, i });
    }

    sort(preSum.begin(), preSum.end(), compare);

    // Update minInd array.
    minInd[0] = preSum[0].second;

    for (i = 1; i < n; i++) {
        minInd[i] = min(minInd[i - 1], preSum[i].second);
    }

    sum = 0;
    for (i = 0; i < n; i++) {
        sum = sum + arr[i];

        // If sum is greater than or equal to 0,
        // then answer is i+1.
        if (sum >= 0)
            maxlen = i + 1;

        // If sum is less than 0, then find if
        // there is a prefix array having sum
        // that needs to be added to current sum to
        // make its value greater than or equal to 0.
        // If yes, then compare length of updated
        // subarray with maximum length found so far.
        else {
            int ind = findInd(preSum, n, sum);
            if (ind != -1 && minInd[ind] < i)
                maxlen = max(maxlen, i - minInd[ind]);
        }
    }

    return maxlen;
}

// Driver code.
int main()
{
    int arr[] = { -2, 1, 6, -3 };
    int n = sizeof(arr) / sizeof(arr[0]);

    int x = 3;

    cout << LongestSub(arr, n, x);
    return 0;
}
```

## 蟒蛇 3

```
# Python3 program to find longest subarray 
# having average greater than or equal to x 

# Function to find index in preSum list of
# tuples upto which all prefix sum values 
# are less than or equal to val. 
def findInd(preSum, n, val):

    # Starting and ending index 
    # of search space. 
    l = 0
    h = n - 1

    # To store required index value
    ans = -1

    # If middle value is less than or 
    # equal to val then index can 
    # lie in mid+1..n else it lies
    # in 0..mid-1
    while (l <= h):
        mid = (l + h) // 2
        if preSum[mid][0] <= val:
            ans = mid
            l = mid + 1
        else:
            h = mid - 1

    return ans

# Function to find Longest subarray
# having average greater than or 
# equal to x. 
def LongestSub(arr, n, x):

    # Update array by subtracting
    # x from each element
    for i in range(n):
        arr[i] -= x

    # Length of Longest subarray. 
    maxlen = 0

    # To store current value of 
    # prefix sum. 
    total = 0

    # To store minimum index value in
    # range 0..i of preSum vector.
    minInd = [None] * n

    # list to store pair of prefix sum 
    # and corresponding ending index value. 
    preSum = []

    # Insert values in preSum vector
    for i in range(n):
        total += arr[i]
        preSum.append((total, i))

    preSum = sorted(preSum)

    # Update minInd array.
    minInd[0] = preSum[0][1]
    for i in range(1, n):
        minInd[i] = min(minInd[i - 1], 
                        preSum[i][1])
    total = 0
    for i in range(n):
        total += arr[i]

        # If sum is greater than or equal 
        # to 0, then answer is i+1
        if total >= 0:
            maxlen = i + 1

        # If sum is less than 0, then find if 
        # there is a prefix array having sum 
        # that needs to be added to current sum to 
        # make its value greater than or equal to 0. 
        # If yes, then compare length of updated 
        # subarray with maximum length found so far
        else:
            ind = findInd(preSum, n, total)
            if (ind != -1) & (minInd[ind] < i):
                maxlen = max(maxlen, i - minInd[ind])

    return maxlen

# Driver Code
if __name__ == '__main__':

    arr = [ -2, 1, 6, -3 ]
    n = len(arr)
    x = 3

    print(LongestSub(arr, n, x))

# This code is contributed by Vikas Chitturi
```

**Output:**

```
2

```

**时间复杂度:**O(nlogn)
T3】辅助空间: O(n)
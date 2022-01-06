# 包含大于 0 的 1 的二进制字符串中的子字符串计数

> 原文:[https://www . geeksforgeeks . org/包含大于 0 的 1 的二进制字符串中的子字符串计数/](https://www.geeksforgeeks.org/count-of-substrings-in-a-binary-string-that-contains-more-1s-than-0s/)

给定一个[二进制字符串](https://www.geeksforgeeks.org/tag/binary-string/) **s** ，任务是计算这样的[子字符串](https://www.geeksforgeeks.org/python-find-all-the-strings-that-are-substrings-to-the-given-list-of-strings/)的数量，其中 **1** 的计数严格大于 **0** 的计数。

**示例**

> **输入:** S = "110011"
> **输出:** 11
> **解释:**
> 1 的计数严格大于 0 的子串有{S[0]}、{S[0]、S[1]}、{S[0]、S[2]}、{ S[0]、S[4]}、{ S[0]、S[5]}、{S[1]、S[1]、
> 
> **输入:**S = " 101 "
> T3】输出: 3

**天真法:**解决问题最简单的方法是[生成所有子串](https://www.geeksforgeeks.org/program-print-substrings-given-string/)并统计每个子串中 **1** s 和 **0** s 的个数。将那些包含 **1** s 的子串的计数增加到大于 **0** s 的计数。最后，打印得到的计数。
***时间复杂度**:O(N<sup>3</sup>)*
***辅助空间:** O(1)*

**高效方法:**上述方法可以使用 [**合并排序算法**](https://www.geeksforgeeks.org/merge-sort/) 进行优化。请遵循以下步骤:

*   初始化一个数组，比如说大小为 **n 的 **nums[]** ，其中 **n** 是字符串的[长度。](https://www.geeksforgeeks.org/c-program-to-find-the-length-of-a-string/)**
*   [穿越弦](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/)。如果 **s[i] == '1'** ，则在 **nums[i]** 中存储 **1** 。否则，设置 **nums[i] = -1** 。
*   更新 **pref[]** 来存储 [**数组 **nums[]** 的前缀和**](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/) 。
*   现在，问题简化为计算数组**pref【】**中**对(I，j)** 的数量，其中**pref【I】<pref【j】**和 **i < j** ，这类似于从后侧计算数组中的倒位[](https://www.geeksforgeeks.org/counting-inversions/)**。**
*   **返回前缀和数组的逆序数作为最终答案。**

**下面是上述方法的实现。**

## **C++14**

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to merge two partitions
// such that the merged array is sorted
void merge(vector<int>& v, int left,
           int mid, int right, int& inversions)
{
    vector<int> temp(right - left + 1);

    int i = left;
    int j = mid + 1;
    int k = 0;
    int cnt = 0;

    while (i <= mid && j <= right) {
        if (v[i] <= v[j]) {
            temp[k++] = v[i++];
        }
        else {
            // Counting inversions
            inversions += (mid - i + 1);

            temp[k++] = v[j++];
        }
    }

    while (i <= mid)
        temp[k++] = v[i++];

    while (j <= right)
        temp[k++] = v[j++];

    k = 0;
    for (int a = left; a <= right; a++) {
        v[a] = temp[k++];
    }
}

// Function to implement merge sort
void mergeSort(vector<int>& v, int left,
               int right, int& inversions)
{
    if (left < right) {
        int mid = (left + right) / 2;

        mergeSort(v, left, mid, inversions);
        mergeSort(v, mid + 1, right, inversions);
        merge(v, left, mid, right, inversions);
    }
}

// Function to calculate number of
// inversions in a given array
int CountInversions(vector<int>& v)
{
    int n = v.size();
    int inversions = 0;

    // Calculate the number of inversions
    mergeSort(v, 0, n - 1, inversions);

    // Return the number of inversions
    return inversions;
}

// Function to count the number of
// substrings that contains more 1s than 0s
int getSubsCount(string& input)
{
    int n = input.length();

    vector<int> nums(n);

    for (int i = 0; i < n; i++) {
        nums[i] = input[i] - '0';

        if (nums[i] == 0)
            nums[i] = -1;
    }

    // Stores the prefix sum array
    vector<int> pref(n);

    int sum = 0;

    for (int i = 0; i < n; i++) {
        sum += nums[i];
        pref[i] = sum;
    }

    int cnt = 0;

    // Stores the count of valid substrings
    for (int i = 0; i < n; i++) {
        if (pref[i] > 0)
            cnt++;
    }

    reverse(pref.begin(), pref.end());

    int inversions = CountInversions(pref);

    int ans = cnt + inversions;

    return ans;
}

// Driver Code
int main()
{

    // Given Input
    string input = "101";

    // Function Call
    int ans = getSubsCount(input);

    cout << ans << endl;

    return 0;
}
```

## **蟒蛇 3**

```
# python 3 program for the above approach

# Function to merge two partitions
# such that the merged array is sorted
def merge(v, left,mid, right, inversions):
    temp = [0 for i in range(right - left + 1)]

    i = left
    j = mid + 1
    k = 0
    cnt = 0

    while (i <= mid and j <= right):
        if (v[i] <= v[j]):
            temp[k] = v[i]
            k += 1
            i += 1

        else:
            # Counting inversions
            inversions += (mid - i + 1)

            temp[k] = v[j]
            k += 1
            j += 1

    while (i <= mid):
        temp[k] = v[i]
        k += 1
        i += 1

    while (j <= right):
        temp[k] = v[j]
        k += 1
        j += 1

    k = 0
    for a in range(left,right+1,1):
        v[a] = temp[k]
        k += 1

# Function to implement merge sort
def mergeSort(v, left, right,inversions):
    if (left < right):
        mid = (left + right) // 2

        mergeSort(v, left, mid, inversions)
        mergeSort(v, mid + 1, right, inversions)
        merge(v, left, mid, right, inversions)

# Function to calculate number of
# inversions in a given array
def CountInversions(v):
    n = len(v)
    inversions = 0

    # Calculate the number of inversions
    mergeSort(v, 0, n - 1, inversions)

    # Return the number of inversions
    return inversions

# Function to count the number of
# substrings that contains more 1s than 0s
def getSubsCount(input):
    n = len(input)

    nums = [0 for i in range(n)]

    for i in range(n):
        nums[i] = ord(input[i]) - 48

        if (nums[i] == 0):
            nums[i] = -1

    # Stores the prefix sum array
    pref = [0 for i in range(n)]

    sum = 0

    for i in range(n):
        sum += nums[i]
        pref[i] = sum

    cnt = 0

    # Stores the count of valid substrings
    for i in range(n):
        if (pref[i] > 0):
            cnt += 1

    pref = pref[:-1]

    inversions = CountInversions(pref)

    ans = cnt + inversions + 1

    return ans

# Driver Code
if __name__ == '__main__':

    # Given Input
    input = "101"

    # Function Call
    ans = getSubsCount(input)
    print(ans)

    # This code is contributed by ipg2016107.
```

****Output:** 

```
3
```** 

*****时间复杂度:** O(NlogN)*
***辅助空间:** O(N)***
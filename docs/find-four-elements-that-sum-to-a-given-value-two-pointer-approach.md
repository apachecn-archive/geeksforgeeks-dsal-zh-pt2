# 找出四个和给定值相加的元素|两点法

> 原文:[https://www . geeksforgeeks . org/find-四元素-给定值之和-双指针方法/](https://www.geeksforgeeks.org/find-four-elements-that-sum-to-a-given-value-two-pointer-approach/)

给定一个大小为 **N** 的整数数组 **arr** 和一个**目标**数，任务是找到其中所有唯一的四胞胎，它们的和等于目标数。

**示例:**

> **输入:** arr[] = {4，1，2，-1，1，-3]，目标= 1
> **输出:**[-3，-1，1，4]，[-3，1，1，2]]
> **解释:**
> 两个四胞胎和等于目标。
> 
> **输入:** arr[] = {2，0，-1，1，-2，2}，目标= 2
> **输出:**[-2，0，2，2]，[-1，0，1，2]]

**两点法:**
这个问题遵循[两点模式](https://www.geeksforgeeks.org/two-pointers-technique/)，与[三重总和为零](https://www.geeksforgeeks.org/find-triplets-array-whose-sum-equal-zero/)有相似之处。

我们可以遵循类似的方法迭代数组，一次取一个数字。在迭代过程中的每一步，我们都将搜索类似于[三元组总和为零](https://www.geeksforgeeks.org/find-triplets-array-whose-sum-equal-zero/)的四胞胎，其总和等于给定的目标。

## C++

```
// C++ program to find four
// elements that sum to a given value

#include <bits/stdc++.h>
using namespace std;

class QuadrupleSumToTarget {

public:
    // Function to find quadruplets
    static vector<vector<int> >
    searchQuadruplets(
        vector<int>& arr,
        int target)
    {
        sort(arr.begin(), arr.end());
        vector<vector<int> > quadruplets;

        for (int i = 0; i < arr.size() - 3; i++) {
            if (i > 0 && arr[i] == arr[i - 1]) {

                // Skip same element
                // to avoid duplicate
                continue;
            }

            for (int j = i + 1; j < arr.size() - 2; j++) {
                if (j > i + 1 && arr[j] == arr[j - 1]) {

                    // Skip same element
                    // to avoid duplicate quad
                    continue;
                }
                searchPairs(
                    arr, target,
                    i, j, quadruplets);
            }
        }
        return quadruplets;
    }

private:
    // Function to search Quadruplets
    static void
    searchPairs(
        const vector<int>& arr,
        int targetSum, int first,
        int second,
        vector<vector<int> >& quadruplets)
    {
        int left = second + 1;
        int right = arr.size() - 1;

        while (left < right) {
            int sum
                = arr[first]
                  + arr[second]
                  + arr[left]
                  + arr[right];

            if (sum == targetSum) {

                // Found the quadruplet
                quadruplets
                    .push_back(
                        { arr[first], arr[second],
                          arr[left],
                          arr[right] });
                left++;
                right--;

                // Skip same element to avoid
                // duplicate quadruplets
                while (left < right
                       && arr[left]
                              == arr[left - 1]) {
                    left++;
                }

                // Skip same element to avoid
                // duplicate quadruplets
                while (left < right
                       && arr[right]
                              == arr[right + 1]) {
                    right--;
                }
            }

            // We need a pair
            // with a bigger sum
            else if (sum < targetSum) {
                left++;
            }

            // We need a pair
            // with a smaller sum
            else {
                right--;
            }
        }
    }
};

void printQuad(
    vector<int>& vec, int target)
{

    // Function call
    auto result
        = QuadrupleSumToTarget::
            searchQuadruplets(
                vec, target);

    // Print Quadruples
    for (int j = 0; j < result.size(); j++) {
        vector<int> vec = result[j];
        if (j == 0)
            cout << "[";

        for (int i = 0; i < vec.size(); i++) {

            if (i == 0)
                cout << "[";
            cout << vec[i];
            if (i != vec.size() - 1)
                cout << ", ";
            else
                cout << "]";
        }

        if (j != result.size() - 1)
            cout << ", ";
        else
            cout << "]";
    }
}

// Driver code
int main(int argc, char* argv[])
{
    vector<int> vec
        = { 4, 1, 2,
            -1, 1, -3 };
    int target = 1;

    printQuad(vec, target);

    return 0;
}
```

**Output:**

```
[[-3, -1, 1, 4], [-3, 1, 1, 2]]

```

**时间复杂度:**排序数组需要 **O(N*logN)** 。总的来说**搜索四胞胎()**将取 **O(N * logN + N^3)** ，这与 **O(N^3)** 是渐近等价的。

**辅助空间复杂度:**上述算法的辅助空间复杂度将为排序所需的 **O(N)** 。

**类似文章:**

1.  [找出和给定值相加的四个元素|集合 1 (n^3 解)](https://www.geeksforgeeks.org/find-four-numbers-with-sum-equal-to-given-sum/)
2.  [找出与给定值相加的四个元素|集合 2 ( O(n^2Logn)解)](https://www.geeksforgeeks.org/find-four-elements-that-sum-to-a-given-value-set-2/)
3.  [找出四个和给定值相加的元素|集合 3 (Hashmap)](https://www.geeksforgeeks.org/find-four-elements-sum-given-value-set-3-hashmap/)
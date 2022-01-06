# 给定总和的四胞胎计数|第 3 组

> 原文:[https://www . geesforgeks . org/给定和集的四胞胎计数-3/](https://www.geeksforgeeks.org/count-of-quadruplets-with-given-sum-set-3/)

给定包含整数元素的四个数组和一个整数**和**，任务是对四胞胎进行计数，使得每个元素从不同的数组中选择，并且所有四个元素的和等于给定的**和**。

**示例:**

> **输入:** P[] = {0，2}，Q[] = {-1，-2}，R[] = {2，1}，S[] = {2，-1}，和= 0
> **输出:** 2
> (0，-1，2，-1)和(2，-2，1，-1)是必需的四胞胎。
> 
> **输入:** P[] = {1，-1，2，3，4}，Q[] = {3，2，4}，R[] = {-2，-1，2，1}，S[] = {4，-1}，sum = 3
> T3】输出: 10

**方法:**本文的[第 1 集](https://www.geeksforgeeks.org/count-of-quadruplets-with-given-sum/)和[第 2 集](https://www.geeksforgeeks.org/count-of-quadruplets-with-given-sum-set-2/)已经讨论了解决这个问题的两种不同方法。这里，将讨论使用[二分搜索法](https://www.geeksforgeeks.org/binary-search/)的方法。
选择任意两个数组，计算所有可能的对和，并将它们存储在一个向量中。现在，选择另外两个数组，计算所有可能的和，对于每个和，比如 **tempSum** ，使用二分搜索法检查**sum–temp**是否存在于之前创建的向量中(在[排序](https://www.geeksforgeeks.org/merge-sort/)之后)。

下面是上述方法的实现:

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the count
// of the required quadruplets
int countQuadruplets(int arr1[], int n1, int arr2[],
                     int n2, int arr3[], int n3,
                     int arr4[], int n4, int value)

{
    vector<int> sum1;
    vector<int>::iterator it;
    vector<int>::iterator it2;
    int cnt = 0;

    // Take every possible pair sum
    // from the two arrays
    for (int i = 0; i < n1; i++) {
        for (int j = 0; j < n2; j++) {

            // Push the sum to a vector
            sum1.push_back(arr1[i] + arr2[j]);
        }
    }

    // Sort the sum vector
    sort(sum1.begin(), sum1.end());

    // Calculate the pair sums from
    // the other two arrays
    for (int i = 0; i < n3; i++) {
        for (int j = 0; j < n4; j++) {

            // Calculate the sum
            int temp = arr3[i] + arr4[j];

            // Check whether temp can be added to any
            // sum stored in the sum1 vector such that
            // the result is the required sum
            if (binary_search(sum1.begin(), sum1.end(), value - temp)) {

                // Add the count of such values from the sum1 vector
                it = lower_bound(sum1.begin(), sum1.end(), value - temp);
                it2 = upper_bound(sum1.begin(), sum1.end(), value - temp);
                cnt = cnt + ((it2 - sum1.begin()) - (it - sum1.begin()));
            }
        }
    }

    return cnt;
}

// Driver code
int main()
{
    int arr1[] = { 0, 2 };
    int n1 = sizeof(arr1) / sizeof(arr1[0]);

    int arr2[] = { -1, -2 };
    int n2 = sizeof(arr2) / sizeof(arr2[0]);

    int arr3[] = { 2, 1 };
    int n3 = sizeof(arr3) / sizeof(arr3[0]);

    int arr4[] = { 2, -1 };
    int n4 = sizeof(arr4) / sizeof(arr4[0]);

    int sum = 0;

    cout << countQuadruplets(arr1, n1, arr2, n2,
                             arr3, n3, arr4, n4, sum);

    return 0;
}
```

**Output:**

```
2

```
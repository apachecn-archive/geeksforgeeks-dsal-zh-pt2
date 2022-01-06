# 最大化给定二进制字符串中具有相同 0 和 1 比率的分区

> 原文:[https://www . geesforgeks . org/maximum-给定二进制字符串中的分区具有相同的 0 和 1 比率/](https://www.geeksforgeeks.org/maximize-partitions-in-given-binary-string-having-same-ratio-of-0s-and-1s/)

给定一个大小为 **N** 的[二进制字符串](https://www.geeksforgeeks.org/tag/binary-string/) **S** ，任务是找到[字符串](https://www.geeksforgeeks.org/string-data-structure/) **S** 的最大分区数，使得所有分区中 **0** 和 **1** 的数量之比相同。

**示例:**

> ***输入:**S = " 010100001 "*
> ***输出:** 3*
> ***解释:***
> *子串【0，2】、【3，5】和【6，8】具有相同的比例“**0′**和**‘1’**为 2:1。因此，最大可能的分区是 3。*
> 
> ***输入:**str = " 001101 "*
> ***输出:** 2*

**朴素方法:**朴素方法是[生成字符串 S](https://www.geeksforgeeks.org/generate-unique-partitions-of-an-integer/) 的所有分区，找到最大频率为 **0** 到 **1** 比值的分区。
***时间复杂度:**O(N * 2<sup>N</sup>)*
***辅助空间:** O(N)*

**有效方法:**要解决这个问题，首先看一些观察:

> 假设有两个前缀字符串获得相同的 **0** 和 **1** 的比率。然后可以将较大的前缀分成两个具有相同比例的前缀。对于 eg-S = " 0101 "**前缀【0，1】**的比例为 **1:1** ，**前缀【0，3】**的比例为 **1:1** ，则可以将字符串分成两部分，比例为 **1:1** 。因此，只需计算与[字符串](https://www.geeksforgeeks.org/string-class-in-java/) **S** 具有相同 0 和 1 比例的前缀数量，并打印具有该比例的前缀数量。

按照以下步骤解决问题:

*   初始化两个整数变量，将 **count_of_0** 和 **count_of_1** 设为 **0** ，分别存储**‘0’**和**‘1’**字符的个数。
*   初始化一个[散列图](https://www.geeksforgeeks.org/hashing-data-structure/)，比如说 **M** ，它存储了“**0′**与“**1′**的频率比。
*   [使用变量 **i** 在范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，N-1】**中迭代，并执行以下步骤:
    *   **如果 S[i]** 等于**‘0’**，则将**计数 _of_0** 增加 **1，**否则将**计数 _of_1** 增加 **1** 。
    *   找到**的[GCD](https://www.geeksforgeeks.org/basic-and-extended-euclidean-algorithms/)count _ of _ 0**和 **count_of_1** 并将其存储在一个变量中，比如 **GCD** 。
    *   如果 **GCD = 0** ，则通过 **1** 增加 **m[{count_of_0，count_of_1}]** 。
    *   如果 **GCD！= 0** ，然后将**m 【{ count _ of _ 0/GCD，count _ of _ 1/GCD }】**的值增加 **1** 。
*   打印 **m[{count_of_0 / GCD，count_of_1 / GCD}]的值**作为答案。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find maximum partition such
// that the ratio of 0 and 1 are same
void maximumPartition(string S)
{

    // Size of string
    int N = S.size();

    // Variable to store the frequency
    // of 0 and 1
    int count_of_0 = 0, count_of_1 = 0;

    // Map to store frequency of ratio
    map<pair<int, int>, int> m;

    int ans;

    // Traverse the string
    for (int i = 0; i < N; i++) {
        // Increment the frequency
        // of 0 by 1 if s[i] = 0
        if (S[i] == '0')
            count_of_0++;
        // Otherwise increment frequency of 1
        else
            count_of_1++;

        int first = count_of_0, second = count_of_1;

        // Find GCD of count_of_0 and count_of_1
        int GCD = __gcd(count_of_0, count_of_1);

        // Convert the count of 0 and count of 1
        // in the coprime numbers
        if (GCD != 0) {
            first = count_of_0 / GCD;
            second = count_of_1 / GCD;
        }

        // Increase the ratio of 0 and 1 by 1
        m[{ first, second }]++;
        ans = m[{ first, second }];
    }

    cout << ans << endl;
}

// Driver Code
int main()
{
    // Given Input
    string S = "001101";

    // Function Call
    maximumPartition(S);
    return 0;
}
```

**Output**

```
2
```

***时间复杂度:** O(N log N)*
***辅助空间:** O(N)*
# 在相同奇偶校验指数下最多使用 K 次交换的字典序最大字符串

> 原文:[https://www . geesforgeks . org/按字典顺序排列的最大字符串最多使用 k 个相同奇偶校验交换索引/](https://www.geeksforgeeks.org/lexicographically-largest-string-using-at-most-k-swaps-at-same-parity-indices/)

给定字符串**S**和正整数 **K** ，任务是在条件为被交换的索引必须都是奇数或都是偶数的情况下，最多使用 **K** 交换来寻找字典上最大的可能的[字符串](https://www.geeksforgeeks.org/string-data-structure/)。

**示例:**

> **输入:** S = "ancqz "，K = 2
> **输出:“**zqcna**”**
> **解释:**在一次交换中，我们可以交换字符‘n’和‘q’，因为它们都处于偶数索引(假设基于 1 的索引为 2 和 4)。字符串变成“aqcnz”。在第二次交换中，我们可以交换字符“a”和“z ”,因为它们都有奇数索引。最后一个字符串“zqcna”是使用 2 次交换操作的最大可能字典。
> 
> 注意:我们不能交换实例“a”和“n”或“n”和“z”，因为其中一个位于奇数索引，而另一个位于偶数索引。
> 
> **输入:** S = "geeksforgeeks "，K = 3
> **输出:“**sreksfoegegg**”**

**幼稚的做法:**幼稚的做法微不足道。使用[贪婪算法](https://www.geeksforgeeks.org/greedy-algorithms/)通过选择当前索引右侧的最大可能字符，使当前索引从左侧开始最大化，该字符也具有相同的索引奇偶校验(即，如果当前索引为奇数，则为奇数，如果当前索引为偶数，则为偶数)。在大气中重复相同的步骤 **K** 次。该方法的时间复杂度为 **O(N <sup>2</sup> )** 。

**高效方法:**使用[优先级队列](https://www.geeksforgeeks.org/priority-queue-set-1-introduction/)可以改进上述方法。按照以下步骤解决问题:

*   创建两个[优先级队列](https://www.geeksforgeeks.org/priority-queue-set-1-introduction/)，一个用于奇数索引字符，另一个用于偶数索引字符。
*   [遍历字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/)中的字符，如果出现偶数索引字符，则在保存偶数字符的[优先级队列](https://www.geeksforgeeks.org/priority-queue-set-1-introduction/)中搜索大于当前索引的索引和大于当前字符的字符。如果有，交换两个字符推送当前字符和我们在[优先级队列](https://www.geeksforgeeks.org/priority-queue-set-1-introduction/)中找到的索引。
*   当奇怪的字符出现时，也要遵循同样的程序。
*   如果 **K** 变为 **0** ，终止循环。
*   合成的[弦](https://www.geeksforgeeks.org/string-data-structure/)将是答案。

下面是上述方法的实现:

## C++

```
// C++ program of the above approach
#include <bits/stdc++.h>
using namespace std;

// Function which returns
// the largest possible string
string lexicographicallyLargest(string S, int K)
{
    // Finding length of the string
    int n = S.length();

    // Creating two priority queues of pairs
    // for odd and even indices separately
    priority_queue<pair<char, int> > pqOdd, pqEven;

    // Storing all possible even
    // indexed values as pairs
    for (int i = 2; i < n; i = i + 2) {
        // Stores pair as {character, index}
        pqEven.push(make_pair(S[i], i));
    }

    // Storing all possible odd indexed
    // values as pairs
    for (int i = 3; i < n; i = i + 2) {
        // Stores pair as {character, index}
        pqOdd.push(make_pair(S[i], i));
    }

    for (int i = 0; i < n; i++) {
        // For even indices
        if (i % 2 == 0) {

            // Removing pairs which
            // cannot be used further
            while (!pqEven.empty()
                   and pqEven.top().second <= i)
                pqEven.pop();

            // If a pair is found whose index comes after
            // the current index and its character is
            // greater than the current character
            if (!pqEven.empty()
                and pqEven.top().first > S[i]) {

                // Swap the current index with index of
                // maximum found character next to it
                swap(S[i], S[pqEven.top().second]);

                int idx = pqEven.top().second;
                pqEven.pop();
                // Push the updated character at idx index
                pqEven.push({ S[idx], idx });
                K--;
            }
        }
        // For odd indices
        else {
            // Removing pairs which cannot
            // be used further

            while (!pqOdd.empty()
                   and pqOdd.top().second <= i)
                pqOdd.pop();

            // If a pair is found whose index comes after
            // the current index and its character is
            // greater than the current character

            if (!pqOdd.empty()
                and pqOdd.top().first > S[i]) {

                // Swap the current index with index of
                // maximum found character next to it
                swap(S[i], S[pqOdd.top().second]);
                int idx = pqOdd.top().second;
                pqOdd.pop();

                // Push the updated character at idx index
                pqOdd.push({ S[idx], idx });
                K--;
            }
        }
        // Breaking out of the loop if K=0
        if (K == 0)
            break;
    }

    return S;
}

// Driver Code
int main()
{
    // Input
    string S = "geeksforgeeks";
    int K = 2;

    // Function Call
    cout << lexicographicallyLargest(S, K);
    return 0;
}
```

**Output:**

```
sreksfoegeekg

```

**时间复杂度:**O(NlogN)
T3】辅助空间:T5**T7O(N)**T10】****
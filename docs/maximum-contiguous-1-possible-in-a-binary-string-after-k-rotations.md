# k 次旋转后二进制字符串中最大可能的连续 1

> 原文:[https://www . geesforgeks . org/maximum-continuous-1-in-a-a-binary-string-after-k-rotations/](https://www.geeksforgeeks.org/maximum-contiguous-1-possible-in-a-binary-string-after-k-rotations/)

给定一个二进制字符串，您可以旋转该字符串的任何子字符串。例如，让字符串用 s 表示，让字符串的第一个元素用 s[0]表示，第二个元素用 s[1]表示，以此类推。
s = "100110111 "

假设，我们旋转从 s[2]开始到 s[4]结束的子串。那么这个操作之后的字符串将是:
结果字符串=“101100111”

现在，您最多可以执行 k 个操作来旋转任何子字符串。你必须告诉在这个字符串中你能做的连续 1 的最大数目，在 k 或小于 k 的子串旋转中。

示例:

> 输入:100011001
> k = 1
> 输出:3
> 说明:
> k 为 1，因此只能旋转一次。旋转从 s[1]开始到 s[5]结束的子字符串。结果字符串将是:111000001。因此，最大连续 1 是 3。
> 
> 输入:001100111000110011100
> k = 2
> 输出:8
> 说明:
> k 为 2，因此可以旋转两次。旋转从 s[6]开始到 s[15]结束的子字符串。第一次旋转后的结果字符串:0011000011000111100。然后，旋转从 s[8]开始到 s[12]结束的子字符串。第二次旋转后的结果字符串:00110000000111111100。因此，连续 1 的最大数量是 8。

**概念求解:**
为了解决这个问题，我们将在多集合中保持原始字符串中连续 1 的部分中 1 的频率。然后在每次旋转时，我们将旋转该子串，使得串中连续 1 的两个部分(具有最大频率)聚集在一起。我们将通过从最大到最小的元素对多集进行排序来做到这一点。我们将取出多集的前 2 个元素，并将它们的总和插入多集。我们将继续这样做，直到 k 个旋转完成，或者多集合中的元素数减少到 1。

```
// C++ program to calculate maximum contiguous
// ones in string
#include <bits/stdc++.h>
using namespace std;

// function to calculate maximum contiguous ones
int maxContiguousOnes(string s, int k)
{

    int i, j, a, b, count;

    // multiset is used to store frequency  of 
    // 1's of each portion of contiguous 1 in 
    // string in decreasing order
    multiset<int, greater<int> > m;

    // this loop calculate all the frequency
    // and stores them in multiset
    for (i = 0; i < s.length(); i++) {
        if (s[i] == '1') {
            count = 0;
            j = i;
            while (s[j] == '1' && j < s.length()) {
                count++;
                j++;
            }
            m.insert(count);
            i = j - 1;
        }
    }

    // if their is no 1 in string, then return 0
    if (m.size() == 0)
        return 0;

    // calculates maximum contiguous 1's on
    // doing rotations
    while (k > 0 && m.size() != 1) {

        // Delete largest two elements
        a = *(m.begin()); 
        m.erase(m.begin()); 
        b = *(m.begin()); 
        m.erase(m.begin()); 

        // insert their sum back into the multiset
        m.insert(a + b); 
        k--;
    }

    // return maximum contiguous ones 
    // possible after k rotations
    return *(m.begin());
}

// Driver code
int main()
{
    string s = "10011110011";
    int k = 1;
    cout << maxContiguousOnes(s, k);
    return 0;
}
```

**Output:**

```
6

```
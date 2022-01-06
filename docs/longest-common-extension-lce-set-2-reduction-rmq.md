# 最长公共分机/ LCE |第 2 集(还原到 RMQ)

> 原文:[https://www . geesforgeks . org/long-common-extension-lce-set-2-reduction-rmq/](https://www.geeksforgeeks.org/longest-common-extension-lce-set-2-reduction-rmq/)

先决条件:

*   [后缀数组|集合 2](https://www.geeksforgeeks.org/suffix-array-set-2-a-nlognlogn-algorithm/)
*   [kasai 的算法](https://www.geeksforgeeks.org/%C2%AD%C2%ADkasais-algorithm-for-construction-of-lcp-array-from-suffix-array/)

最长公共扩展(LCE)问题考虑一个字符串 **s** ，并为每对(L，R)计算从 L 和 R 开始的 **s** 的最长子字符串。在 LCE，在每个查询中，我们必须回答从索引 L 和 R 开始的最长公共前缀的长度。
**示例:**
**字符串**:【阿巴巴巴】
**查询:** LCE(1，2)，LCE(1，6) 5)
找出从给定索引开始的最长公共前缀的长度， **(1，2)、(1，6)和(0，5)** 。
突出显示的字符串“绿色”是从相应查询的索引- L 和 R 开始的最长公共前缀。我们必须找到从索引- **(1，2)、(1，6)和(0，5)** 开始的最长公共前缀的长度。

![Longest Common Extension](img/939034d902777406075a4f62c0af1883.png)

在[集合 1](https://www.geeksforgeeks.org/longest-common-extension-lce-set-1-introduction-and-naive-method/) 中，我们解释了在许多查询中寻找字符串 LCE 长度的简单方法。在这个集合中，我们将展示如何将 LCE 问题简化为 RMQ 问题，从而降低朴素方法的渐近时间复杂度。

**将 LCE 降为**[**RMQ**T5】](https://www.geeksforgeeks.org/range-minimum-query-for-static-array/)

让输入字符串为 **S** ，查询的形式为 **LCE(L，R)** 。让 s 的后缀数组为 **Suff[]** ，lcp 数组为 **lcp[]** 。
S 的两个后缀 S <sub>L</sub> 和 S <sub>R</sub> 之间最长的公共扩展可以通过以下方式从 lcp 数组中获得。

*   设 low 为 S 的后缀中 S <sub>L</sub> 的秩(即 suf【low】= L)。
*   设 S 的后缀中 S <sub>R</sub> 的等级为高，不失一般性，我们假设低<为高。
*   那么 S <sub>L</sub> 和 S <sub>R</sub> 最长的公共延长线就是 lcp(低，高)= min <sub>(低< =k <高)</sub>LCP【k】。

**证明:**Let S<sub>L</sub>= S<sub>L</sub>…S<sub>L+C</sub>…S<sub>n</sub>和 S<sub>R</sub>= S<sub>R</sub>…S<sub>R+C</sub>…S<sub>n</sub>，让 C 成为 S <sub>L</sub> 和 S <sub>R</sub> 最长的共同延伸我们假设字符串 S 有一个哨点字符，这样 S 的后缀除了它自己之外，都不是任何其他后缀的前缀。

*   如果 low = high–1，那么 i = low，lcp[low] = c 是 S <sub>L</sub> 和 S <sub>R</sub> 最长的公共延伸，我们就完成了。
*   如果 low < high -1，则选择 I，这样 lcp[i]就是 lcp 数组的区间[low，high]中的最小值。我们有两种可能的情况:
    *   如果 c < lcp[i] we have a contradiction because S <sub>L</sub> 。。。S <sub>L+lcp[i]-1</sub> = S <sub>R</sub> 。。。S <sub>R</sub> +lcp[i]-1 通过 lcp 表的定义，以及 LCP 的条目对应 s 的排序后缀的事实。
    *   如果 c > lcp[i]，让 high = suf[I]，这样 S <sub>high</sub> 就是与位置 I 相关的后缀，S <sub>i</sub> 就是这样 s <sub>high</sub> 。。。s <sub>高+lcp[i]-1</sub> = S <sub>L</sub> 。。。S <sub>L+lcp[i]-1</sub> 和 s <sub>高</sub>。。。s <sub>高+lcp[i]-1</sub> = S <sub>R</sub> 。。。S <sub>R+lcp[i]-1</sub> ，但自 S <sub>L</sub> 起。。。S <sub>L+c-1</sub> = S <sub>R</sub> 。。。S <sub>R+c-1</sub> 我们有 lcp 数组应该是错误排序的，这是矛盾的。

因此，我们有 c = lcp[i]
因此，我们已经将我们最长的公共扩展查询简化为 lcp 中范围内的范围最小查询。

**算法**

*   为了找到低和高，我们必须首先计算后缀数组，然后从后缀数组中计算逆后缀数组。
*   我们还需要 lcp 数组，因此我们使用 Kasai 的算法从后缀数组中找到 lcp 数组。
*   完成上述操作后，我们只需为每个查询找到 lcp 数组中从索引低到高的最小值(如上所述)。

最小值是该查询的 LCE 长度。
**实施**

## C

```
// A C++ Program to find the length of longest common
// extension using Direct Minimum Algorithm
#include<bits/stdc++.h>
using namespace std;

// Structure to represent a query of form (L,R)
struct Query
{
    int L, R;
};

// Structure to store information of a suffix
struct suffix
{
    int index;  // To store original index
    int rank[2]; // To store ranks and next rank pair
};

// A utility function to get minimum of two numbers
int minVal(int x, int y) { return (x < y)? x: y; }

// A utility function to get minimum of two numbers
int maxVal(int x, int y) { return (x > y)? x: y; }

// A comparison function used by sort() to compare
// two suffixes Compares two pairs, returns 1 if
// first pair is smaller
int cmp(struct suffix a, struct suffix b)
{
    return (a.rank[0] == b.rank[0])?
                   (a.rank[1] < b.rank[1]):
                   (a.rank[0] < b.rank[0]);
}

// This is the main function that takes a string 'txt'
// of size n as an argument, builds and return the
// suffix array for the given string
vector<int> buildSuffixArray(string txt, int n)
{
    // A structure to store suffixes and their indexes
    struct suffix suffixes[n];

    // Store suffixes and their indexes in an array
    // of structures.
    // The structure is needed to sort the suffixes
    // alphabetically and maintain their old indexes
    // while sorting
    for (int i = 0; i < n; i++)
    {
        suffixes[i].index = i;
        suffixes[i].rank[0] = txt[i] - 'a';
        suffixes[i].rank[1] =
                 ((i+1) < n)? (txt[i + 1] - 'a'): -1;
    }

    // Sort the suffixes using the comparison function
    // defined above.
    sort(suffixes, suffixes+n, cmp);

    // At his point, all suffixes are sorted according
    // to first 2 characters.  Let us sort suffixes
    // according to first 4/ characters, then first 8
    // and so on

    // This array is needed to get the index in suffixes[]
    // from original index.  This mapping is needed to get
    // next suffix.
    int ind[n];

    for (int k = 4; k < 2*n; k = k*2)
    {
        // Assigning rank and index values to first suffix
        int rank = 0;
        int prev_rank = suffixes[0].rank[0];
        suffixes[0].rank[0] = rank;
        ind[suffixes[0].index] = 0;

        // Assigning rank to suffixes
        for (int i = 1; i < n; i++)
        {
            // If first rank and next ranks are same as
            // that of previous/ suffix in array, assign
            // the same new rank to this suffix
            if (suffixes[i].rank[0] == prev_rank &&
                suffixes[i].rank[1] == suffixes[i-1].rank[1])
            {
                prev_rank = suffixes[i].rank[0];
                suffixes[i].rank[0] = rank;
            }
            else // Otherwise increment rank and assign
            {
                prev_rank = suffixes[i].rank[0];
                suffixes[i].rank[0] = ++rank;
            }
            ind[suffixes[i].index] = i;
        }

        // Assign next rank to every suffix
        for (int i = 0; i < n; i++)
        {
            int nextindex = suffixes[i].index + k/2;
            suffixes[i].rank[1] = (nextindex < n)?
                           suffixes[ind[nextindex]].rank[0]: -1;
        }

        // Sort the suffixes according to first k characters
        sort(suffixes, suffixes+n, cmp);
    }

    // Store indexes of all sorted suffixes in the suffix array
    vector<int>suffixArr;
    for (int i = 0; i < n; i++)
        suffixArr.push_back(suffixes[i].index);

    // Return the suffix array
    return  suffixArr;
}

/* To construct and return LCP */
vector<int> kasai(string txt, vector<int> suffixArr,
                              vector<int> &invSuff)
{
    int n = suffixArr.size();

    // To store LCP array
    vector<int> lcp(n, 0);

    // Fill values in invSuff[]
    for (int i=0; i < n; i++)
        invSuff[suffixArr[i]] = i;

    // Initialize length of previous LCP
    int k = 0;

    // Process all suffixes one by one starting from
    // first suffix in txt[]
    for (int i=0; i<n; i++)
    {
        /* If the current suffix is at n-1, then we don’t
           have next substring to consider. So lcp is not
           defined for this substring, we put zero. */
        if (invSuff[i] == n-1)
        {
            k = 0;
            continue;
        }

        /* j contains index of the next substring to
           be considered  to compare with the present
           substring, i.e., next string in suffix array */
        int j = suffixArr[invSuff[i]+1];

        // Directly start matching from k'th index as
        // at-least k-1 characters will match
        while (i+k<n && j+k<n && txt[i+k]==txt[j+k])
            k++;

        lcp[invSuff[i]] = k; // lcp for the present suffix.

        // Deleting the starting character from the string.
        if (k>0)
            k--;
    }

    // return the constructed lcp array
    return lcp;
}

// A utility function to find longest common extension
// from index - L and index - R
int LCE(vector<int> lcp, vector<int>invSuff, int n,
        int L, int R)
{
    // Handle the corner case
    if (L == R)
        return (n-L);

    int low = minVal(invSuff[L], invSuff[R]);
    int high = maxVal(invSuff[L], invSuff[R]);

    int length = lcp[low];

    for (int i=low+1; i<high; i++)
    {
        if (lcp[i] < length)
            length = lcp[i];
    }

    return (length);
}

// A function to answer queries of longest common extension
void LCEQueries(string str, int n, Query q[],
                             int m)
{
    // Build a suffix array
    vector<int>suffixArr = buildSuffixArray(str, str.length());

    // An auxiliary array to store inverse of suffix array
    // elements. For example if suffixArr[0] is 5, the
    // invSuff[5] would store 0.  This is used to get next
    // suffix string from suffix array.
    vector<int> invSuff(n, 0);

    // Build a lcp vector
    vector<int>lcp = kasai(str, suffixArr, invSuff);

    for (int i=0; i<m; i++)
    {
        int L = q[i].L;
        int R = q[i].R;

        printf ("LCE (%d, %d) = %d\n", L, R,
                        LCE(lcp, invSuff, n, L, R));
    }

    return;
}

// Driver Program to test above functions
int main()
{
    string str = "abbababba";
    int n = str.length();

    // LCA Queries to answer
    Query q[] = {{1, 2}, {1, 6}, {0, 5}};
    int m = sizeof(q)/sizeof(q[0]);

    LCEQueries(str, n, q, m);

    return (0);
}
```

输出:

```
LCE (1, 2) = 1
LCE (1, 6) = 3
LCE (0, 5) = 4
```

**RMQ 法归约分析**
**时间复杂度:**

*   构建 lcp 和后缀数组需要 **O(N.logN)** 时间。
*   回答每个查询需要**O(| invsuf[R]–invsuf[L]|)**。

因此总的时间复杂度是**O(n . logn+Q .(| inv suff[R]–inv suff[L]|))**
其中，
**Q**= LCE 查询数。
**N** =输入字符串的长度。
**invSuff[]** =输入字符串的逆后缀数组。
虽然这看起来是一个低效的算法，但是该算法在回答 LCE 查询方面通常优于所有其他算法。
我们将在下一集详细描述这种方法的性能。

**辅助空间:**我们使用 **O(N)** 辅助空间来存储 lcp、后缀和逆后缀数组。

**参考:**

*   [http://www . science direct . com/science/article/pii/s 1570866710000377](http://www.sciencedirect.com/science/article/pii/S1570866710000377)

本文由**拉希特·贝尔瓦亚尔**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。

如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。
# 通过翻转给定二进制字符串中最多 K 个位来最大化分配权重的总和

> 原文:[https://www . geeksforgeeks . org/通过在给定二进制字符串中翻转最多 k 位来最大化分配权重的总和/](https://www.geeksforgeeks.org/maximize-sum-of-assigned-weights-by-flipping-at-most-k-bits-in-given-binary-string/)

给定一个长度为 **N** 的[二进制字符串](https://www.geeksforgeeks.org/tag/binary-string/) **字符串**和一个整数 **K** ，任务是通过翻转给定二进制字符串中最多 K 个位来找到分配权重的最大可能和。分配给该字符串字符的权重如下:

*   如果一个字符是**‘0’**，那么权重就是 **0** 。
*   如果一个字符是**‘1’**，它前面的字符也是**‘1’**，那么权重就是 **2** 。
*   如果一个字符是**‘1’**并且它前面没有字符或者它前面的字符是**‘0’**，那么权重就是 **1** 。

**示例:**

> **输入:** str = "10100 "，K = 2
> **输出:** 7
> **解释:**
> **第一次翻转:**翻转索引 1 处的字符，字符串变为“11100”。
> **第二次翻转:**翻转索引 3 处的字符，字符串变为“11110”。
> 得到的字符串的权重为 1 + 2 + 2 + 2 + 0 = 7，最大。
> 
> **输入:** str = "100101 "，K = 1
> **输出:** 6
> **解释:**
> **第一次翻转:**翻转索引 5 处的字符，字符串变为“100111”。
> 得到的字符串的权重为 1 + 0 + 0 + 1 + 2 + 2 = 6，最大。

**进场:**出现在一个**【1】**之后的人物**【1】**的权重是所有人物中最大的，所以为了最大化和，尽量多造一些这样的 **1s** 。将 **0s** 翻转到 **1** 的段可以按如下优先顺序排列:

*   **第一优先级:**翻转两个 **1s** 之间的所有 **0s** ，这将使表格 **10…01** 的段的重量增加(2*(所包含的 **0s** 的数量)+ 1)。如果 x 大于或等于 **0s 的个数**否则用 2*(括起来的 0s 个数)括起来。
*   **第二优先级“**翻转 **0s** 在字符串中第一个出现的 **1s** 之前的字符串开头，这将使表单段 **0…01** 的权重增加 2*(翻转的 0s 的数量)。
*   **第三优先级:**在字符串中最后一个出现的 **1** 之后的字符串末尾翻转 **0s** ，这将使表单段 **10…0** 的权重增加 2*(翻转的 0s 数量)。

按照上面的优先级翻转给定字符串的字符，使权重最大化，然后在**最多 K 次**翻转后找到结果字符串的权重。

下面是该方法的实现:

## C++

```
// C++ program of the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find maximum sum of
// weights of binary string after
// at most K flips
int findMax(string s, int n, int k)
{
    int ans = 0;

    // Stores lengths of substrings
    // of the form 1..00..1s
    int l = 0;

    // Stores the index of last 1
    // encountered in the string
    int ind = -1;

    // Stores the index of first 1
    // encountered
    int indf = -1;

    // Stores lengths of all substrings
    // having of 0s enclosed by 1s
    // at both ends
    multiset<int> ls;

    // Traverse the string
    for (int i = 0; i < n; i++) {
        // If character is 0
        if (s[i] == '0')
            l++;

        // If character is 1
        // First Priority
        else if (s[i] == '1'
                 && l > 0 && ans != 0) {
            ls.insert(l);
            l = 0;
        }

        // Second Priority
        if (s[i] == '1') {
            ind = i;
            l = 0;
            if (indf == -1)
                indf = i;

            // Add according to the
            // first priority
            if (i > 0 && s[i - 1] == '1')
                ans += 2;
            else
                ans += 1;
        }
    }

    // Stores length of the shortest
    // substring of 0s
    int curr;

    // Convert shortest substrings
    // of 0s to 1s
    while (k > 0 && !ls.empty()) {
        curr = *ls.begin();

        // Add according to the
        // first priority
        if (k >= curr) {
            ans += (2 * curr + 1);
            k -= curr;
        }

        // Add according to the
        // third priority
        else {
            ans += (2 * k);
            k = 0;
        }
        ls.erase(ls.begin());
    }

    // If more 0s can be made into 1,
    // then check for 0s at ends
    if (k > 0) {
        // Update the ans
        ans += (2 * min(k,
                        n - (ind + 1))
                - 1);
        k -= min(k, n - (ind + 1));

        if (ind > -1)
            ans++;
    }

    // If K is non-zero, then flip 0s
    // at the beginning
    if (k > 0) {
        ans += (min(indf, k) * 2 - 1);

        if (indf > -1)
            ans++;
    }

    // Return the final weights
    return ans;
}

// Driver Code
int main()
{
    // Given string str
    string str = "1110000101";

    int N = str.length();

    // Given K flips
    int K = 3;

    // Function Call
    cout << findMax(str, N, K);

    return 0;
}
```

## 蟒蛇 3

```
# Python 3 program of the above approach

# Function to find maximum sum of
# weights of binary string after
# at most K flips
def findMax( s, n, k):

    ans = 0;

    # Stores lengths of substrings
    # of the form 1..00..1s
    l = 0;

    # Stores the index of last 1
    # encountered in the string
    ind = -1;

    # Stores the index of first 1
    # encountered
    indf = -1;

    # Stores lengths of all substrings
    # having of 0s enclosed by 1s
    # at both ends
    ls = set([])

    # Traverse the string
    for i in range(n):
        # If character is 0
        if (s[i] == '0'):
            l+=1

        # If character is 1
        # First Priority
        elif (s[i] == '1'
                 and l > 0 and ans != 0):
            ls.add(l);
            l = 0;

        # Second Priority
        if (s[i] == '1') :
            ind = i;
            l = 0;
            if (indf == -1):
                indf = i;

            # Add according to the
            # first priority
            if (i > 0 and s[i - 1] == '1'):
                ans += 2;
            else:
                ans += 1;

    # Stores length of the shortest
    # substring of 0s
    curr = 0

    # Convert shortest substrings
    # of 0s to 1s
    while (k > 0 and len(ls)!=0):
        for i in ls:
          curr = i
          break

        # Add according to the
        # first priority
        if (k >= curr):
            ans += (2 * curr + 1);
            k -= curr;

        # Add according to the
        # third priority
        else :
            ans += (2 * k);
            k = 0;

        ls.remove(curr);

    # If more 0s can be made into 1,
    # then check for 0s at ends
    if (k > 0) :
        # Update the ans
        ans += (2 * min(k,
                        n - (ind + 1))
                - 1);
        k -= min(k, n - (ind + 1));

        if (ind > -1):
            ans+=1

    # If K is non-zero, then flip 0s
    # at the beginning
    if (k > 0):
        ans += (min(indf, k) * 2 - 1);

        if (indf > -1):
            ans+=1

    # Return the final weights
    return ans

# Driver Code
if __name__ == "__main__":

    # Given string str
    s = "1110000101";

    N = len(s)

    # Given K flips
    K = 3;

    # Function Call
    print(findMax(s, N, K));

    # This code is contributed by chitranayal
```

**Output:** 

```
14
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)
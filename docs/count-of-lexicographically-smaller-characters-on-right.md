# 右侧字典上较小字符的计数

> 原文:[https://www . geeksforgeeks . org/按字典顺序排列的较小字符数/](https://www.geeksforgeeks.org/count-of-lexicographically-smaller-characters-on-right/)

给定一个仅由小写英文字母组成的字符串。任务是统计每个索引处字符右侧按字母顺序排列的较小字符的总数。

**示例:**

> **输入:** str = "edcba"
> **输出:** 4 3 2 1 0
> **说明:**
> 索引 0 右侧小于
> T10】e 的字符数为 **dcba** = 4
> 索引 1 右侧小于
> T16】d 的字符数为 **cba** = 小于
> T22】c 的索引 2 为 **ba** = 2
> 小于
> T28】b 的索引 3 右侧的字符数为 **a** = 1
> 小于
> T34】a 的索引 4 右侧的字符数为 **'\0'** = 0
> 
> **输入:**str = " eaaa "
> T3】输出:3 0 0 0 0

**天真方法:**
想法是逐一遍历字符串每个索引右侧的所有字符，并打印字母顺序较小的字符数。

## C++

```
#include <bits/stdc++.h>
using namespace std;

// function to count the smaller
// characters at the right of index i
void countSmaller(string str)
{

    // store the length of string
    int n = str.length();
    for (int i = 0; i < n; i++) {

        // for each index initialize
        // count as zero
        int cnt = 0;
        for (int j = i + 1; j < n; j++) {

            // increment the count if
            // characters are smaller
            // than at ith index
            if (str[j] < str[i]) {
                cnt += 1;
            }
        }

        // print the count of characters
        // smaller than the index i
        cout << cnt << " ";
    }
}

// Driver code
int main()
{
    // input string
    string str = "edcba";
    countSmaller(str);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
class GFG
{

// function to count the smaller
// characters at the right of index i
static void countSmaller(String str)
{

    // store the length of String
    int n = str.length();
    for (int i = 0; i < n; i++)
    {

        // for each index initialize
        // count as zero
        int cnt = 0;
        for (int j = i + 1; j < n; j++)
        {

            // increment the count if
            // characters are smaller
            // than at ith index
            if (str.charAt(j) < str.charAt(i))
            {
                cnt += 1;
            }
        }

        // print the count of characters
        // smaller than the index i
        System.out.print(cnt+ " ");
    }
}

// Driver code
public static void main(String[] args)
{
    // input String
    String str = "edcba";
    countSmaller(str);
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# function to count the smaller
# characters at the right of index i
def countSmaller(str):

    # store the length of String
    n = len(str);
    for i in range(n):

        # for each index initialize
        # count as zero
        cnt = 0;
        for j in range(i + 1, n):

            # increment the count if
            # characters are smaller
            # than at ith index
            if (str[j] < str[i]):
                cnt += 1;

        # print the count of characters
        # smaller than the index i
        print(cnt, end =" ");

# Driver code
if __name__ == '__main__':

    # input String
    str = "edcba";
    countSmaller(str);

# This code is contributed by PrinciRaj1992
```

## C#

```
using System;

class GFG
{

// function to count the smaller
// characters at the right of index i
static void countSmaller(String str)
{

    // store the length of String
    int n = str.Length;
    for (int i = 0; i < n; i++)
    {

        // for each index initialize
        // count as zero
        int cnt = 0;
        for (int j = i + 1; j < n; j++)
        {

            // increment the count if
            // characters are smaller
            // than at ith index
            if (str[j] < str[i])
            {
                cnt += 1;
            }
        }

        // print the count of characters
        // smaller than the index i
        Console.Write(cnt+ " ");
    }
}

// Driver code
public static void Main(String[] args)
{
    // input String
    String str = "edcba";
    countSmaller(str);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// function to count the smaller
// characters at the right of index i
function countSmaller(str)
{

    // store the length of string
    var n = str.length;
    for (var i = 0; i < n; i++) {

        // for each index initialize
        // count as zero
        var cnt = 0;
        for (var j = i + 1; j < n; j++) {

            // increment the count if
            // characters are smaller
            // than at ith index
            if (str[j] < str[i]) {
                cnt += 1;
            }
        }

        // print the count of characters
        // smaller than the index i
        document.write( cnt + " ");
    }
}

// Driver code
// input string
var str = "edcba";
countSmaller(str);

</script>
```

**Output:** 

```
4 3 2 1 0
```

**时间复杂度:**O(**N<sup>2</sup>T5)，其中 N =弦的长度
**辅助空间:** O(1)** 

**更好的做法:**思路是使用自平衡 BST。
自我平衡的二叉查找树(AVL，红黑，..等等)可以用来得到在 O(N log N)时间复杂度下的解。我们可以扩充这些树，使得每个节点 N 都包含以 N 为根的子树的大小。
我们从右到左遍历字符串，在一个 AVL 树中逐个插入所有元素。在 AVL 树中插入新密钥时，我们首先将密钥与根进行比较。如果键大于根，那么它大于根的左子树中的所有节点。所以我们把左边子树的大小加到正在插入的键的较小元素的数量上。我们对根以下的所有节点递归地遵循相同的方法。
上述办法的实施请参照[本](https://www.geeksforgeeks.org/count-smaller-elements-on-right-side/)条。
**时间复杂度:**O(**N * log N**)
**辅助空间:** O( **N** )

**高效方法:**
想法是使用散列技术，因为字符串只由小写字母组成。所以这里我们可以取一个大小为 **26** 的数组，用来存储索引右侧较小字符的数量。
从右侧遍历数组，不断更新哈希数组中的字符数。现在，为了找到右边较小字符的计数，我们可以简单地遍历大小为 26 的散列数组，以计数到目前为止遇到的较小字符。

## C++

```
#include <bits/stdc++.h>
using namespace std;

// Function to count the smaller
// characters on the right of index i
void countSmaller(string str)
{
    // store the length of string
    int n = str.length();

    // initialize each elements of
    // arr to zero
    int arr[26] = { 0 };

    // array to store count of smaller characters on
    // the right side of that index
    int ans[n];

    for (int i = n - 1; i >= 0; i--) {

        arr[str[i] - 'a']++;

        // initialize the variable to store
        // the count of characters smaller
        // than that at index i
        int ct = 0;

        // adding the count of characters
        // smaller than index i
        for (int j = 0; j < str[i] - 'a'; j++) {
            ct += arr[j];
        }
        ans[i] = ct;
    }

    // print the count of characters smaller
    // than index i stored in ans array
    for (int i = 0; i < n; i++) {
        cout << ans[i] << " ";
    }
}

// Driver Code
int main()
{
    string str = "edcbaa";
    countSmaller(str);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
class GFG
{

// Function to count the smaller
// characters on the right of index i
static void countSmaller(String str)
{
    // store the length of String
    int n = str.length();

    // initialize each elements of
    // arr to zero
    int arr[] = new int[26];

    // array to store count of smaller characters on
    // the right side of that index
    int ans[] = new int[n];

    for (int i = n - 1; i >= 0; i--)
    {

        arr[str.charAt(i) - 'a']++;

        // initialize the variable to store
        // the count of characters smaller
        // than that at index i
        int ct = 0;

        // adding the count of characters
        // smaller than index i
        for (int j = 0; j < str.charAt(i) - 'a'; j++)
        {
            ct += arr[j];
        }
        ans[i] = ct;
    }

    // print the count of characters smaller
    // than index i stored in ans array
    for (int i = 0; i < n; i++)
    {
        System.out.print(ans[i] + " ");
    }
}

// Driver Code
public static void main(String[] args)
{
    String str = "edcbaa";
    countSmaller(str);
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Function to count the smaller
# characters on the right of index i
def countSmaller(str):

    # store the length of String
    n = len(str);

    # initialize each elements of
    # arr to zero
    arr = [0]*26;

    # array to store count of smaller characters on
    # the right side of that index
    ans = [0]*n;

    for i in range(n - 1, -1, -1):

        arr[ord(str[i] ) - ord('a')] += 1;

        # initialize the variable to store
        # the count of characters smaller
        # than that at index i
        ct = 0;

        # adding the count of characters
        # smaller than index i
        for j in range(ord(str[i] ) - ord('a')):
            ct += arr[j];

        ans[i] = ct;

    # print the count of characters smaller
    # than index i stored in ans array
    for i in range(n):
        print(ans[i], end = " ");

# Driver Code
if __name__ == '__main__':
    str = "edcbaa";
    countSmaller(str);

# This code is contributed by Rajput-Ji
```

## C#

```
using System;

class GFG
{

// Function to count the smaller
// characters on the right of index i
static void countSmaller(String str)
{
    // store the length of String
    int n = str.Length;

    // initialize each elements of
    // arr to zero
    int []arr = new int[26];

    // array to store count of smaller characters on
    // the right side of that index
    int []ans = new int[n];

    for (int i = n - 1; i >= 0; i--)
    {

        arr[str[i] - 'a']++;

        // initialize the variable to store
        // the count of characters smaller
        // than that at index i
        int ct = 0;

        // adding the count of characters
        // smaller than index i
        for (int j = 0; j < str[i] - 'a'; j++)
        {
            ct += arr[j];
        }
        ans[i] = ct;
    }

    // print the count of characters smaller
    // than index i stored in ans array
    for (int i = 0; i < n; i++)
    {
        Console.Write(ans[i] + " ");
    }
}

// Driver Code
public static void Main(String[] args)
{
    String str = "edcbaa";
    countSmaller(str);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Function to count the smaller
// characters on the right of index i
function countSmaller(str)
{
    // store the length of string
    var n = str.length;

    // initialize each elements of
    // arr to zero
    var arr = Array(26).fill(0);

    // array to store count of smaller characters on
    // the right side of that index
    var ans = Array(n);

    for (var i = n - 1; i >= 0; i--) {

        arr[str[i].charCodeAt(0) - 'a'.charCodeAt(0)]++;

        // initialize the variable to store
        // the count of characters smaller
        // than that at index i
        var ct = 0;

        // adding the count of characters
        // smaller than index i
        for (var j = 0; j < str[i].charCodeAt(0) - 'a'.charCodeAt(0); j++) {
            ct += arr[j];
        }
        ans[i] = ct;
    }

    // print the count of characters smaller
    // than index i stored in ans array
    for (var i = 0; i < n; i++) {
        document.write( ans[i] + " ");
    }
}

// Driver Code
var str = "edcbaa";
countSmaller(str);

</script>
```

**Output:** 

```
5 4 3 2 0 0
```

**时间复杂度:**O(N * 26)
T3】辅助空间: O(N+26)
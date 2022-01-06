# 通过以任意顺序连接 N 个二进制字符串可能出现的反转对的最小数量

> 原文:[https://www . geeksforgeeks . org/最小反转对数-通过以任意顺序串联 n 个二进制字符串可能/](https://www.geeksforgeeks.org/minimum-count-of-inversion-pairs-possible-by-concatenating-n-binary-strings-in-any-order/)

给定数组形式的 **N** 个字符串**字符串**，每个字符串长度为 **M** ，并且只包含字符“ **a** 和“ **b** ”。任务是在**以任意顺序串联**所有 **N** 串形成的结果串中，找到**反转对**可能的最小数量的计数，而不改变任何单个串的顺序。

> 一个**倒位对**在一个字符串 **S** 中是一对索引 **(i，j)** 这样 i < j 和 **Si = 'b '，Sj = 'a'** 。
> 
> 比如字符串**S = " abababbb "**包含 3 个逆序:(2，3)、(2，5)、(4，5)。

**示例:**

> **输入:N** = 3，M = 2，str = {**“ba”**、**“aa”**、**“ab”**}
> **输出:** 2
> **解释:**如果我们按照 S2+S1+S3 =**aabaab**的顺序连接字符串，那么反转对将位于 **(3，4)** 和
> 
> ****输入:** N = 2，M = 2，str = {**【b】**，**【b】**}
> **输出:** 0**

****方法:**这个问题可以通过 [**贪婪算法**](http://www.geeksforgeeks.org/greedy-algorithms/) 来解决，方法应该是将字符数较高的字符串' **b** '保留在右端。**

**按照以下步骤解决问题:**

1.  **取一个大小为 **n** 的字符串向量来接收输入。**
2.  **[根据特定字符串中“ **b** 的计数，使用比较器对字符串的向量](https://www.geeksforgeeks.org/sorting-a-vector-in-c/)进行排序。**
3.  **取一个空字符串，让我们说 **res =“”。****
4.  **遍历完排序后的向量后，将当前字符串添加到字符串**RES****
5.  **遍历字符串 **res** 并记录**【b】**的出现次数，每当您遇到字符**【a】**时，将到目前为止看到的**【b】**的数量添加到 **ans** 变量中，因为使用该变量**【a】**您可以将到目前为止看到的多个**【b】**配对。** 

**下面是上述方法的实现:**

## **C++**

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Comparator function to sort the vectors
// of strings
bool cmp(string& s1, string& s2)
{
    return count(s1.begin(), s1.end(), 'b')
           < count(s2.begin(), s2.end(), 'b');
}

// Function to find the inversion pairs
int findInversion(vector<string> arr, int N, int M)
{
    // Sort the vector
    sort(arr.begin(), arr.end(), cmp);
    string res = "";

    // Concatenate the strings
    for (int i = 0; i < N; i++) {
        res = res + arr[i];
    }

    // Count number of 'b'
    int cnt = 0;

    // Count the total number of
    // inversion pairs in the entire
    int inversionPairs = 0;

    // N*M =  new size of the concatenated string
    for (int i = 0; i < N * M; i++) {
        // If the current character is 'b'
        // then increase the count of cnt
        if (res[i] == 'b') {

            cnt += 1;
            continue;
        }
        // Add the cnt because that number of
        // pairs can be formed to that that 'a'
        else {
            inversionPairs = inversionPairs + cnt;
        }
    }
    return inversionPairs;
}

// Driver Function
int main()
{

    int N = 3, M = 2;
    vector<string> arr = { "ba" , "aa" , "ab" };

    // Calling the function
    int ans = findInversion(arr, N, M);

    // Printing the answer
    cout << ans << "\n";

    return 0;
}
```

## **蟒蛇 3**

```
# Python program for the above approach

# Comparator function to sort the vectors
# of strings
def cmp(s):
    s1 = s[0]
    s2 = s[1]
    b_in_s1 = 0
    b_in_s2 = 0

    for i in s1:
        if (i == 'b'):
            b_in_s1 += 1
    for i in s2:
        if (i == 'b'):
            b_in_s2 += 1

    if(b_in_s1 == b_in_s2):
        return 0
    return 1 if b_in_s1 - b_in_s2 else -1;

# Function to find the inversion pairs
def findInversion(arr, N, M):

    # Sort the vector
    #arr.sort(key=cmp);
    arr.sort(key=cmp)
    res = "";

    # Concatenate the strings
    for i in range(N):
        res = res + arr[i];

    # Count number of 'b'
    cnt = 0;

    # Count the total number of
    # inversion pairs in the entire
    inversionPairs = 0;

    # N*M =  new size of the concatenated string
    for i in range(N * M):

        # If the current character is 'b'
        # then increase the count of cnt
        if (res[i] == 'b'):

            cnt += 1;
            continue;

        # Add the cnt because that number of
        # pairs can be formed to that that 'a'
        else:
            inversionPairs = inversionPairs + cnt;
    return inversionPairs;

# Driver Function
N = 3
M = 2;
arr = ["ba", "aa", "ab"];

# Calling the function
ans = findInversion(arr, N, M);

# Printing the answer
print(ans);

# This code is contributed by saurabh_jaiswal.
```

## **java 描述语言**

```
<script>
// Javascript program for the above approach

// Comparator function to sort the vectors
// of strings
function cmp(s1, s2) {
    let b_in_s1 = 0
    let b_in_s2 = 0

    for (i of s1)
        if (i == 'b')
            b_in_s1++;
    for (i of s2)
        if (i == 'b')
            b_in_s2++;

    return b_in_s1 - b_in_s2;
}

// Function to find the inversion pairs
function findInversion(arr, N, M)
{

    // Sort the vector
    arr.sort(cmp);
    let res = "";

    // Concatenate the strings
    for (let i = 0; i < N; i++) {
        res = res + arr[i];
    }

    // Count number of 'b'
    let cnt = 0;

    // Count the total number of
    // inversion pairs in the entire
    let inversionPairs = 0;

    // N*M =  new size of the concatenated string
    for (let i = 0; i < N * M; i++) {
        // If the current character is 'b'
        // then increase the count of cnt
        if (res[i] == 'b') {

            cnt += 1;
            continue;
        }
        // Add the cnt because that number of
        // pairs can be formed to that that 'a'
        else {
            inversionPairs = inversionPairs + cnt;
        }
    }
    return inversionPairs;
}

// Driver Function
let N = 3, M = 2;
let arr = ["ba", "aa", "ab"];

// Calling the function
let ans = findInversion(arr, N, M);

// Printing the answer
document.write(ans);

// This code is contributed by saurabh_jaiswal.
</script>
```

****Output**

```
2
```** 

*****时间复杂度:*** O(NlogN)
***辅助空间:*** O(N*M)**
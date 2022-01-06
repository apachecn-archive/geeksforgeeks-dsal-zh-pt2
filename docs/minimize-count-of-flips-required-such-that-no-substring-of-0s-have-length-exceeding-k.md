# 最小化所需的翻转次数，使得 0 的子串长度不超过 K

> 原文:[https://www . geeksforgeeks . org/最小化翻转次数-要求 0 的子串长度不超过-k/](https://www.geeksforgeeks.org/minimize-count-of-flips-required-such-that-no-substring-of-0s-have-length-exceeding-k/)

给定一个长度为 **N** 的二进制字符串**和一个整数 **K** ，其中 **K** 在范围内(1 ≤ K ≤ N)，任务是找到需要对给定字符串执行的最小翻转次数(将 **0** s 转换为 **1** 或相反)，使得结果字符串不包含一起的 **K** 或更多零。**

**示例:**

> **输入:** str = "11100000011 "，K = 3
> **输出:** 2
> **解释:**
> 翻转 6 <sup>th</sup> 和 7 <sup>th</sup> 字符将字符串修改为“11100110011”。
> 因此，长度为 3 或更长的字符串中不存在 0 的子字符串。
> 
> **输入:** str = "110011 "，K = 1
> **输出:** 2
> 翻转第 3 个和第 4 个字符，然后 str = "11111 "，不包含 1 个或多个零。

**天真方法:**最简单的方法是生成给定字符串的所有可能的子字符串，对于每个子字符串，检查它是否只由 0 组成。如果发现是真的，检查它的长度是否超过 K。如果发现为真，则计算该子串所需的翻转次数。最后，打印获得的翻转次数。

***时间复杂度:**O(2<sup>N</sup>)*
***辅助空间:** O(N)*

**有效方法:**要使结果字符串中连续零的计数小于 **K** ，选择仅由长度为 **≥ K** 的零组成的子字符串。因此，问题简化为寻找每个子串中的最小翻转。最终结果将是所有这些子片段的最小翻转的总和。以下是步骤:

1.  将**结果**初始化为 **0** 并将连续零的计数(比如 **cnt_zeros** ) 初始化为 **0** 。
2.  横向移动绳子，遇到**‘0’**时，将**CNT _ zero**增加 **1** 。
3.  如果**CNT _ zero**等于 **K** ，则增加**结果**，并将**CNT _ zero**设置为 **0** 。
4.  当**“1”**到来时，将**CNT _ zero**设置为 **0** ，因为连续零的计数应该变为 **0** 。

以下执行上述方法:

## C++

```
// C++ program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to return minimum
// number of flips required
int min_flips(string& str, int k)
{
    // Base Case
    if (str.size() == 0)
        return 0;

    // Stores the count of
    // minimum number of flips
    int ans = 0;

    // Stores the count of zeros
    // in current substring
    int cnt_zeros = 0;

    for (char ch : str) {

        // If current character is 0
        if (ch == '0') {

            // Continue ongoing
            // substring
            ++cnt_zeros;
        }
        else {

            // Start a new substring
            cnt_zeros = 0;
        }

        // If k consecutive
        // zeroes are obtained
        if (cnt_zeros == k) {
            ++ans;

            // End segment
            cnt_zeros = 0;
        }
    }

    // Return the result
    return ans;
}

// Driver Code
int main()
{
    string str = "11100000011";
    int k = 3;

    // Function call
    cout << min_flips(str, k);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
class GFG{

// Function to return minimum
// number of flips required
static int min_flips(String str, int k)
{

    // Base Case
    if (str.length() == 0)
        return 0;

    // Stores the count of
    // minimum number of flips
    int ans = 0;

    // Stores the count of zeros
    // in current subString
    int cnt_zeros = 0;

    for(char ch : str.toCharArray())
    {

        // If current character is 0
        if (ch == '0')
        {

            // Continue ongoing
            // subString
            ++cnt_zeros;
        }
        else
        {

            // Start a new subString
            cnt_zeros = 0;
        }

        // If k consecutive
        // zeroes are obtained
        if (cnt_zeros == k)
        {
            ++ans;

            // End segment
            cnt_zeros = 0;
        }
    }

    // Return the result
    return ans;
}

// Driver Code
public static void main(String[] args)
{
    String str = "11100000011";
    int k = 3;

    // Function call
    System.out.print(min_flips(str, k));
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to return minimum
# number of flips required
def min_flips(strr, k):

    # Base Case
    if (len(strr) == 0):
        return 0

    # Stores the count of
    # minimum number of flips
    ans = 0

    # Stores the count of zeros
    # in current sub
    cnt_zeros = 0

    for ch in strr:

        # If current character is 0
        if (ch == '0'):

            # Continue ongoing
            # sub
            cnt_zeros += 1
        else:

            # Start a new sub
            cnt_zeros = 0

        # If k consecutive
        # zeroes are obtained
        if (cnt_zeros == k):
            ans += 1

            # End segment
            cnt_zeros = 0

    # Return the result
    return ans

# Driver Code
if __name__ == '__main__':

    strr = "11100000011"
    k = 3

    # Function call
    print(min_flips(strr, k))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program to implement
// the above approach
using System;

class GFG{

// Function to return minimum
// number of flips required
static int min_flips(String str, int k)
{

    // Base Case
    if (str.Length == 0)
        return 0;

    // Stores the count of
    // minimum number of flips
    int ans = 0;

    // Stores the count of zeros
    // in current subString
    int cnt_zeros = 0;

    foreach(char ch in str.ToCharArray())
    {

        // If current character is 0
        if (ch == '0')
        {

            // Continue ongoing
            // subString
            ++cnt_zeros;
        }
        else
        {

            // Start a new subString
            cnt_zeros = 0;
        }

        // If k consecutive
        // zeroes are obtained
        if (cnt_zeros == k)
        {
            ++ans;

            // End segment
            cnt_zeros = 0;
        }
    }

    // Return the result
    return ans;
}

// Driver Code
public static void Main(String[] args)
{
    String str = "11100000011";
    int k = 3;

    // Function call
    Console.Write(min_flips(str, k));
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// javascript program for the
// above approach

// Function to return minimum
// number of flips required
function min_flips(str, k)
{

    // Base Case
    if (str.length == 0)
        return 0;

    // Stores the count of
    // minimum number of flips
    let ans = 0;

    // Stores the count of zeros
    // in current subString
    let cnt_zeros = 0;

    for(let ch in str.split(''))
    {

        // If current character is 0
        if (str[ch] == '0')
        {

            // Continue ongoing
            // subString
            ++cnt_zeros;
        }
        else
        {

            // Start a new subString
            cnt_zeros = 0;
        }

        // If k consecutive
        // zeroes are obtained
        if (cnt_zeros == k)
        {
            ++ans;

            // End segment
            cnt_zeros = 0;
        }
    }

    // Return the result
    return ans;
}

// Driver Code

    let str = "11100000011";
    let k = 3;

    // Function call
    document.write(min_flips(str, k));

 // This code is contributed by decode2207.
</script>
```

**Output:** 

```
2
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)
# 连续 0 和 1 相等的子串计数

> 原文:[https://www . geeksforgeeks . org/子串计数-具有相等的连续 0 和 1/](https://www.geeksforgeeks.org/count-of-sub-strings-with-equal-consecutive-0s-and-1s/)

仅给定二进制字符串 **0 的**和 **1 的**的字符串。任务是统计字符串**串**的子串总数，使得每个子串在其中具有相等数量的连续**0**和**1**。
**示例**

> **输入:** str = "010011"
> **输出:** 4
> **解释:**
> 连续 0 和 1 的子串为“01”、“10”、“0011”、“01”。因此，计数为 4。
> **注:**
> 两个“01”位置不同:[0，1]和[3，4]。
> “010011”具有相同数量的 0 和 1，但它们不是连续的。
> **输入:** str = "0001110010"
> **输出:** 7
> **解释:**
> 连续 0 和 1 的子串为“000111”、“0011”、“01”、“1100”、“10”、“01”、“10”。

**进场:**

*   计算从字符串开始的连续 0(或 1)的数量。
*   然后从字符串**字符串**中 0(或 1)计数结束的位置开始计算连续 1(或 0)的数量。
*   具有连续 0 和 1 的子字符串总数是在以上两步中找到的连续 0 和 1 的最小计数。
*   重复以上步骤，直到弦**弦**结束。

以下是上述方法的实现:

## C++

```
// C++ implementation of the
// above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the count
// of substrings with equal no.
// of consecutive 0's and 1's
int countSubstring(string& S, int& n)
{
    // To store the total count
    // of substrings
    int ans = 0;

    int i = 0;

    // Traversing the string
    while (i < n) {

        // Count of consecutive
        // 0's & 1's
        int cnt0 = 0, cnt1 = 0;

        // Counting subarrays of
        // type "01"
        if (S[i] == '0') {

            // Count the consecutive
            // 0's
            while (i < n && S[i] == '0') {
                cnt0++;
                i++;
            }

            // If consecutive 0's
            // ends then check for
            // consecutive 1's
            int j = i;

            // Counting consecutive 1's
            while (j < n && S[j] == '1') {
                cnt1++;
                j++;
            }
        }

        // Counting subarrays of
        // type "10"
        else {

            // Count consecutive 1's
            while (i < n && S[i] == '1') {
                cnt1++;
                i++;
            }

            // If consecutive 1's
            // ends then check for
            // consecutive 0's
            int j = i;

            // Count consecutive 0's
            while (j < n && S[j] == '0') {
                cnt0++;
                j++;
            }
        }

        // Update the total count
        // of substrings with
        // minimum of (cnt0, cnt1)
        ans += min(cnt0, cnt1);
    }

    // Return answer
    return ans;
}

// Driver code
int main()
{
    string S = "0001110010";
    int n = S.length();

    // Function to print the
    // count of substrings
    cout << countSubstring(S, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the
// above approach
class GFG{

    // Function to find the count
    // of substrings with equal no.
    // of consecutive 0's and 1's
    static int countSubstring(String S, int n)
    {
        // To store the total count
        // of substrings
        int ans = 0;

        int i = 0;

        // Traversing the string
        while (i < n) {

            // Count of consecutive
            // 0's & 1's
            int cnt0 = 0, cnt1 = 0;

            // Counting subarrays of
            // type "01"
            if (S.charAt(i) == '0') {

                // Count the consecutive
                // 0's
                while (i < n && S.charAt(i) == '0') {
                    cnt0++;
                    i++;
                }

                // If consecutive 0's
                // ends then check for
                // consecutive 1's
                int j = i;

                // Counting consecutive 1's
                while (j < n && S.charAt(j) == '1') {
                    cnt1++;
                    j++;
                }
            }

            // Counting subarrays of
            // type "10"
            else {

                // Count consecutive 1's
                while (i < n && S.charAt(i) == '1') {
                    cnt1++;
                    i++;
                }

                // If consecutive 1's
                // ends then check for
                // consecutive 0's
                int j = i;

                // Count consecutive 0's
                while (j < n && S.charAt(j) == '0') {
                    cnt0++;
                    j++;
                }
            }

            // Update the total count
            // of substrings with
            // minimum of (cnt0, cnt1)
            ans += Math.min(cnt0, cnt1);
        }

        // Return answer
        return ans;
    }

    // Driver code
    static public void main(String args[])
    {
        String S = "0001110010";
        int n = S.length();

        // Function to print the
        // count of substrings
        System.out.println(countSubstring(S, n));
    }
}

// This code is contributed by Yash_R
```

## 蟒蛇 3

```
# Python3 implementation of the
# above approach

# Function to find the count
# of substrings with equal no.
# of consecutive 0's and 1's
def countSubstring(S, n) :

    # To store the total count
    # of substrings
    ans = 0;

    i = 0;

    # Traversing the string
    while (i < n) :

        # Count of consecutive
        # 0's & 1's
        cnt0 = 0; cnt1 = 0;

        # Counting subarrays of
        # type "01"
        if (S[i] == '0') :

            # Count the consecutive
            # 0's
            while (i < n and S[i] == '0') :
                cnt0 += 1;
                i += 1;

            # If consecutive 0's
            # ends then check for
            # consecutive 1's
            j = i;

            # Counting consecutive 1's
            while (j < n and S[j] == '1') :
                cnt1 += 1;
                j += 1;

        # Counting subarrays of
        # type "10"
        else :

            # Count consecutive 1's
            while (i < n and S[i] == '1') :
                cnt1 += 1;
                i += 1;

            # If consecutive 1's
            # ends then check for
            # consecutive 0's
            j = i;

            # Count consecutive 0's
            while (j < n and S[j] == '0') :
                cnt0 += 1;
                j += 1;

        # Update the total count
        # of substrings with
        # minimum of (cnt0, cnt1)
        ans += min(cnt0, cnt1);

    # Return answer
    return ans;

# Driver code
if __name__ == "__main__" :
    S = "0001110010";
    n = len(S);

    # Function to print the
    # count of substrings
    print(countSubstring(S, n));

# This code is contributed by Yash_R
```

## C#

```
// C# implementation of the
// above approach
using System;

class GFG{

    // Function to find the count
    // of substrings with equal no.
    // of consecutive 0's and 1's
    static int countSubstring(string S, int n)
    {
        // To store the total count
        // of substrings
        int ans = 0;

        int i = 0;

        // Traversing the string
        while (i < n) {

            // Count of consecutive
            // 0's & 1's
            int cnt0 = 0, cnt1 = 0;

            // Counting subarrays of
            // type "01"
            if (S[i] == '0') {

                // Count the consecutive
                // 0's
                while (i < n && S[i] == '0') {
                    cnt0++;
                    i++;
                }

                // If consecutive 0's
                // ends then check for
                // consecutive 1's
                int j = i;

                // Counting consecutive 1's
                while (j < n && S[j] == '1') {
                    cnt1++;
                    j++;
                }
            }

            // Counting subarrays of
            // type "10"
            else {

                // Count consecutive 1's
                while (i < n && S[i] == '1') {
                    cnt1++;
                    i++;
                }

                // If consecutive 1's
                // ends then check for
                // consecutive 0's
                int j = i;

                // Count consecutive 0's
                while (j < n && S[j] == '0') {
                    cnt0++;
                    j++;
                }
            }

            // Update the total count
            // of substrings with
            // minimum of (cnt0, cnt1)
            ans += Math.Min(cnt0, cnt1);
        }

        // Return answer
        return ans;
    }

    // Driver code
    static public void Main ()
    {
        string S = "0001110010";
        int n = S.Length;

        // Function to print the
        // count of substrings
        Console.WriteLine(countSubstring(S, n));
    }
}

// This code is contributed by Yash_R
```

## java 描述语言

```
<script>

// Javascript implementation of the
// above approach    

    // Function to find the count
    // of substrings with equal no.
    // of consecutive 0's and 1's
    function countSubstring( S , n)
    {
        // To store the total count
        // of substrings
        var ans = 0;

        var i = 0;

        // Traversing the string
        while (i < n) {

            // Count of consecutive
            // 0's & 1's
            var cnt0 = 0, cnt1 = 0;

            // Counting subarrays of
            // type "01"
            if (S.charAt(i) == '0') {

                // Count the consecutive
                // 0's
                while (i < n && S.charAt(i) == '0')
                {
                    cnt0++;
                    i++;
                }

                // If consecutive 0's
                // ends then check for
                // consecutive 1's
                var j = i;

                // Counting consecutive 1's
                while (j < n && S.charAt(j) == '1')
                {
                    cnt1++;
                    j++;
                }
            }

            // Counting subarrays of
            // type "10"
            else {

                // Count consecutive 1's
                while (i < n && S.charAt(i) == '1')
                {
                    cnt1++;
                    i++;
                }

                // If consecutive 1's
                // ends then check for
                // consecutive 0's
                var j = i;

                // Count consecutive 0's
                while (j < n && S.charAt(j) == '0')
                {
                    cnt0++;
                    j++;
                }
            }

            // Update the total count
            // of substrings with
            // minimum of (cnt0, cnt1)
            ans += Math.min(cnt0, cnt1);
        }

        // Return answer
        return ans;
    }

    // Driver code
        var S = "0001110010";
        var n = S.length;

        // Function to print the
        // count of substrings
        document.write(countSubstring(S, n));

// This code contributed by umadevi9616

</script>
```

**Output:** 

```
7
```

**时间复杂度:** O(N)，其中 N =字符串长度。
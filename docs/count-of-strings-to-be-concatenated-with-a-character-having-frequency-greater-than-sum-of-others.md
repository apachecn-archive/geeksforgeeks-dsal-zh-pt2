# 要与频率大于其他字符总和的字符连接的字符串数

> 原文:[https://www . geesforgeks . org/要与频率大于其他字符总和的字符连接的字符串计数/](https://www.geeksforgeeks.org/count-of-strings-to-be-concatenated-with-a-character-having-frequency-greater-than-sum-of-others/)

给定一个包含 **N** 个字符串的数组**arr【】**，任务是找到**个最大**个可以连接的字符串，使得一个字符的频率**大于所有其他字符的频率之和**。

**示例:**

> **输入:**arr[]:{“qpr”，pppsp，“t”}
> **输出:** 3
> **解释:**将 3 个字符串全部串联得到:“aprpppspt”。字符“p”的频率是 5，所有其他频率的总和是 4。
> 
> **输入:**arr[]:{“bcdba”、“abaa”、“acc”、“abcbc”}
> T3】输出: 2

**方法:**要解决此问题，请执行以下步骤:

1.  对所有字符进行迭代，即从“a”到“z”，并在每次迭代中找到该字符在所有字符串中的净频率。这里，净频率可以通过减去所有其他频率来计算，这意味着如果净频率大于 0，则该角色的频率大于所有其他频率的总和。将这些频率存储在向量 **v** 中。
2.  现在，按降序排列 v。
3.  然后为每个字符找到可以组合的最大字符串数，使该字符的频率大于其他频率的总和。
4.  返回最大可能的答案。

下面是上述方法的实现:

## C++

```
// C++ implementation for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function of find the
// frequency of all characters after
// reducing the sum of
// other frequencies in strings
vector<int> frequency(vector<string>& arr,
                      int ch)
{

    // Vector to store frequency
    vector<int> v;

    // Iterate over the array of strings
    for (int i = 0; i < arr.size(); i++) {

        string s = arr[i];

        // Variable to store frequencies
        int net_freq = 0;

        // Iterate over the string
        for (auto x : s) {
            // If x is equal
            // to current character
            // increment net_freq by 1
            if (x == ch)
                net_freq++;

            // Else decrement net_freq by 1
            else
                net_freq--;
        }

        // After the iteration of string
        // store the frequency in vector
        v.push_back(net_freq);
    }

    return v;
}

// Function to find
// the longest string that
// can be made from
// a given vector of strings
int longestConcatenatedStr(
    vector<string>& arr)
{
    // Variable to store maximum count
    int mx = 0;

    // Iterate over all alphabets
    for (char ch = 'a'; ch <= 'z'; ch++) {

        // Vector to store the
        // net_frequency of character
        // ch after reducing
        // the sum of all other
        // frequencies in all strings
        vector<int> v = frequency(arr, ch);

        // Sort the vector in decreasing order
        sort(v.begin(), v.end(),
             greater<int>());

        // Variable to store answer
        int ans = 0;

        int sum = 0;
        for (auto x : v) {
            sum += x;

            // If sum is greater than 0
            // increment ans by 1
            if (sum > 0) {
                ans++;
            }
        }

        // Keep track of the maximum one
        mx = max(mx, ans);
    }
    // Return the maximum value
    return mx;
}

// Driver Code
int main()
{
    vector<string> arr
        = { "abac", "bacbc", "aacab" };

    cout << longestConcatenatedStr(arr);

    return 0;
}
```

## 蟒蛇 3

```
# python implementation for the above approach

# Function of find the
# frequency of all characters after
# reducing the sum of
# other frequencies in strings
def frequency(arr, ch):

    # Vector to store frequency
    v = []

    # Iterate over the array of strings
    for i in range(0, len(arr)):

        s = arr[i]

        # Variable to store frequencies
        net_freq = 0

        # Iterate over the string
        for x in s:

            # If x is equal
            # to current character
            # increment net_freq by 1
            if (x == ch):
                net_freq += 1

            # Else decrement net_freq by 1
            else:
                net_freq -= 1

        # After the iteration of string
        # store the frequency in vector
        v.append(net_freq)

    return v

# Function to find
# the longest string that
# can be made from
# a given vector of strings
def longestConcatenatedStr(arr):

    # Variable to store maximum count
    mx = 0

    # Iterate over all alphabets
    for ch in range(0, 26):

        # Vector to store the
        # net_frequency of character
        # ch after reducing
        # the sum of all other
        # frequencies in all strings
        v = frequency(arr, chr(ch + ord('a')))

        # Sort the vector in decreasing order
        v.sort(reverse=True)

        # Variable to store answer
        ans = 0

        sum = 0
        for x in v:
            sum += x

            # If sum is greater than 0
            # increment ans by 1
            if (sum > 0):
                ans += 1

        # Keep track of the maximum one
        mx = max(mx, ans)

    # Return the maximum value
    return mx

# Driver Code
if __name__ == "__main__":

    arr = ["abac", "bacbc", "aacab"]

    print(longestConcatenatedStr(arr))

# This code is contributed by rakeshsahni
```

## java 描述语言

```
<script>

       // JavaScript Program to implement
       // the above approach

       // Function of find the
       // frequency of all characters after
       // reducing the sum of
       // other frequencies in strings
       function frequency(arr, ch) {

           // Vector to store frequency
           let v = [];

           // Iterate over the array of strings
           for (let i = 0; i < arr.length; i++) {

               let s = arr[i];

               // Variable to store frequencies
               let net_freq = 0;

               // Iterate over the string
               for (let x of s)
               {

                   // If x is equal
                   // to current character
                   // increment net_freq by 1
                   if (x == ch)
                       net_freq++;

                   // Else decrement net_freq by 1
                   else
                       net_freq--;
               }

               // After the iteration of string
               // store the frequency in vector
               v.push(net_freq);
           }

           return v;
       }

       // Function to find
       // the longest string that
       // can be made from
       // a given vector of strings
       function longestConcatenatedStr(
           arr)
      {

           // Variable to store maximum count
           let mx = 0;

           // Iterate over all alphabets
           for (let ch = 'a'; ch <= 'z'; ch++) {

               // Vector to store the
               // net_frequency of character
               // ch after reducing
               // the sum of all other
               // frequencies in all strings
               let v = frequency(arr, ch);

               // Sort the vector in decreasing order
               v.sort(function (a, b) { return b - a })

               // Variable to store answer
               let ans = 0;

               let sum = 0;
               for (let x of v) {
                   sum += x;

                   // If sum is greater than 0
                   // increment ans by 1
                   if (sum > 0) {
                       ans++;
                   }
               }

               // Keep track of the maximum one
               mx = Math.max(mx, ans);
           }

           // Return the maximum value
           return mx;
       }

       // Driver Code
       let arr
           = ["abac", "bacbc", "aacab"];

       document.write(longestConcatenatedStr(arr));

   // This code is contributed by Potta Lokesh
   </script>
```

**Output**

```
2
```

**时间复杂度:**O(NlogN)
T3】辅助空间: O(N)
# 包含‘1’的最长子串

> 原文:[https://www . geesforgeks . org/long-substring-containing-1/](https://www.geeksforgeeks.org/longest-substring-containing-1/)

给定一个[二进制字符串](https://www.geeksforgeeks.org/tag/binary-string/)，任务是打印最长的[子字符串](https://www.geeksforgeeks.org/substring-in-cpp/)的长度，其中只包含**‘1’**。

**示例:**

> **输入:** 110
> **输出:** 2
> **说明:**仅包含‘1’的最长子串长度为“11”。
> 
> **输入:**11101110
> T3】输出: 3

**进场:** [遍历字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/)并统计遇到的连续 **1** 的数量。将最大数量的连续 **1** s 存储在一个变量中，比如 **max** 。最后打印得到的 **max** 的值。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find length of
// longest substring containing '1'
int maxlength(string s)
{
    int n = s.length(), i, j;
    int ans = 0;
    for (i = 0; i <= n - 1; i++) {

        // Count the number of contiguous 1's
        if (s[i] == '1') {

            int count = 1;
            for (j = i + 1; j <= n - 1
                            && s[j] == '1';
                 j++)
                count++;
            ans = max(ans, count);
        }
    }
    return ans;
}

// Driver Code
int main()
{
    string s = "11101110";

    cout << maxlength(s) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find length
// of longest substring containing '1'

class GFG {

    // Function to find length of
    // of longest substring containing '1'
    static int maxlength(String s)
    {
        int n = s.length(), i, j;
        int ans = 0;
        for (i = 0; i <= n - 1; i++) {

            // Count the number of contiguous 1's
            if (s.charAt(i) == '1') {

                int count = 1;
                for (j = i + 1;
                     j <= n - 1 && s.charAt(j) == '1'; j++)
                    count++;
                ans = Math.max(ans, count);
            }
        }
        return ans;
    }

    public static void main(String[] args)
    {
        String s = "11101110";

        System.out.println(
            "Length of longest substring containing '1' = "
            + maxlength(s));
    }
}
```

## 蟒蛇 3

```
# Python program for the above approach

# Function to find length of
# longest substring containing '1'
def maxlength(s):
    n = len(s)
    ans = 0;
    for i in range(n):

        # Count the number of contiguous 1's
        if (s[i] == '1'):
            count = 1
            j = i + 1
            while(j <= n - 1 and s[j] == '1'):
                count += 1
                j += 1
            ans = max(ans, count)
    return ans

# Driver Code
s = "11101110";
print(maxlength(s))

# This code is contributed by Shivani
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to find length of
// of longest substring containing '1'
static int maxlength(String s)
{
    int n = s.Length, i, j;
    int ans = 0;

    for(i = 0; i <= n - 1; i++)
    {

        // Count the number of contiguous 1's
        if (s[i] == '1')
        {
            int count = 1;
            for(j = i + 1;
                j <= n - 1 && s[j] == '1';
                j++)
                count++;

            ans = Math.Max(ans, count);
        }
    }
    return ans;
}

// Driver code
public static void Main(String[] args)
{
    String s = "11101110";

    Console.Write(maxlength(s));
}
}

// This code is contributed by shivanisinghss2110
```

## java 描述语言

```
<script>

        // JavaScript program for the above approach;

        // Function to find length of
        // longest substring containing '1'
        function maxlength(s)
        {
            let n = s.length, i, j;
            let ans = 0;
            for (i = 0; i <= n - 1; i++) {

                // Count the number of contiguous 1's
                if (s[i] == '1') {

                    let count = 1;
                    for (j = i + 1; j <= n - 1
                        && s[j] == '1';
                        j++)
                        count++;
                    ans = Math.max(ans, count);
                }
            }
            return ans;
        }

        // Driver Code
        let s = "11101110";
        document.write(maxlength(s));

// This code is contributed by Potta Lokesh
    </script>
```

**Output:** 

```
3
```

**时间复杂度:**O(N<sup>2</sup>)
T5】辅助空间: O(1)
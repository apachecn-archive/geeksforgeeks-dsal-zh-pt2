# 最大化回文串的数量

> 原文:[https://www . geeksforgeeks . org/最大化回文字符串的数量/](https://www.geeksforgeeks.org/maximize-the-number-of-palindromic-strings/)

给定 N 个二进制字符串 b1，b2，b3…10 亿任务是找到最大数量的二进制字符串，您可以通过多次交换任意对字符来使其成为回文。字符可以来自同一个字符串，也可以来自不同的字符串
**示例:**

```
Input: N=3
1110
100110
010101
Output: 2
Explanation:
b1 = 1110
b2 = 100110 - > 110010
b3 = 010101 ->  110010
Now swap last 0 in s2 and s3
with 1's in s1
Final string become
b1 = 1000
b2 = 110011
b3 = 110011

where b1 and b2 are a palindrome

Input: N=3
1
1000
111110
Output: 3
```

**进场:**
弦的长度不变。同样重要的是要注意，如果给我们一个奇数长度的二进制字符串，那么我们总是可以这样交换字符，将该字符串转换为回文。这是因为如果长度是奇数，那么我们要么有(偶数个 0 和奇数个 1)要么有(偶数个 1 和奇数个 0)。所以它总是可以以这样的方式放置，使字符串回文。
现在作为我们的 ans 可以是 N 或者 N-1。我们必须考虑 ans 为 N 的情况。因此，我们得到了 N 个二进制字符串。如果至少有 1 个奇数长度的字符串，那么我们的 ans 肯定是 N.

*   抓住所有的 0 和 1，把他们从他们的位置上移走。然后我们将至少有一对 0 或 1，然后将它们对称地放入它们的自由点(跳过奇数长度的中间)。所以到目前为止，所有偶数长度的字符串都被填充，奇数长度的字符串在中间有一个自由点，可以很容易地用剩余的字符填充。所以在这种情况下，我们的 ans 将是 n。
*   现在，另一个案例。如果我们有所有的 N 个偶数长度的字符串，并且 1 和 0 的总数是偶数(即 1 的总数是偶数，0 的总数是偶数)，那么在这种情况下，我们的 ans 也将是 N。这是因为 1 和 0 可以对称地放置在所有的 N 个字符串中，使它们回文。否则，我们的 ans 将是 N-1。

以下是上述方法的实现:

## C++

```
// C++ program for the
// above approach
#include <bits/stdc++.h>
using namespace std;

int max_palindrome(string s[], int n)
{
    int flag = 0;
    for (int i = 0; i < n; i++) {
        // To check if there is
        // any string of odd length
        if (s[i].size() % 2 != 0) {
            flag = 1;
        }
    }

    // If there is at least
    // 1 string of odd
    // length.
    if (flag == 1) {
        return n;
    }

    int z = 0, o = 0;

    // If all the strings are
    // of even length.
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < s[i].size(); j++) {
            // Count of 0's in all
            // the strings
            if (s[i][j] == '0')
                z++;
            // Count of 1's in
            // all the strings
            else
                o++;
        }
    }
    // If z is even
    // and o is even
    // then ans will be N.
    if (o % 2 == 0 && z % 2 == 0) {
        return n;
    }
    // Otherwise ans will be N-1.
    else {
        return n - 1;
    }
}

// Driver code
int main()
{
    int n = 3;
    string s[n] = { "1110", "100110", "010101" };
    cout << max_palindrome(s, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG
{

    static int max_palindrome(String []s, int n)
    {
        int flag = 0;
        for (int i = 0; i < n; i++)
        {
            // To check if there is
            // any string of odd length
            if (s[i].length() % 2 != 0)
            {
                flag = 1;
            }
        }

        // If there is at least
        // 1 string of odd
        // length.
        if (flag == 1)
        {
            return n;
        }

        int z = 0;
        int o = 0;

        // If all the strings are
        // of even length.
        for (int i = 0; i < n; i++)
        {
            for (int j = 0; j < s[i].length(); j++)
            {
                // Count of 0's in all
                // the strings
                if (s[i].charAt(j) == '0')
                    z += 1;

                // Count of 1's in
                // all the strings
                else
                    o += 1;
            }
        }

        // If z is even
        // and o is even
        // then ans will be N.
        if (o % 2 == 0 && z % 2 == 0)
        {
            return n;
        }

        // Otherwise ans will be N-1.
        else
        {
            return n - 1;
        }
    }

    // Driver code
    public static void main (String[] args)
    {
        int n = 3;
        String s[] = {"1110", "100110", "010101" };
        System.out.println(max_palindrome(s, n));
    }
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 program for the above approach
def max_palindrome(s, n) :

    flag = 0;
    for i in range(n) :

        # To check if there is
        # any string of odd length
        if (len(s[i]) % 2 != 0) :
            flag = 1;

    # If there is at least
    # 1 string of odd
    # length.
    if (flag == 1) :
        return n;

    z = 0; o = 0;

    # If all the strings are
    # of even length.
    for i in range(n) :
        for j in range(len(s[i])) :

            # Count of 0's in all
            # the strings
            if (s[i][j] == '0') :
                z += 1;

            # Count of 1's in
            # all the strings
            else :
                o += 1;

    # If z is even
    # and o is even
    # then ans will be N.
    if (o % 2 == 0 and z % 2 == 0) :
        return n;

    # Otherwise ans will be N-1.
    else :
        return n - 1;

# Driver code
if __name__ == "__main__" :

    n = 3;
    s = [ "1110", "100110", "010101" ];

    print(max_palindrome(s, n));

# This code is contributed by AnkitRai01
```

## C#

```
// C# program for the above approach
using System;

class GFG
{

    static int max_palindrome(string []s, int n)
    {
        int flag = 0;
        for (int i = 0; i < n; i++)
        {
            // To check if there is
            // any string of odd length
            if (s[i].Length % 2 != 0)
            {
                flag = 1;
            }
        }

        // If there is at least
        // 1 string of odd
        // length.
        if (flag == 1)
        {
            return n;
        }

        int z = 0;
        int o = 0;

        // If all the strings are
        // of even length.
        for (int i = 0; i < n; i++)
        {
            for (int j = 0; j < s[i].Length; j++)
            {
                // Count of 0's in all
                // the strings
                if (s[i][j] == '0')
                    z += 1;

                // Count of 1's in
                // all the strings
                else
                    o += 1;
            }
        }

        // If z is even
        // and o is even
        // then ans will be N.
        if (o % 2 == 0 && z % 2 == 0)
        {
            return n;
        }

        // Otherwise ans will be N-1.
        else
        {
            return n - 1;
        }
    }

    // Driver code
    public static void Main ()
    {
        int n = 3;
        string []s = {"1110", "100110", "010101" };
        Console.WriteLine(max_palindrome(s, n));
    }
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>
    // Javascript program for the above approach

    function max_palindrome(s, n)
    {
        let flag = 0;
        for (let i = 0; i < n; i++)
        {
            // To check if there is
            // any string of odd length
            if (s[i].length % 2 != 0)
            {
                flag = 1;
            }
        }

        // If there is at least
        // 1 string of odd
        // length.
        if (flag == 1)
        {
            return n;
        }

        let z = 0;
        let o = 0;

        // If all the strings are
        // of even length.
        for (let i = 0; i < n; i++)
        {
            for (let j = 0; j < s[i].length; j++)
            {
                // Count of 0's in all
                // the strings
                if (s[i][j] == '0')
                    z += 1;

                // Count of 1's in
                // all the strings
                else
                    o += 1;
            }
        }

        // If z is even
        // and o is even
        // then ans will be N.
        if (o % 2 == 0 && z % 2 == 0)
        {
            return n;
        }

        // Otherwise ans will be N-1.
        else
        {
            return n - 1;
        }
    }

    let n = 3;
    let s = ["1110", "100110", "010101"];
    document.write(max_palindrome(s, n));

// This code is contributed by divyeshrabadiya07.
</script>
```

**Output:** 

```
2
```
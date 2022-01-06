# 字典上最小的奇数数字串

> 原文:[https://www . geeksforgeeks . org/按字典顺序排列的最小数字串奇数位数/](https://www.geeksforgeeks.org/lexicographically-smallest-numeric-string-having-odd-digit-counts/)

给定一个正整数 **N** ，任务是[生成一个字典上最小的数字串](https://www.geeksforgeeks.org/lexicographically-smallest-string-formed-by-appending-a-character-from-the-first-k-characters-of-a-given-string/)，大小为 **N** ，每个数字有一个奇数计数。

**示例:**

> **输入:** N = 4
> **输出:** 1112
> **解释:**
> 数字 1 和数字 2 都有偶数计数，是字典中可能的最小字符串。
> 
> **输入:** N = 5
> **输出:** 11111
> **解释:**
> 数字 1 有奇数计数，是可能的字典最小字符串。

**方法:**给定的问题可以基于这样的观察来解决:[如果 **N** 的值是**甚至**](https://www.geeksforgeeks.org/check-if-a-number-is-odd-or-even-using-bitwise-operators/) ，那么得到的字符串包含 **1s** 、**(N–1)**的次数后跟单个 **2** 是可能的最小字典顺序字符串。否则，生成的字符串包含 **1s** 、 **N** 的次数是可能的最小字典顺序字符串。

下面是上述方法的实现:

## C++14

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to construct lexicographically
// smallest numeric string having an odd
// count of each characters
string genString(int N)
{
    // Stores the resultant string
    string ans = "";

    // If N is even
    if (N % 2 == 0) {
        ans = string(N - 1, '1') + '2';
    }

    // Otherwise
    else {
        ans = string(N, '1');
    }

    return ans;
}

// Driver code
int main()
{
    int N = 5;
    cout << genString(N);

    return 0;
}
```

## 蟒蛇 3

```
# python program for the above approach
# Function to construct lexicographically
# smallest numeric string having an odd
# count of each characters
def genString(N):

    # Stores the resultant string
    ans = ""

    # If N is even
    if (N % 2 == 0) :
        ans = "".join("1" for i in range(N-1))
        ans = ans + "2"

    # Otherwise
    else :
        ans = "".join("1" for i in range(N))

    return ans

# Driver code
if __name__ == "__main__":
    N = 5
    print(genString(N))

# This code is contributed by anudeep23042002
```

## C#

```
// C# program for the above approach
using System;
class GFG {

    // Function to construct lexicographically
    // smallest numeric string having an odd
    // count of each characters
    static string genString(int N)
    {

        // Stores the resultant string
        string ans = "";

        // If N is even
        if (N % 2 == 0) {
            for (int i = 0; i < N - 1; i++)
                ans += '1';
            ans += '2';
        }

        // Otherwise
        else {
            for (int i = 0; i < N; i++)
                ans += '1';
        }

        return ans;
    }

    // Driver code
    public static void Main()
    {
        int N = 5;
        Console.WriteLine(genString(N));
    }
}

// This code is contributed by ukasp.
```

## java 描述语言

```
<script>
        // JavaScript Program to implement
        // the above approach

        // Function to construct lexicographically
        // smallest numeric string having an odd
        // count of each characters
        function genString(N)
        {

            // Stores the resultant string
            let ans = "";

            // If N is even
            if (N % 2 == 0) {
                ans = '1'.repeat(N - 1) + '2';
            }

            // Otherwise
            else {
                ans = '1'.repeat(N);
            }

            return ans;
        }

        // Driver code
        let N = 5;
        document.write(genString(N));

     // This code is contributed by Potta Lokesh
    </script>
```

**Output:** 

```
11111
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)
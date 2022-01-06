# 字符总和等于 N 的字典上最大的字符串

> 原文:[https://www . geeksforgeeks . org/按字典顺序排列的最大字符总和等于 n 的字符串/](https://www.geeksforgeeks.org/lexicographically-largest-string-with-sum-of-characters-equal-to-n/)

给定一个正整数 **N** ，任务是找到由小写英文字母组成的字典上最大的字符串，使得该字符串的字符总和等于 **N** ，其中**a ' = 1**，**b ' = 2**，**c ' = 3**，…..，以及**‘z’**=**26**。

**示例:**

> **输入:** N = 30
> **输出:** zd
> **解释:**
> 形成的字典上最大的字符串是“zd”，其字符位置之和为(26 + 4) = 30(= N)。
> 
> **输入:**N = 14
> T3】输出: n

**方法:**要使字典上最大的字符串，想法是打印字符 **z** 、 **N/26** 的次数，然后在英文字母中的 **(N%26 + 1) <sup>第</sup>** 位置打印字符。按照以下步骤解决问题:

*   初始化一个[字符串](https://www.geeksforgeeks.org/string-data-structure/)，比如说**和**，它存储所需的按字典顺序最大的字符串。
*   迭代至 **N** 至少为 **26** ，执行以下步骤:
    *   将字符 **z** 添加到字符串**和**中。
    *   将 **N** 的值递减 **26** 。
*   将**字符(N + 'a')** 的值添加到字符串**和**中。
*   完成上述步骤后，将**和**的值打印为结果字符串。

以下是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to construct the
// lexicographically largest string
// having sum of characters as N
string getString(int N)
{

    // Stores the resulting string
    string ans = "";

    // Iterate until N is at least 26
    while (N >= 26) {

        // Append 'z' to the string ans
        ans += 'z';

        // Decrement N by 26
        N -= 26;
    }

    // Append character at index (N + 'a')
    ans += char(N + 'a' - 1);

    // Return the resultant string
    return ans;
}

// Driver Code
int main()
{
    int N = 30;
    cout << getString(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// java program for the above approach
import java.io.*;
import java.lang.*;
import java.util.*;

public class GFG {

    // Function to construct the
    // lexicographically largest string
    // having sum of characters as N
    static String getString(int N)
    {

        // Stores the resulting string
        String ans = "";

        // Iterate until N is at least 26
        while (N >= 26) {

            // Append 'z' to the string ans
            ans += 'z';

            // Decrement N by 26
            N -= 26;
        }

        // Append character at index (N + 'a')
        ans += (char)(N + 'a' - 1);

        // Return the resultant string
        return ans;
    }

    // Driver Code
    public static void main(String[] args)
    {

        int N = 30;
        System.out.print(getString(N));
    }
}

// This code is contributed by Kingash.
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to construct the
# lexicographically largest string
# having sum of characters as N
def getString(N):

    # Stores the resulting string
    ans = ""

    # Iterate until N is at least 26
    while (N >= 26):

        # Append 'z' to the string ans
        ans += 'z'

        # Decrement N by 26
        N -= 26

    # Append  character at index (N + 'a')
    ans += chr(N + ord('a') - 1)

    # Return the resultant string
    return ans

# Driver Code
if __name__ == '__main__':
    N = 30
    print(getString(N))

# This code is contributed by mohit kumar 29.
```

## C#

```
// C# program for the above approach
using System;

public class GFG {

    // Function to construct the
    // lexicographically largest string
    // having sum of characters as N
    static string getString(int N)
    {

        // Stores the resulting string
        string ans = "";

        // Iterate until N is at least 26
        while (N >= 26) {

            // Append 'z' to the string ans
            ans += 'z';

            // Decrement N by 26
            N -= 26;
        }

        // Append character at index (N + 'a')
        ans += (char)(N + 'a' - 1);

        // Return the resultant string
        return ans;
    }

    // Driver Code
    public static void Main(string[] args)
    {

        int N = 30;
        Console.WriteLine(getString(N));
    }
}

// This code is contributed by ukasp.
```

## java 描述语言

```
<script>
    // Javascript program for the above approach

// Function to construct the
// lexicographically largest string
// having sum of characters as N
function getString(N){

    // Stores the resulting string
    let ans = ""

    // Iterate until N is at least 26
    while (N >= 26){

        // Append 'z' to the string ans
        ans += 'z'

        // Decrement N by 26
        N -= 26
    }
    // Append character at index (N + 'a')
    ans += String.fromCharCode(N + 'a'.charCodeAt(0) - 1)

    // Return the resultant string
    return ans
}

// Driver Code
    let N = 30
    document.write(getString(N))

// This code is contributed by Saurabh Jaiswal
</script>
```

**Output:** 

```
zd
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)
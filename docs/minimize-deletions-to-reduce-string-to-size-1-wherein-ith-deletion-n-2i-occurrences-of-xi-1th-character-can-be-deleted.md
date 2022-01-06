# 最小化删除以将字符串减小到大小 1，其中通过删除，第(X+i-1)个字符的 N/2^i 出现可以被删除

> 原文:[https://www . geesforgeks . org/minimum-deletes-to-reduction-string-size-1-其中-with-delete-n-2i-出现次数-xi-第 1 个字符-可以删除/](https://www.geeksforgeeks.org/minimize-deletions-to-reduce-string-to-size-1-wherein-ith-deletion-n-2i-occurrences-of-xi-1th-character-can-be-deleted/)

给定长度为 **N** 的字符串 **str** 和一个字符 **X** ，其中 **N** 总是为 **2 <sup>k</sup>** 的形式，任务是找到将字符串的大小减少到 **1** 所需的最小替换操作，其中 **i <sup>th</sup>** 删除， **N/2 <sup>i</sup>**

**示例:**

> **输入:**str = " cdaaaaabb "，X = 'A'
> **输出:** 4
> **说明:**给定字符串的替换操作可以按如下方式进行:
> 
> 1.  将第一个索引处的“C”替换为“A”。
> 2.  将第二个索引处的“D”替换为“A”。
> 3.  将第五个索引处的“A”替换为“D”。
> 4.  将第六个索引处的“A”替换为“C”。
> 
> 因此，字符串变成 str = " AAAADCBB "。在第一次删除(8/2 <sup>1</sup> )时，可以从字符串的前面删除(A+1-1) <sup>第</sup>个字符。因此，字符串变成 str =“DCBB”。类似地，在第二次删除(8/2 <sup>2</sup> )时，出现(A+2-1) <sup>第</sup>个字符，即“B”字符可以从字符串后面删除。因此，字符串变成 str =“DC”。类似地，在第三次删除后，字符串变成长度为 1 的 str =“D”。因此，所需更换操作的数量是 4，这是可能的最小数量。
> 
> **输入:** str = "QRQP "，X = ' P '
> T3】输出: 1

**方法:**给定的问题可以通过使用与[二分搜索法](https://www.geeksforgeeks.org/binary-search/)结构相似的[递归](https://www.geeksforgeeks.org/recursion/)来解决。在每次删除过程中，可以观察到有 2 种可能的选择。它们如下:

1.  用“X”替换给定字符串前半部分的所有字符，并递归调用 X = X + 1 的剩余半部分。
2.  或者，用“X”替换给定字符串后半部分的所有字符，并递归调用 X = X + 1 的剩余部分。

因此，使用上述观察创建一个[递归函数](https://www.geeksforgeeks.org/recursive-functions/)，通过计算字符串前半部分需要替换为 X 的索引数量，并递归调用剩余的半部分，从两种可能性中选择最小的移动，反之亦然。

下面是上述方法的实现:

## C++

```
// C++ implementation for the above approach
#include <bits/stdc++.h>
using namespace std;

// Recursive function to find minimum
// replacements required to reduce the
// size of the given string to 1
int minReplacment(string s, char x)
{
    // Base Case
    if (s.size() == 1) {
        return s[0] != x;
    }

    // Stores the middle index
    int mid = s.size() / 2;

    // Recursive call for left half
    int cntl = minReplacment(
        string(s.begin(), s.begin() + mid), x + 1);
    cntl += s.size() / 2
            - count(s.begin() + mid, s.end(), x);

    // Recursive call for right half
    int cntr = minReplacment(
        string(s.begin() + mid, s.end()), x + 1);
    cntr += s.size() / 2
            - count(s.begin(), s.begin() + mid, x);

    // Return Answer
    return min(cntl, cntr);
}

// Driver Code
int main()
{
    int N = 8;
    string str = "CDAAAABB";
    char X = 'A';

    cout << minReplacment(str, X);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
/*package whatever //do not write package name here */
// Java code for the above approach
import java.util.*;

class GFG {
    public static int count(String str, char c)
    {
        int ct = 0;

        for (int i = 0; i < str.length(); i++) {
            char currChar = str.charAt(i);
            if (currChar == c)
                ct += 1;
        }

        return ct;
    }

    // Recursive function to find minimum
    // replacements required to reduce the
    // size of the given string to 1
    static int minReplacment(String s, char x)
    {
        // Base Case
        if (s.length() == 1) {
            if (s.charAt(0) == x)
                return 1;
            return 0;
        }

        // Stores the middle index
        int mid = s.length() / 2;

        // Recursive call for left half
        char p = (char)(x + 1);
        int cntl = minReplacment(s.substring(0, mid), p);
        cntl = cntl + s.length() / 2
               - count(s.substring(mid, s.length()), x);

        // Recursive call for right half
        char t = (char)(x + 1);
        int cntr = minReplacment(
            s.substring(mid, s.length()), t);
        cntr = cntr + s.length() / 2
               - count(s.substring(0, mid), x);

        // Return Answer
        return Math.min(cntl + 1, cntr);
    }

    // Driver Code
    public static void main(String[] args)
    {

        int N = 8;
        String str = "CDAAAABB";
        char X = 'A';
        System.out.println(minReplacment(str, X));
    }
}

// This code is contributed by Potta Lokesh
```

## 蟒蛇 3

```
# Python 3 implementation for the above approach

# Recursive function to find minimum
# replacements required to reduce the
# size of the given string to 1
def minReplacment(s,  x):

    # Base Case
    if (len(s) == 1):
        return s[0] != x

    # Stores the middle index
    mid = len(s) // 2

    # Recursive call for left half
    cntl = minReplacment(
        s[:mid], chr(ord(x) + 1))
    cntl += len(s) // 2 - s[mid:].count(x)

    # Recursive call for right half
    cntr = minReplacment(
        s[mid:], chr(ord(x) + 1))
    cntr += len(s) // 2 - s[:mid].count(x)

    # Return Answer
    return min(cntl, cntr)

# Driver Code
if __name__ == "__main__":

    N = 8
    st = "CDAAAABB"
    X = 'A'

    print(minReplacment(st, X))

    # This code is contributed by ukasp.
```

## C#

```
/*package whatever //do not write package name here */
// C# code for the above approach
using System;

public class GFG {
    public static int count(String str, char c)
    {
        int ct = 0;

        for (int i = 0; i < str.Length; i++) {
            char currChar = str[i];
            if (currChar == c)
                ct += 1;
        }

        return ct;
    }

    // Recursive function to find minimum
    // replacements required to reduce the
    // size of the given string to 1
    static int minReplacment(String s, char x)
    {
        // Base Case
        if (s.Length == 1) {
            if (s[0] == x)
                return 1;
            return 0;
        }

        // Stores the middle index
        int mid = s.Length / 2;

        // Recursive call for left half
        char p = (char)(x + 1);
        int cntl = minReplacment(s.Substring(0, mid), p);
        cntl = cntl + s.Length / 2
               - count(s.Substring(mid, s.Length-mid), x);

        // Recursive call for right half
        char t = (char)(x + 1);
        int cntr = minReplacment(
            s.Substring(mid, s.Length-mid), t);
        cntr = cntr + s.Length / 2
               - count(s.Substring(0, mid), x);

        // Return Answer
        return Math.Min(cntl + 1, cntr);
    }

    // Driver Code
    public static void Main(String[] args)
    {
        String str = "CDAAAABB";
        char X = 'A';
        Console.WriteLine(minReplacment(str, X));
    }
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>
// Javascript implementation for the above approach

function count(str, c) {
    let ct = 0;

    for (let i = 0; i < str.length; i++) {
        let currChar = str[i];
        if (currChar == c)
            ct += 1;
    }

    return ct;
}

// Recursive function to find minimum
// replacements required to reduce the
// size of the given string to 1
function minReplacment(s, x) {
    // Base Case
    if (s.length == 1) {
        if(s[0] == x){
            return 1
        }
        return 0
    }

    // Stores the middle index
    let mid = Math.floor(s.length / 2);

    // Recursive call for left half
    let cntl = minReplacment(s.substring(0, mid), String.fromCharCode(x.charCodeAt(0) + 1));
    cntl += Math.floor(s.length / 2) - count(s.substring(mid, s.length), x);

    // Recursive call for right half
    let cntr = minReplacment(new String(s.substring(mid, s.length)), String.fromCharCode(x.charCodeAt(0) + 1));
    cntr += Math.floor(s.length / 2) - count(s.substring(0, mid), x);

    // Return Answer
    return Math.min(cntl + 1, cntr);
}

// Driver Code

let N = 8;
let str = "CDAAAABB";
let X = 'A';

document.write(minReplacment(str, X));

// This code is contributed by gfgking.
</script>
```

**Output**

```
4
```

***时间复杂度:** O(N*log N)*
***辅助空间:** O(1)*
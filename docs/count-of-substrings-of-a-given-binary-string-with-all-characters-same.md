# 给定二进制字符串中所有字符都相同的子字符串计数

> 原文:[https://www . geeksforgeeks . org/给定二进制字符串的子字符串计数-所有字符-相同/](https://www.geeksforgeeks.org/count-of-substrings-of-a-given-binary-string-with-all-characters-same/)

给定仅包含 **0** 和 **1** 的二进制字符串**字符串**，任务是分别找到仅包含 **1s** 和 **0s** 的子字符串数量，即所有字符相同。

**示例:**

> **输入:** str = "011"
> **输出:** 4
> **解释:**
> 三个子串分别为“1*”*、“1”“11”，其中只有 1，还有一个子串只包含“0”。
> 
> **输入:** str = "0000"
> **输出:** 10
> **说明:**
> 不存在全为 1 的子串。

**天真方法:**想法是[生成给定字符串](https://www.geeksforgeeks.org/program-print-substrings-given-string/)的所有可能的子字符串。对于每个子字符串，检查该字符串是否包含全部 1 或全部 0。如果包含，则计算该子字符串。打印上述操作后的子字符串计数。

*时间复杂度:O(N <sup>3</sup> )*
*辅助空间:O(N)*

**高效进场:**思路是利用[滑动窗口](https://www.geeksforgeeks.org/window-sliding-technique/)和[两个指针进场](https://www.geeksforgeeks.org/two-pointers-technique/)的概念。以下是查找仅包含 **1s** 的子串的计数的步骤:

1.  初始化两个指针，分别为***【L】******【R】***，并将它们初始化为 **0** 。
2.  现在迭代给定的字符串，检查当前字符是否等于 1。如果是，则通过增加 **R** 的值来扩展窗口。
3.  如果当前字符是 **0** ，那么窗口 **L 到 R–1**包含所有 1。
4.  将 **L 到 R–1**的子串数加到答案为**((R–L)*(R–L+1))/2**上，并递增 **R** ，将 **L 重新初始化为 R** 。
5.  重复这个过程，直到 **L 和 R** 相互交叉。
6.  在**步骤 4** 中打印所有子串的计数。
7.  要计算所有 **0s** 的子串数量，翻转给定的字符串，即所有 **0s** 将转换为 **1s** ，反之亦然。
8.  对**翻转字符串**中的字符 **1** 重复上述从**步骤 1 到步骤 4** 的步骤，获取其中只包含 **0s** 的子字符串的计数并打印该计数。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <iostream>
using namespace std;

// Function to count number of
// sub-strings of a given binary
// string that contains only 1
int countSubAllOnes(string s)
{
    int l = 0, r = 0, ans = 0;

    // Iterate untill L and R cross
    // each other
    while (l <= r) {

        // Check if reached the end
        // of string
        if (r == s.length()) {
            ans += ((r - l) * (r - l + 1)) / 2;
            break;
        }

        // Check if encountered '1'
        // then extend window
        if (s[r] == '1')
            r++;

        // Check if encountered '0' then
        // add number of strings of
        // current window and change the
        // values for both l and r
        else {

            ans += ((r - l) * (r - l + 1)) / 2;
            l = r + 1;
            r++;
        }
    }

    // Return the answer
    return ans;
}

// Function to flip the bits of string
void flip(string& s)
{

    for (int i = 0; s[i]; i++) {
        if (s[i] == '1')
            s[i] = '0';
        else
            s[i] = '1';
    }
  cout<<s<<endl;
}

// Function to count number of
// sub-strings of a given binary
// string that contains only 0s & 1s
int countSubAllZerosOnes(string s)
{

    // count of substring
    // which contains only 1s
    int only_1s = countSubAllOnes(s);

    // Flip the character of string s
    // 0 to 1 and 1 to 0 to count the
    // substring with consecutive 0s
    flip(s);
  cout<<s<<endl;

    // count of substring
    // which contains only 0s
    int only_0s = countSubAllOnes(s);

    return only_0s + only_1s;
}

// Driver Code
int main()
{
    // Given string str
    string s = "011";

    // Function Call
    cout << countSubAllZerosOnes(s) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to count number of
// sub-Strings of a given binary
// String that contains only 1
static int countSubAllOnes(String s)
{
    int l = 0, r = 0, ans = 0;

    // Iterate untill L and R cross
    // each other
    while (l <= r)
    {

        // Check if reached the end
        // of String
        if (r == s.length())
        {
            ans += ((r - l) * (r - l + 1)) / 2;
            break;
        }

        // Check if encountered '1'
        // then extend window
        if (s.charAt(r) == '1')
            r++;

        // Check if encountered '0' then
        // add number of Strings of
        // current window and change the
        // values for both l and r
        else
        {
            ans += ((r - l) * (r - l + 1)) / 2;
            l = r + 1;
            r++;
        }
    }

    // Return the answer
    return ans;
}

// Function to flip the bits of String
static String flip(char []s)
{
    for(int i = 0; i < s.length; i++)
    {
        if (s[i] == '1')
            s[i] = '0';
        else
            s[i] = '1';
    }
    return String.valueOf(s);
}

// Function to count number of
// sub-Strings of a given binary
// String that contains only 0s & 1s
static int countSubAllZerosOnes(String s)
{

    // count of subString
    // which contains only 1s
    int only_1s = countSubAllOnes(s);

    // Flip the character of String s
    // 0 to 1 and 1 to 0 to count the
    // subString with consecutive 0s
    s = flip(s.toCharArray());

    // count of subString
    // which contains only 0s
    int only_0s = countSubAllOnes(s);

    return only_0s + only_1s;
}

// Driver Code
public static void main(String[] args)
{

    // Given String str
    String s = "011";

    // Function call
    System.out.print(countSubAllZerosOnes(s) + "\n");
}
}

// This code is contributed by Rohit_ranjan
```

## 蟒蛇 3

```
# Python3 program for
# the above approach

# Function to count number of
# sub-strings of a given binary
# string that contains only 1
def countSubAllOnes(s):

    l, r, ans = 0, 0, 0

    # Iterate untill L and R cross
    # each other
    while (l <= r):

        # Check if reached the end
        # of string
        if (r == len(s)):
            ans += ((r - l) *
                    (r - l + 1)) // 2
            break

        # Check if encountered '1'
        # then extend window
        if (s[r] == '1'):
            r += 1

        # Check if encountered '0' then
        # add number of strings of
        # current window and change the
        # values for both l and r
        else :
            ans += ((r - l) *
                    (r - l + 1)) // 2
            l = r + 1
            r += 1

    # Return the answer
    return ans

# Function to flip the bits of string
def flip(s):

    arr = list(s)
    for i in range (len(s)):
        if (arr[i] == '1'):
            arr[i] = '0'
        else:
            arr[i] = '1'
    s = ''.join(arr)
    return s

# Function to count number of
# sub-strings of a given binary
# string that contains only 0s & 1s
def countSubAllZerosOnes(s):

    # count of substring
    # which contains only 1s
    only_1s = countSubAllOnes(s)

    # Flip the character of string s
    # 0 to 1 and 1 to 0 to count the
    # substring with consecutive 0s
    s = flip(s)

    # count of substring
    # which contains only 0s
    only_0s = countSubAllOnes(s)

    return only_0s + only_1s

# Driver Code
if __name__ == "__main__":

    # Given string str
    s  = "011"

    # Function Call
    print (countSubAllZerosOnes(s))

# This code is contributed by Chitranayal
```

## C#

```
// C# program for the above approach
using System;
class GFG{

// Function to count number of
// sub-Strings of a given binary
// String that contains only 1
static int countSubAllOnes(String s)
{
    int l = 0, r = 0, ans = 0;

    // Iterate untill L and R cross
    // each other
    while (l <= r)
    {

        // Check if reached the end
        // of String
        if (r == s.Length)
        {
            ans += ((r - l) * (r - l + 1)) / 2;
            break;
        }

        // Check if encountered '1'
        // then extend window
        if (s[r] == '1')
            r++;

        // Check if encountered '0' then
        // add number of Strings of
        // current window and change the
        // values for both l and r
        else
        {
            ans += ((r - l) * (r - l + 1)) / 2;
            l = r + 1;
            r++;
        }
    }

    // Return the answer
    return ans;
}

// Function to flip the bits of String
static String flip(char []s)
{
    for(int i = 0; i < s.Length; i++)
    {
        if (s[i] == '1')
            s[i] = '0';
        else
            s[i] = '1';
    }
    return String.Join("",s);
}

// Function to count number of
// sub-Strings of a given binary
// String that contains only 0s & 1s
static int countSubAllZerosOnes(String s)
{

    // count of subString
    // which contains only 1s
    int only_1s = countSubAllOnes(s);

    // Flip the character of String s
    // 0 to 1 and 1 to 0 to count the
    // subString with consecutive 0s
    s = flip(s.ToCharArray());

    // count of subString
    // which contains only 0s
    int only_0s = countSubAllOnes(s);

    return only_0s + only_1s;
}

// Driver Code
public static void Main(String[] args)
{

    // Given String str
    String s = "011";

    // Function call
    Console.Write(countSubAllZerosOnes(s) + "\n");
}
}

// This code is contributed by Rohit_ranjan
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to count number of
// sub-strings of a given binary
// string that contains only 1
function countSubAllOnes(s)
{
    var l = 0, r = 0, ans = 0;

    // Iterate untill L and R cross
    // each other
    while (l <= r) {

        // Check if reached the end
        // of string
        if (r == s.length) {
            ans += ((r - l) * (r - l + 1)) / 2;
            break;
        }

        // Check if encountered '1'
        // then extend window
        if (s[r] == '1')
            r++;

        // Check if encountered '0' then
        // add number of strings of
        // current window and change the
        // values for both l and r
        else {

            ans += ((r - l) * (r - l + 1)) / 2;
            l = r + 1;
            r++;
        }
    }

    // Return the answer
    return ans;
}

// Function to flip the bits of string
function flip(s)
{

    for (var i = 0; s[i]; i++) {
        if (s[i] == '1')
            s[i] = '0';
        else
            s[i] = '1';
    }

  return s;
}

// Function to count number of
// sub-strings of a given binary
// string that contains only 0s & 1s
function countSubAllZerosOnes(s)
{

    // count of substring
    // which contains only 1s
    var only_1s = countSubAllOnes(s);

    // Flip the character of string s
    // 0 to 1 and 1 to 0 to count the
    // substring with consecutive 0s
    s = flip(s.split(''));

    // count of substring
    // which contains only 0s
    var only_0s = countSubAllOnes(s);

    return only_0s + only_1s;
}

// Driver Code

// Given string str
var s = "011";

// Function Call
document.write( countSubAllZerosOnes(s));

// This code is contributed by famously.
</script>
```

**Output:** 

```
4
```

**时间复杂度:*****O(N)*****其中 N 是给定字符串的长度。
**辅助空间:** *O(1)***
# 通过反转具有偶数个 1 的子串

可能得到的字典上最大的字符串

> 原文:[https://www . geeksforgeeks . org/按字典顺序排列的最大可能倒排字符串-具有偶数个 1 的子字符串/](https://www.geeksforgeeks.org/lexicographically-largest-string-possible-by-reversing-substrings-having-even-number-of-1s/)

给定一个[二进制字符串](https://www.geeksforgeeks.org/tag/binary-string/) **S** ，任务是通过反转具有偶数个 **1s** 的子字符串，将给定的字符串 **S** 转换为其字典最大形式。

**示例:**

> **输入:**S =“10101”
> **输出:** 11010
> **解释:**
> 反转子串{S[0]，…，S[2]}将 S 修改为“10101”。
> 反转子串{S[1]，…，S[4]}将 S 修改为“11010”。
> 现在，不能选择任何其他子串，因为每个子串要么具有奇数个 1，要么在字典上小于前一个字符串。因此，11010 是可以执行的字典上最大的字符串。
> 
> **输入:**S = " 0101 "
> T3】输出: 1010

**逼近:**思路是从第一个索引开始，[遍历字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/)直到字符串中 **1s** 的总数变为偶数。一旦找到恰好有偶数个 **1s** 的索引，[将字符串](https://www.geeksforgeeks.org/reverse-a-string-in-java/)从起始索引反转到结束索引。对每个索引重复这个过程，以获得字典中最大的字符串。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the lexicographically
// maximum string by reversing substrings
// having even numbers of 1s
void lexicographicallyMax(string s)
{
    // Store size of string
    int n = s.size();

    // Traverse the string
    for (int i = 0; i < n; i++) {

        // Count the number of 1s
        int count = 0;

        // Stores the starting index
        int beg = i;

        // Stores the end index
        int end = i;

        // Increment count, when 1
        // is encountered
        if (s[i] == '1')
            count++;

        // Traverse the remaining string
        for (int j = i + 1; j < n; j++) {
            if (s[j] == '1')
                count++;

            if (count % 2 == 0
                && count != 0) {
                end = j;
                break;
            }
        }

        // Reverse the string from
        // starting and end index
        reverse(s.begin() + beg,
                s.begin() + end + 1);
    }

    // Printing the string
    cout << s << "\n";
}

// Driver Code
int main()
{
    string S = "0101";
    lexicographicallyMax(S);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to find the lexicographically
// maximum string by reversing substrings
// having even numbers of 1s
static void lexicographicallyMax(String s)
{

    // Store size of string
    int n = s.length();

    // Traverse the string
    for(int i = 0; i < n; i++)
    {

        // Count the number of 1s
        int count = 0;

        // Stores the starting index
        int beg = i;

        // Stores the end index
        int end = i;

        // Increment count, when 1
        // is encountered
        if (s.charAt(i) == '1')
            count++;

        // Traverse the remaining string
        for(int j = i + 1; j < n; j++)
        {
            if (s.charAt(j) == '1')
                count++;

            if (count % 2 == 0 &&
                count != 0)
            {
                end = j;
                break;
            }
        }

        // Reverse the string from
        // starting and end index
        s = reverse(s, beg, end + 1);
    }

    // Printing the string
   System.out.println(s);
}

static String reverse(String s, int beg, int end)
{
    StringBuilder x = new StringBuilder("");

    for(int i = 0; i < beg; i++)
        x.append(s.charAt(i));
    for(int i = end - 1; i >= beg; i--)
        x.append(s.charAt(i));
    for(int i = end; i < s.length(); i++)
        x.append(s.charAt(i));

    return x.toString();
}

// Driver Code
public static void main(String args[])
{
    String S = "0101";

    lexicographicallyMax(S);
}
}

// This code is contributed by jyoti369
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the lexicographically
# maximum string by reversing substrings
# having even numbers of 1s
def lexicographicallyMax(s):

    # Store size of string
    n = len(s)

    # Traverse the string
    for i in range(n):

        # Count the number of 1s
        count = 0

        # Stores the starting index
        beg = i

        # Stores the end index
        end = i

        # Increment count, when 1
        # is encountered
        if (s[i] == '1'):
            count += 1

        # Traverse the remaining string
        for j in range(i + 1, n):
            if (s[j] == '1'):
                count += 1

            if (count % 2 == 0 and count != 0):
                end = j
                break

        # temp is for Reverse the string from
        # starting and end index
        temp = s[beg : end + 1]
        temp = temp[::-1]
        s = s[0 : beg] + temp + s[end + 1 :]

    # Printing the string
    print(s)

# Driver Code
S = "0101"

lexicographicallyMax(S)

# This code is contributed by avanitrachhadiya2155
```

## C#

```
// C# program for the above approach
using System;
using System.Text;
class GFG
{

// Function to find the lexicographically
// maximum string by reversing substrings
// having even numbers of 1s
static void lexicographicallyMax(String s)
{

    // Store size of string
    int n = s.Length;

    // Traverse the string
    for(int i = 0; i < n; i++)
    {

        // Count the number of 1s
        int count = 0;

        // Stores the starting index
        int beg = i;

        // Stores the end index
        int end = i;

        // Increment count, when 1
        // is encountered
        if (s[i] == '1')
            count++;

        // Traverse the remaining string
        for(int j = i + 1; j < n; j++)
        {
            if (s[j] == '1')
                count++;
            if (count % 2 == 0 &&
                count != 0)
            {
                end = j;
                break;
            }
        }

        // Reverse the string from
        // starting and end index
        s = reverse(s, beg, end + 1);
    }

    // Printing the string
   Console.WriteLine(s);
}

static String reverse(String s, int beg, int end)
{
    StringBuilder x = new StringBuilder("");

    for(int i = 0; i < beg; i++)
        x.Append(s[i]);
    for(int i = end - 1; i >= beg; i--)
        x.Append(s[i]);
    for(int i = end; i < s.Length; i++)
        x.Append(s[i]);

    return x.ToString();
}

// Driver Code
public static void Main(String []args)
{
    String S = "0101";
    lexicographicallyMax(S);
}
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to find the lexicographically
// maximum string by reversing substrings
// having even numbers of 1s
function lexicographicallyMax(s)
{
    // Store size of string
    var n = s.length;

    // Traverse the string
    for (var i = 0; i < n; i++) {

        // Count the number of 1s
        var count = 0;

        // Stores the starting index
        var beg = i;

        // Stores the end index
        var end = i;

        // Increment count, when 1
        // is encountered
        if (s[i] == '1')
            count++;

        // Traverse the remaining string
        for (var j = i + 1; j < n; j++) {
            if (s[j] == '1')
                count++;

            if (count % 2 == 0
                && count != 0) {
                end = j;
                break;
            }
        }

        // Reverse the string from
        // starting and end index
        for(var i = beg; i<parseInt((end+1)/2);i++)
        {
            let temp = s[i] ;
            s[i] = s[end - i+1] ;
            s[end -i+1 ] = temp;
        }
    }

    // Printing the string
    document.write( s.join("") + "<br>");
}

// Driver Code
var S = "0101".split('');
lexicographicallyMax(S);

</script>
```

**Output:** 

```
1010
```

***时间复杂度:***O(N<sup>2</sup>)
***辅助空间:*** O(1)
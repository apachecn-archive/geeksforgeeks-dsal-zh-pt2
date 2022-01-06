# 十进制等效值大于或等于 K 的子串计数

> 原文:[https://www . geesforgeks . org/substrings-count-其十进制等值大于或等于-k/](https://www.geeksforgeeks.org/count-of-substrings-whose-decimal-equivalent-is-greater-than-or-equal-to-k/)

给定一个整数 **K** 和一个长度为 **N** 的[二进制串](https://www.geeksforgeeks.org/tag/binary-string/) **S** ，任务是找出其十进制等价大于或等于 **K** 的[子串](https://www.geeksforgeeks.org/program-print-substrings-given-string/)的数量。

**示例:**

> **输入:** K = 3，S =“11100”
> **输出:** 8
> **说明:**
> 有 8 个这样的子串，其小数等价大于等于 3，如下所述:
> 子串–小数等价
> “100”–4、
> “1100”–12、
> “1100”–28、
> “110”–6、
> 
> **输入:** K = 5，S = "10110110"
> **输出:** 19
> **说明:**
> 这样的子串有 19 个，其十进制等价大于等于 5。

**天真方法:** [找出所有的子串](https://www.geeksforgeeks.org/program-print-substrings-given-string/)，对于每个子串，将其从二进制转换为十进制，并检查它是否大于或等于 k。计算找到的每个这样的子串的数量。

**有效方法:使用双指针技术**

1.  想法是维持[两分](https://www.geeksforgeeks.org/two-pointers-technique/) **L** 和 **R** 。
2.  将子串右指针“R”的位置固定为**长度–1**，并循环迭代，直到 R 的值为正:
    *   将 L 的值初始化为 R，以考虑长度为 1 的子串
    *   将 L 的值减 1，直到长度为*R–L+1*的子串的十进制等价大于或等于 K
    *   将计数器增加 l 左边的位数。

下面是上述方法的实现:

## C++

```
// C++ implementation to count the
// substrings whose decimal equivalent
// is greater than or equal to K
#include <bits/stdc++.h>
using namespace std;

// Function to count number of
// substring whose decimal equivalent
// is greater than or equal to K
unsigned long long countSubstr(
    string& s, int k)
{

    int n = s.length();

    // Left pointer of the substring
    int l = n - 1;

    // Right pointer of the substring
    int r = n - 1;
    int arr[n];
    int last_indexof1 = -1;

    // Loop to maintain the last
    // occurrence of the 1 in the string
    for (int i = 0; i < n; i++) {
        if (s[i] == '1') {
            arr[i] = i;
            last_indexof1 = i;
        }
        else {
            arr[i] = last_indexof1;
        }
    }

    // Variable to count the substring
    unsigned long long no_of_substr = 0;

    // Loop to maintain the every
    // possible end index of the substring
    for (r = n - 1; r >= 0; r--) {
        l = r;

        // Loop to find the substring
        // whose decimal equivalent is
        // greater than or equal to K
        while (l >= 0
               && (r - l + 1) <= 64
               && stoull(
                      s.substr(l, r - l + 1), 0, 2)
                      < k) {
            l--;
        }

        // Condition to check no
        // of bits is out of bound
        if (r - l + 1 <= 64)
            no_of_substr += l + 1;
        else {
            no_of_substr += arr[l + 1] + 1;
        }
    }
    return no_of_substr;
}

// Driver Code
int main()
{
    string s = "11100";
    unsigned long long int k = 3;
    cout << countSubstr(s, k);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to count the
// subStrings whose decimal equivalent
// is greater than or equal to K
import java.util.*;

class GFG{

// Function to count number of
// subString whose decimal equivalent
// is greater than or equal to K
static long countSubstr(
    String s, int k)
{

    int n = s.length();

    // Left pointer of the subString
    int l = n - 1;

    // Right pointer of the subString
    int r = n - 1;
    int []arr = new int[n];
    int last_indexof1 = -1;

    // Loop to maintain the last
    // occurrence of the 1 in the String
    for (int i = 0; i < n; i++) {
        if (s.charAt(i) == '1') {
            arr[i] = i;
            last_indexof1 = i;
        }
        else {
            arr[i] = last_indexof1;
        }
    }

    // Variable to count the subString
    long no_of_substr = 0;

    // Loop to maintain the every
    // possible end index of the subString
    for (r = n - 1; r >= 0; r--) {
        l = r;

        // Loop to find the subString
        // whose decimal equivalent is
        // greater than or equal to K
        while (l >= 0
               && (r - l + 1) <= 64
               && Integer.valueOf(s.substring(l, r + 1),2)
                      < k) {
            l--;
        }

        // Condition to check no
        // of bits is out of bound
        if (r - l + 1 <= 64)
            no_of_substr += l + 1;
        else {
            no_of_substr += arr[l + 1] + 1;
        }
    }
    return no_of_substr;
}

// Driver Code
public static void main(String[] args)
{
    String s = "11100";
    int k = 3;
    System.out.println(countSubstr(s, k));
}
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 implementation to count the
# substrings whose decimal equivalent
# is greater than or equal to K

# Function to count number of
# substring whose decimal equivalent
# is greater than or equal to K
def countSubstr(s, k):

    n = len(s)

    # Left pointer of the substring
    l = n - 1

    # Right pointer of the substring
    r = n - 1
    arr = [0]*n
    last_indexof1 = -1

    # Loop to maintain the last
    # occurrence of the 1 in the string
    for i in range(n):
        if (s[i] == '1'):
            arr[i] = i
            last_indexof1 = i

        else:
            arr[i] = last_indexof1

    # Variable to count the substring
    no_of_substr = 0

    # Loop to maintain the every
    # possible end index of the substring
    for r in range(n - 1, -1, -1):
        l = r

        # Loop to find the substring
        # whose decimal equivalent is
        # greater than or equal to K
        while (l >= 0 and (r - l + 1) <= 64 and int(s[l:r + 1], 2)< k):
            l -= 1

        # Condition to check no
        # of bits is out of bound
        if (r - l + 1 <= 64):
            no_of_substr += l + 1
        else:
            no_of_substr += arr[l + 1] + 1

    return no_of_substr

# Driver Code

s = "11100"
k = 3
print(countSubstr(s, k))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# implementation to count the
// subStrings whose decimal equivalent
// is greater than or equal to K
using System;

class GFG{

// Function to count number of
// subString whose decimal equivalent
// is greater than or equal to K
static long countSubstr(
    String s, int k)
{

    int n = s.Length;

    // Left pointer of the subString
    int l = n - 1;

    // Right pointer of the subString
    int r = n - 1;
    int []arr = new int[n];
    int last_indexof1 = -1;

    // Loop to maintain the last
    // occurrence of the 1 in the String
    for (int i = 0; i < n; i++) {
        if (s[i] == '1') {
            arr[i] = i;
            last_indexof1 = i;
        }
        else {
            arr[i] = last_indexof1;
        }
    }

    // Variable to count the subString
    long no_of_substr = 0;

    // Loop to maintain the every
    // possible end index of the subString
    for (r = n - 1; r >= 0; r--) {
        l = r;

        // Loop to find the subString
        // whose decimal equivalent is
        // greater than or equal to K
        while (l >= 0
               && (r - l + 1) <= 64 && (int)(Convert.ToInt32(s.Substring(l, r + 1-l), 2))
                      < k) {
            l--;
        }

        // Condition to check no
        // of bits is out of bound
        if (r - l + 1 <= 64)
            no_of_substr += l + 1;
        else {
            no_of_substr += arr[l + 1] + 1;
        }
    }
    return no_of_substr;
}

// Driver Code
public static void Main(String[] args)
{
    String s = "11100";
    int k = 3;
    Console.WriteLine(countSubstr(s, k));
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>
// Javascript implementation to count the
// subStrings whose decimal equivalent
// is greater than or equal to K

// Function to count number of
// subString whose decimal equivalent
// is greater than or equal to K
function countSubstr(s,k)
{
    let n = s.length;

    // Left pointer of the subString
    let l = n - 1;

    // Right pointer of the subString
    let r = n - 1;
    let arr = new Array(n);
    let last_indexof1 = -1;

    // Loop to maintain the last
    // occurrence of the 1 in the String
    for (let i = 0; i < n; i++) {
        if (s[i] == '1') {
            arr[i] = i;
            last_indexof1 = i;
        }
        else {
            arr[i] = last_indexof1;
        }
    }

    // Variable to count the subString
    let no_of_substr = 0;

    // Loop to maintain the every
    // possible end index of the subString
    for (r = n - 1; r >= 0; r--) {
        l = r;

        // Loop to find the subString
        // whose decimal equivalent is
        // greater than or equal to K
        while (l >= 0
               && (r - l + 1) <= 64
               && parseInt(s.substring(l, r + 1),2)
                      < k) {
            l--;
        }

        // Condition to check no
        // of bits is out of bound
        if (r - l + 1 <= 64)
            no_of_substr += l + 1;
        else {
            no_of_substr += arr[l + 1] + 1;
        }
    }
    return no_of_substr;
}

// Driver Code
let s = "11100";
let k = 3;
document.write(countSubstr(s, k));

// This code is contributed by unknown2108
</script>
```

**Output:** 

```
8
```
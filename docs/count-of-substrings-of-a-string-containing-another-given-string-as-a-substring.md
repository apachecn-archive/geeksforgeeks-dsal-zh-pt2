# 包含另一个给定字符串作为子字符串的字符串的子字符串计数

> 原文:[https://www . geesforgeks . org/包含另一个给定字符串的字符串子字符串计数/T1](https://www.geeksforgeeks.org/count-of-substrings-of-a-string-containing-another-given-string-as-a-substring/)

给定两个[字符串](https://www.geeksforgeeks.org/string-data-structure/) **S** 和 **T** ，任务是计算包含字符串 **T** 的 **S** 的子字符串数量。

**示例:**

> **输入:** S = "dabc "，T = "ab"
> **输出:** 4
> **说明:**以 T 为子串的 S 的子串有:
> 
> 1.  S[0，2]=“dab”
> 2.  S[1，2] = "ab "
> 3.  S[1，3]=“ABC”
> 4.  S[0，3]=“dabc”
> 
> **输入:**S = " hshshs " T = " hs "
> T3】输出: 25

**方法:**思路是[生成**S**T5】的所有子串，检查每个子串中是否包含 **T** 。按照以下步骤解决问题:](https://www.geeksforgeeks.org/program-print-substrings-given-string/)

*   初始化一个变量，比如说**计数**，用 **0** 存储所需子串的数量。
*   [找到给定字符串的所有子串 **S**](https://www.geeksforgeeks.org/program-print-substrings-given-string/) 并将其存储在辅助数组**arr【】**中。
*   [遍历给定的数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **arr[]** ，对于其中的每一个字符串，[检查该字符串中是否存在字符串 T](https://www.geeksforgeeks.org/string-find-in-cpp/)。如果出现 **T** ，将**计数**增加 **1** 。
*   完成上述步骤后，**计数**的值即为结果计数。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to store all substrings of S
vector<string> subString(string s, int n)
{
    // Stores the substrings of S
    vector<string> v;

    // Pick start point in outer loop
    // and lengths of different strings
    // for a given starting point
    for (int i = 0; i < n; i++) {

        for (int len = 1;
             len <= n - i; len++) {

            string find = s.substr(i, len);
            v.push_back(find);
        }
    }

    // Return the array containing
    // substrings of S
    return v;
}

// Function to check if a string is
// present in another string
int IsPresent(string& str, string& target)
{
    // Check if target is in the
    // string str or not
    if (str.find(target)
        != string::npos) {
        return 1;
    }

    return -1;
}

// Function to count the substring of S
// containing T in it as substring
void countSubstrings(string& S, string& T)
{

    // Store all substrings of S in
    // the array v[]
    vector<string> v = subString(S, S.length());

    // Store required count of substrings
    int ans = 0;

    // Iterate through all the
    // substrings of S
    for (auto it : v) {

        // If string T is present in the
        // current substring, then
        // increment the ans
        if (IsPresent(it, T) != -1) {
            ans++;
        }
    }

    // Print the answer
    cout << ans;
}

// Driver code
int main()
{
    string S = "dabc";
    string T = "ab";

    // Function Call
    countSubstrings(S, T);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
class GFG
{

// Function to store all subStrings of S
static Vector<String> subString(String s, int n)
{

    // Stores the subStrings of S
    Vector<String> v = new Vector<>();

    // Pick start point in outer loop
    // and lengths of different Strings
    // for a given starting point
    for (int i = 0; i < n; i++)
    {

        for (int len = 1;
             len <= n - i; len++)
        {

            String find = s.substring(i, i + len);
            v.add(find);
        }
    }

    // Return the array containing
    // subStrings of S
    return v;
}

// Function to check if a String is
// present in another String
static int IsPresent(String str, String target)
{

    // Check if target is in the
    // String str or not
    if (str.contains(target))
    {
        return 1;
    }
    return -1;
}

// Function to count the subString of S
// containing T in it as subString
static void countSubStrings(String S, String T)
{

    // Store all subStrings of S in
    // the array v[]
    Vector<String> v = subString(S, S.length());

    // Store required count of subStrings
    int ans = 0;

    // Iterate through all the
    // subStrings of S
    for (String it : v)
    {

        // If String T is present in the
        // current subString, then
        // increment the ans
        if (IsPresent(it, T) != -1)
        {
            ans++;
        }
    }

    // Print the answer
    System.out.print(ans);
}

// Driver code
public static void main(String[] args)
{
    String S = "dabc";
    String T = "ab";

    // Function Call
    countSubStrings(S, T);

}
}

// This code is contributed by Princi Singh
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to store all substrings of S
def subString(s, n):

    # Stores the substrings of S
    v = []

    # Pick start point in outer loop
    # and lengths of different strings
    # for a given starting point
    for i in range(n):

        for len in range(1, n - i + 1):

            find = s[i : i + len]
            v.append(find)

    # Return the array containing
    # substrings of S
    return v

# Function to check if a is
# present in another string
def IsPresent(str, target):

    # Check if target is in the
    # str or not
    if (target in str):
        return 1

    return -1

# Function to count the subof S
# containing T in it as substring
def countSubstrings(S, T):

    # Store all substrings of S in
    # the array v[]
    v = subString(S, len(S))

    # Store required count of substrings
    ans = 0

    # Iterate through all the
    # substrings of S
    for it in v:

        # If T is present in the
        # current substring, then
        # increment the ans
        if (IsPresent(it, T) != -1):
            ans += 1

    # Print the answer
    print(ans)

# Driver code
if __name__ == '__main__':
    S = "dabc"
    T = "ab"

    #Function Call
    countSubstrings(S, T)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;
class GFG
{

    // Function to store all subStrings of S
    static List<string> subString(string s, int n)
    {

        // Stores the subStrings of S
        List<string> v = new List<string>();

        // Pick start point in outer loop
        // and lengths of different Strings
        // for a given starting point
        for (int i = 0; i < n; i++)
        {
            for (int len = 1; len <= n - i; len++)
            {
                string find = s.Substring(i, len);
                v.Add(find);
            }
        }

        // Return the array containing
        // subStrings of S
        return v;
    }

    // Function to check if a String is
    // present in another String
    static int IsPresent(string str, string target)
    {

        // Check if target is in the
        // String str or not
        if (str.Contains(target))
        {
            return 1;
        }
        return -1;
    }

    // Function to count the subString of S
    // containing T in it as subString
    static void countSubStrings(string S, string T)
    {

        // Store all subStrings of S in
        // the array v[]
        List<string> v = subString(S, S.Length);

        // Store required count of subStrings
        int ans = 0;

        // Iterate through all the
        // subStrings of S
        foreach(string it in v)
        {

            // If String T is present in the
            // current subString, then
            // increment the ans
            if (IsPresent(it, T) != -1)
            {
                ans++;
            }
        }

        // Print the answer
        Console.WriteLine(ans);
    }

    // Driver code
    public static void Main(string[] args)
    {
        string S = "dabc";
        string T = "ab";

        // Function Call
        countSubStrings(S, T);
    }
}

// This code is contributed by chitranayal
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to store all substrings of S
function subString(s, n)
{
    // Stores the substrings of S
    var v = [];

    var i,len;
    // Pick start point in outer loop
    // and lengths of different strings
    // for a given starting point
    for (i = 0; i < n; i++) {

        for (len = 1;
             len <= n - i; len++) {

            var find = s.substr(i, len);
            v.push(find);
        }
    }

    // Return the array containing
    // substrings of S
    return v;
}

// Function to check if a string is
// present in another string
function IsPresent(str, target)
{
    // Check if target is in the
    // string str or not
    if (str.includes(target))
    {
        return 1;
    }

    return -1;
}

// Function to count the substring of S
// containing T in it as substring
function countSubstrings(S, T)
{

    // Store all substrings of S in
    // the array v[]
    var v = subString(S, S.length);

    // Store required count of substrings
    var ans = 0;
    var i;
    // Iterate through all the
    // substrings of S
    for (i=0;i<v.length;i++) {

        // If string T is present in the
        // current substring, then
        // increment the ans
        if (IsPresent(v[i], T) != -1) {
            ans++;
        }
    }

    // Print the answer
    document.write(ans);
}

// Driver code
    var S = "dabc";
    var T = "ab";

    // Function Call
    countSubstrings(S, T);

</script>
```

**Output:** 

```
4
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(N <sup>2</sup> )*
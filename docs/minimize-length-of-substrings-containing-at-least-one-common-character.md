# 最小化包含至少一个公共字符的子串的长度

> 原文:[https://www . geeksforgeeks . org/最小化包含至少一个公共字符的子字符串长度/](https://www.geeksforgeeks.org/minimize-length-of-substrings-containing-at-least-one-common-character/)

给定一个字符串 **str** ，任务是找到子字符串的**最小**长度，使得来自 **str** 的该长度的所有子字符串包含至少一个**公共字符**。如果得不到这样的长度，打印 **-1** 。

**示例:**

> **输入:** str = "saad"
> **输出:** 2
> **解释:**
> 给定字符串的所有长度为**两个**的子字符串为{**“sa”、“aa”、“ad”**}。
> 由于**‘a’**在所有子串中是公共的，因此具有至少一个公共字符的子串的最小可能长度是 **2** 。
> 
> **输入:** str = "geeksforgeeks"
> **输出:** 7
> **解释:**
> 长度为 7 的所有可能子串如下:
> 
> *   g **e** eksfo
> *   **t1 的前传**
> *   **e** ksforg
> *   ksforg〔t0〕e〔t1〕
> *   SFE〔t0〕e〔t1〕
> *   锻造 **e** k
> *   大麦〔t0〕e〔t1〕ks
> 
> *由于所有子串都有一个共同字符****【e】****，至少有一个共同字符的子串的最小可能长度为****7****。*

**方法:**这个问题可以通过 [**【二分搜索法】**](https://www.geeksforgeeks.org/binary-search/) 手法轻松解决。按照以下步骤解决问题:

*   将**低电平**初始化为 **1** ，将**高电平**初始化为一段字符串**字符串**。
*   在低和高之间找到**中间**。
*   如果给定字符串的所有子字符串中有一个**通用**字符，则将**高**更新为**中 1。**
*   如果不是这样，不如更新**低**为一**中+ 1** 。
*   对**字母表**中所有 26 个可能的字符重复上述步骤。

下面是上述方法的实现:

## C++

```
// C++ Program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check and return if
// substrings of length mid has a
// common character a
bool check(string& str, int mid, char a)
{

    // Length of the string
    int n = str.size();

    // Initialise the first
    // occurrence of character a
    int previous = -1, i;

    for (i = 0; i < n; ++i) {

        if (str[i] == a) {

            // Check that distance b/w
            // the current and previous
            // occurrence of character a
            // is less than or equal to mid
            if (i - previous > mid) {
                return false;
            }
            previous = i;
        }
    }

    // If distance exceeds mid
    if (i - previous > mid)
        return false;
    else
        return true;
}

// Function to check for all the
// alphabets, if substrings of
// length mid have a character common
bool possible(string& str, int mid)
{

    // Check for all 26 alphabets
    for (int i = 0; i < 26; ++i) {

        // Check that char i + a is
        // common in all the substrings
        // of length mid

        if (check(str, mid, i + 'a'))
            return true;
    }

    // If no characters is common
    return false;
}

// Function to calculate and return
// the minm length of substrings
int findMinLength(string& str)
{

    // Initialise low and high
    int low = 1, high = str.length();

    // Perform binary search
    while (low <= high) {

        // Update mid
        int mid = (low + high) / 2;

        // Check if one common character is
        // present in the length of the mid
        if (possible(str, mid))
            high = mid - 1;
        else
            low = mid + 1;
    }

    // Returns the minimum length
    // that contain one
    // common character
    return high + 1;
}

// Function to check if all
// characters are distinct
bool ifAllDistinct(string str)
{
    set<char> s;
    for (char c : str) {
        s.insert(c);
    }

    return s.size() == str.size();
}

// Driver Code
int main()
{

    string str = "geeksforgeeks";

    if (ifAllDistinct(str))
        cout << -1 << endl;
    else
        cout << findMinLength(str);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;

class GFG{

// Function to check and return if
// subStrings of length mid has a
// common character a
static boolean check(char[] str, int mid,
                     char a)
{

    // Length of the String
    int n = str.length;

    // Initialise the first
    // occurrence of character a
    int previous = -1, i;

    for(i = 0; i < n; ++i)
    {
        if (str[i] == a)
        {

            // Check that distance b/w
            // the current and previous
            // occurrence of character a
            // is less than or equal to mid
            if (i - previous > mid)
            {
                return false;
            }
            previous = i;
        }
    }

    // If distance exceeds mid
    if (i - previous > mid)
        return false;
    else
        return true;
}

// Function to check for all the
// alphabets, if subStrings of
// length mid have a character common
static boolean possible(char[] str, int mid)
{

    // Check for all 26 alphabets
    for(int i = 0; i < 26; ++i)
    {

        // Check that char i + a is
        // common in all the subStrings
        // of length mid
        if (check(str, mid, (char)(i + 'a')))
            return true;
    }

    // If no characters is common
    return false;
}

// Function to calculate and return
// the minm length of subStrings
static int findMinLength(char[] str)
{

    // Initialise low and high
    int low = 1, high = str.length;

    // Perform binary search
    while (low <= high)
    {

        // Update mid
        int mid = (low + high) / 2;

        // Check if one common character is
        // present in the length of the mid
        if (possible(str, mid))
            high = mid - 1;
        else
            low = mid + 1;
    }

    // Returns the minimum length
    // that contain one
    // common character
    return high + 1;
}

// Function to check if all
// characters are distinct
static boolean ifAllDistinct(String str)
{
    HashSet<Character> s = new HashSet<Character>();
    for(char c : str.toCharArray())
    {
        s.add(c);
    }
    return s.size() == str.length();
}

// Driver Code
public static void main(String[] args)
{
    String str = "geeksforgeeks";

    if (ifAllDistinct(str))
        System.out.print(-1 + "\n");
    else
        System.out.print(findMinLength(
               str.toCharArray()));
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to check and return if
# substrings of length mid has a
# common character a
def check(st, mid, a):

    # Length of the string
    n = len(st)

    # Initialise the first
    # occurrence of character a
    previous = -1

    for i in range(n):
        if (st[i] == chr(a)):

            # Check that distance b/w
            # the current and previous
            # occurrence of character a
            # is less than or equal to mid
            if (i - previous > mid):
                return False

            previous = i    

    # If distance exceeds mid
    if (i - previous > mid):
        return False
    else:
        return True

# Function to check for all the
# alphabets, if substrings of
# length mid have a character common
def possible(st, mid):

    # Check for all 26 alphabets
    for i in range(26):

        # Check that char i + a is
        # common in all the substrings
        # of length mid
        if (check(st, mid, i + ord('a'))):
            return True

    # If no characters is common
    return False

# Function to calculate and return
# the minm length of substrings
def findMinLength(st):

    # Initialise low and high
    low = 1
    high = len(st)

    # Perform binary search
    while (low <= high):

        # Update mid
        mid = (low + high) // 2

        # Check if one common character is
        # present in the length of the mid
        if (possible(st, mid)):
            high = mid - 1
        else:
            low = mid + 1

    # Returns the minimum length
    # that contain one
    # common character
    return high + 1

# Function to check if all
# characters are distinct
def ifAllDistinct( st):

    s = []
    for c in st:
        s.append(c)

    return len(set(s)) == len(st)

# Driver Code
if __name__ == "__main__":

    st = "geeksforgeeks"

    if (ifAllDistinct(st)):
        print("-1")
    else:
        print(findMinLength(st))

# This code is contributed by chitranayal
```

## C#

```
// C# program to implement
// the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to check and return if
// subStrings of length mid has a
// common character a
static bool check(char[] str, int mid,
                  char a)
{

    // Length of the String
    int n = str.Length;

    // Initialise the first
    // occurrence of character a
    int previous = -1, i;

    for(i = 0; i < n; ++i)
    {
        if (str[i] == a)
        {

            // Check that distance b/w
            // the current and previous
            // occurrence of character a
            // is less than or equal to mid
            if (i - previous > mid)
            {
                return false;
            }
            previous = i;
        }
    }

    // If distance exceeds mid
    if (i - previous > mid)
        return false;
    else
        return true;
}

// Function to check for all the
// alphabets, if subStrings of
// length mid have a character common
static bool possible(char[] str, int mid)
{

    // Check for all 26 alphabets
    for(int i = 0; i < 26; ++i)
    {

        // Check that char i + a is
        // common in all the subStrings
        // of length mid
        if (check(str, mid, (char)(i + 'a')))
            return true;
    }

    // If no characters is common
    return false;
}

// Function to calculate and return
// the minm length of subStrings
static int findMinLength(char[] str)
{

    // Initialise low and high
    int low = 1, high = str.Length;

    // Perform binary search
    while (low <= high)
    {

        // Update mid
        int mid = (low + high) / 2;

        // Check if one common character is
        // present in the length of the mid
        if (possible(str, mid))
            high = mid - 1;
        else
            low = mid + 1;
    }

    // Returns the minimum length
    // that contain one
    // common character
    return high + 1;
}

// Function to check if all
// characters are distinct
static bool ifAllDistinct(String str)
{
    HashSet<char> s = new HashSet<char>();
    foreach(char c in str.ToCharArray())
    {
        s.Add(c);
    }
    return s.Count == str.Length;
}

// Driver Code
public static void Main(String[] args)
{
    String str = "geeksforgeeks";

    if (ifAllDistinct(str))
        Console.Write(-1 + "\n");
    else
        Console.Write(findMinLength(
            str.ToCharArray()));
}
}

// This code is contributed by gauravrajput1
```

## java 描述语言

```
<script>

// JavaScript program to implement
// the above approach

// Function to check and return if
// subStrings of length mid has a
// common character a
function check(str, mid, a)
{

    // Length of the String
    var n = str.length;

    // Initialise the first
    // occurrence of character a
    var previous = -1,
    i;

    for(i = 0; i < n; ++i)
    {
        if (str[i] === a)
        {

            // Check that distance b/w
            // the current and previous
            // occurrence of character a
            // is less than or equal to mid
            if (i - previous > mid)
            {
                return false;
            }
            previous = i;
        }
    }

    // If distance exceeds mid
    if (i - previous > mid)
        return false;
    else
        return true;
}

// Function to check for all the
// alphabets, if subStrings of
// length mid have a character common
function possible(str, mid)
{

    // Check for all 26 alphabets
    for(var i = 0; i < 26; ++i)
    {
        // Check that char i + a is
        // common in all the subStrings
        // of length mid

        if (check(str, mid,
            String.fromCharCode(
            i + "a".charCodeAt(0))))
            return true;
    }

    // If no characters is common
    return false;
}

// Function to calculate and return
// the minm length of subStrings
function findMinLength(str)
{

    // Initialise low and high
    var low = 1,
    high = str.length;

    // Perform binary search
    while (low <= high)
    {

        // Update mid
        var mid = parseInt((low + high) / 2);

        // Check if one common character is
        // present in the length of the mid
        if (possible(str, mid))
            high = mid - 1;
        else
            low = mid + 1;
    }

    // Returns the minimum length
    // that contain one
    // common character
    return high + 1;
}

// Function to check if all
// characters are distinct
function ifAllDistinct(str)
{
    var s = new Array();
    var temp = str.split("");

    for(const c of temp)
    {
        s.push(c);
    }
    var set = new Set(s);
    return set.size === str.length;
}

// Driver Code
var str = "geeksforgeeks";

if (ifAllDistinct(str))
    document.write(-1 + "<br>");
else
    document.write(
        findMinLength(str.split("")));

// This code is contributed by rdtank 

</script>
```

**Output:** 

```
7
```

***时间复杂度:**O(26 * N * log(N))*
***辅助空间:** O(1)*
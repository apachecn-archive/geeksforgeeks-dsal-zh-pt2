# 计算子串串联形成回文的字符串对

> 原文:[https://www . geesforgeks . org/count-对字符串-其子字符串串联-形成回文/](https://www.geeksforgeeks.org/count-pair-of-strings-whose-concatenation-of-substrings-form-a-palindrome/)

给定一个字符串数组 **arr[]** ，任务是计算子字符串串联形成回文的字符串对。
**例:**

> **输入:**arr[]= {“gfg”，“gfg”}
> **输出:** 1
> **解释:**
> 选择 s1 和 s2 的一种可能方式是 S1 =“gf”，S2 =“g”，这样 s1 + s2 即“gfg”就是回文。
> **输入:**arr[]= {“ABC”，B = "def"}
> **输出:** 0

**逼近**:问题中的关键观察是，如果两个字符串都至少有一个共同的字符，比如说‘c’，那么我们可以形成一个回文字符串。因此，检查数组中的所有对，看字符串中是否有公共字符。
以下是上述办法的实施情况:

## C++

```
// C++ implementation to count of
// palindromic Palindromic Substrings
// that can be formed from the array

#include<bits/stdc++.h>
using namespace std;

// Function to to check if possible
// to make palindromic substring
bool isPossible(string A, string B)
{

        sort(B.begin(),B.end());
        int c=0;
        for(int i = 0; i < (int)A.size(); i++)
            if(binary_search(B.begin(),B.end(),A[i]))
                return true;
    return false;
}

// Function to count of Palindromic Substrings
// that can be formed from the array.
int countPalindromicSubstrings(string s[], int n)
{
    // variable to store count
    int count = 0;

    // Traverse through all the pairs
    // in the array
    for(int i = 0; i < n; i++){
        for(int j = i + 1; j < n; j++)
            if(isPossible(s[i], s[j]))
                count++;
    }
    return count;
}

// Driver Code
int main()
{
    string arr[] = { "gfg", "gfg" };
    int n = 2;
    cout << countPalindromicSubstrings(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to count of
// palindromic Palindromic SubStrings
// that can be formed from the array
import java.util.*;

class GFG{

// Function to to check if possible
// to make palindromic subString
static boolean isPossible(String A, String B)
{
    B = sortString(B);

    for(int i = 0; i < (int)A.length(); i++)
        if(Arrays.binarySearch(B.toCharArray(),
                               A.charAt(i)) > -1)
           return true;

    return false;
}

// Function to count of Palindromic SubStrings
// that can be formed from the array.
static int countPalindromicSubStrings(String s[],
                                      int n)
{

    // Variable to store count
    int count = 0;

    // Traverse through all the pairs
    // in the array
    for(int i = 0; i < n; i++)
    {
        for(int j = i + 1; j < n; j++)
            if(isPossible(s[i], s[j]))
                count++;
    }
    return count;
}

static String sortString(String inputString)
{

    // Convert input string to char array
    char tempArray[] = inputString.toCharArray();

    // Sort tempArray
    Arrays.sort(tempArray);

    // Return new sorted string
    return new String(tempArray);
}

// Driver Code
public static void main(String[] args)
{
    String arr[] = { "gfg", "gfg" };
    int n = 2;

    System.out.print(countPalindromicSubStrings(arr, n));
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 implementation to count of
# palindromic Palindromic Substrings
# that can be formed from the array

# Function to to check if possible
# to make palindromic substring
def isPossible(A, B):

    B = sorted(B)
    c = 0

    for i in range(len(A)):
        if A[i] in B:
            return True
    return False

# Function to count of Palindromic
# Substrings that can be formed
# from the array.
def countPalindromicSubstrings(s, n):

    # Variable to store count
    count = 0

    # Traverse through all
    # Substrings in the array
    for i in range(n):
        for j in range(i + 1, n):
            if(isPossible(s[i], s[j])):
                count += 1
    return count

# Driver Code
arr = ["gfg", "gfg"]
n = 2
print(countPalindromicSubstrings(arr, n))

# This code is contributed by avanitrachhadiya2155
```

## C#

```
// C# implementation to count of
// palindromic Palindromic SubStrings
// that can be formed from the array
using System;
class GFG{

// Function to to check if possible
// to make palindromic subString
static bool isPossible(String A, String B)
{
    B = sortString(B);

    for(int i = 0; i < (int)A.Length; i++)
        if(Array.BinarySearch(B.ToCharArray(),
                               A[i]) > -1)
           return true;

    return false;
}

// Function to count of Palindromic SubStrings
// that can be formed from the array.
static int countPalindromicSubStrings(String []s,
                                      int n)
{

    // Variable to store count
    int count = 0;

    // Traverse through all the pairs
    // in the array
    for(int i = 0; i < n; i++)
    {
        for(int j = i + 1; j < n; j++)
            if(isPossible(s[i], s[j]))
                count++;
    }
    return count;
}

static String sortString(String inputString)
{

    // Convert input string to char array
    char []tempArray = inputString.ToCharArray();

    // Sort tempArray
    Array.Sort(tempArray);

    // Return new sorted string
    return new String(tempArray);
}

// Driver Code
public static void Main(String[] args)
{
    String []arr = { "gfg", "gfg" };
    int n = 2;

    Console.Write(countPalindromicSubStrings(arr, n));
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>
// Javascript implementation

// Function to to check if possible
// to make palindromic substring
function isPossible(A, B)
{
    B = B.split('').sort().join('');
    var c=0;
    for(var i = 0; i < A.length; i++)
        if(B.indexOf(A[i]) != -1)
            return true;
    return false;
}

// Function to count of Palindromic Substrings
// that can be formed from the array.
function countPalindromicSubstrings(s, n)
{
    // variable to store count
    var count = 0;

    // Traverse through all the pairs
    // in the array
    for(var i = 0; i < n; i++){
        for(var j = i + 1; j < n; j++)
            if(isPossible(s[i], s[j]))
                count++;
    }
    return count;
}

// Driver Code
var arr = ["gfg", "gfg"]
var n = 2
document.write(countPalindromicSubstrings(arr, n))

// This code is contributed by shubhamsingh10
</script>
```

**Output:** 

```
1
```
# 最长的字符串，它是至少两个字符串的前缀字符串

> 原文:[https://www . geesforgeks . org/最长字符串(至少两个字符串中的前缀字符串)/](https://www.geeksforgeeks.org/longest-string-which-is-prefix-string-of-at-least-two-strings/)

给定一组相同长度的字符串，我们需要找到最长字符串的长度，它是至少两个字符串的前缀字符串。

**例:**

```
Input:  ["abcde", "abcsd", "bcsdf", "abcda", "abced"]
Output: 4
Explanation:  
Longest prefix string is "abcd".

Input:  ["pqrstq", "pwxyza", "abcdef", "pqrstu"]
Output: 5
```

**方法:**

*   Iterate each character from the 0th position, and check whether the character appears in at least two strings at the current position.
*   If so, the next location is recursively called. Otherwise,
*   Use current _ position–1 to take the current maximum value and update the maximum value.
*   Finally, the maximum value is returned.

## c++

```
// C++ program to find longest
// string which is prefix string
// of at least two strings
#include<bits/stdc++.h>
using namespace std;
int max1=0;

// Function to find Max length
// of the prefix
int MaxLength(vector<string> v, int i,
                                int m)
{
    // Base case
    if(i>=m)
    {
        return m-1;
    }

    // Iterating over all the alphabets
    for(int k = 0; k < 26; k++)
    {
        char c = 'a' + k;
        vector<string> v1;

        // Checking if char exists in
        // current string or not
        for(int j = 0; j < v.size(); j++)
        {
            if(v[j][i] == c)
            {
                v1.push_back(v[j]);
            }
        }

        // If atleast 2 string have
        // that character
        if(v1.size()>=2)
        {
           // Recursive call to i+1
           max1=max(max1,
                    MaxLength(v1, i+1, m));
        }
        else
        {
            max1=max(max1, i - 1);
        }
    }
    return max1;
}

// Driver code
int main()
{
  // Initialising strings 
  string s1, s2, s3, s4, s5;

  s1 = "abcde";
  s2 = "abcsd";
  s3 = "bcsdf";
  s4 = "abcda";
  s5 = "abced";

  vector<string> v;

  // push strings into vectors.
  v.push_back(s1);
  v.push_back(s2);
  v.push_back(s3);
  v.push_back(s4);
  v.push_back(s5);

  int m = v[0].size();

  cout<<MaxLength(v, 0, m) + 1<<endl;

  return 0;
}
```

## Java

```
// Java program to find longest
// String which is prefix String
// of at least two Strings
import java.util.*;
class GFG{
static int max1 = 0;

// Function to find Max length
// of the prefix
static int MaxLength(Vector<String> v,
                     int i, int m)
{
    // Base case
    if(i>=m)
    {
        return m-1;
    }

    // Iterating over all the alphabets
    for(int k = 0; k < 26; k++)
    {
        char c = (char)('a' + k);
        Vector<String> v1 = new Vector<String>();

        // Checking if char exists in
        // current String or not
        for(int j = 0; j < v.size(); j++)
        {
            if(v.get(j).charAt(i) == c)
            {
                v1.add(v.get(j));
            }
        }

        // If atleast 2 String have
        // that character
        if(v1.size() >= 2)
        {
           // Recursive call to i+1
           max1=Math.max(max1,
                         MaxLength(v1, i + 1, m));
        }
        else
        {
            max1=Math.max(max1, i - 1);
        }
    }
    return max1;
}

// Driver code
public static void main(String[] args)
{
  // Initialising Strings 
  String s1, s2, s3, s4, s5; 
  s1 = "abcde";
  s2 = "abcsd";
  s3 = "bcsdf";
  s4 = "abcda";
  s5 = "abced";

  Vector<String> v = new Vector<String>();

  // push Strings into vectors.
  v.add(s1);
  v.add(s2);
  v.add(s3);
  v.add(s4);
  v.add(s5);

  int m = v.get(0).length();   
  System.out.print(MaxLength(v, 0, m) + 1);
}
}

// This code is contributed by shikhasingrajput
```

## python 3

```
# Python3 program to find longest
# string which is prefix string
# of at least two strings

max1 = 0

# Function to find max length
# of the prefix
def MaxLength(v, i, m):

    global max1

    # Base case
    if(i >= m):
        return m - 1

    # Iterating over all the alphabets
    for k in range(26):
        c = chr(ord('a') + k)
        v1 = []

        # Checking if char exists in
        # current string or not
        for j in range(len(v)):
            if(v[j][i] == c):
                v1.append(v[j])

        # If atleast 2 string have
        # that character
        if(len(v1) >= 2):

            # Recursive call to i+1
            max1 = max(max1, MaxLength(v1, i + 1, m))
        else:
            max1 = max(max1, i - 1)

    return max1

# Driver code
if __name__ == '__main__':

    # Initialising strings
    s1 = "abcde"
    s2 = "abcsd"
    s3 = "bcsdf"
    s4 = "abcda"
    s5 = "abced"
    v = []

    # Push strings into vectors.
    v.append(s1)
    v.append(s2)
    v.append(s3)
    v.append(s4)
    v.append(s5)

    m = len(v[0])

    print(MaxLength(v, 0, m) + 1)

# This code is contributed by BhupendraSingh
```

T31】c#T3T35】JavascriptT4输出:

```
4
```

T43】
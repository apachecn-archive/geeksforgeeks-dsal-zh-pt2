# 字典上最小的 K 长度子串，包含最大数量的元音

> 原文:[https://www . geeksforgeeks . org/按字典顺序排列-最小 k 长度-包含子串-最大元音数量/](https://www.geeksforgeeks.org/lexicographically-smallest-k-length-substring-containing-maximum-number-of-vowels/)

给定仅包含小写英文字母的字符串**和一个整数 **K** ，任务是找到一个 **K** 长度的子字符串，该子字符串包含最大数量的元音(即*“a”、“e”、“I”、“o”、“u”*)。如果有多个这样的子字符串，则返回按字典序最小的子字符串。** 

**示例:**

> **输入:** str = "geeksforgeeks "，K = 4
> **输出:** eeks
> **解释:**
> 元音数最多的子串是“geek”，“eeks”包含 2 个元音。但是“eeks”在词汇上是最小的。
> **输入:**str = " ceebaceefo "，K = 3
> **输出:** ace
> **解释:**
> 从词典学上看，元音数量最多的子串是“ace”。

**天真方法:**
为了解决上面提到的问题，我们必须[生成长度为 **K**](https://www.geeksforgeeks.org/program-print-substrings-given-string/) 的所有子串，并存储包含最大数量元音的所有这样的子串中字典最小的子串。
***时间复杂度:** O(N <sup>2</sup> )*

**高效方法:**
上述过程可以通过创建元音的 [**前缀和数组**](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/)*****pref[]***来优化，其中**with**索引包含从 **0** 到带有索引的**的元音计数。任何子串**str【l:r】**的元音计数可以由 **pref[r]-pref[l-1]** 给出。然后，[找到元音数最多的字典最小子串](https://www.geeksforgeeks.org/lexicographically-smallest-and-largest-substring-of-size-k/)。
以下是上述方法的实施:****

## **C++**

```
// C++ program to find
// lexicographically smallest
// K-length substring containing
// maximum number of vowels

#include <bits/stdc++.h>
using namespace std;

// Function that prints the
// lexicographically smallest
// K-length substring containing
// maximum number of vowels
string maxVowelSubString(
    string str, int K)
{
    // Store the length of the string
    int N = str.length();

    // Initialize a prefix sum array
    int pref[N];

    // Loop through the string to
    // create the prefix sum array
    for (int i = 0; i < N; i++) {

        // Store 1 at the index
        // if it is a vowel
        if (str[i] == 'a'
            or str[i] == 'e'
            or str[i] == 'i'
            or str[i] == 'o'
            or str[i] == 'u')
            pref[i] = 1;

        // Otherwise, store 0
        else
            pref[i] = 0;

        // Process the prefix array
        if (i)
            pref[i] += pref[i - 1];
    }

    // Initialize the variable to store
    // maximum count of vowels
    int maxCount = pref[K - 1];

    // Initialize the variable
    // to store substring
    // with maximum count of vowels
    string res = str.substr(0, K);

    // Loop through the prefix array
    for (int i = K; i < N; i++) {

        // Store the current
        // count of vowels
        int currCount
            = pref[i]
              - pref[i - K];

        // Update the result if current count
        // is greater than maximum count
        if (currCount > maxCount) {

            maxCount = currCount;
            res = str.substr(i - K + 1, K);
        }

        // Update lexicographically smallest
        // substring if the current count
        // is equal to the maximum count
        else if (currCount == maxCount) {

            string temp
                = str.substr(
                    i - K + 1, K);

            if (temp < res)
                res = temp;
        }
    }

    // Return the result
    return res;
}

// Driver Program
int main()
{
    string str = "ceebbaceeffo";
    int K = 3;

    cout << maxVowelSubString(str, K);

    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java program to find
// lexicographically smallest
// K-length substring containing
// maximum number of vowels
class GFG{

// Function that prints the
// lexicographically smallest
// K-length substring containing
// maximum number of vowels
static String maxVowelSubString(String str,
                                int K)
{
  // Store the length of the string
  int N = str.length();

  // Initialize a prefix sum array
  int []pref = new int[N];

  // Loop through the string to
  // create the prefix sum array
  for (int i = 0; i < N; i++)
  {
    // Store 1 at the index
    // if it is a vowel
    if (str.charAt(i) == 'a' ||
        str.charAt(i) == 'e' ||
        str.charAt(i) == 'i' ||
        str.charAt(i) == 'o' ||
        str.charAt(i) == 'u')
      pref[i] = 1;

    // Otherwise, store 0
    else
      pref[i] = 0;

    // Process the prefix array
    if (i != 0)
      pref[i] += pref[i - 1];
  }

  // Initialize the variable to store
  // maximum count of vowels
  int maxCount = pref[K - 1];

  // Initialize the variable
  // to store substring
  // with maximum count of vowels
  String res = str.substring(0, K);

  // Loop through the prefix array
  for (int i = K; i < N; i++)
  {
    // Store the current
    // count of vowels
    int currCount = pref[i] -
                    pref[i - K];

    // Update the result if current count
    // is greater than maximum count
    if (currCount > maxCount)
    {
      maxCount = currCount;
      res = str.substring(i - K + 1,
                          i + 1);
    }

    // Update lexicographically smallest
    // substring if the current count
    // is equal to the maximum count
    else if (currCount == maxCount)
    {
      String temp = str.substring(i - K + 1,
                                  i + 1);

      if (temp.compareTo(res) < 0)
        res = temp;
    }
  }

  // Return the result
  return res;
}

// Driver Code
public static void main(String []args)
{
  String str = "ceebbaceeffo";
  int K = 3;
  System.out.print(maxVowelSubString(str, K));
}
}

// This code is contributed by Chitranayal
```

## **蟒蛇 3**

```
# Python3 program to find
# lexicographically smallest
# K-length substring containing
# maximum number of vowels

# Function that prints the
# lexicographically smallest
# K-length substring containing
# maximum number of vowels
def maxVowelSubString(str1, K):

    # Store the length of the string
    N = len(str1)

    # Initialize a prefix sum array
    pref = [0 for i in range(N)]

    # Loop through the string to
    # create the prefix sum array
    for i in range(N):

        # Store 1 at the index
        # if it is a vowel
        if (str1[i] == 'a' or
            str1[i] == 'e' or
            str1[i] == 'i' or
            str1[i] == 'o' or
            str1[i] == 'u'):
            pref[i] = 1

        # Otherwise, store 0
        else:
            pref[i] = 0

        # Process the prefix array
        if (i):
            pref[i] += pref[i - 1]

    # Initialize the variable to
    # store maximum count of vowels
    maxCount = pref[K - 1]

    # Initialize the variable
    # to store substring with
    # maximum count of vowels
    res = str1[0:K]

    # Loop through the prefix array
    for i in range(K, N):

        # Store the current
        # count of vowels
        currCount = pref[i] - pref[i - K]

        # Update the result if current count
        # is greater than maximum count
        if (currCount > maxCount):
            maxCount = currCount
            res = str1[i - K + 1 : i + 1]

        # Update lexicographically smallest
        # substring if the current count
        # is equal to the maximum count
        elif (currCount == maxCount):
            temp = str1[i - K + 1 : i + 1]

            if (temp < res):
                res = temp

    # Return the result
    return res

# Driver code
if __name__ == '__main__':

    str1 = "ceebbaceeffo"
    K = 3

    print(maxVowelSubString(str1, K))

# This code is contributed by Surendra_Gangwar
```

## **C#**

```
// C# program to find
// lexicographically smallest
// K-length substring containing
// maximum number of vowels
using System;
class GFG{

// Function that prints the
// lexicographically smallest
// K-length substring containing
// maximum number of vowels
static string maxVowelSubString(string str,
                                int K)
{
    // Store the length of the string
    int N = str.Length;

    // Initialize a prefix sum array
    int []pref = new int[N];

    // Loop through the string to
    // create the prefix sum array
    for (int i = 0; i < N; i++)
    {

        // Store 1 at the index
        // if it is a vowel
        if (str[i] == 'a' ||
            str[i] == 'e' ||
            str[i] == 'i' ||
            str[i] == 'o' ||
            str[i] == 'u')
            pref[i] = 1;

        // Otherwise, store 0
        else
            pref[i] = 0;

        // Process the prefix array
        if (i != 0)
            pref[i] += pref[i - 1];
    }

    // Initialize the variable to store
    // maximum count of vowels
    int maxCount = pref[K - 1];

    // Initialize the variable
    // to store substring
    // with maximum count of vowels
    string res = str.Substring(0, K);

    // Loop through the prefix array
    for (int i = K; i < N; i++)
    {

        // Store the current
        // count of vowels
        int currCount = pref[i] -
                        pref[i - K];

        // Update the result if current count
        // is greater than maximum count
        if (currCount > maxCount)
        {
            maxCount = currCount;
            res = str.Substring(i - K + 1, K);
        }

        // Update lexicographically smallest
        // substring if the current count
        // is equal to the maximum count
        else if (currCount == maxCount)
        {
            string temp = str.Substring(i - K + 1, K);

            if (string.Compare(temp, res) == -1)
                res = temp;
        }
    }

    // Return the result
    return res;
}

// Driver Code
public static void Main()
{
    string str = "ceebbaceeffo";
    int K = 3;

    Console.Write(maxVowelSubString(str, K));
}
}

// This code is contributed by Code_Mech
```

## **java 描述语言**

```
<script>

// Javascript program to find
// lexicographically smallest
// K-length substring containing
// maximum number of vowels

// Function that prints the
// lexicographically smallest
// K-length substring containing
// maximum number of vowels
function maxVowelSubString(str, K)
{
    // St||e the length of the string
    var N = str.length;

    // Initialize a prefix sum array
    var pref = Array(N);

    // Loop through the string to
    // create the prefix sum array
    for(var i = 0; i < N; i++) {

        // St||e 1 at the index
        // if it is a vowel
        if (str[i] == 'a'
            || str[i] == 'e'
            || str[i] == 'i'
            || str[i] == 'o'
            || str[i] == 'u')
            pref[i] = 1;

        // Otherwise, st||e 0
        else
            pref[i] = 0;

        // Process the prefix array
        if (i)
            pref[i] += pref[i - 1];
    }

    // Initialize the variable to st||e
    // maximum count of vowels
    var maxCount = pref[K - 1];

    // Initialize the variable
    // to st||e substring
    // with maximum count of vowels
    var res = str.substring(0, K);

    // Loop through the prefix array
    for (var i = K; i < N; i++) {

        // St||e the current
        // count of vowels
        var currCount
            = pref[i]
              - pref[i - K];

        // Update the result if current count
        // is greater than maximum count
        if (currCount > maxCount) {

            maxCount = currCount;
            res = str.substring(i - K + 1, i - 1);
        }

        // Update lexicographically smallest
        // substring if the current count
        // is equal to the maximum count
        else if (currCount == maxCount) {

            var temp
                = str.substring(
                    i - K + 1, i + 1);

            if (temp < res)
                res = temp;
        }
    }

    // Return the result
    return res;
}

// Driver Program
var str = "ceebbaceeffo";
var K = 3;
document.write( maxVowelSubString(str, K));

</script>
```

****Output**

```
ace
```** 

*****时间复杂度:** O(N)***

****空间优化方法:****

**我们可以使用滑动窗口来更新每个最大值的结果，而不是存储前缀和。**

## **C++**

```
#include <iostream>
using namespace std;

// Helper function to check if a character is a vowel
bool isVowel(char c)
{
    return c == 'a' or c == 'e' or c == 'i' or c == 'o'
           or c == 'u';
}

// Function to find the maximum vowel substring
string maxVowelSubstring(string s, int k)
{
    int maxCount = 0; // initialize maxCount as 0
    string res = s.substr(
        0, k); // and result as first substring of size k
    for (int i = 0, count = 0; i < s.size();
         i++) // iterate through the string
    {
        if (isVowel(
                s[i])) // if current character is a vowel
            count++; // then increase count
        if (i >= k
            and isVowel(
                s[i - k])) // if character that is leaving
                           // the window is a vowel
            count--; // then decrease count

        if (count > maxCount) // if we get a substring
                              // having more vowels
        {
            maxCount = count; // update count
            if (i >= k)
                res = s.substr(i - k + 1,
                               k); // and update result
        }
        if (count == maxCount
            and i >= k) // if we get a substring with same
                        // maximum number of vowels
        {
            string t = s.substr(i - k + 1, k);
            if (t < res) // then check if it is
                         // lexicographically smaller than
                         // current result and update it
                res = t;
        }
    }
    return res;
}

// Driver code
int main()
{
    string str = "geeksforgeeks";
    int k = 4;
    cout << maxVowelSubstring(str, k);
    return 0;
}
```

## **java 描述语言**

```
<script>

    // Helper function to check if a character is a vowel
    function isVowel(c)
    {
        return (c == 'a' || c == 'e' || c == 'i' || c == 'o'
               || c == 'u');
    }

    // Function to find the maximum vowel substring
    function maxVowelSubstring(s, k)
    {
        // initialize maxCount as 0
        let maxCount = 0;
        // and result as first substring of size k
        let res = s.substr(0, k);
        // iterate through the string
        for (let i = 0, count = 0; i < s.length; i++)
        {
            // if current character is a vowel
            if (isVowel(s[i]))
                count++; // then increase count

            // if character that is leaving 
            if (i >= k && isVowel(s[i - k]))
                               // the window is a vowel
                count--; // then decrease count

            if (count > maxCount) // if we get a substring
                                  // having more vowels
            {
                maxCount = count; // update count
                if (i >= k)
                    // and update result
                    res = s.substr(i - k + 1, k);
            }
            // if we get a substring with same
            if (count == maxCount && i >= k)
                            // maximum number of vowels
            {
                let t = s.substr(i - k + 1, k);
                if (t < res) // then check if it is
                             // lexicographically smaller than
                             // current result and update it
                    res = t;
            }
        }
        return res;
    }

    let str = "geeksforgeeks";
    let k = 4;
    document.write(maxVowelSubstring(str, k));

</script>
```

****Output**

```
eeks
```** 

*****时间复杂度:** O(N)*
***空间复杂度:** O(1)***
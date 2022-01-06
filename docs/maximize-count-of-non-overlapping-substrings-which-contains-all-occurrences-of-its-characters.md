# 最大化包含所有字符的非重叠子串的计数

> 原文:[https://www . geeksforgeeks . org/最大化非重叠子字符串的计数-包含其字符的所有出现次数/](https://www.geeksforgeeks.org/maximize-count-of-non-overlapping-substrings-which-contains-all-occurrences-of-its-characters/)

给定由小写字母组成的[字符串](https://www.geeksforgeeks.org/string-data-structure/) **字符串**，任务是找到最大数量的非重叠[子字符串](https://www.geeksforgeeks.org/program-print-substrings-given-string/)，使得每个子字符串包含整个字符串中所有出现的字符。如果存在多个具有相同数量子字符串的解决方案，则打印具有最小总长度的解决方案。

**示例:**

> **输入:**str = " abb CCD "
> **输出** : bb cc d
> **解释:**
> 子串的最大数量是这样的，即其字符在字符串中的所有出现都存在。
> 
> 子字符串是{{d，bb，cc}，{d，abba，cc}}
> 
> 因此，最小可能长度的子字符串是{d，bb，cc}。
> 
> **输入:**输出: e f ccc

**方法:**使用[贪婪技术](https://www.geeksforgeeks.org/greedy-algorithms/)可以解决问题。按照以下步骤解决问题:

*   初始化一个[数组](https://www.geeksforgeeks.org/vector-in-cpp-stl/)，比如 **res[]** ，来存储需要的子串。
*   初始化两个[数组](https://www.geeksforgeeks.org/arrays-in-c-cpp/)，比如 **L[]** 和 **R[]** ，分别存储给定字符串所有可能字符的最左边和最右边的索引。
*   [遍历字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-python/)并存储给定字符串的所有可能字符的最左边和最右边的索引。
*   使用变量 **i** 遍历字符串，检查 **i** 是否是 **str[i]** 的最左侧索引，检查从 i <sup>第</sup>个位置开始的子字符串是否与由直到 **str[i -1]** 的字符组成的任何子字符串不重叠。如果发现为真，则将当前子字符串追加到 **res[]** 中。
*   最后，打印 **res[]** 数组。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to check if substring contains all
// occurrences of each character of str or not
int checkValid(string str,int i, int L[], int R[]){

    // Stores rightmost index of str[i]
    int right = R[str[i] - 'a'];

    // Traverse the current substring
    for (int j = i; j < right; j++){

        // If leftmost index of str[j]
        // less than i
        if (L[str[j] - 'a'] < i)
            return -1;

        // Update right   
        right = max(right, R[str[j] - 'a']);
    }

    return right;
 }

// Function to find maximum number of substring
// that satisfy the condition
vector<string> maxcntOfSubstrings(string str) {

    // Stores all substrings that
    // satisfy the condition 
    vector<string> res;

    // Stores length of str
    int n = str.length();

    // Stores leftmost index
    // of each character
    int L[26];

    // Stores rightmost index
    // of each character
    int R[26];

    // Initialize L[] and R[]
    for(int i = 0; i <26; i++) {

        // Initialize L[i]
        // and R[i]
        L[i] = R[i] = -1;
    }

    // Traverse the string
    for (int i = 0; i < n; i++) {

        // If str[i] not
        // already occurred
        if (L[str[i] - 'a'] == -1) {

            // Update leftmost index
            // of str[i]
            L[str[i] - 'a'] = i;

        }

        // Update rightmost index
        // of str[i]
        R[str[i]-'a'] = i;
    }

    // Stores rightmost index of last
    // substring inserted into res[]
    int right = -1;

    // Traverse the string
    for (int i = 0; i < n; i++) {

        // If i is leftmost index of str[i]
        if (i == L[str[i] - 'a']) {

            // Check if a new substring starting
            // from i satisfies the conditions or not
            int new_right = checkValid(str, i,
                                        L, R);

            // If the substring starting from i
            // satisfies the conditions
            if(new_right != -1){

                // Stores the substring starting from
                // i that satisfy the condition
                string sub = str.substr(i,
                        new_right - i + 1);

                // If the substring overlaps
                // with another substring            
                if(new_right < right){

                    // Stores sub to the last
                    // of res
                    res.back() = sub;
                }
                else {

                    // If sub not overlaps to
                    // other string then  append
                    // sub to the end of res
                    res.push_back(sub);
                }

                // Update right
                right = new_right;
            }
        }
    }
        return res;
}

// Driver Code
int main()
{
    string str = "abbaccd";

    // Stores maximum number of substring
    // that satisfy the condition
    vector<string> res
      = maxcntOfSubstrings(str);

    // Print all substring
    for(auto sub : res) {
        cout<<sub<<" ";
    }
}

```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;

class GFG{

// Function to check if subString contains all
// occurrences of each character of str or not
static int checkValid(String str, int i,
                         int L[], int R[])
{

    // Stores rightmost index of str.charAt(i)
    int right = R[(int)(str.charAt(i)) - 97];

    // Traverse the current subString
    for(int j = i; j < right; j++)
    {

        // If leftmost index of str[j]
        // less than i
        if (L[(int)(str.charAt(j)) - 97] < i)
            return -1;

        // Update right   
        right = Math.max(right,
                         R[(int)(str.charAt(j)) - 97]);
    }
    return right;
}

// Function to find maximum number of subString
// that satisfy the condition
static Vector<String> maxcntOfSubStrings(String str)
{

    // Stores all subStrings that
    // satisfy the condition 
    Vector<String> res = new Vector<String>();

    // Stores length of str
    int n = str.length();

    // Stores leftmost index
    // of each character
    int []L = new int[26];

    // Stores rightmost index
    // of each character
    int []R = new int[26];

    // Initialize L[] and R[]
    for(int i = 0; i < 26; i++)
    {

        // Initialize L[i]
        // and R[i]
        L[i] = R[i] = -1;
    }

    // Traverse the String
    for(int i = 0; i < n; i++)
    {

        // If str.charAt(i) not
        // already occurred
        if (L[(int)(str.charAt(i)) - 97] == -1)
        {

            // Update leftmost index
            // of str.charAt(i)
            L[(int)(str.charAt(i)) - 97] = i;
        }

        // Update rightmost index
        // of str.charAt(i)
        R[(int)(str.charAt(i)) - 97] = i;
    }

    // Stores rightmost index of last
    // subString inserted into res[]
    int right = -1;

    // Traverse the String
    for(int i = 0; i < n; i++)
    {

        // If i is leftmost index of str.charAt(i)
        if (i == L[(int)(str.charAt(i)) - 97])
        {

            // Check if a new subString starting
            // from i satisfies the conditions or not
            int new_right = checkValid(str, i, L, R);

            // If the subString starting from i
            // satisfies the conditions
            if (new_right != -1)
            {

                // Stores the subString starting from
                // i that satisfy the condition
                String sub = str.substring(i,
                                           new_right + 1);

                // If the subString overlaps
                // with another subString            
                if(new_right < right)
                {

                    // Stores sub to the last
                    // of res
                    res.set(res.size() - 1, sub);
                }
                else
                {

                    // If sub not overlaps to
                    // other String then  append
                    // sub to the end of res
                    res.add(sub);
                }

                // Update right
                right = new_right;
            }
        }
    }
    return res;
}

// Driver Code
public static void main(String args[])
{
    String str = "abbaccd";

    // Stores maximum number of subString
    // that satisfy the condition
    Vector<String> res = maxcntOfSubStrings(str);

    // Print all subString
    for(int i = 0; i < res.size(); i++)
    {
        System.out.print(res.get(i) + " ");
    }
}
}

// This code is contributed by SURENDRA_GANGWAR
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to check if subcontains
# all occurrences of each character
# of str or not
def checkValid(str,i, L, R):

    # Stores rightmost index
    # of str[i]
    right = R[ord(str[i]) -
              ord('a')]

    # Traverse the current sub
    for j in range(i, right):

        # If leftmost index of str[j]
        # less than i
        if (L[ord(str[j]) -
              ord('a')] < i):
            return -1

        # Update right
        right = max(right, R[ord(str[j]) -
                             ord('a')])

    return right

# Function to find maximum
# number of sub that satisfy
# the condition
def maxcntOfSubstrings(str):

    # Stores all substrings that
    # satisfy the condition
    res = []

    # Stores length of str
    n = len(str)

    # Stores leftmost index
    # of each character
    L = [-1] * 26

    # Stores rightmost index
    # of each character
    R = [-1] * 26

    for j, i in enumerate(str):
        x = ord(i) - ord('a')

        # If str[i] not 
        # already occurred
        if L[x] == -1:

            # Update leftmost index
            # of str[i]            
            L[x] = j

        # Update rightmost index 
        # of str[i]            
        R[x] = j

    # Stores rightmost index of
    # last substring inserted
    # into res[] 
    right = -1

    for j, i in enumerate(str):
        x = ord(i) - ord('a')

        # If i is leftmost index
        # of str[i]
        if j == L[x]:

            # Check if a new substring
            # starting from i satisfies
            # the conditions or not            
            new_right = checkValid(str, j,
                                   L, R)

            # If the substring starting
            # from i satisfies the conditions
            if new_right != -1:

                # Stores the substring starting
                # from i that satisfy the condition
                sub = str[j : new_right + 1]

                # If the substring overlaps
                # with another substring
                if new_right < right:
                    res[-1] = sub
                else:

                    # If sub not overlaps to 
                    # other string then  append
                    # sub to the end of res
                    res.append(sub)
                right = new_right

    return res

# Driver Code
if __name__ == '__main__':

    str = "abbaccd"

    # Stores maximum number of sub
    # that satisfy the condition
    res = maxcntOfSubstrings(str)

    # Print sub
    for sub in res:
        print(sub, end = " ")

# This code is contributed by Mohit Kumar 29
```

## C#

```
// C# program to implement
// the above approach
using System;
using System.Collections.Generic;
class GFG {

    // Function to check if substring contains all
    // occurrences of each character of str or not
    static int checkValid(string str,int i, int[] L, int[] R)
    {

        // Stores rightmost index of str[i]
        int right = R[str[i] - 'a'];

        // Traverse the current substring
        for (int j = i; j < right; j++){

            // If leftmost index of str[j]
            // less than i
            if (L[str[j] - 'a'] < i)
                return -1;

            // Update right   
            right = Math.Max(right, R[str[j] - 'a']);
        }

        return right;
     }

    // Function to find maximum number of substring
    // that satisfy the condition
    static List<string> maxcntOfSubstrings(string str)
    {

        // Stores all substrings that
        // satisfy the condition
        List<string> res = new List<string>();

        // Stores length of str
        int n = str.Length;

        // Stores leftmost index
        // of each character
        int[] L = new int[26];

        // Stores rightmost index
        // of each character
        int[] R = new int[26];

        // Initialize L[] and R[]
        for(int i = 0; i <26; i++)
        {

            // Initialize L[i]
            // and R[i]
            L[i] = R[i] = -1;
        }

        // Traverse the string
        for (int i = 0; i < n; i++)
        {

            // If str[i] not
            // already occurred
            if (L[str[i] - 'a'] == -1)
            {

                // Update leftmost index
                // of str[i]
                L[str[i] - 'a'] = i;       
            }

            // Update rightmost index
            // of str[i]
            R[str[i]-'a'] = i;
        }

        // Stores rightmost index of last
        // substring inserted into res[]
        int right = -1;

        // Traverse the string
        for (int i = 0; i < n; i++)
        {

            // If i is leftmost index of str[i]
            if (i == L[str[i] - 'a'])
            {

                // Check if a new substring starting
                // from i satisfies the conditions or not
                int new_right = checkValid(str, i, L, R);

                // If the substring starting from i
                // satisfies the conditions
                if(new_right != -1){

                    // Stores the substring starting from
                    // i that satisfy the condition
                    string sub = str.Substring(i, new_right - i + 1);

                    // If the substring overlaps
                    // with another substring            
                    if(new_right < right){

                        // Stores sub to the last
                        // of res
                        res[res.Count - 1] = sub;
                    }
                    else {

                        // If sub not overlaps to
                        // other string then  append
                        // sub to the end of res
                        res.Add(sub);
                    }

                    // Update right
                    right = new_right;
                }
            }
        }
            return res;
    }

  // Driver code
  static void Main() {
        string str = "abbaccd";

        // Stores maximum number of substring
        // that satisfy the condition
        List<string> res = maxcntOfSubstrings(str);

        // Print all substring
        foreach(string sub in res) {
            Console.Write(sub + " ");
        }
  }
}

// This code is contributed by divyeshrabadiya
```

## java 描述语言

```
<script>
      // JavaScript program to implement
      // the above approach
      // Function to check if substring contains all
      // occurrences of each character of str or not
      function checkValid(str, i, L, R) {
        // Stores rightmost index of str[i]
        var right = R[str[i].charCodeAt(0) - "a".charCodeAt(0)];

        // Traverse the current substring
        for (var j = i; j < right; j++) {
          // If leftmost index of str[j]
          // less than i
          if (L[str[j].charCodeAt(0) - "a".charCodeAt(0)] < i)
              return -1;

          // Update right
          right = Math.max(right, R[str[j].charCodeAt(0) - "a".charCodeAt(0)]);
        }

        return right;
      }

      // Function to find maximum number of substring
      // that satisfy the condition
      function maxcntOfSubstrings(str) {
        // Stores all substrings that
        // satisfy the condition
        var res = [];

        // Stores length of str
        var n = str.length;

        // Stores leftmost index
        // of each character
        var L = new Array(26).fill(-1);

        // Stores rightmost index
        // of each character
        var R = new Array(26).fill(-1);

        // Traverse the string
        for (var i = 0; i < n; i++) {
          var x = str[i].charCodeAt(0) - "a".charCodeAt(0);
          // If str[i] not
          // already occurred
          if (L[x] === -1) {
            // Update leftmost index
            // of str[i]
            L[x] = i;
          }

          // Update rightmost index
          // of str[i]
          R[x] = i;
        }

        // Stores rightmost index of last
        // substring inserted into res[]
        var right = -1;

        // Traverse the string
        for (var i = 0; i < n; i++) {
          var x = str[i].charCodeAt(0) - "a".charCodeAt(0);

          // If i is leftmost index of str[i]
          if (i === L[x]) {
            // Check if a new substring starting
            // from i satisfies the conditions or not
            var new_right = checkValid(str, i, L, R);

            // If the substring starting from i
            // satisfies the conditions
            if (new_right !== -1) {
              // Stores the substring starting from
              // i that satisfy the condition
              var sub = str.substring(i, new_right + 1);

              // If the substring overlaps
              // with another substring
              if (new_right < right) {
                // Stores sub to the last
                // of res
                res[res.length - 1] = sub;
              }
              else {
                // If sub not overlaps to
                // other string then append
                // sub to the end of res
                res.push(sub);
              }

              // Update right
              right = new_right;
            }
          }
        }
        return res;
      }

      // Driver code
      var str = "abbaccd";

      // Stores maximum number of substring
      // that satisfy the condition
      var res = maxcntOfSubstrings(str);

      // Print all substring
      for (const sub of res) {
        document.write(sub + " ");
      }
</script>
```

**Output:** 

```
bb cc d
```

***时间复杂度:** O(N * 26)*
***辅助空间:** O(26)*
# 最大子串长度，其字符频率大于或等于子串的一半

> 原文:[https://www . geeksforgeeks . org/最大子串长度，其字符频率大于或等于子串的一半/](https://www.geeksforgeeks.org/length-of-the-largest-substring-which-have-character-with-frequency-greater-than-or-equal-to-half-of-the-substring/)

给定一个由从“a”到“z”的字符组成的字符串 **S** 。任务是找到 S 的最大子串的长度，其中包含子串中频率大于或等于子串长度一半的字符。
**注**:对于奇数长度的子串，要计算半长考虑整数除法。例如，11 的一半是 5。

**示例:**

```
Input : S = "ababbbacbcbcca" 
Output : 13
Substring from index 1(0-based indexing) to index 13, 
"babbbacbcbcca" have b's frequency equals to 6 which is 
equal to half of the length of substring (13/2 = 6).

Input : S = "abcde"
Output : 3 
```

**简单方法**:想法是找到 **S** 的所有子串，对于每个子串，找到每个字符的频率，并将其与子串长度的一半进行比较。现在，在满足条件的所有子串中，输出是具有最大长度的子串的长度。

**高效方法** :
首先，观察字符串 s 中只能有 26 个不同的字符。因此，逐个考虑每个字符的频率是否大于或等于子字符串的长度。
因此，为了找到满足条件的最长可能子串的长度，对于每个字符，我们将制作字符计数的前缀数组。例如，对于 S = "abacdaef "，前缀数组' a '将是，比如说 **freq[]** ，[1，1，2，2，3，3，3]。
我们希望满足以下条件:

```
freq[r] - freq[l - 1] >= (r - l)/2, where l, r are the indices.
```

另外，我们可以写，

```
(2 * freq[r]) - r >= (2 * freq[l - 1]) - l
```

因此，找到两个数组 **r[]** 和 **l[]** ，其中 r[I]=(2 * freq[I])–I 和 l[I]=(2 * freq[l–1])–l，对于 1<= I<= s 的长度。
现在，对于 **r[]** 中的每一个 **i** ，使用二分搜索法找到**l[**中的下限，使得索引最小找到最大的一个。
然后对每个字符循环上述方法。
以下是上述方法的实施:

## C++

```
// C++ implementation of the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to return the length of the longest
// sub string having frequency of a character
// greater than half of the length of the
// sub string
int maxLength(string s, int n)
{
    int ans = INT_MIN;
    vector<int> A, L, R;
    int freq[n + 5];

    // for each of the character 'a' to 'z'
    for (int i = 0; i < 26; i++) {
        int count = 0;
        memset(freq, 0, sizeof freq);

        // finding frequency prefix array of the
        // character
        for (int j = 0; j < n; j++) {
            if (s[j] - 'a' == i)
                count++;
            freq[j] = count;
        }

        // Finding the r[] and l[] arrays.
        for (int j = 0; j < n; j++) {
            L.push_back((2 * freq[j - 1]) - j);
            R.push_back((2 * freq[j]) - j);
        }

        int max_len = INT_MIN;
        int min_val = INT_MAX;

        // for each j from 0 to n
        for (int j = 0; j < n; j++) {
            min_val = min(min_val, L[j]);
            A.push_back(min_val);

            int l = 0, r = j;

            // Finding the lower bound of i.
            while (l <= r) {
                int mid = (l + r) >> 1;
                if (A[mid] <= R[j]) {
                    max_len = max(max_len, j - mid + 1);
                    r = mid - 1;
                }
                else {
                    l = mid + 1;
                }
            }
        }

        // storing the maximum value of i - j + 1
        ans = max(ans, max_len);

        // clearing all the vector so that it clearing
        // be use for other character.
        A.clear();
        R.clear();
        L.clear();
    }

    return ans;
}

// Driver Code
int main()
{
    string s = "ababbbacbcbcca";
    int n = s.length();

    cout << maxLength(s, n) << '\n';

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
import java.util.*;

class GFG
{

// Function to return the length of the longest
// sub string having frequency of a character
// greater than half of the length of the
// sub string
static int maxLength(String s, int n)
{
    int ans = Integer.MIN_VALUE;
    Vector<Integer> A = new Vector<Integer>();
    Vector<Integer> L = new Vector<Integer>();
    Vector<Integer> R = new Vector<Integer>();

    int []freq = new int[n + 5];

    // for each of the character 'a' to 'z'
    for (int i = 0; i < 26; i++)
    {
        int count = 0;

        // finding frequency prefix array of the
        // character
        for (int j = 0; j < n; j++)
        {
            if (s.charAt(j) - 'a' == i)
                count++;
            freq[j] = count;
        }

        // Finding the r[] and l[] arrays.
        for (int j = 1; j < n; j++)
        {
            L.add((2 * freq[j - 1]) - j);
            R.add((2 * freq[j]) - j);
        }

        int max_len = Integer.MIN_VALUE;
        int min_val = Integer.MAX_VALUE;

        // for each j from 0 to n
        for (int j = 0; j < L.size(); j++)
        {
            min_val = Math.min(min_val, L.get(j));
            A.add(min_val);

            int l = 0, r = j;

            // Finding the lower bound of i.
            while (l <= r)
            {
                int mid = (l + r) >> 1;
                if (A.get(mid) <= R.get(j))
                {
                    max_len = Math.max(max_len,
                                       j - mid + 1);
                    r = mid - 1;
                }
                else
                {
                    l = mid + 1;
                }
            }
        }

        // storing the maximum value of i - j + 1
        ans = Math.max(ans, max_len);

        // clearing all the vector so that it clearing
        // be use for other character.
        A.clear();
        R.clear();
        L.clear();
    }
    return ans;
}

// Driver Code
public static void main(String[] args)
{
    String s = "ababbbacbcbcca";
    int n = s.length();

    System.out.println(maxLength(s, n));
}
}

// This code is contributed by Princi Singh
```

## 蟒蛇 3

```
# Python3 implementation of the above approach
import sys

# Function to return the length
# of the longest sub string
# having frequency of a character
# greater than half of the length
# of the sub string
def maxLength(s, n) :

    ans = -(sys.maxsize + 1);
    A, L, R = [], [], [];
    freq = [0] * (n + 5);

    # for each of the character 'a' to 'z'
    for i in range(26) :
        count = 0;

        # finding frequency prefix array
        # of the character
        for j in range(n) :
            if (ord(s[j]) - ord('a') == i) :
                count += 1;

            freq[j] = count;

        # Finding the r[] and l[] arrays.
        for j in range(n) :
            L.append((2 * freq[j - 1]) - j);
            R.append((2 * freq[j]) - j);

        max_len = -(sys.maxsize + 1);
        min_val = sys.maxsize ;

        # for each j from 0 to n
        for j in range(n) :
            min_val = min(min_val, L[j]);
            A.append(min_val);

            l = 0; r = j;

            # Finding the lower bound of i.
            while (l <= r) :
                mid = (l + r) >> 1;
                if (A[mid] <= R[j]) :
                    max_len = max(max_len, j - mid + 1);
                    r = mid - 1;

                else :
                    l = mid + 1;

        # storing the maximum value of i - j + 1
        ans = max(ans, max_len);

        # clearing all the vector so that it can
        # be used for other characters.
        A.clear();
        R.clear();
        L.clear();

    return ans;

# Driver Code
if __name__ == "__main__" :

    s = "ababbbacbcbcca";
    n = len(s);

    print(maxLength(s, n));

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the above approach
using System;
using System.Collections.Generic;

class GFG
{

// Function to return the length of the longest
// sub string having frequency of a character
// greater than half of the length of the
// sub string
static int maxLength(String s, int n)
{
    int ans = int.MinValue;
    List<int> A = new List<int>();
    List<int> L = new List<int>();
    List<int> R = new List<int>();

    int []freq = new int[n + 5];

    // for each of the character 'a' to 'z'
    for (int i = 0; i < 26; i++)
    {
        int count = 0;

        // finding frequency prefix array of the
        // character
        for (int j = 0; j < n; j++)
        {
            if (s[j] - 'a' == i)
                count++;
            freq[j] = count;
        }

        // Finding the r[] and l[] arrays.
        for (int j = 1; j < n; j++)
        {
            L.Add((2 * freq[j - 1]) - j);
            R.Add((2 * freq[j]) - j);
        }

        int max_len = int.MinValue;
        int min_val = int.MaxValue;

        // for each j from 0 to n
        for (int j = 0; j < L.Count; j++)
        {
            min_val = Math.Min(min_val, L[j]);
            A.Add(min_val);

            int l = 0, r = j;

            // Finding the lower bound of i.
            while (l <= r)
            {
                int mid = (l + r) >> 1;
                if (A[mid] <= R[j])
                {
                    max_len = Math.Max(max_len,
                                       j - mid + 1);
                    r = mid - 1;
                }
                else
                {
                    l = mid + 1;
                }
            }
        }

        // storing the maximum value of i - j + 1
        ans = Math.Max(ans, max_len);

        // clearing all the vector so that it can
        // be used for other characters.
        A.Clear();
        R.Clear();
        L.Clear();
    }
    return ans;
}

// Driver Code
public static void Main(String[] args)
{
    String s = "ababbbacbcbcca";
    int n = s.Length;

    Console.WriteLine(maxLength(s, n));
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
      // JavaScript implementation of the above approach
      // Function to return the length of the longest
      // sub string having frequency of a character
      // greater than half of the length of the
      // sub string
      function maxLength(s, n) {
        var ans = -2147483648;
        var A = [];
        var L = [];
        var R = [];

        var freq = new Array(n + 5).fill(0);

        // for each of the character 'a' to 'z'
        for (var i = 0; i < 26; i++) {
          var count = 0;

          // finding frequency prefix array of the
          // character
          for (var j = 0; j < n; j++) {
            if (s[j].charCodeAt(0) - "a".charCodeAt(0) === i)
                count++;
            freq[j] = count;
          }

          // Finding the r[] and l[] arrays.
          for (var j = 1; j < n; j++) {
            L.push(2 * freq[j - 1] - j);
            R.push(2 * freq[j] - j);
          }

          var max_len = -2147483648;
          var min_val = 2147483648;

          // for each j from 0 to n
          for (var j = 0; j < L.length; j++) {
            min_val = Math.min(min_val, L[j]);
            A.push(min_val);

            var l = 0,
              r = j;

            // Finding the lower bound of i.
            while (l <= r) {
              var mid = (l + r) >> 1;
              if (A[mid] <= R[j]) {
                max_len = Math.max(max_len, j - mid + 1);
                r = mid - 1;
              }
              else {
                l = mid + 1;
              }
            }
          }

          // storing the maximum value of i - j + 1
          ans = Math.max(ans, max_len);

          // clearing all the vector so that it can
          // be used for other characters.
          A = [];
          R = [];
          L = [];
        }
        return ans;
      }

      // Driver Code
      var s = "ababbbacbcbcca";
      var n = s.length;

      document.write(maxLength(s, n));
</script>
```

**Output:** 

```
13
```

**时间复杂度:** O(26*N*logN)

**辅助空间:** O(1)
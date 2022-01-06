# 字符串最大化部分的长度，使得字符串的每个字符出现在一个子字符串中

> 原文:[https://www . geeksforgeeks . org/最大化字符串分区长度，使得字符串中的每个字符都出现在一个子字符串中/](https://www.geeksforgeeks.org/lengths-of-maximized-partitions-of-a-string-such-that-each-character-of-the-string-appears-in-one-substring/)

给定字符串**字符串**由小写字母组成，将给定字符串拆分成尽可能多的子字符串，这样给定字符串中的每个字符都出现在一个子字符串中。任务是打印所有这些分区的长度。

**示例:**

> **输入:** str = "acbbcc"
> **输出:** 1 5
> **解释:**
> 字符串的每个字符最多出现在一个分区中的可能分区是“a”和“cbbcc”。
> 因此，长度为{1，5}
> 
> **输入:**str = " abaccbdeffed "
> **输出:** 6 6
> **解释:**
> 字符串的每个字符最多出现在一个分区中的可能分区是“abaccb”和“defed”。
> 因此，长度为{6，6}

**进场:**使用[贪婪进场](https://www.geeksforgeeks.org/greedy-algorithms/)可以轻松解决这个问题。按照下面给出的步骤解决问题。

1.  将所有字符的最后一个索引存储在**字符串**T5 中。
2.  由于字符串只包含**小写**字母，只需使用固定大小的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**26**来存储每个字符的最后一个索引。
3.  [重复给定的字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-python/)，并按照以下步骤操作:
    *   如果字符的最后一个位置超过当前索引，则将当前字符添加到分区中，并增加分区的长度。
    *   如果当前字符的最后一个索引等于当前索引，则存储其长度并继续下一个字符，以此类推。
4.  完成上述步骤后，打印所有存储的长度。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the length of
// all partitions of a string such
// that each characters occurs in
// a single substring
void partitionString(string s)
{
    int n = s.size();

    // Stores last index of string s
    vector<int> ans;

    if (n == 0) {
        cout << "-1";
        return;
    }

    // Find the last position of
    // each letter in the string
    vector<int> last_pos(26, -1);

    for (int i = n - 1; i >= 0; --i) {

        // Update the last index
        if (last_pos[s[i] - 'a'] == -1) {
            last_pos[s[i] - 'a'] = i;
        }
    }

    int minp = -1, plen = 0;

    // Iterate the given string
    for (int i = 0; i < n; ++i) {

        // Get the last index of s[i]
        int lp = last_pos[s[i] - 'a'];

        // Extend the current partition
        // characters last pos
        minp = max(minp, lp);

        // Increase len of partition
        ++plen;

        // if the current pos of
        // character equals the min pos
        // then the end of partition
        if (i == minp) {

            // Store the length
            ans.push_back(plen);
            minp = -1;
            plen = 0;
        }
    }

    // Print all the partition lengths
    for (int i = 0;
         i < (int)ans.size(); i++) {
        cout << ans[i] << " ";
    }
}

// Driver Code
int main()
{
    // Given string str
    string str = "acbbcc";

    // Function Call
    partitionString(str);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for
// the above approach
import java.util.*;
class GFG{

// Function to find the length of
// all partitions of a String such
// that each characters occurs in
// a single subString
static void partitionString(String s)
{
  int n = s.length();

  // Stores last index of String s
  Vector<Integer> ans =
         new Vector<Integer>();

  if (n == 0)
  {
    System.out.print("-1");
    return;
  }

  // Find the last position of
  // each letter in the String
  int []last_pos = new int[26];
  Arrays.fill(last_pos, -1);

  for (int i = n - 1; i >= 0; --i)
  {
    // Update the last index
    if (last_pos[s.charAt(i) - 'a'] == -1)
    {
      last_pos[s.charAt(i) - 'a'] = i;
    }
  }

  int minp = -1, plen = 0;

  // Iterate the given String
  for (int i = 0; i < n; ++i)
  {
    // Get the last index of s[i]
    int lp = last_pos[s.charAt(i) - 'a'];

    // Extend the current partition
    // characters last pos
    minp = Math.max(minp, lp);

    // Increase len of partition
    ++plen;

    // if the current pos of
    // character equals the min pos
    // then the end of partition
    if (i == minp)
    {
      // Store the length
      ans.add(plen);
      minp = -1;
      plen = 0;
    }
  }

  // Print all the partition lengths
  for (int i = 0; i < (int)ans.size(); i++)
  {
    System.out.print(ans.get(i) + " ");
  }
}

// Driver Code
public static void main(String[] args)
{
  // Given String str
  String str = "acbbcc";

  // Function Call
  partitionString(str);
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the length of
# all partitions of a string such
# that each characters occurs in
# a single substring
def partitionString(s):

    n = len(s)

    # Stores last index of string s
    ans = []

    if (n == 0):
        print("-1")
        return

    # Find the last position of
    # each letter in the string
    last_pos = [-1] * 26

    for i in range(n - 1 , -1 , -1):

        # Update the last index
        if (last_pos[ord(s[i]) - ord('a')] == -1):
            last_pos[ord(s[i]) - ord('a')] = i

    minp = -1
    plen = 0

    # Iterate the given string
    for i in range(n):

        # Get the last index of s[i]
        lp = last_pos[ord(s[i]) - ord('a')]

        # Extend the current partition
        # characters last pos
        minp = max(minp, lp)

        # Increase len of partition
        plen += 1

        # if the current pos of
        # character equals the min pos
        # then the end of partition
        if (i == minp):

            # Store the length
            ans.append(plen)
            minp = -1
            plen = 0

    # Print all the partition lengths
    for i in range(len(ans)):
        print(ans[i], end = " ")

# Driver Code

# Given string str
str = "acbbcc"

# Function call
partitionString(str)

# This code is contributed by code_hunt
```

## C#

```
// C# program for
// the above approach
using System;
using System.Collections.Generic;
class GFG{

// Function to find the length of
// all partitions of a String such
// that each characters occurs in
// a single subString
static void partitionString(String s)
{
  int n = s.Length;

  // Stores last index of String s
  List<int> ans = new List<int>();

  if (n == 0)
  {
    Console.Write("-1");
    return;
  }

  // Find the last position of
  // each letter in the String
  int []last_pos = new int[26];
  for (int i = 0; i < 26; ++i)
  {
    last_pos[i] = -1; 
  }

  for (int i = n - 1; i >= 0; --i)
  {
    // Update the last index
    if (last_pos[s[i] - 'a'] == -1)
    {
      last_pos[s[i] - 'a'] = i;
    }
  }

  int minp = -1, plen = 0;

  // Iterate the given String
  for (int i = 0; i < n; ++i)
  {
    // Get the last index of s[i]
    int lp = last_pos[s[i] - 'a'];

    // Extend the current partition
    // characters last pos
    minp = Math.Max(minp, lp);

    // Increase len of partition
    ++plen;

    // if the current pos of
    // character equals the min pos
    // then the end of partition
    if (i == minp)
    {
      // Store the length
      ans.Add(plen);
      minp = -1;
      plen = 0;
    }
  }

  // Print all the partition lengths
  for (int i = 0; i < (int)ans.Count; i++)
  {
    Console.Write(ans[i] + " ");
  }
}

// Driver Code
public static void Main(String[] args)
{
  // Given String str
  String str = "acbbcc";

  // Function Call
  partitionString(str);
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>
// javascript program for the
// above approach

// Function to find the length of
// all partitions of a String such
// that each characters occurs in
// a single subString
function partitionString(s)
{
  let n = s.length;

  // Stores last index of String s
  let ans = [];

  if (n == 0)
  {
    document.write("-1");
    return;
  }

  // Find the last position of
  // each letter in the String
  let last_pos = Array(26).fill(-1);

  for (let i = n - 1; i >= 0; --i)
  {
    // Update the last index
    if (last_pos[s[i].charCodeAt() - 'a'.charCodeAt()] == -1)
    {
      last_pos[s[i].charCodeAt() - 'a'.charCodeAt()] = i;
    }
  }

  let minp = -1, plen = 0;

  // Iterate the given String
  for (let i = 0; i < n; ++i)
  {
    // Get the last index of s[i]
    let lp = last_pos[s[i].charCodeAt() - 'a'.charCodeAt()];

    // Extend the current partition
    // characters last pos
    minp = Math.max(minp, lp);

    // Increase len of partition
    ++plen;

    // if the current pos of
    // character equals the min pos
    // then the end of partition
    if (i == minp)
    {
      // Store the length
      ans.push(plen);
      minp = -1;
      plen = 0;
    }
  }

  // Print all the partition lengths
  for (let i = 0; i < ans.length; i++)
  {
    document.write(ans[i] + " ");
  }
}

// Driver Code

     // Given String str
  let str = "acbbcc";

  // Function Call
  partitionString(str);

// This code is contributed by avijitmondal1998.
</script>
```

**Output:** 

```
1 5
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)
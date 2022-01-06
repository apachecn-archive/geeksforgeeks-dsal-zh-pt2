# 通过分别串联 N1 时间和 N2 时间

，将 S2 在 S1 的出现次数最大化为一个子序列

> 原文:[https://www . geeksforgeeks . org/通过分别连接-n1-和-N2-次来最大化-S2-in-S1-as-subsequence-time/](https://www.geeksforgeeks.org/maximize-count-of-occurrences-of-s2-in-s1-as-a-subsequence-by-concatenating-n1-and-n2-times-respectively/)

给定两个长度分别为 **N** 和 **M** 的[字符串](https://www.geeksforgeeks.org/string-data-structure/)**S1****S2**，以及两个正整数 **N1** 和 **N2** ，任务是通过串接字符串**S1**找到与 **S2** 相等的 **S1** 的非重叠[子序列](https://www.geeksforgeeks.org/print-subsequences-string/)

**示例:**

> **输入:**S1 =“ACB”，S2 =“ab”，N1 = 4，N2 = 2
> **输出:** 2
> **解释:**
> 串联字符串 S1，N1 ( = 4)次将 S1 修改为“acbacbacbacb”。
> 将字符串 S2、N2 ( = 2)串联起来，将 S2 改为“abab”。
> 由于字符串 S2 在 S1 作为非重叠子序列出现两次，因此所需的输出为 2。
> 
> **输入:**S1 =“ABC”，S2 =“a”，N1 = 1，N2 = 1
> T3】输出: 1

**方法:**这个问题可以用[检查一个字符串是否是另一个字符串的子序列](https://www.geeksforgeeks.org/given-two-strings-find-first-string-subsequence-second/)的概念来解决。
按照以下步骤解决问题:

*   [遍历字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-python/)**【S2】**的字符，检查字符串 **S1** 中是否存在 **S2** 的所有字符。如果发现为假，则不可能有这样的 **S1** 的子序列，通过将字符串 **S1** 、 **N1** 次和字符串 **S2** 、 **N2** 次串联起来，可以使其等于 **S2** 。
*   [循环迭代字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-python/)**【S1】****N1**的字符。对于每一个**I<sup>th</sup>T9】索引，检查 **S1** 到**I<sup>th</sup>T15】索引的子序列是否存在，是否等于 **S2** 。如果发现为真，则增加计数。****
*   最后，在执行上述操作后，将获得的计数除以 **N2** 作为所需答案打印出来。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>

using namespace std;

// Function to count maximum number of
// occurrences of s2 as subsequence in s1
// by concatenating s1, n1 times and s2, n2 times
int getMaxRepetitions(string s1, int n1,
                      string s2, int n2)
{

  int temp1[26] = {0}, temp2[26] = {0};

  for(char i:s1) temp1[i - 'a']++;

  for(char i:s2) temp2[i - 'a']++;

  for(int i = 0; i < 26; i++)
  {
    if(temp2[i] > temp1[i]) return 0;
  }

  // Stores number of times
  // s1 is traversed
  int s1_reps = 0;

  // Stores number of times
  // s2 is traversed
  int s2_reps = 0;

  // Mapping index of s2 to number
  // of times s1 and s2 are traversed
  map<int, pair<int, int> > s2_index_to_reps;
  s2_index_to_reps[0] = {0, 0};

  // Stores index of s1 circularly
  int i = 0;

  // Stores index of s2 circularly
  int j = 0;

  // Traverse the string s1, n1 times
  while (s1_reps < n1){

    // If current character of both
    // the string are equal
    if (s1[i] == s2[j])

      // Update j
      j += 1;

    // Update i
    i += 1;

    // If j is length of s2
    if (j == s2.size())
    {
      // Update j for
      // circular traversal
      j = 0;

      // Update s2_reps
      s2_reps += 1;
    }

    // If i is length of s1
    if (i == s1.size())
    {

      // Update i for
      // circular traversal
      i = 0;

      // Update s1_reps
      s1_reps += 1;

      // If already mapped j
      // to (s1_reps, s2_reps)
      if (s2_index_to_reps.find(j) !=
          s2_index_to_reps.end())
        break;

      // Mapping j to (s1_reps, s2_reps)
      s2_index_to_reps[j] = {s1_reps, s2_reps};
    }
  }

  // If s1 already traversed n1 times
  if (s1_reps == n1)
    return s2_reps / n2;

  // Otherwise, traverse string s1 by multiple of
  // s1_reps and update both s1_reps and s2_reps
  int initial_s1_reps = s2_index_to_reps[j].first ,
  initial_s2_reps = s2_index_to_reps[j].second;
  int loop_s1_reps = s1_reps - initial_s1_reps;
  int loop_s2_reps = s2_reps - initial_s2_reps;
  int loops = (n1 - initial_s1_reps);

  // Update s2_reps
  s2_reps = initial_s2_reps + loops * loop_s2_reps;

  // Update s1_reps
  s1_reps = initial_s1_reps + loops * loop_s1_reps;

  // If s1 is traversed less than n1 times
  while (s1_reps < n1)
  {

    // If current character in both
    // the string are equal
    if (s1[i] == s2[j])

      // Update j
      j += 1;

    // Update i
    i += 1;

    // If i is length of s1
    if (i == s1.size())
    {

      // Update i for circular traversal
      i = 0;

      // Update s1_reps
      s1_reps += 1;
    }

    // If j is length of ss
    if (j == s2.size())
    {

      // Update j for circular traversal
      j = 0;

      // Update s2_reps
      s2_reps += 1;
    }
  }
  return s2_reps / n2;
}

// Driver Code
int main()
{
  string s1 = "acb";
  int n1 = 4;
  string s2 = "ab";
  int n2 = 2;

  cout << (getMaxRepetitions(s1, n1, s2, n2));

  return 0;
}

// This code is contributed by mohit kumar 29.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.lang.*;
import java.util.*;

class GFG{

// Function to count maximum number of
// occurrences of s2 as subsequence in s1
// by concatenating s1, n1 times and s2, n2 times
static int getMaxRepetitions(String s1, int n1,
                             String s2, int n2)
{
    int temp1[] = new int[26], temp2[] = new int[26];

    for(char i : s1.toCharArray())
        temp1[i - 'a']++;

    for(char i : s2.toCharArray())
        temp2[i - 'a']++;

    for(int i = 0; i < 26; i++)
    {
        if (temp2[i] > temp1[i])
            return 0;
    }

    // Stores number of times
    // s1 is traversed
    int s1_reps = 0;

    // Stores number of times
    // s2 is traversed
    int s2_reps = 0;

    // Mapping index of s2 to number
    // of times s1 and s2 are traversed
    HashMap<Integer, int[]> s2_index_to_reps = new HashMap<>();
    s2_index_to_reps.put(0, new int[] { 0, 0 });

    // Stores index of s1 circularly
    int i = 0;

    // Stores index of s2 circularly
    int j = 0;

    // Traverse the string s1, n1 times
    while (s1_reps < n1)
    {

        // If current character of both
        // the string are equal
        if (s1.charAt(i) == s2.charAt(j))

            // Update j
            j += 1;

        // Update i
        i += 1;

        // If j is length of s2
        if (j == s2.length())
        {

            // Update j for
            // circular traversal
            j = 0;

            // Update s2_reps
            s2_reps += 1;
        }

        // If i is length of s1
        if (i == s1.length())
        {

            // Update i for
            // circular traversal
            i = 0;

            // Update s1_reps
            s1_reps += 1;

            // If already mapped j
            // to (s1_reps, s2_reps)
            if (!s2_index_to_reps.containsKey(j))
                break;

            // Mapping j to (s1_reps, s2_reps)
            s2_index_to_reps.put(
                j, new int[] { s1_reps, s2_reps });
        }
    }

    // If s1 already traversed n1 times
    if (s1_reps == n1)
        return s2_reps / n2;

    // Otherwise, traverse string s1 by multiple of
    // s1_reps and update both s1_reps and s2_reps
    int initial_s1_reps = s2_index_to_reps.get(j)[0],
        initial_s2_reps = s2_index_to_reps.get(j)[1];
    int loop_s1_reps = s1_reps - initial_s1_reps;
    int loop_s2_reps = s2_reps - initial_s2_reps;
    int loops = (n1 - initial_s1_reps);

    // Update s2_reps
    s2_reps = initial_s2_reps + loops * loop_s2_reps;

    // Update s1_reps
    s1_reps = initial_s1_reps + loops * loop_s1_reps;

    // If s1 is traversed less than n1 times
    while (s1_reps < n1)
    {

        // If current character in both
        // the string are equal
        if (s1.charAt(i) == s2.charAt(j))

            // Update j
            j += 1;

        // Update i
        i += 1;

        // If i is length of s1
        if (i == s1.length())
        {

            // Update i for circular traversal
            i = 0;

            // Update s1_reps
            s1_reps += 1;
        }

        // If j is length of ss
        if (j == s2.length())
        {

            // Update j for circular traversal
            j = 0;

            // Update s2_reps
            s2_reps += 1;
        }
    }
    return s2_reps / n2;
}

// Driver Code
public static void main(String[] args)
{
    String s1 = "acb";
    int n1 = 4;
    String s2 = "ab";
    int n2 = 2;

    System.out.println(
        getMaxRepetitions(s1, n1, s2, n2));
}
}

// This code is contributed by Kingash
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to count maximum number of
# occurrences of s2 as subsequence in s1
# by concatenating s1, n1 times and s2, n2 times
def getMaxRepetitions(s1, n1, s2, n2):

    # If all the characters of s2 are not present in s1
    if any(c for c in set(s2) if c not in set(s1)):
        return 0

    # Stores number of times
    # s1 is traversed
    s1_reps = 0

    # Stores number of times
    # s2 is traversed
    s2_reps = 0

    # Mapping index of s2 to number
    # of times s1 and s2 are traversed
    s2_index_to_reps = { 0 : (0, 0)}

    # Stores index of s1 circularly
    i = 0

    # Stores index of s2 circularly
    j = 0

    # Traverse the string s1, n1 times
    while s1_reps < n1:

        # If current character of both
        # the string are equal
        if s1[i] == s2[j]:

            # Update j
            j += 1

        # Update i   
        i += 1

        # If j is length of s2
        if j == len(s2):

            # Update j for
            # circular traversal
            j = 0

            # Update s2_reps
            s2_reps += 1

        # If i is length of s1
        if i == len(s1):

            # Update i for
            # circular traversal
            i = 0

            # Update s1_reps
            s1_reps += 1

            # If already mapped j
            # to (s1_reps, s2_reps)
            if j in s2_index_to_reps:
                break

            # Mapping j to (s1_reps, s2_reps)   
            s2_index_to_reps[j] = (s1_reps, s2_reps)

    # If s1 already traversed n1 times
    if s1_reps == n1:
        return s2_reps // n2

    # Otherwise, traverse string s1 by multiple of
    # s1_reps and update both s1_reps and s2_reps

    initial_s1_reps, initial_s2_reps = s2_index_to_reps[j]
    loop_s1_reps = s1_reps - initial_s1_reps
    loop_s2_reps = s2_reps - initial_s2_reps
    loops = (n1 - initial_s1_reps)

    # Update s2_reps
    s2_reps = initial_s2_reps + loops * loop_s2_reps

    # Update s1_reps
    s1_reps = initial_s1_reps + loops * loop_s1_reps

    # If s1 is traversed less than n1 times
    while s1_reps < n1:

        # If current character in both
        # the string are equal
        if s1[i] == s2[j]:

            # Update j
            j += 1

        # Update i   
        i += 1

        # If i is length of s1
        if i == len(s1):

            # Update i for circular traversal
            i = 0

            # Update s1_reps
            s1_reps += 1

        # If j is length of ss
        if j == len(s2):

            # Update j for circular traversal
            j = 0

            # Update s2_reps
            s2_reps += 1

    return s2_reps // n2

# Driver Code
if __name__ == '__main__':
    s1 = "acb"
    n1 = 4
    s2 = "ab"
    n2 = 2

    print(getMaxRepetitions(s1, n1, s2, n2))
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to count maximum number of
// occurrences of s2 as subsequence in s1
// by concatenating s1, n1 times and s2, n2 times
function getMaxRepetitions(s1,n1,s2,n2)
{
    let temp1 = new Array(26);
    let temp2 = new Array(26);

    for(let i = 0; i < 26; i++)
    {
        temp1[i] = 0;
        temp2[i] = 0;
    }

    for(let i = 0; i < s1.split("").length; i++)
        temp1[s1[i].charCodeAt(0) - 'a'.charCodeAt(0)]++;

    for(let i = 0; i < s2.split("").length; i++)
        temp2[s2[i].charCodeAt(0) - 'a'.charCodeAt(0)]++;

    for(let i = 0; i < 26; i++)
    {
        if (temp2[i] > temp1[i])
            return 0;
    }

    // Stores number of times
    // s1 is traversed
    let s1_reps = 0;

    // Stores number of times
    // s2 is traversed
    let s2_reps = 0;

    // Mapping index of s2 to number
    // of times s1 and s2 are traversed
    let s2_index_to_reps = new Map();
    s2_index_to_reps.set(0, [ 0, 0 ]);

    // Stores index of s1 circularly
    let i = 0;

    // Stores index of s2 circularly
    let j = 0;

    // Traverse the string s1, n1 times
    while (s1_reps < n1)
    {

        // If current character of both
        // the string are equal
        if (s1[i] == s2[j])

            // Update j
            j += 1;

        // Update i
        i += 1;

        // If j is length of s2
        if (j == s2.length)
        {

            // Update j for
            // circular traversal
            j = 0;

            // Update s2_reps
            s2_reps += 1;
        }

        // If i is length of s1
        if (i == s1.length)
        {

            // Update i for
            // circular traversal
            i = 0;

            // Update s1_reps
            s1_reps += 1;

            // If already mapped j
            // to (s1_reps, s2_reps)
            if (!s2_index_to_reps.has(j))
                break;

            // Mapping j to (s1_reps, s2_reps)
            s2_index_to_reps.set(
                j, [s1_reps, s2_reps ]);
        }
    }

    // If s1 already traversed n1 times
    if (s1_reps == n1)
        return s2_reps / n2;

    // Otherwise, traverse string s1 by multiple of
    // s1_reps and update both s1_reps and s2_reps
    let initial_s1_reps = s2_index_to_reps.get(j)[0],
        initial_s2_reps = s2_index_to_reps.get(j)[1];
    let loop_s1_reps = s1_reps - initial_s1_reps;
    let loop_s2_reps = s2_reps - initial_s2_reps;
    let loops = (n1 - initial_s1_reps);

    // Update s2_reps
    s2_reps = initial_s2_reps + loops * loop_s2_reps;

    // Update s1_reps
    s1_reps = initial_s1_reps + loops * loop_s1_reps;

    // If s1 is traversed less than n1 times
    while (s1_reps < n1)
    {

        // If current character in both
        // the string are equal
        if (s1[i] == s2[j])

            // Update j
            j += 1;

        // Update i
        i += 1;

        // If i is length of s1
        if (i == s1.length)
        {

            // Update i for circular traversal
            i = 0;

            // Update s1_reps
            s1_reps += 1;
        }

        // If j is length of ss
        if (j == s2.length)
        {

            // Update j for circular traversal
            j = 0;

            // Update s2_reps
            s2_reps += 1;
        }
    }
    return s2_reps / n2;
}

// Driver Code
let s1 = "acb";
let n1 = 4;
let s2 = "ab";
let n2 = 2;
document.write(getMaxRepetitions(s1, n1, s2, n2));

// This code is contributed by unknown2108
</script>
```

**Output:** 

```
2
```

***时间复杂度:** O((N + M) * n1)*
***辅助空间:** O(1)*
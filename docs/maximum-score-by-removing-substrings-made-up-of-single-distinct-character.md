# 通过删除由单个不同字符组成的子串获得的最大得分

> 原文:[https://www . geesforgeks . org/通过移除子字符串获得最大分数-由单个不同字符组成/](https://www.geeksforgeeks.org/maximum-score-by-removing-substrings-made-up-of-single-distinct-character/)

给定一个大小均为 **N** 的[二进制字符串](https://www.geeksforgeeks.org/tag/binary-string/) **S** 和一个[数组](https://www.geeksforgeeks.org/array-data-structure/)**A【】**，任务是通过移除任意长度的[子字符串](https://www.geeksforgeeks.org/substring-in-cpp/)，比如说 **K** ，由相同的字符组成，并将**A【K】**添加到分数中来找到可能的最大分数。

**示例:**

> **输入:**S =【abb】，A =【1，3，1】
> **输出:** 4
> **解释:**
> 最初，得分= 0，S =【abb】
> 去掉子串{S[1]，..S[2]}，长度为 2，并添加 A[2]进行评分。因此，S 修饰为“一”。分数= 3。
> 去掉长度为 1 的子串{S[0]}，加上 A[1]进行评分。因此，S 修饰为" "。分数= 4。
> 
> **输入:**S =【abb】，A =【2，3，1】
> **输出:** 6
> **说明:**
> 最初，得分= 0，S =【abb】。
> 去掉长度为 1 的子串{S[2]}，加上 A[1]进行评分。因此，S 修饰为“ab”。得分= 1
> 去掉长度为 1 的子串{S[1]}，加上 A[1]得分。因此，S 修饰为“一”。Score = 4
> 去掉长度为 1 的子串{S[0]}，加上 A[1]进行评分。因此，S 修饰为" "。分数= 6

**天真的做法:**解决这个问题最简单的思路就是用[递归](https://www.geeksforgeeks.org/recursion/)。[迭代字符串的字符](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/)。如果遇到仅由一个不同字符组成的[子字符串](https://www.geeksforgeeks.org/substring-in-java/)，则继续搜索或删除[子字符串](https://www.geeksforgeeks.org/substring-in-java/)，并递归调用剩余字符串的函数。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check if the string s consists
// of a single distinct character or not
bool isUnique(string s)
{
    set<char> Set;
    for(char c : s)
    {
      Set.insert(c);
    }
    return Set.size() == 1;
}

// Function to calculate the maximum
// score possible by removing substrings
int maxScore(string s, int a[])
{
    int n = s.length();

    // If string is empty
    if (n == 0)
      return 0;

    // If length of string is 1
    if (n == 1)
      return a[0];

    // Store the maximum result
    int mx = -1;

    // Try to remove all substrings that
    // satisfy the condition and check
    // for resultant string after removal
    for (int i = 0; i < n; i++)
    {
      for (int j = i; j < n; j++)
      {

        // Store the substring {s[i], .., s[j]}
        string sub = s.substr(i, j + 1);

        // Check if the substring contains
        // only a single distinct character
        if (isUnique(sub))
          mx = max(mx, a[sub.length() - 1] + maxScore(s.substr(0, i) + s.substr(j + 1), a));
      }
    }

    // Return the maximum score
    return mx;
}

int main()
{
    string s = "011";
    int a[] = { 1, 3, 1 };
    cout << maxScore(s, a)-1;

    return 0;
}

// This code is contributed by mukesh07.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
class GFG
{

  // Function to check if the string s consists
  // of a single distinct character or not
  static boolean isUnique(String s)
  {
    HashSet<Character> set = new HashSet<>();
    for (char c : s.toCharArray())
      set.add(c);
    return set.size() == 1;
  }

  // Function to calculate the maximum
  // score possible by removing substrings
  static int maxScore(String s, int[] a)
  {
    int n = s.length();

    // If string is empty
    if (n == 0)
      return 0;

    // If length of string is 1
    if (n == 1)
      return a[0];

    // Store the maximum result
    int mx = -1;

    // Try to remove all substrings that
    // satisfy the condition and check
    // for resultant string after removal
    for (int i = 0; i < n; i++)
    {
      for (int j = i; j < n; j++)
      {

        // Store the substring {s[i], .., s[j]}
        String sub = s.substring(i, j + 1);

        // Check if the substring contains
        // only a single distinct character
        if (isUnique(sub))
          mx = Math.max(
          mx,
          a[sub.length() - 1]
          + maxScore(
            s.substring(0, i)
            + s.substring(j + 1),
            a));
      }
    }

    // Return the maximum score
    return mx;
  }

  // Driver Code
  public static void main(String args[])
  {
    String s = "011";
    int a[] = { 1, 3, 1 };
    System.out.print(maxScore(s, a));
  }
}

// This code is contributed by hemanth gadarla.
```

## 蟒蛇 3

```
# Python program for the above approach

# Function to check if the string s consists
# of a single distinct character or not
def isUnique(s):
    return True if len(set(s)) == 1 else False

# Function to calculate the maximum
# score possible by removing substrings
def maxScore(s, a):
    n = len(s)

    # If string is empty
    if n == 0:
        return 0

    # If length of string is 1
    if n == 1:
        return a[0]

    # Store the maximum result
    mx = -1

    # Try to remove all substrings that
    # satisfy the condition and check
    # for resultant string after removal
    for i in range(n):
        for j in range(i, n):

            # Store the substring {s[i], .., s[j]}
            sub = s[i:j + 1]

            # Check if the substring contains
            # only a single distinct character
            if isUnique(sub):
                mx = max(mx, a[len(sub)-1]
                         + maxScore(s[:i]+s[j + 1:], a))

        # Return the maximum score
    return mx

# Driver Code
if __name__ == "__main__":

    s = "011"
    a = [1, 3, 1]
    print(maxScore(s, a))
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;
class GFG {

    // Function to check if the string s consists
  // of a single distinct character or not
  static bool isUnique(string s)
  {
    HashSet<char> set = new HashSet<char>();
    foreach(char c in s)
      set.Add(c);
    return set.Count == 1;
  }

  // Function to calculate the maximum
  // score possible by removing substrings
  static int maxScore(string s, int[] a)
  {
    int n = s.Length;

    // If string is empty
    if (n == 0)
      return 0;

    // If length of string is 1
    if (n == 1)
      return a[0];

    // Store the maximum result
    int mx = -1;

    // Try to remove all substrings that
    // satisfy the condition and check
    // for resultant string after removal
    for (int i = 0; i < n; i++)
    {
      for (int j = i; j < n; j++)
      {

        // Store the substring {s[i], .., s[j]}
        string sub = s.Substring(i, j + 1 - i);

        // Check if the substring contains
        // only a single distinct character
        if (isUnique(sub))
          mx = Math.Max(
          mx,
          a[sub.Length - 1]
          + maxScore(
            s.Substring(0, i)
            + s.Substring(j + 1),
            a));
      }
    }

    // Return the maximum score
    return mx;
  }

  // Driver code
  static void Main() {
    string s = "011";
    int[] a = { 1, 3, 1 };
    Console.Write(maxScore(s, a));
  }
}

// This code is contributed by suresh07.
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to check if the string s consists
// of a single distinct character or not
function isUnique( s)
 {
    var set = new Set();
    for(let i = 0 ; i< s.length ; i++)
    {
      set.add(s[i]);
    }
    return set.size == 1;
 }

// Function to calculate the maximum
// score possible by removing substrings
function maxScore( s, a)
{
    let n = s.length;

    // If string is empty
    if (n == 0)
      return 0;

    // If length of string is 1
    if (n == 1)
      return a[0];

    // Store the maximum result
    let mx = -1;

    // Try to remove all substrings that
    // satisfy the condition and check
    // for resultant string after removal
    for (let i = 0; i < n; i++)
    {
      for (let j = i; j < n; j++)
      {

        // Store the substring {s[i], .., s[j]}
        let sub = s.substring(i, j + 1);

        // Check if the substring contains
        // only a single distinct character
        if (isUnique(sub))
          mx = Math.max(
          mx,
          a[sub.length - 1]
          + maxScore(
            s.substring(0, i)
            + s.substring(j + 1),
            a));
      }
    }

    // Return the maximum score
    return mx;
  }

// Driver Code

let s = "011";
let a = [ 1, 3, 1 ];
document.write(maxScore(s, a));

</script>
```

**Output:** 

```
4
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*

**高效方法:**为了优化上述方法，想法是使用[记忆](https://www.geeksforgeeks.org/tabulation-vs-memoization/)存储递归调用的结果，并使用[双指针技术](https://www.geeksforgeeks.org/two-pointers-technique/)存储仅由 1 个不同字符组成的[子串](https://www.geeksforgeeks.org/substring-in-java/)。
按照以下步骤解决问题:

*   声明一个[递归函数](https://www.geeksforgeeks.org/recursive-functions/)，以字符串为输入找到需要的结果。
*   初始化一个数组，说 **dp[]** 记住结果。
    *   如果该值已经存储在数组 **dp[]** 中，则返回结果。
    *   否则，请执行以下步骤:
        *   考虑基本情况，如果弦的[大小为 **0，**返回 **0** 。如果等于 **1** ，则返回**A【1】**。](https://www.geeksforgeeks.org/5-different-methods-find-length-string-c/)
        *   初始化一个变量，比如 **res** ，来存储当前函数调用的结果。
        *   初始化[两个指针](https://www.geeksforgeeks.org/two-pointers-technique/)，说**头**和**尾**，表示子串的开始和结束索引。
        *   [生成满足给定条件的子串](https://www.geeksforgeeks.org/python-get-all-substrings-of-given-string/)，对于每个子串，递归调用剩余串的函数。将最高分存储在 **res** 中。
        *   将结果存储在 **dp[]** 数组中并返回。
    *   打印函数返回的值作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Initialize a dictionary to
// store the precomputed results
map<string,int> dp;

// Function to calculate the maximum
// score possible by removing substrings
int maxScore(string s, vector<int> a)
{

  // If s is present in dp[] array
  if (dp.find(s) != dp.end())
    return dp[s];

  // Base Cases:
  int n = s.size();

  // If length of string is 0
  if (n == 0)
    return 0;

  // If length of string is 1
  if (n == 1)
    return a[0];

  // Put head pointer at start
  int head = 0;

  // Initialize the max variable
  int mx = -1;

  // Generate the substrings
  // using two pointers
  while (head < n)
  {
    int tail = head;
    while (tail < n)
    {

      // If s[head] and s[tail]
      // are different
      if (s[tail] != s[head])
      {

        // Move head to
        // tail and break
        head = tail;
        break;
      }

      // Store the substring
      string sub = s.substr(head, tail + 1);

      // Update the maximum
      mx = max(mx, a[sub.size() - 1] +
               maxScore(s.substr(0, head) +
                        s.substr(tail + 1,s.size()), a));

      // Move the tail
      tail += 1;
    }
    if (tail == n)
      break;
  }

  // Store the score
  dp[s] = mx;
  return mx;
}

// Driver Code
int main()
{
  string s = "abb";
  vector<int> a = {1, 3, 1};
  cout<<(maxScore(s, a)-1);
}

// This code is contributed by mohit kumar 29.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Initialize a dictionary to
// store the precomputed results
static Map<String, Integer> dp = new HashMap<>();

// Function to calculate the maximum
// score possible by removing substrings
static int maxScore(String s, int[] a)
{

    // If s is present in dp[] array
    if (dp.containsKey(s))
        return dp.get(s);

    // Base Cases:
    int n = s.length();

    // If length of string is 0
    if (n == 0)
        return 0;

    // If length of string is 1
    if (n == 1)
        return a[0];

    // Put head pointer at start
    int head = 0;

    // Initialize the max variable
    int mx = -1;

    // Generate the substrings
    // using two pointers
    while (head < n)
    {
        int tail = head;
        while (tail < n)
        {

            // If s[head] and s[tail]
            // are different
            if (s.charAt(tail) != s.charAt(head))
            {

                // Move head to
                // tail and break
                head = tail;
                break;
            }

            // Store the substring
            String sub = s.substring(head, tail + 1);

            // Update the maximum
            mx = Math.max(
                mx, a[sub.length() - 1] +
                maxScore(s.substring(0, head) +
                s.substring(tail + 1, s.length()), a));

            // Move the tail
            tail += 1;
        }
        if (tail == n)
            break;
    }

    // Store the score
    dp.put(s, mx);
    return mx;
}

// Driver code
public static void main(String[] args)
{
    String s = "abb";
    int[] a = { 1, 3, 1 };

    System.out.println((maxScore(s, a)));
}
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python program for the above approach

# Initialize a dictionary to
# store the precomputed results
dp = dict()

# Function to calculate the maximum
# score possible by removing substrings
def maxScore(s, a):

    # If s is present in dp[] array
    if s in dp:
        return dp[s]

    # Base Cases:
    n = len(s)

    # If length of string is 0
    if n == 0:
        return 0

    # If length of string is 1
    if n == 1:
        return a[0]

    # Put head pointer at start
    head = 0

    # Initialize the max variable
    mx = -1

    # Generate the substrings
    # using two pointers
    while head < n:
        tail = head
        while tail < n:

            # If s[head] and s[tail]
            # are different
            if s[tail] != s[head]:

                  # Move head to
                # tail and break
                head = tail
                break

            # Store the substring
            sub = s[head:tail + 1]

            # Update the maximum
            mx = max(mx, a[len(sub)-1]
                     + maxScore(s[:head] + s[tail + 1:], a))

            # Move the tail
            tail += 1
        if tail == n:
            break

    # Store the score
    dp[s] = mx
    return mx

# Driver Code
if __name__ == "__main__":

    s = "abb"
    a = [1, 3, 1]

    print(maxScore(s, a))
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Initialize a dictionary to
// store the precomputed results
static Dictionary<string,
                  int> dp = new Dictionary<string,
                                           int>();

// Function to calculate the maximum
// score possible by removing substrings
static int maxScore(string s, int[] a)
{

    // If s is present in dp[] array
    if (dp.ContainsKey(s))
        return dp[s];

    // Base Cases:
    int n = s.Length;

    // If length of string is 0
    if (n == 0)
        return 0;

    // If length of string is 1
    if (n == 1)
        return a[0];

    // Put head pointer at start
    int head = 0;

    // Initialize the max variable
    int mx = -1;

    // Generate the substrings
    // using two pointers
    while (head < n)
    {
        int tail = head;
        while (tail < n)
        {

            // If s[head] and s[tail]
            // are different
            if (s[tail] != s[head])
            {

                // Move head to
                // tail and break
                head = tail;
                break;
            }

            // Store the substring
            string sub = s.Substring(head, tail + 1-head);

            // Update the maximum
            mx = Math.Max(
                mx, a[sub.Length - 1] +
                maxScore(s.Substring(0, head) +
                s.Substring(tail + 1, s.Length-tail - 1), a));

            // Move the tail
            tail += 1;
        }
        if (tail == n)
            break;
    }

    // Store the score
    dp.Add(s, mx);
    return mx;
}

// Driver code
static public void Main()
{
    string s = "abb";
    int[] a = { 1, 3, 1 };

    Console.WriteLine((maxScore(s, a)));
}
}

// This code is contributed by patel2127
```

## java 描述语言

```
<script>

    // JavaScript program for the above approach

    // Initialize a dictionary to
    // store the precomputed results
    let dp = new Map();

    // Function to calculate the maximum
    // score possible by removing substrings
    function maxScore(s, a)
    {

        // If s is present in dp[] array
        if (dp.has(s))
            return dp.get(s);

        // Base Cases:
        let n = s.length;

        // If length of string is 0
        if (n == 0)
            return 0;

        // If length of string is 1
        if (n == 1)
            return a[0];

        // Put head pointer at start
        let head = 0;

        // Initialize the max variable
        let mx = -1;

        // Generate the substrings
        // using two pointers
        while (head < n)
        {
            let tail = head;
            while (tail < n)
            {

                // If s[head] and s[tail]
                // are different
                if (s[tail] != s[head])
                {

                    // Move head to
                    // tail and break
                    head = tail;
                    break;
                }

                // Store the substring
                let sub = s.substring(head, head + tail + 1);

                // Update the maximum
                mx = Math.max(
                    mx, a[sub.length - 1] +
                    maxScore(s.substring(0, head) +
                    s.substring(tail + 1, tail + 1 + s.length), a));

                // Move the tail
                tail += 1;
            }
            if (tail == n)
                break;
        }

        // Store the score
        dp.set(s, mx);
        return mx;
    }

    let s = "abb";
    let a = [ 1, 3, 1 ];

    document.write((maxScore(s, a))-1);

</script>
```

**Output:** 

```
4
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)
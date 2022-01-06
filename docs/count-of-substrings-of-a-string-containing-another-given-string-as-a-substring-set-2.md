# 包含另一个给定字符串作为子字符串的字符串的子字符串计数|集合 2

> 原文:[https://www . geesforgeks . org/包含另一个给定字符串的字符串子字符串计数集-2/](https://www.geeksforgeeks.org/count-of-substrings-of-a-string-containing-another-given-string-as-a-substring-set-2/)

给定两个长度分别为 **N** 和 **M** 的[字符串](https://www.geeksforgeeks.org/string-data-structure/) **S** 和 **T** ，任务是统计其中包含字符串 **T** 的 **S** 的子字符串数量作为子字符串。

**示例:**

> ***输入:** S = "dabc "，T = "ab"*
> ***输出:** 4*
> ***解释:***
> *包含 T 作为子串的 S 的子串有:*
> 
> 1.  *S[0，2]=“dab”*
> 2.  *S[1，2]=“ab”*
> 3.  *S[1，3]=“ABC”*
> 4.  *S[0，3]=“dabc”*
> 
> ***输入:**S = " hshshshs " T = " hs "*
> T5**输出:** 25

**幼稚的做法:**最简单的解决问题的方法，参考本文[之前的帖子](https://www.geeksforgeeks.org/count-of-substrings-of-a-string-containing-another-given-string-as-a-substring/)。

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(N <sup>2</sup> )*

**高效途径:**优化上述途径，思路是找出 **S** 中 **T** 的所有出现。每当在 **S** 中发现 **T** 时，将包含本次 **T** 的所有子串相加，不包括之前已经计算过的子串。按照以下步骤解决问题:

*   初始化一个变量，说**回答**，存储子串的个数。
*   初始化一个变量，比如说**最后一个**，将 **T** 最后一次出现的起始索引存储在 **S** 中。
*   使用变量迭代范围**【0，N–M】**，比如 **i** 。
    *   检查子串 **S[i，i + M]** 是否等于 **T** 。如果发现为真，则在中加上**(I+1–最后)*(N –( I+M–1))**回答，将**最后的**更新为 **(i + 1)。**
    *   否则，继续下一个迭代。
*   完成以上步骤后，打印**答案**的值作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to count the substrings of
// string containing another given
// string as a substring
void findOccurrences(string S, string T)
{
    // Store length of string S
    int n1 = S.size();

    // Store length of string T
    int n2 = T.size();

    // Store the required count of
    // substrings
    int ans = 0;

    // Store the starting index of
    // last occurence of T in S
    int last = 0;

    // Iterate in range [0, n1-n2]
    for (int i = 0; i <= n1 - n2; i++) {

        // Check if substring from i
        // to i + n2 is equal to T
        bool chk = true;

        // Check if substring from i
        // to i + n2 is equal to T
        for (int j = 0; j < n2; j++) {

            // Mark chk as false and
            // break the loop
            if (T[j] != S[i + j]) {
                chk = false;
                break;
            }
        }

        // If chk is true
        if (chk) {

            // Add (i + 1 - last) *
            // (n1 - (i + n2 - 1))
            // to answer
            ans += (i + 1 - last)
                   * (n1 - (i + n2 - 1));

            // Update the last to i + 1
            last = i + 1;
        }
    }

    // Print the answer
    cout << ans;
}

// Driver code
int main()
{
    string S = "dabc", T = "ab";

    // Function Call
    findOccurrences(S, T);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG{

// Function to count the substrings of
// string containing another given
// string as a substring
static void findOccurrences(String S, String T)
{

    // Store length of string S
    int n1 = S.length();

    // Store length of string T
    int n2 = T.length();

    // Store the required count of
    // substrings
    int ans = 0;

    // Store the starting index of
    // last occurence of T in S
    int last = 0;

    // Iterate in range [0, n1-n2]
    for (int i = 0; i <= n1 - n2; i++)
    {

        // Check if substring from i
        // to i + n2 is equal to T
        boolean chk = true;

        // Check if substring from i
        // to i + n2 is equal to T
        for (int j = 0; j < n2; j++)
        {

            // Mark chk as false and
            // break the loop
            if (T.charAt(j) != S.charAt(i + j))
            {
                chk = false;
                break;
            }
        }

        // If chk is true
        if (chk)
        {

            // Add (i + 1 - last) *
            // (n1 - (i + n2 - 1))
            // to answer
            ans += (i + 1 - last)
                   * (n1 - (i + n2 - 1));

            // Update the last to i + 1
            last = i + 1;
        }
    }

    // Print the answer
    System.out.println(ans);
}

  // Driver code
  public static void main (String[] args)
  {
    String S = "dabc", T = "ab";

    // Function Call
    findOccurrences(S, T);
  }
}

// This code is contributed by AnkThon
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to count the substrings of
# containing another given
# as a sub
def findOccurrences(S, T):

    # Store length of S
    n1 = len(S)

    # Store length of T
    n2 = len(T)

    # Store the required count of
    # substrings
    ans = 0

    # Store the starting index of
    # last occurence of T in S
    last = 0

    # Iterate in range [0, n1-n2]
    for i in range(n1 - n2 + 1):

        # Check if subfrom i
        # to i + n2 is equal to T
        chk = True

        # Check if subfrom i
        # to i + n2 is equal to T
        for j in range(n2):

            # Mark chk as false and
            # break the loop
            if (T[j] != S[i + j]):
                chk = False
                break

        # If chk is true
        if (chk):

            # Add (i + 1 - last) *
            # (n1 - (i + n2 - 1))
            # to answer
            ans += (i + 1 - last) * (n1 - (i + n2 - 1))

            # Update the last to i + 1
            last = i + 1

    # Prthe answer
    print(ans)

# Driver code
if __name__ == '__main__':
    S,T = "dabc","ab"

    # Function Call
    findOccurrences(S, T)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;

class GFG
{

// Function to count the substrings of
// string containing another given
// string as a substring
static void findOccurrences(String S, String T)
{

    // Store length of string S
    int n1 = S.Length;

    // Store length of string T
    int n2 = T.Length;

    // Store the required count of
    // substrings
    int ans = 0;

    // Store the starting index of
    // last occurence of T in S
    int last = 0;

    // Iterate in range [0, n1-n2]
    for (int i = 0; i <= n1 - n2; i++)
    {

        // Check if substring from i
        // to i + n2 is equal to T
        bool chk = true;

        // Check if substring from i
        // to i + n2 is equal to T
        for (int j = 0; j < n2; j++)
        {

            // Mark chk as false and
            // break the loop
            if (T[j] != S[i + j])
            {
                chk = false;
                break;
            }
        }

        // If chk is true
        if (chk)
        {

            // Add (i + 1 - last) *
            // (n1 - (i + n2 - 1))
            // to answer
            ans += (i + 1 - last)
                   * (n1 - (i + n2 - 1));

            // Update the last to i + 1
            last = i + 1;
        }
    }

    // Print the answer
    Console.WriteLine(ans);
}

  // Driver code
  public static void Main(String[] args)
  {
    String S = "dabc", T = "ab";

    // Function Call
    findOccurrences(S, T);
  }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// JavaScript program for above approach

// Function to count the substrings of
// string containing another given
// string as a substring
function findOccurrences(S, T)
{

    // Store length of string S
    let n1 = S.length;

    // Store length of string T
    let n2 = T.length;

    // Store the required count of
    // substrings
    let ans = 0;

    // Store the starting index of
    // last occurence of T in S
    let last = 0;

    // Iterate in range [0, n1-n2]
    for (let i = 0; i <= n1 - n2; i++)
    {

        // Check if substring from i
        // to i + n2 is equal to T
        let chk = true;

        // Check if substring from i
        // to i + n2 is equal to T
        for (let j = 0; j < n2; j++)
        {

            // Mark chk as false and
            // break the loop
            if (T[j] != S[i + j])
            {
                chk = false;
                break;
            }
        }

        // If chk is true
        if (chk)
        {

            // Add (i + 1 - last) *
            // (n1 - (i + n2 - 1))
            // to answer
            ans += (i + 1 - last)
                   * (n1 - (i + n2 - 1));

            // Update the last to i + 1
            last = i + 1;
        }
    }

    // Prlet the answer
    document.write(ans);
}

// Driver Code

     let S = "dabc", T = "ab";

    // Function Call
    findOccurrences(S, T);

</script>
```

**Output:** 

```
4
```

***时间复杂度:** O(N*M)*
***辅助空间:** O(1)*
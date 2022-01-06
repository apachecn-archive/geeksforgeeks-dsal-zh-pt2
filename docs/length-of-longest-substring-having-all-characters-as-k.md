# 所有字符为 K 的最长子串长度

> 原文:[https://www . geesforgeks . org/最长子串长度全字符为-k/](https://www.geeksforgeeks.org/length-of-longest-substring-having-all-characters-as-k/)

给定一个字符串 **S** 和一个字符 **K** 。任务是找到所有字符都与字符 k 相同的 S 的最长子串的长度。

**示例:**

> **输入:**S = " ABCD 1111 AAC "，K = '1'
> **输出:** 4
> **说明:**
> 1111 是长度为 4 的最大子串。
> 
> **输入:** S = "#1234#@@abcd "，K = '@'
> **输出:** 2
> **说明:**
> @@是长度为 2 的最大子串。

**方法:**思想是迭代字符串并检查以下两个条件:

*   如果当前字符与字符 K 相同**，则将计数器的值增加 1。**
*   **如果当前字符与 K 不同，则更新先前的计数并将计数器重新初始化为 0。**
*   **重复以上步骤，直到字符串的长度。**

**下面是上述方法的实现:**

## **C++**

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the length of
// longest sub-string having all
// characters same as character K
int length_substring(string S, char K)
{
    // Initialize variables
    int curr_cnt = 0, prev_cnt = 0, max_len;

    // Iterate till size of string
    for (int i = 0; i < S.size(); i++) {

        // Check if current character is K
        if (S[i] == K) {
            curr_cnt += 1;
        }

        else {
            prev_cnt = max(prev_cnt, curr_cnt);
            curr_cnt = 0;
        }
    }

    prev_cnt = max(prev_cnt, curr_cnt);

    // Assingning the max
    // value to max_len
    max_len = prev_cnt;

    return max_len;
}

// Driver code
int main()
{
    string S = "abcd1111aabc";
    char K = '1';

    // Function call
    cout << length_substring(S, K);
    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java program for
// the above approach
import java.util.*;
class GFG {

// Function to find the length of
// longest sub-string having all
// characters same as character K
static int length_substring(String S,
                            char K)
{
  // Initialize variables
  int curr_cnt = 0, prev_cnt = 0,
      max_len;

  // Iterate till size of string
  for (int i = 0; i < S.length(); i++)
  {
    // Check if current character is K
    if (S.charAt(i) == K)
    {
      curr_cnt += 1;
    }
    else
    {
      prev_cnt = Math.max(prev_cnt,
                          curr_cnt);
      curr_cnt = 0;
    }
  }

  prev_cnt = Math.max(prev_cnt,
                      curr_cnt);

  // Assingning the max
  // value to max_len
  max_len = prev_cnt;

  return max_len;
}

// Driver code
public static void main(String[] args)
{
  String S = "abcd1111aabc";
  char K = '1';

  // Function call
  System.out.print(length_substring(S, K));
}
}

// This code is contributed by Chitranayal
```

## **蟒蛇 3**

```
# Python3 program for the above approach

# Function to find the length of
# longest sub-string having all
# characters same as character K
def length_substring(S, K):

    # Initialize variables
    curr_cnt = 0
    prev_cnt = 0
    max_len = 0

    # Iterate till size of string
    for i in range(len(S)):

        # Check if current character is K
        if (S[i] == K):
            curr_cnt += 1
        else:
            prev_cnt = max(prev_cnt,
                           curr_cnt)
            curr_cnt = 0

    prev_cnt = max(prev_cnt, curr_cnt)

    # Assingning the max
    # value to max_len
    max_len = prev_cnt

    return max_len

# Driver code
if __name__ == '__main__':

    S = "abcd1111aabc"
    K = '1'

    # Function call
    print(length_substring(S, K))

# This code is contributed by mohit kumar 29
```

## **C#**

```
// C# program for the above approach
using System;

class GFG{

// Function to find the length of
// longest sub-string having all
// characters same as character K
static int length_substring(string S, char K)
{

    // Initialize variables
    int curr_cnt = 0, prev_cnt = 0, max_len;

    // Iterate till size of string
    for(int i = 0; i < S.Length; i++)
    {

        // Check if current character is K
        if (S[i] == K)
        {
            curr_cnt += 1;
        }
        else
        {
            prev_cnt = Math.Max(prev_cnt,
                                curr_cnt);
            curr_cnt = 0;
        }
    }
    prev_cnt = Math.Max(prev_cnt, curr_cnt);

    // Assingning the max
    // value to max_len
    max_len = prev_cnt;
    return max_len;
}

// Driver code
static public void Main()
{
    string S = "abcd1111aabc";
    char K = '1';

    // Function call
    Console.WriteLine(length_substring(S, K));
}
}

// This code is contributed by rag2127
```

## **java 描述语言**

```
<script>

// Javascript program for
// the above approach

// Function to find the length of
// longest sub-string having all
// characters same as character K
function length_substring(S, K)
{

    // Initialize variables
    let curr_cnt = 0, prev_cnt = 0,
    max_len;

    // Iterate till size of string
    for(let i = 0; i < S.length; i++)
    {

        // Check if current character is K
        if (S[i] == K)
        {
            curr_cnt += 1;
        }
        else
        {
            prev_cnt = Math.max(prev_cnt,
                                curr_cnt);
            curr_cnt = 0;
        }
    }

    prev_cnt = Math.max(prev_cnt,
                        curr_cnt);

    // Assingning the max
    // value to max_len
    max_len = prev_cnt;

    return max_len;
}

// Driver code
let S = "abcd1111aabc";
let K = '1';

// Function call
document.write(length_substring(S, K));

// This code is contributed by avanitrachhadiya2155

</script>
```

****Output:** 

```
4
```** 

****时间复杂度:**O(N)
T3】辅助空间: O(1)**
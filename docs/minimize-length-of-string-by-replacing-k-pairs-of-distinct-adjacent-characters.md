# 通过替换 K 对不同的相邻字符来最小化字符串的长度

> 原文:[https://www . geeksforgeeks . org/通过替换 k 对不同的相邻字符来最小化字符串长度/](https://www.geeksforgeeks.org/minimize-length-of-string-by-replacing-k-pairs-of-distinct-adjacent-characters/)

给定长度为 **N** 的字符串 **str** ，任务是通过最多用单个字符 **K** 次替换任意一对不相等的相邻字符，找到给定字符串可以减少的最小长度。

**示例:**

> **输入** : str = "aabc "，K =1
> **输出:** 3
> **说明:**
> 将“bc”替换为单个字符“d”，K 减 1。
> 因此，str 修饰为“aad”。
> 由于 K = 0，字符串的最小长度为 3。
> 
> **输入:** str= "aabc "，K = 2
> T3】输出: 2

**天真方法:**最简单的方法是[遍历字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-python/) **K** 次，在每次遍历过程中，检查给定字符串的任意一对相邻字符是否不同。如果发现为真，则用与其相邻字符不相等的单个字符替换这两个字符。最后，打印字符串的最小长度。

***时间复杂度:** O(N * K)*
***辅助空间:** O(1)*

**高效方法:**为了优化上述方法，思路是[遍历给定字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-python/)并检查给定字符串的任意一对相邻字符是否不同。如果发现为真，则打印**最大值(1，(N–K))**的值。否则，打印 **N** 。按照以下步骤解决问题:

1.  [遍历给定的字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-python/) **字符串**，检查相邻字符对是否不同。
2.  如果发现为真，则打印 **max(1，(N–K))**作为所需答案。
3.  否则，打印 **N** 作为所需答案。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to minimize the length
// of the string by replacing distinct
// pairs of adjacent characters
int MinLen(string str, int K)
{
    // Stores the length
    // of the given string
    int N = str.length();

    // Stores the index
    // of the given string
    int i = 0;

    // Traverse the given string
    while (i < N - 1) {

        // If two adjacent
        // characters are distinct
        if (str[i] != str[i + 1]) {
            break;
        }
        i++;
    }

    // If all characters
    // are equal
    if (i == N - 1) {
        return N;
    }

    // If all characters
    // are distinct
    return max(1, N - K);
}

// Driver Code
int main()
{
    string str = "aabc";
    int K = 1;
    cout << MinLen(str, K);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
class GFG{

// Function to minimize the
// length of the String by
// replacing distinct pairs
// of adjacent characters
static int MinLen(String str,
                  int K)
{
  // Stores the length
  // of the given String
  int N = str.length();

  // Stores the index
  // of the given String
  int i = 0;

  // Traverse the given String
  while (i < N - 1)
  {
    // If two adjacent
    // characters are distinct
    if (str.charAt(i) !=
        str.charAt(i + 1))
    {
      break;
    }
    i++;
  }

  // If all characters
  // are equal
  if (i == N - 1)
  {
    return N;
  }

  // If all characters
  // are distinct
  return Math.max(1, N - K);
}

// Driver Code
public static void main(String[] args)
{
  String str = "aabc";
  int K = 1;
  System.out.print(MinLen(str, K));
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to minimize the length
# of the by replacing distinct
# pairs of adjacent characters
def MinLen(str, K):

    # Stores the length
    # of the given string
    N = len(str)

    # Stores the index
    # of the given string
    i = 0

    # Traverse the given string
    while (i < N - 1):

        # If two adjacent
        # haracters are distinct
        if (str[i] != str[i + 1]):
            break

        i += 1

    # If all characters
    # are equal
    if (i == N - 1):
        return N

    # If all characters
    # are distinct
    return max(1, N - K)

# Driver Code
if __name__ == '__main__':

    str = "aabc"
    K = 1

    print(MinLen(str, K))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program to implement
// the above approach
using System;
class GFG{

// Function to minimize the
// length of the String by
// replacing distinct pairs
// of adjacent characters
static int MinLen(String str,
                  int K)
{
  // Stores the length
  // of the given String
  int N = str.Length;

  // Stores the index
  // of the given String
  int i = 0;

  // Traverse the given String
  while (i < N - 1)
  {
    // If two adjacent
    // characters are distinct
    if (str[i] != str[i + 1])
    {
      break;
    }
    i++;
  }

  // If all characters
  // are equal
  if (i == N - 1)
  {
    return N;
  }

  // If all characters
  // are distinct
  return Math.Max(1, N - K);
}

// Driver Code
public static void Main(String[] args)
{
  String str = "aabc";
  int K = 1;
  Console.Write(MinLen(str, K));
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript program to implement
// the above approach   

// Function to minimize the
    // length of the String by
    // replacing distinct pairs
    // of adjacent characters
    function MinLen( str , K)
    {
        // Stores the length
        // of the given String
        var N = str.length;

        // Stores the index
        // of the given String
        var i = 0;

        // Traverse the given String
        while (i < N - 1) {
            // If two adjacent
            // characters are distinct
            if (str.charAt(i) != str.charAt(i + 1))
            {
                break;
            }
            i++;
        }

        // If all characters
        // are equal
        if (i == N - 1) {
            return N;
        }

        // If all characters
        // are distinct
        return Math.max(1, N - K);
    }

    // Driver Code

        var str = "aabc";
        var K = 1;
        document.write(MinLen(str, K));

// This code contributed by gauravrajput1

</script>
```

**Output:** 

```
3
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)
# 找到最多 K 个正常字符的最长子串长度

> 原文:[https://www . geeksforgeeks . org/find-最多 k 个正常字符的最长子字符串长度/](https://www.geeksforgeeks.org/find-length-of-longest-substring-with-at-most-k-normal-characters/)

给定一个由小英文字母组成的**字符串 P** 和一个 **26 位字符串 Q** ，其中 **1 代表特殊字符**， **0 代表 26 个英文字母的普通字符**。任务是找出最多有 K 个正常字符的最长子串的长度。

**示例:**

> **输入:** P =“正常”，Q =“000000000000000000000000000”，K=1
> **输出:** 1
> **说明:**在字符串 Q 中所有字符都正常。
> 因此，我们可以选择长度为 1 的任何子串。
> 
> **输入:** P =“长颈鹿”，Q =“011111001111111111110111111”，K=2
> **输出:** 3
> **说明:**P 中来自 Q 的正常字符为{a，f，g，r}。
> 因此，最多有 2 个正常字符的可能子串是{gir，ira，ffe}。
> 所有子串的最大长度为 3。

**方法:**
为了解决上面提到的问题，我们将使用两个指针的概念。因此，保持子串的左右指针和正常字符的计数。增加右边的索引，直到正常字符数最多为 k。然后用到目前为止遇到的最大长度的子字符串更新答案。递增左索引，递减计数，直到大于 k 为止
下面是上述方法的实现:

## C++

```
// C++ implementation to Find
// length of longest substring
// with at most K normal characters
#include <bits/stdc++.h>
using namespace std;

// Function to find maximum
// length of normal substrings
int maxNormalSubstring(string& P, string& Q,
                       int K, int N)
{

    if (K == 0)
        return 0;

    // keeps count of normal characters
    int count = 0;

    // indexes of substring
    int left = 0, right = 0;

    // maintain length of longest substring
    // with at most K normal characters
    int ans = 0;

    while (right < N) {

        while (right < N && count <= K) {

            // get position of character
            int pos = P[right] - 'a';

            // check if current character is normal
            if (Q[pos] == '0') {

                // check if normal characters
                // count exceeds K
                if (count + 1 > K)

                    break;

                else
                    count++;
            }

            right++;

            // update answer with substring length
            if (count <= K)
                ans = max(ans, right - left);
        }

        while (left < right) {

            // get position of character
            int pos = P[left] - 'a';

            left++;

            // check if character is
            // normal then decrement count
            if (Q[pos] == '0')

                count--;

            if (count < K)
                break;
        }
    }

    return ans;
}

// Driver code
int main()
{
    // initialise the string
    string P = "giraffe", Q = "01111001111111111011111111";

    int K = 2;

    int N = P.length();

    cout << maxNormalSubstring(P, Q, K, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to Find
// length of longest subString
// with at most K normal characters
class GFG{

// Function to find maximum
// length of normal subStrings
static int maxNormalSubString(char []P, char []Q,
                       int K, int N)
{

    if (K == 0)
        return 0;

    // keeps count of normal characters
    int count = 0;

    // indexes of subString
    int left = 0, right = 0;

    // maintain length of longest subString
    // with at most K normal characters
    int ans = 0;

    while (right < N) {

        while (right < N && count <= K) {

            // get position of character
            int pos = P[right] - 'a';

            // check if current character is normal
            if (Q[pos] == '0') {

                // check if normal characters
                // count exceeds K
                if (count + 1 > K)

                    break;

                else
                    count++;
            }

            right++;

            // update answer with subString length
            if (count <= K)
                ans = Math.max(ans, right - left);
        }

        while (left < right) {

            // get position of character
            int pos = P[left] - 'a';

            left++;

            // check if character is
            // normal then decrement count
            if (Q[pos] == '0')

                count--;

            if (count < K)
                break;
        }
    }

    return ans;
}

// Driver code
public static void main(String[] args)
{
    // initialise the String
    String P = "giraffe", Q = "01111001111111111011111111";

    int K = 2;

    int N = P.length();

    System.out.print(maxNormalSubString(P.toCharArray(), Q.toCharArray(), K, N));
}
}

// This code is contributed by Princi Singh
```

## 蟒蛇 3

```
# Function to find maximum
# length of normal substrings
def maxNormalSubstring(P, Q, K, N):

    if (K == 0):
        return 0

    # keeps count of normal characters
    count = 0

    # indexes of substring
    left, right = 0, 0

    # maintain length of longest substring
    # with at most K normal characters
    ans = 0

    while (right < N):

        while (right < N and count <= K):

            # get position of character
            pos = ord(P[right]) - ord('a')

            # check if current character is normal
            if (Q[pos] == '0'):

                # check if normal characters
                # count exceeds K
                if (count + 1 > K):
                    break
                else:
                    count += 1

            right += 1

            # update answer with substring length
            if (count <= K):
                ans = max(ans, right - left)

        while (left < right):

            # get position of character
            pos = ord(P[left]) - ord('a')

            left += 1

            # check if character is
            # normal then decrement count
            if (Q[pos] == '0'):
                count -= 1

            if (count < K):
                break

    return ans

# Driver code
if(__name__ == "__main__"):
    # initialise the string
    P = "giraffe"
    Q = "01111001111111111011111111"

    K = 2

    N = len(P)

    print(maxNormalSubstring(P, Q, K, N))

# This code is contributed by skylags
```

## C#

```
// C# implementation to Find
// length of longest subString
// with at most K normal characters
using System;

public class GFG{

// Function to find maximum
// length of normal subStrings
static int maxNormalSubString(char []P, char []Q,
                    int K, int N)
{

    if (K == 0)
        return 0;

    // keeps count of normal characters
    int count = 0;

    // indexes of subString
    int left = 0, right = 0;

    // maintain length of longest subString
    // with at most K normal characters
    int ans = 0;

    while (right < N) {

        while (right < N && count <= K) {

            // get position of character
            int pos = P[right] - 'a';

            // check if current character is normal
            if (Q[pos] == '0') {

                // check if normal characters
                // count exceeds K
                if (count + 1 > K)

                    break;

                else
                    count++;
            }

            right++;

            // update answer with subString length
            if (count <= K)
                ans = Math.Max(ans, right - left);
        }

        while (left < right) {

            // get position of character
            int pos = P[left] - 'a';

            left++;

            // check if character is
            // normal then decrement count
            if (Q[pos] == '0')

                count--;

            if (count < K)
                break;
        }
    }

    return ans;
}

// Driver code
public static void Main(String[] args)
{
    // initialise the String
    String P = "giraffe", Q = "01111001111111111011111111";

    int K = 2;

    int N = P.Length;

    Console.Write(maxNormalSubString(P.ToCharArray(),
                     Q.ToCharArray(), K, N));
}
}

// This code contributed by Princi Singh
```

## java 描述语言

```
<script>

// Javascript implementation to Find
// length of longest substring
// with at most K normal character

// Function to find maximum
// length of normal substrings
function maxNormalSubstring(P, Q, K, N)
{

    if (K == 0)
        return 0;

    // keeps count of normal characters
    var count = 0;

    // indexes of substring
    var left = 0, right = 0;

    // maintain length of longest substring
    // with at most K normal characters
    var ans = 0;

    while (right < N) {

        while (right < N && count <= K) {

            // get position of character
            var pos = P[right].charCodeAt(0) - 'a'.charCodeAt(0);

            // check if current character is normal
            if (Q[pos] == '0') {

                // check if normal characters
                // count exceeds K
                if (count + 1 > K)

                    break;

                else
                    count++;
            }

            right++;

            // update answer with substring length
            if (count <= K)
                ans = Math.max(ans, right - left);
        }

        while (left < right) {

            // get position of character
            var pos = P[left].charCodeAt(0) - 'a'.charCodeAt(0);

            left++;

            // check if character is
            // normal then decrement count
            if (Q[pos] == '0')
                count--;

            if (count < K)
                break;
        }
    }

    return ans;
}

// Driver code
// initialise the string
var P = "giraffe", Q = "01111001111111111011111111";
var K = 2;
var N = P.length;
document.write( maxNormalSubstring(P, Q, K, N));

</script>
```

**Output:** 

```
3
```

**时间复杂度:**以上方法耗时 O(N)。
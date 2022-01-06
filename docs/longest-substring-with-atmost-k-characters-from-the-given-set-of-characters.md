# 给定字符集中最多 K 个字符的最长子串

> 原文:[https://www . geeksforgeeks . org/给定字符集的最长带-atmat-k-字符子串/](https://www.geeksforgeeks.org/longest-substring-with-atmost-k-characters-from-the-given-set-of-characters/)

给定一个字符串 **S** ，一个整数 **K** 和一组字符 **Q[]** ，任务是从给定的字符集 **Q[]** 中找到包含最多 K 个字符的字符串 **S** 中最长的子字符串。
**举例:**

> **输入:**S =“normal”，Q = {“a”、“o”、“n”、“b”、“r”、“l”}，K = 1
> **输出:** 1
> **说明:**
> 给定字符串 S 中的所有字符都以数组形式出现。
> 因此，我们可以选择长度为 1 的任意子串。
> **输入:** S =“长颈鹿”，Q = {“a”、“f”、“g”、“r”}，K = 2
> **输出:** 3
> **解释:**
> 来自给定集合的具有 atmost 2 字符的可能子串为{“gir”、“ira”、“FFE”}
> 所有子串的最大长度为 3。

**方法:**思路是使用[两个指针](https://www.geeksforgeeks.org/two-pointers-technique/)的概念来考虑最大长度的子串，这样它最多包含给定集合中的 K 个字符。以下是该方法的示例:

*   保持两个指针 ***左*** 和 ***右*** 为 0，以考虑这些指针之间的字符串。
*   增加 ***右侧*** 指针，直到给定集合中的字符最多为 k
*   将最长的子字符串更新为右指针和左指针之间的差值。

```
cur_max = max(cur_max, right - left)
```

*   递增左侧**指针，如果从两个指针移出的字符是给定集合的字符，则将该集合的字符数递减 1。**
*   **同样，重复上述步骤，直到右指针不等于字符串的长度。**

**以下是上述方法的实现:** 

## **C++**

```
// C++ implementation to find the
// longest substring in the string
// which contains atmost K characters
// from the given set of characters

#include <bits/stdc++.h>

using namespace std;

// Function to find the longest
// substring in the string
// which contains atmost K characters
// from the given set of characters
int maxNormalSubstring(string& P,
        set<char> Q, int K, int N)
{

    // Base Condition
    if (K == 0)
        return 0;

    // Count for Characters
    // from set in substring
    int count = 0;

    // Two pointers
    int left = 0, right = 0;
    int ans = 0;

    // Loop to iterate until
    // right pointer is not
    // equal to N
    while (right < N) {

        // Loop to increase the substring
        // length until the characters from
        // set are at most K
        while (right < N && count <= K) {

            // Check if current pointer
            // points a character from set
            if (Q.find(P[right]) != Q.end()){

                // If the count of the
                // char is exceeding the limit
                if (count + 1 > K)
                    break;
                else
                    count++;
            }

            right++;

            // update answer with
            // substring length
            if (count <= K)
                ans = max(ans, right - left);
        }

        // Increment the left pointer until
        // the count is less than or equal to K
        while (left < right) {
            left++;

            // If the character which comes out is normal character
            // then decrement the count by 1
            if (Q.find(P[left-1]) != Q.end())
                count--;

            if (count < K)
                break;
        }
    }

    return ans;
}

// Driver Code
int main()
{
    string P = "giraffe";
    set<char> Q;

    // Construction of set
    Q.insert('a');
    Q.insert('f');
    Q.insert('g');
    Q.insert('r');
    int K = 2;
    int N = P.length();

    // output result
    cout << maxNormalSubstring(P, Q, K, N);

    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java implementation to find the
// longest substring in the string
// which contains atmost K characters
// from the given set of characters
import java.util.*;

class GFG{

// Function to find the longest
// substring in the string
// which contains atmost K characters
// from the given set of characters
static int maxNormalSubstring(String P,
                              Set<Character> Q,
                              int K, int N)
{

    // Base Condition
    if (K == 0)
        return 0;

    // Count for Characters
    // from set in substring
    int count = 0;

    // Two pointers
    int left = 0, right = 0;
    int ans = 0;

    // Loop to iterate until
    // right pointer is not
    // equal to N
    while (right < N)
    {

        // Loop to increase the substring
        // length until the characters from
        // set are at most K
        while (right < N && count <= K)
        {

            // Check if current pointer
            // points a character from set
            if (Q.contains(P.charAt(right)))
            {

                // If the count of the
                // char is exceeding the limit
                if (count + 1 > K)
                    break;
                else
                    count++;
            }
            right++;

            // update answer with
            // substring length
            if (count <= K)
                ans = Math.max(ans, right - left);
        }

        // Increment the left pointer until
        // the count is less than or equal to K
        while (left < right)
        {
            left++;

            // If the character which comes out
            // then decrement the count by 1
            if (Q.contains(P.charAt(left-1)))
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
    String P = "giraffe";
    Set<Character> Q = new HashSet<>();

    // Construction of set
    Q.add('a');
    Q.add('f');
    Q.add('g');
    Q.add('r');

    int K = 2;
    int N = P.length();

    // Output result
    System.out.println(maxNormalSubstring(P, Q,
                                          K, N));
}
}

// This code is contributed by offbeat
```

## **蟒蛇 3**

```
# Python3 implementation to find the
# longest substring in the string
# which contains atmost K characters
# from the given set of characters

# Function to find the longest
# substring in the string
# which contains atmost K characters
# from the given set of characters
def maxNormalSubstring(P, Q, K, N):

    # Base Condition
    if (K == 0):
        return 0

    # Count for Characters
    # from set in substring
    count = 0

    # Two pointers
    left = 0
    right = 0
    ans = 0

    # Loop to iterate until
    # right pointer is not
    # equal to N
    while (right < N):

        # Loop to increase the substring
        # length until the characters from
        # set are at most K
        while (right < N and count <= K):

            # Check if current pointer
            # points a character from set
            if (P[right] in Q):

                # If the count of the
                # char is exceeding the limit
                if (count + 1 > K):
                    break
                else:
                    count += 1

            right += 1

            # update answer with
            # substring length
            if (count <= K):
                ans = max(ans, right - left)

        # Increment the left pointer until
        # the count is less than or equal to K
        while (left < right):
            left += 1

            # If the character which comes out
            # then decrement the count by 1
            if (P[left-1] in Q):
                count -= 1

            if (count < K):
                break

    return ans

# Driver Code
P = "giraffe"
Q = {chr}

# Construction of set
Q.add('a')
Q.add('f')
Q.add('g')
Q.add('r')
K = 2
N = len(P)

# Output result
print(maxNormalSubstring(P, Q, K, N))

# This code is contributed by Sanjit_Prasad
```

****Output:** 

```
3
```** 

****业绩分析:**** 

*   ****时间复杂度:** O(N)**
*   ****辅助空间:** O(1)**
# 通过替换给定字符串的字符以最小的移动形成的字典上最大的字符串

> 原文:[https://www . geeksforgeeks . org/按字典顺序排列的最大字符串通过替换给定字符串中的字符最小移动数/](https://www.geeksforgeeks.org/lexicographically-largest-string-formed-in-minimum-moves-by-replacing-characters-of-given-string/)

给定由 **N** 个小写英文字符组成的[字符串](https://www.geeksforgeeks.org/string-data-structure/) **S** ，任务是通过将字符串 **S** 替换为任意小写英文字母一次，将字符串**S**修改为包含第一个 **min(N，26)** 个小写英文字母的字符串，从而按字典顺序打印最大的字符串。

**示例:**

> **输入:** N = 9，S =“abceffh”
> **输出:**abceffhd
> **解释:**
> 将 S[2](= 'c ')替换为“I”，将 S[7]( = 'h ')替换为“d”，字符串修改为“abceffhd”，这是在最少 2 个移动中可能出现的最大词汇量。
> 
> **输入:** N = 5，S = " abbb "
> **输出:** aedcb
> **解释:**
> 将 S[1](= 'b ')替换为‘e’，S[2](= 'b ')替换为‘d’，S[3](= 'b ')替换为‘c’，字符串修改为“aedcb”，这是最少 3 个移动中可能出现的最大的字典值。

**方法:**给定的问题可以通过用需要插入到字符串中的最大字符替换重复的或不应该是字符串一部分的字符来解决，直到字符串不包含所有需要的字符。按照以下步骤解决问题:

*   初始化一个 [hashmap](https://www.geeksforgeeks.org/how-to-create-an-unordered_map-of-pairs-in-c/) ，说 **M** ，[将字符串 **S** 的每个字符的频率存储在**M**T9】中。](https://www.geeksforgeeks.org/frequency-of-each-character-in-a-string-using-unordered_map-in-c/)
*   初始化一个字符[数组](https://www.geeksforgeeks.org/array-data-structure/)，说 **V** 来存储字符串中不存在的[字符。](https://www.geeksforgeeks.org/find-uncommon-characters-two-strings/)
*   [从**‘a’**开始迭代第一个 min( **N，26)** 字符](https://www.geeksforgeeks.org/c-c-while-loop-with-examples/)，如果当前字符不在 **M** 中，则将当前字符推至 **V、**。
*   初始化一个变量， **j** 指向数组的最后一个元素。
*   [使用变量 **i** 遍历给定的字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/)、 **S** ，并执行以下步骤:
    *   如果**S【I】>V【j】**那么[继续](https://www.geeksforgeeks.org/continue-statement-cpp/)。
    *   如果 **M[S[i]] > 1** 或**S[I]≥“a”+min(N，26)** ，则执行以下操作:
        *   将 **1** 减去**M【S[I]】**，将 **S** 中的**S【I】**替换为**V【j】**。
        *   将 **j** 的值减少 **1** 。
    *   如果 **j** 小于 **0** ，则断开。
*   初始化两个变量，说 **r** 为 **N-1** 和 **l** 为 **0** 。
*   当 **r** 大于 **0** 且 **l** 小于或等于 **j** 时迭代，并执行以下步骤:
    *   如果 **M[S[r]] > 1** 或 **S[r] ≥ 'a'+min(N，26)** ，则执行以下操作:
        *   将 **1** 减去**M【S[r]】**，将 **S** 中的**S【r】**替换为**V【l】**。
        *   将 **l** 的值增加 **1** 。
    *   将 **r** 减少 **1。**
*   最后，完成以上步骤后，[打印字符串，结果为](https://www.geeksforgeeks.org/strings-in-c-2/) **S** 。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to print the lexicographically
// the largest string obtained in process
// of obtaining a string containing first
// N lower case english alphabtes
string lexicographicallyMaximum(string S, int N)
{

    // Store the frequency of each
    // character
    unordered_map<char, int> M;

    // Traverse the string S
    for (int i = 0; i < N; ++i) {
        M[S[i]]++;
    }

    // Stores the characters which are
    // not appearing in S
    vector<char> V;

    for (char i = 'a'; i < (char)('a' + min(N, 25)); ++i) {
        if (M[i] == 0) {
            V.push_back(i);
        }
    }

    // Stores the index of the largest
    // character in the array V, that
    // need to be replaced
    int j = V.size() - 1;

    // Traverse the string, S
    for (int i = 0; i < N; ++i) {

        // If frequency of S[i] is greater
        // than 1 or it is outside the range
        if (S[i] >= ('a' + min(N, 25)) || M[S[i]] > 1) {

            if (V[j] < S[i])
                continue;

            // Decrement its frequency by
            // 1
            M[S[i]]--;

            // Update S[i]
            S[i] = V[j];

            // Decrement j by 1
            j--;
        }

        if (j < 0)
            break;
    }

    int l = 0;
    // Traverse the string, S
    for (int i = N - 1; i >= 0; i--) {
        if (l > j)
            break;

        if (S[i] >= ('a' + min(N, 25)) || M[S[i]] > 1) {

            // Decrement its frequency by
            // 1
            M[S[i]]--;

            // Update S[i]
            S[i] = V[l];

            // increment l by 1
            l++;
        }
    }
    // Return S
    return S;
}

// Driver Code
int main()
{
    // Given Input
    string S = "abccefghh";
    int N = S.length();

    // Function Call
    cout << lexicographicallyMaximum(S, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
public class Main
{
    // Function to print the lexicographically
    // the largest string obtained in process
    // of obtaining a string containing first
    // N lower case english alphabtes
    static String lexicographicallyMaximum(String S, int N)
    {
        // Store the frequency of each
        // character
        HashMap<Character, Integer> M = new HashMap<>();

        // Traverse the string S
        for(int i = 0; i < N; ++i)
        {
            if (M.containsKey(S.charAt(i)))
               M.put(S.charAt(i), M.get(S.charAt(i)) + 1);
            else
                M.put(S.charAt(i), 1);
        }

        // Stores the characters which are
        // not appearing in S
        Vector<Character> V = new Vector<Character>();

        for(char i = 'a';
                 i < (char)('a' + Math.min(N, 25)); ++i)
        {
            if (M.containsKey(i) == false)
            {
                V.add(i);
            }
        }

        // Stores the index of the largest
        // character in the array V, that
        // need to be replaced
        int j = V.size() - 1;

        // Traverse the string, S
        for(int i = 0; i < N; ++i)
        {

            // If frequency of S[i] is greater
            // than 1 or it is outside the range
            if (S.charAt(i) >= ('a' + Math.min(N, 25)) ||
               (M.containsKey(S.charAt(i)) &&  M.get(S.charAt(i)) > 1))
            {
                if (V.get(j) < S.charAt(i))
                    continue;

                // Decrement its frequency by
                // 1
                M.put(S.charAt(i), M.get(S.charAt(i)) - 1);

                // Update S[i]
                S = S.substring(0, i) + V.get(j) + S.substring(i + 1);

                // Decrement j by 1
                j--;
            }
            if (j < 0)
                break;
        }
        int l = 0;

        // Traverse the string, S
        for(int i = N - 1; i >= 0; i--)
        {
            if (l > j)
                break;

            if (S.charAt(i) >=  ('a' + Math.min(N, 25)) ||
                M.containsKey(S.charAt(i)) && M.get(S.charAt(i)) > 1)
            {

                // Decrement its frequency by
                // 1
                M.put(S.charAt(i), M.get(S.charAt(i)) - 1);

                // Update S[i]
                S = S.substring(0, i) + V.get(l) + S.substring(i + 1);

                // Increment l by 1
                l++;
            }
        }

        // Return S
        return S;
    }

    public static void main(String[] args)
    {

        // Given Input
        String S = "abccefghh";
        int N = S.length();

        // Function Call
        System.out.println(lexicographicallyMaximum(S, N));
    }
}

// This code is contributed by mukesh07.
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to print the lexicographically
# the largest string obtained in process
# of obtaining a string containing first
# N lower case english alphabtes
def lexicographicallyMaximum(S, N):

    # Store the frequency of each
    # character
    M = {}

    # Traverse the string S
    for i in range(N):
        if S[i] in M:
           M[S[i]] += 1
        else:
            M[S[i]] = 1

    # Stores the characters which are
    # not appearing in S
    V = []

    for i in range(ord('a'), ord('a') + min(N, 25)):
        if i not in M:
            V.append(chr(i))

    # Stores the index of the largest
    # character in the array V, that
    # need to be replaced
    j = len(V) - 1

    # Traverse the string, S
    for i in range(N):

        # If frequency of S[i] is greater
        # than 1 or it is outside the range
        if (ord(S[i]) >= (ord('a') + min(N, 25)) or
           (S[i] in M and  M[S[i]] > 1)):
            if (ord(V[j]) < ord(S[i])):
                continue

            # Decrement its frequency by
            # 1
            M[S[i]] -= 1

            # Update S[i]
            S = S[0:i] + V[j] + S[(i + 1):]

            # Decrement j by 1
            j -= 1

        if (j < 0):
            break

    l = 0

    # Traverse the string, S
    for i in range(N - 1, -1, -1):
        if (l > j):
            break

        if (ord(S[i]) >= (ord('a') + min(N, 25)) or
            S[i] in M and M[S[i]] > 1):

            # Decrement its frequency by
            # 1
            M[S[i]] -= 1

            # Update S[i]
            S = S[0:i] + V[l] + S[(i + 1):]

            # Increment l by 1
            l += 1

    s = list(S)
    s[len(s) - 1] = 'd'
    S = "".join(s)

    # Return S
    return S

# Driver code

# Given Input
S = "abccefghh"
N = len(S)

# Function Call
print(lexicographicallyMaximum(S, N))

# This code is contributed by rameshtravel07
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to print the lexicographically
// the largest string obtained in process
// of obtaining a string containing first
// N lower case english alphabtes
static string lexicographicallyMaximum(string S, int N)
{

    // Store the frequency of each
    // character
    Dictionary<char,
               int> M = new Dictionary<char,
                                       int>();

    // Traverse the string S
    for(int i = 0; i < N; ++i)
    {
        if (M.ContainsKey(S[i]))
           M[S[i]]++;
        else
            M.Add(S[i], 1);
    }

    // Stores the characters which are
    // not appearing in S
    List<char> V = new List<char>();

    for(char i = 'a';
             i < (char)('a' + Math.Min(N, 25)); ++i)
    {
        if (M.ContainsKey(i) == false)
        {
            V.Add(i);
        }
    }

    // Stores the index of the largest
    // character in the array V, that
    // need to be replaced
    int j = V.Count - 1;

    // Traverse the string, S
    for(int i = 0; i < N; ++i)
    {

        // If frequency of S[i] is greater
        // than 1 or it is outside the range
        if (S[i] >= ('a' + Math.Min(N, 25)) ||
           (M.ContainsKey(S[i]) &&  M[S[i]] > 1))
        {
            if (V[j] < S[i])
                continue;

            // Decrement its frequency by
            // 1
            M[S[i]]--;

            // Update S[i]
            S = S.Substring(0, i) + V[j] +
                S.Substring(i + 1);

            // Decrement j by 1
            j--;
        }
        if (j < 0)
            break;
    }
    int l = 0;

    // Traverse the string, S
    for(int i = N - 1; i >= 0; i--)
    {
        if (l > j)
            break;

        if (S[i] >=  ('a' + Math.Min(N, 25)) ||
            M.ContainsKey(S[i]) && M[S[i]] > 1)
        {

            // Decrement its frequency by
            // 1
            M[S[i]]--;

            // Update S[i]
            S = S.Substring(0, i) + V[l] +
                S.Substring(i + 1);

            // Increment l by 1
            l++;
        }
    }

    // Return S
    return S;
}

// Driver Code
public static void Main()
{

    // Given Input
    string S = "abccefghh";
    int N = S.Length;

    // Function Call
    Console.Write(lexicographicallyMaximum(S, N));
}
}

// This code is contributed by bgangwar59
```

## java 描述语言

```
<script>
    // Javascript program for the above approach

    // Function to print the lexicographically
    // the largest string obtained in process
    // of obtaining a string containing first
    // N lower case english alphabtes
    function lexicographicallyMaximum(S, N)
    {

        // Store the frequency of each
        // character
        let M = new Map();

        // Traverse the string S
        for(let i = 0; i < N; ++i)
        {
            if (M.has(S[i]))
               M.set(S[i], M.get(S[i]) + 1);
            else
                M.set(S[i], 1);
        }

        // Stores the characters which are
        // not appearing in S
        let V = [];

        for(let i = 'a'.charCodeAt();
                 i < ('a'.charCodeAt() + Math.min(N, 25)); ++i)
        {
            if (M.has(String.fromCharCode(i)) == false)
            {
                V.push(String.fromCharCode(i));
            }
        }

        // Stores the index of the largest
        // character in the array V, that
        // need to be replaced
        let j = V.length - 1;

        // Traverse the string, S
        for(let i = 0; i < N; ++i)
        {

            // If frequency of S[i] is greater
            // than 1 or it is outside the range
            if (S[i].charCodeAt() >= ('a'.charCodeAt() + Math.min(N, 25)) ||
               (M.has(S[i]) &&  M.get(S[i]) > 1))
            {
                if (V[j].charCodeAt() < S[i].charCodeAt())
                    continue;

                // Decrement its frequency by
                // 1
                M.set(S[i], M.get(S[i])-1);

                // Update S[i]
                S = S.substr(0, i) + V[j] +
                    S.substr(i + 1);

                // Decrement j by 1
                j--;
            }
            if (j < 0)
                break;
        }
        let l = 0;

        // Traverse the string, S
        for(let i = N - 1; i >= 0; i--)
        {
            if (l > j)
                break;

            if (S[i].charCodeAt() >=  ('a'.charCodeAt() + Math.min(N, 25)) ||
                M.has(S[i]) && M.get(S[i]) > 1)
            {

                // Decrement its frequency by
                // 1
                M.set(S[i], M.get(S[i])-1);

                // Update S[i]
                S = S.substr(0, i) + V[l] +
                    S.substr(i + 1);

                // Increment l by 1
                l++;
            }
        }

        // Return S
        return S;
    }

    // Given Input
    let S = "abccefghh";
    let N = S.length;

    // Function Call
    document.write(lexicographicallyMaximum(S, N));

  // This code is contributed by divyeshrabadiya07.
</script>
```

**Output**

```
abicefghd
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)
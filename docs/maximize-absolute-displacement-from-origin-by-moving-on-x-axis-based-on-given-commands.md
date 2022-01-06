# 根据给定的命令通过在 X 轴上移动最大化相对于原点的绝对位移

> 原文:[https://www . geesforgeks . org/通过基于给定命令在 x 轴上移动来最大化从原点的绝对位移/](https://www.geeksforgeeks.org/maximize-absolute-displacement-from-origin-by-moving-on-x-axis-based-on-given-commands/)

给定一个长度为 **N、**的[字符串](https://www.geeksforgeeks.org/string-data-structure/) **S** ，其中字符串的每个字符等于**【L】【R】**或**，任务是从原点 **(0，0)** 开始，按照 X 轴上给定的命令移动，找到相对于原点的最大绝对位移:**

*   ****‘L’:**在负 X 方向移动一个单位。**
*   ****‘R’:**向正 X 方向移动一个单位。**
*   ****'？':**可以在负 X 或正 X 方向移动一个单位。**

****示例:****

> ****输入:**S =“LL？？R"
> **输出:** 3
> **解释:**
> 可能的移动方式之一是:**
> 
> 1.  **S[0] = 'L '，在-ve X 方向移动一个单位，这样位移就等于-1。**
> 2.  **S[1] = 'L '，在-ve X 方向移动一个单位，这样位移就等于-2。**
> 3.  **S[2] = '？'，在-ve X 方向移动一个单位，所以位移等于-3。**
> 4.  **S[3] = '？'，在-ve X 方向移动一个单位，所以位移等于-4。**
> 5.  **S[4] = 'R '，在+ve X 方向移动一个单位，这样位移就等于-3。**
> 
> **因此，绝对位移为 abs(-3)=3，也是可能的最大绝对位移。**
> 
>  ****输入:** S =？RRR？”
> T3】输出: 5**

****天真的方法:**解决问题最简单的方法就是尝试替换**“？”**用**【L】**或**【R】**使用[递归](https://www.geeksforgeeks.org/recursion/)然后打印得到的最大绝对位移。**

**下面是上述方法的实现:**

## **C++**

```
// C++ program for the above approach
#include <iostream>
using namespace std;
// Recursive function to find the maximum
// absolute displacement from origin by
// performing the given set of moves
int DistRecursion(string S, int i, int dist)
{
    // If i is equal to N
    if (i == S.length())
        return abs(dist);

    // If S[i] is equal to 'L'
    if (S[i] == 'L')
        return DistRecursion(S, i + 1, dist - 1);

    // If S[i] is equal to 'R'
    if (S[i] == 'R')
        return DistRecursion(S, i + 1, dist + 1);

    // If S[i] is equal to '?'
    return max(DistRecursion(S, i + 1, dist - 1),
               DistRecursion(S, i + 1, dist + 1));
}
// Function to find the maximum absolute
// displacement from the origin

int maxDistance(string S)
{

    // Return the maximum absolute
    // displacement
    return DistRecursion(S, 0, 0);
}

// Driver Code
int main()
{
    // Input
    string S = "?RRR?";

    // Function call

    cout << maxDistance(S);
    return 0;
}

// This code is contributed by lokesh potta.
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java program for the above approach
import java.util.*;
class GFG {

    // Recursive function to find the maximum
    // absolute displacement from origin by
    // performing the given set of moves
    static int DistRecursion(String S, int i, int dist)
    {
        char[] ch = S.toCharArray();
        // If i is equal to N
        if (i == ch.length)
            return Math.abs(dist);

        // If S[i] is equal to 'L'
        if (ch[i] == 'L')
            return DistRecursion(S, i + 1, dist - 1);

        // If S[i] is equal to 'R'
        if (ch[i] == 'R')
            return DistRecursion(S, i + 1, dist + 1);

        // If S[i] is equal to '?'
        return Math.max(DistRecursion(S, i + 1,

                                      dist - 1),
                        DistRecursion(S, i + 1, dist + 1));
    }

    // Function to find the maximum absolute
    // displacement from the origin
    static int maxDistance(String S)
    {

        // Return the maximum absolute
        // displacement
        return DistRecursion(S, 0, 0);
    }

    // Driver Code
    public static void main(String[] args)
    {

        // Input
        String S = "?RRR?";

        // Function call
        System.out.print(maxDistance(S));
    }
}

// This code is contributed by ukasp.
```

## **蟒蛇 3**

```
# Python3 program for the above approach

# Recursive function to find the maximum
# absolute displacement from origin by
# performing the given set of moves

def DistRecursion(S, i, dist):

    # If i is equal to N
    if i == len(S):
        return abs(dist)

    # If S[i] is equal to 'L'
    if S[i] == 'L':
        return DistRecursion(S, i + 1, dist-1)

    # If S[i] is equal to 'R'
    if S[i] == 'R':
        return DistRecursion(S, i + 1, dist + 1)

    # If S[i] is equal to '?'
    return max(DistRecursion(S, i + 1, dist-1),
               DistRecursion(S, i + 1, dist + 1))

# Function to find the maximum absolute
# displacement from the origin
def maxDistance(S):

    # Return the maximum absolute
    # displacement
    return DistRecursion(S, 0, 0)

# Driver Code

# Input
S = "?RRR?"

# Function call
print(maxDistance(S))
```

## **C#**

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Recursive function to find the maximum
// absolute displacement from origin by
// performing the given set of moves
static int DistRecursion(string S, int i, int dist)
{

    // If i is equal to N
    if (i == S.Length)
        return Math.Abs(dist);

    // If S[i] is equal to 'L'
    if (S[i] == 'L')
        return DistRecursion(S, i + 1, dist - 1);

    // If S[i] is equal to 'R'
    if (S[i] == 'R')
        return DistRecursion(S, i + 1, dist + 1);

    // If S[i] is equal to '?'
    return Math.Max(DistRecursion(S, i + 1,

                                  dist - 1),
                    DistRecursion(S, i + 1, dist + 1));
}

// Function to find the maximum absolute
// displacement from the origin
static int maxDistance(string S)
{

    // Return the maximum absolute
    // displacement
    return DistRecursion(S, 0, 0);
}

// Driver Code
public static void Main()
{

    // Input
    string S = "?RRR?";

    // Function call
    Console.Write(maxDistance(S));
}
}

// This code is contributed by SURENDRA_GANGWAR
```

## **java 描述语言**

```
<script>

// JavaScript program for the above approach

// Recursive function to find the maximum
// absolute displacement from origin by
// performing the given set of moves
function DistRecursion(S, i, dist) {
    // If i is equal to N
    if (i == S.length)
        return Math.abs(dist);

    // If S[i] is equal to 'L'
    if (S[i] == 'L')
        return DistRecursion(S, i + 1, dist - 1);

    // If S[i] is equal to 'R'
    if (S[i] == 'R')
        return DistRecursion(S, i + 1, dist + 1);

    // If S[i] is equal to '?'
    return Math.max(DistRecursion(S, i + 1, dist - 1),
        DistRecursion(S, i + 1, dist + 1));
}
// Function to find the maximum absolute
// displacement from the origin

function maxDistance(S) {

    // Return the maximum absolute
    // displacement
    return DistRecursion(S, 0, 0);
}

// Driver Code

// Input
let S = "?RRR?";

// Function call

document.write(maxDistance(S));

// This code is contributed by _saurabh_jaiswal

</script>
```

****Output**

```
5
```** 

*****时间复杂度:**O(2<sup>N</sup>)*
***辅助空间:** O(1)***

****有效方法:**上述方法可以基于观察到当**“？”时将获得最大绝对位移来优化**替换为[最大出现字符](https://www.geeksforgeeks.org/return-maximum-occurring-character-in-the-input-string/)。按照以下步骤解决问题:**

*   **[在 **S** 中找到字符](https://www.geeksforgeeks.org/python-count-occurrences-of-a-character-in-string/)**【L】**的计数，并将其存储在变量 say **l** 中。**
*   **[在 **S** 中找到字符](https://www.geeksforgeeks.org/python-count-occurrences-of-a-character-in-string/)**【R】**的计数，并将其存储在一个变量中，比如 **r** 。**
*   **将答案打印为**N–min(l，r)****

**下面是上述方法的实现:**

## **C++**

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

int count(string s, char c) {
    int ans = 0;
    for(int i = 0; i < s.length(); i++)
    {
        if (c == s[i])
        {
            ans++;
        }
    }
    return ans;
}

// Function to find the maximum absolute
// displacement from the origin
int maxDistance(string S) {

    // Stores the count of 'L'
    int l = count(S, 'L');

    // Stores the count of 'R'
    int r = count(S, 'R');

    // Stores the length of S
    int N = S.length();

    // Return the answer
    return abs(N - min(l, r));
}

int main()
{
    // Input
    string S = "?RRR?";

    // Function call
    cout << maxDistance(S);

    return 0;
}

// This code is contributed by divyesh072019.
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java program for the above approach

// Function to find the maximum absolute
// displacement from the origin
class GFG {
    static int maxDistance(String S) {

        // Stores the count of 'L'
        int l = count(S, 'L');

        // Stores the count of 'R'
        int r = count(S, 'R');

        // Stores the length of S
        int N = S.length();

        // Return the answer
        return Math.abs(N - Math.min(l, r));

    }

    private static int count(String s, char c) {
        int ans = 0;
        for (char i : s.toCharArray())
            if (c == i)
                ans++;
        return ans;
    }

    // Driver Code
    public static void main(String[] args) {

        // Input
        String S = "?RRR?";

        // Function call
        System.out.println(maxDistance(S));
    }
}

// This code is contributed by 29AjayKumar
```

## **蟒蛇 3**

```
# Python program for the above approach

# Function to find the maximum absolute
# displacement from the origin

def maxDistance(S):

    # Stores the count of 'L'
    l = S.count('L')

    # Stores the count of 'R'
    r = S.count('R')

    # Stores the length of S
    N = len(S)

    # Return the answer
    return abs(N - min(l, r))

# Driver Code

# Input
S = "?RRR?"

# Function call
print(maxDistance(S))
```

## **C#**

```
// C# program for the above approach

// Function to find the maximum absolute
// displacement from the origin
using System; 

public class GFG {
    static int maxDistance(String S) {

        // Stores the count of 'L'
        int l = count(S, 'L');

        // Stores the count of 'R'
        int r = count(S, 'R');

        // Stores the length of S
        int N = S.Length;

        // Return the answer
        return Math.Abs(N - Math.Min(l, r));

    }

    private static int count(String s, char c) {
        int ans = 0;
        foreach (char i in s.ToCharArray())
            if (c == i)
                ans=ans+1;
        return ans;
    }

    // Driver Code
    public static void Main(String[] args) {

        // Input
        String S = "?RRR?";

        // Function call
        Console.WriteLine(maxDistance(S));
    }
}

// This code is contributed by 29AjayKumar
```

## **java 描述语言**

```
<script>
// javascript program for the above approach

// Function to find the maximum absolute
// displacement from the origin
    function maxDistance(S)
    {

        // Stores the count of 'L'
        var l = count(S, 'L');

        // Stores the count of 'R'
        var r = count(S, 'R');

        // Stores the length of S
        var N = S.length;

        // Return the answer
        return Math.abs(N - Math.min(l, r));

    }

    function count(s, c) {
        var ans = 0;
        for (var i in s.split(''))
            if (c == i)
                ans++;
        return ans;
    }

// Driver Code

// Input
var S = "?RRR?";

// Function call
document.write(maxDistance(S));

// This code is contributed by 29AjayKumar
</script>
```

****Output**

```
5
```** 

*****时间复杂度:**O(N)*
T5**辅助空间:** O(1)**
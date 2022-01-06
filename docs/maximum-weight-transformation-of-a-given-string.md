# 给定字符串的最大权重变换

> 原文:[https://www . geesforgeks . org/给定字符串的最大权重转换/](https://www.geeksforgeeks.org/maximum-weight-transformation-of-a-given-string/)

给定一个仅由 A 和 B 组成的字符串。我们可以通过切换任意字符将给定的字符串转换成另一个字符串。因此，给定字符串的许多转换都是可能的。任务是找到最大权重变换的权重。

使用以下公式计算字符串的权重。

```
Weight of string = Weight of total pairs + 
                   weight of single characters - 
                   Total number of toggles.

Two consecutive characters are considered as pair only if they 
are different. 
Weight of a single pair (both character are different) = 4
Weight of a single character = 1 
```

**示例:**

```
Input: str = "AA"
Output: 3
Transformations of given string are "AA", "AB", "BA" and "BB". 
Maximum weight transformation is "AB" or "BA".  And weight
is "One Pair - One Toggle" = 4-1 = 3.

Input: str = "ABB"
Output: 5
Transformations are "ABB", "ABA", "AAB", "AAA", "BBB", 
"BBA", "BAB" and "BAA"
Maximum weight is of original string 4+1 (One Pair + 1
character)
```

```
If (n == 1)
   maxWeight(str[0..n-1]) = 1

Else If str[0] != str[1]
// Max of two cases: First character considered separately
//                   First pair considered separately 
maxWeight(str[0..n-1]) = Max (1 + maxWeight(str[1..n-1]),
                              4 + getMaxRec(str[2..n-1])
Else
// Max of two cases: First character considered separately
//                   First pair considered separately 
// Since first two characters are same and a toggle is 
// required to form a pair, 3 is added for pair instead 
// of 4         
maxWeight(str[0..n-1]) = Max (1 + maxWeight(str[1..n-1]),
                              3 + getMaxRec(str[2..n-1])
```

如果我们画出完整的递归树，我们可以观察到许多子问题被一次又一次地解决。由于相同的子问题被再次调用，这个问题具有重叠子问题的性质。所以最小二乘和问题同时具有动态规划问题的两个性质(见[这个](https://www.geeksforgeeks.org/overlapping-subproblems-property-in-dynamic-programming-dp-1/)和[这个](https://www.geeksforgeeks.org/optimal-substructure-property-in-dynamic-programming-dp-2/))。像其他典型的[动态规划(DP)问题](https://www.geeksforgeeks.org/archives/tag/dynamic-programming)。

下面是一个基于记忆的解决方案。查找表用于查看问题是否已经计算出来。

## C++

```
// C++ program to find maximum weight
// transformation of a given string
#include<bits/stdc++.h>
using namespace std;

// Returns weight of the maximum
// weight transformation
int getMaxRec(string &str, int i, int n,
                           int lookup[])
{
    // Base case
    if (i >= n) return 0;

    //If this subproblem is already solved
    if (lookup[i] != -1) return lookup[i];

    // Don't make pair, so
    // weight gained is 1
    int ans = 1 + getMaxRec(str, i + 1, n,
                                  lookup);

    // If we can make pair
    if (i + 1 < n)
    {
    // If elements are dissimilar,
    // weight gained is 4
    if (str[i] != str[i+1])
        ans = max(4 + getMaxRec(str, i + 2,
                                n, lookup), ans);

    // if elements are similar so for
    // making a pair we toggle any of them.
    // Since toggle cost is 1 so
    // overall weight gain becomes 3
    else ans = max(3 + getMaxRec(str, i + 2,
                                 n, lookup), ans);
    }

    // save and return maximum
    // of above cases
    return lookup[i] = ans;
}

// Initializes lookup table
// and calls getMaxRec()
int getMaxWeight(string str)
{
    int n = str.length();

    // Create and initialize lookup table
    int lookup[n];
    memset(lookup, -1, sizeof lookup);

    // Call recursive function
    return getMaxRec(str, 0, str.length(),
                                 lookup);
}

// Driver Code
int main()
{
    string str = "AAAAABB";
    cout << "Maximum weight of a transformation of "
          << str << " is " << getMaxWeight(str);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find maximum
// weight transformation of a
// given string
class GFG {

    // Returns weight of the maximum
    // weight transformation
    static int getMaxRec(String str, int i,
            int n, int[] lookup)
    {
        // Base case
        if (i >= n)
        {
            return 0;
        }

        // If this subproblem is already solved
        if (lookup[i] != -1)
        {
            return lookup[i];
        }

        // Don't make pair, so
        // weight gained is 1
        int ans = 1 + getMaxRec(str, i + 1,
                            n, lookup);

        // If we can make pair
        if (i + 1 < n)
        {

            // If elements are dissimilar,
            // weight gained is 4
            if (str.charAt(i) != str.charAt(i + 1))
            {
                ans = Math.max(4 + getMaxRec(str, i + 2,
                                n, lookup), ans);
            }

            // if elements are similar so for
            // making a pair we toggle any of
            // them. Since toggle cost is
            // 1 so overall weight gain becomes 3
            else
            {
                ans = Math.max(3 + getMaxRec(str, i + 2,
                                n, lookup), ans);
            }
        }

        // save and return maximum
        // of above cases
        return lookup[i] = ans;
    }

    // Initializes lookup table
    // and calls getMaxRec()
    static int getMaxWeight(String str)
    {
        int n = str.length();

        // Create and initialize lookup table
        int[] lookup = new int[n];
        for (int i = 0; i < n; i++)
        {
            lookup[i] = -1;
        }

        // Call recursive function
        return getMaxRec(str, 0, str.length(),
                            lookup);
    }

    // Driver Code
    public static void main(String[] args)
    {

        String str = "AAAAABB";
        System.out.println("Maximum weight of a"
                        + " transformation of "
                        + str + " is "
                        + getMaxWeight(str));
    }
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to find maximum weight
# transformation of a given string

# Returns weight of the maximum
# weight transformation
def getMaxRec(string, i, n, lookup):

    # Base Case
    if i >= n:
        return 0

    # If this subproblem is already solved
    if lookup[i] != -1:
        return lookup[i]

    # Don't make pair, so
    # weight gained is 1
    ans = 1 + getMaxRec(string, i + 1, n,
                        lookup)

    # If we can make pair
    if i + 1 < n:

        # If elements are dissimilar
        if string[i] != string[i + 1]:
            ans = max(4 + getMaxRec(string, i + 2,
                                    n, lookup), ans)
        # if elements are similar so for
        # making a pair we toggle any of them.
        # Since toggle cost is 1 so
        # overall weight gain becomes 3
        else:
            ans = max(3 + getMaxRec(string, i + 2,
                                    n, lookup), ans)
    # save and return maximum
    # of above cases
    lookup[i] = ans
    return ans

# Initializes lookup table
# and calls getMaxRec()
def getMaxWeight(string):

    n = len(string)

    # Create and initialize lookup table
    lookup = [-1] * (n)

    # Call recursive function
    return getMaxRec(string, 0,
                     len(string), lookup)

# Driver Code
if __name__ == "__main__":
    string = "AAAAABB"
    print("Maximum weight of a transformation of",
           string, "is", getMaxWeight(string))

# This code is contributed by vibhu4agarwal
```

## C#

```
// C# program to find maximum
// weight transformation of a
// given string
using System;

class GFG
{
// Returns weight of the maximum
// weight transformation
static int getMaxRec(string str, int i,
                     int n, int []lookup)
{
    // Base case
    if (i >= n) return 0;

    //If this subproblem is already solved
    if (lookup[i] != -1) return lookup[i];

    // Don't make pair, so
    // weight gained is 1
    int ans = 1 + getMaxRec(str, i + 1,
                            n, lookup);

    // If we can make pair
    if (i + 1 < n)
    {
    // If elements are dissimilar,
    // weight gained is 4
    if (str[i] != str[i + 1])
        ans = Math.Max(4 + getMaxRec(str, i + 2,
                                     n, lookup), ans);

    // if elements are similar so for
    // making a pair we toggle any of
    // them. Since toggle cost is
    // 1 so overall weight gain becomes 3
    else ans = Math.Max(3 + getMaxRec(str, i + 2,
                                      n, lookup), ans);
    }

    // save and return maximum
    // of above cases
    return lookup[i] = ans;
}

// Initializes lookup table
// and calls getMaxRec()
static int getMaxWeight(string str)
{
    int n = str.Length;

    // Create and initialize lookup table
    int[] lookup = new int[n];
    for(int i = 0 ; i < n ; i++)
    lookup[i] = -1;

    // Call recursive function
    return getMaxRec(str, 0, str.Length,
                                 lookup);
}

// Driver Code
public static void Main()
{
    string str = "AAAAABB";
    Console.Write("Maximum weight of a" +
                  " transformation of " +
                           str + " is " +
                      getMaxWeight(str));
}
}

// This code is contributed by Sumit Sudhakar
```

## java 描述语言

```
<script>
    // Javascript program to find maximum
    // weight transformation of a
    // given string

    // Returns weight of the maximum
    // weight transformation
    function getMaxRec(str, i, n, lookup)
    {
        // Base case
        if (i >= n)
        {
            return 0;
        }

        // If this subproblem is already solved
        if (lookup[i] != -1)
        {
            return lookup[i];
        }

        // Don't make pair, so
        // weight gained is 1
        let ans = 1 + getMaxRec(str, i + 1, n, lookup);

        // If we can make pair
        if (i + 1 < n)
        {

            // If elements are dissimilar,
            // weight gained is 4
            if (str[i] != str[i + 1])
            {
                ans = Math.max(4 + getMaxRec(str, i + 2,
                                n, lookup), ans);
            }

            // if elements are similar so for
            // making a pair we toggle any of
            // them. Since toggle cost is
            // 1 so overall weight gain becomes 3
            else
            {
                ans = Math.max(3 + getMaxRec(str, i + 2,
                                n, lookup), ans);
            }
        }

        // save and return maximum
        // of above cases
        return lookup[i] = ans;
    }

    // Initializes lookup table
    // and calls getMaxRec()
    function getMaxWeight(str)
    {
        let n = str.length;

        // Create and initialize lookup table
        let lookup = new Array(n);
        lookup.fill(0);
        for (let i = 0; i < n; i++)
        {
            lookup[i] = -1;
        }

        // Call recursive function
        return getMaxRec(str, 0, str.length, lookup);
    }

    let str = "AAAAABB";
    document.write("Maximum weight of a"
                       + " transformation of "
                       + str + " is "
                       + getMaxWeight(str));

  // This code is contributed by decode2207.
</script>
```

**输出:**

```
Maximum weight of a transformation of AAAAABB is 11 
```

感谢 Gaurav Ahirwar 提供上述解决方案。
发现有不正确的地方请写评论，或者想分享更多以上讨论话题的信息
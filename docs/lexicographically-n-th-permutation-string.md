# 字符串的第 n 次字典排列

> 原文:[https://www . geeksforgeeks . org/词典-n-th-置换-string/](https://www.geeksforgeeks.org/lexicographically-n-th-permutation-string/)

给定一个长度为 m 的字符串，其中只包含小写字母。你必须按字典顺序找到字符串的第 n 个排列。

**例:**

```
Input : str[] = "abc", n = 3
Output : Result = "bac"
Explanation : All possible permutation in
sorted order: abc, acb, bac, bca, cab, cba

Input : str[] = "aba", n = 2
Output : Result = "aba"
Explanation : All possible permutation
in sorted order: aab, aba, baa

```

先决条件:[使用 STL 对给定字符串进行排列](https://www.geeksforgeeks.org/permutations-of-a-given-string-using-stl/)

打印第 n 个排列背后的想法很简单，我们应该使用 STL(在上面的链接中解释)来寻找下一个排列，并一直做到第 n 个排列。在第 n 次迭代之后，我们应该脱离循环，然后打印字符串，这是我们的第 n 次置换。

```
    long int i = 1;
    do
    {
        // check for nth iteration
        if (i == n)
            break;
       i++; // keep incrementing the iteration
    } while (next_permutation(str.begin(), str.end()));

    // print string after nth iteration
   print str;

```

## c++

```
// C++ program to print nth permutation with
// using next_permute()
#include <bits/stdc++.h>
using namespace std;

// Function to print nth permutation
// using next_permute()
void nPermute(string str, long int n)
{
    // Sort the string in lexicographically
    // ascending order
    sort(str.begin(), str.end());

    // Keep iterating until
    // we reach nth position
    long int i = 1;
    do {
        // check for nth iteration
        if (i == n)
            break;

        i++;
    } while (next_permutation(str.begin(), str.end()));

    // print string after nth iteration
    cout << str;
}

// Driver code
int main()
{
    string str = "GEEKSFORGEEKS";
    long int n = 100;
    nPermute(str, n);
    return 0;
}
```

## Java

```
// Java program to print nth permutation with
// using next_permute()
import java.util.*;

class GFG 
{

// Function to print nth permutation
// using next_permute()
static void nPermute(char[] str, int n)
{
    // Sort the string in lexicographically
    // ascending order
    Arrays.sort(str);

    // Keep iterating until
    // we reach nth position
    int i = 1;
    do {
        // check for nth iteration
        if (i == n)
            break;

        i++;
    } while (next_permutation(str));

    // print string after nth iteration
    System.out.println(String.valueOf(str));
}

static boolean next_permutation(char[] p)
{
    for (int a = p.length - 2; a >= 0; --a)
        if (p[a] < p[a + 1])
        for (int b = p.length - 1;; --b)
            if (p[b] > p[a]) 
            {
                char t = p[a];
                p[a] = p[b];
                p[b] = t;
                for (++a, b = p.length - 1; a < b; ++a, --b)
                {
                    t = p[a];
                    p[a] = p[b];
                    p[b] = t;
                }
                return true;
            }
    return false;
} 

// Driver code
public static void main(String[] args) 
{
    String str = "GEEKSFORGEEKS";
    int n = 100;
    nPermute(str.toCharArray(), n);
}
}

// This code contributed by Rajput-Ji
```

## python 3

```
# Python3 program to print nth permutation 
# with using next_permute()

# next_permutation method implementation
def next_permutation(L):
    n = len(L)
    i = n - 2
    while i >= 0 and L[i] >= L[i + 1]:
        i -= 1

    if i == -1:
        return False

    j = i + 1
    while j < n and L[j] > L[i]:
        j += 1
    j -= 1

    L[i], L[j] = L[j], L[i]

    left = i + 1
    right = n - 1

    while left < right:
        L[left], L[right] = L[right], L[left]
        left += 1
        right -= 1

    return True

# Function to print nth permutation
# using next_permute()
def nPermute(string, n):
    string = list(string)
    new_string = []

    # Sort the string in lexicographically
    # ascending order
    string.sort()
    j = 2

    # Keep iterating until
    # we reach nth position
    while next_permutation(string):
        new_string = string

        # check for nth iteration
        if j == n:
            break
        j += 1

    # print string after nth iteration
    print(''.join(new_string))

# Driver Code
if __name__ == "__main__":
    string = "GEEKSFORGEEKS"
    n = 100
    nPermute(string, n)

# This code is contributed by
# sanjeev2552
```

## c#

```
// C# program to print nth permutation with 
// using next_permute()
using System;

class GFG 
{ 

// Function to print nth permutation 
// using next_permute() 
static void nPermute(char[] str, int n) 
{ 
    // Sort the string in lexicographically 
    // ascending order 
    Array.Sort(str); 

    // Keep iterating until 
    // we reach nth position 
    int i = 1; 
    do 
    { 
        // check for nth iteration 
        if (i == n) 
            break; 

        i++; 
    } while (next_permutation(str)); 

    // print string after nth iteration 
    Console.WriteLine(String.Join("",str)); 
} 

static bool next_permutation(char[] p) 
{ 
    for (int a = p.Length - 2; a >= 0; --a) 
        if (p[a] < p[a + 1]) 
        for (int b = p.Length - 1;; --b) 
            if (p[b] > p[a]) 
            { 
                char t = p[a]; 
                p[a] = p[b]; 
                p[b] = t; 
                for (++a, b = p.Length - 1; a < b; ++a, --b) 
                { 
                    t = p[a]; 
                    p[a] = p[b]; 
                    p[b] = t; 
                } 
                return true; 
            } 
    return false; 
} 

// Driver code 
public static void Main() 
{ 
    String str = "GEEKSFORGEEKS"; 
    int n = 100; 
    nPermute(str.ToCharArray(), n); 
} 
} 

/* This code contributed by PrinciRaj1992 */
```

**输出:**

```
EEEEFGGRKSOSK

```

[查找字符串的第 n 次字典排列|集合 2](https://www.geeksforgeeks.org/find-n-th-lexicographically-permutation-string-set-2/)

本文由**[Shivam Pradhan(anuj _ charm)](https://www.linkedin.com/in/imanuj/)**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。

如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。
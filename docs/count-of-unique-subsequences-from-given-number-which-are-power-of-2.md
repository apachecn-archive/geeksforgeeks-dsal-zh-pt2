# 给定数量的唯一子序列的计数，其为 2 的幂

> 原文:[https://www . geeksforgeeks . org/给定数字的唯一子序列计数是 2 的幂/](https://www.geeksforgeeks.org/count-of-unique-subsequences-from-given-number-which-are-power-of-2/)

给定一个大小为 **N** 且包含范围为**【0-9】**的数字的[字符串](https://www.geeksforgeeks.org/string-data-structure/) **S** ，任务是打印一个字符串的所有[唯一子序列的计数，这些子序列是 **2** 的幂。](https://www.geeksforgeeks.org/generating-distinct-subsequences-of-a-given-string-in-lexicographic-order/)

**示例:**

> **输入:** S = "1216389"
> **输出:** 5
> **解释:**
> 2 的幂的所有可能的唯一子序列是:{1，2，16，128，8}
> 
> **输入:** S = "12"
> **输出:** 2
> **解释:**
> 2 的幂的所有可能的唯一子序列是:{1，2}。

**方法:**这个问题可以通过[生成字符串的所有子序列](https://www.geeksforgeeks.org/print-subsequences-string-iterative-method/) **S** 然后检查[这个数字是否是 **2**](https://www.geeksforgeeks.org/program-to-find-whether-a-no-is-power-of-two/) 的幂来解决。按照以下步骤解决问题:

*   初始化一个[集合](https://www.geeksforgeeks.org/hashset-in-java/)说， **allUniqueSubSeq** 存储子序列，是 **2** 的幂。
*   定义一个[递归函数](https://www.geeksforgeeks.org/recursive-functions/)，说 **uniqueSubSeq(S，ans，index)** ，执行以下步骤:
    *   基本情况:如果**指数**等于 **N，**则如果， **(int)ans，** [为 2](https://www.geeksforgeeks.org/program-to-find-whether-a-no-is-power-of-two/) 的幂，则将 **ans** 插入[集合](https://www.geeksforgeeks.org/hashset-in-java/) **allUniqueSubSeq** 。
    *   否则，有两种情况:
        *   如果[字符串](https://www.geeksforgeeks.org/string-class-in-java/) **ans** 中追加了 **S【索引】**，则调用带有参数 **S** 、 **ans + S【索引】**、 **index+1 的函数**uniquesubeq**。**
        *   如果[字符串](https://www.geeksforgeeks.org/string-data-structure/) **ans** 中没有追加 **S【索引】**，则调用带有参数 **S** 、 **ans** 、 **index + 1** 的函数**uniquesubeq**。
*   最后，执行上述步骤后，调用函数， **uniqueSubSeq(S，“”，0)** ，然后打印 **allUniqueSubSeq.size()** 作为答案。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Set to store subsequences that are
// power of 2
unordered_set<string> allUniqueSubSeq;

// Function to check whether the number
// is power of 2 or not
bool checkpower(int n)
{
    if ((n & (n - 1)) == 0)
    {
        return true;
    }
    return false;
}

// Auxiliary recursive Function to find
// all the unique subsequences of a string
// that are the power of 2
void uniqueSubSeq(string S, int N, string ans,
                            int index)
{

    // If index is equal to N
    if (index == N)
    {
        if (ans.length() != 0)

            // If the number is
            // power of 2
            if (checkpower(stoi(ans)))
            {

                // Insert the String
                // in the set
                allUniqueSubSeq.insert(ans);
            }
        return;
    }

    // Recursion call, if the S[index]
    // is inserted in ans
    uniqueSubSeq(S, N, ans + S[index], index + 1);

    // Recursion call, if S[index] is
    // not inserted in ans
    uniqueSubSeq(S, N, ans, index + 1);
}

// Function to find count of all the unique
// subsequences of a string that are the
// power of 2
int Countsubsequneces(string S, int N)
{

    // Function Call
    uniqueSubSeq(S, N, "", 0);

    // Return the length of set
    // allUniqueSubSeq
    return allUniqueSubSeq.size();
}

// Driver Code
int main()
{

    // Given Input
    string S = "1216389";
    int N = S.length();

    // Function call
    cout << Countsubsequneces(S, N);

    return 0;
}

// This code is contributed by maddler
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.util.*;
public class main {

    // Set to store subsequences that are
    // power of 2
    static HashSet<String> allUniqueSubSeq
        = new HashSet<>();

    // Function to check whether the number
    // is power of 2 or not
    static boolean checkpower(int n)
    {
        if ((n & (n - 1)) == 0) {
            return true;
        }
        return false;
    }

    // Auxiliary recursive Function to find
    // all the unique subsequences of a string
    // that are the power of 2
    static void uniqueSubSeq(String S, int N, String ans,
                             int index)
    {

        // If index is equal to N
        if (index == N) {

            if (ans.length() != 0)

                // If the number is
                // power of 2
                if (checkpower(
                        Integer.parseInt(ans.trim()))) {

                    // Insert the String
                    // in the set
                    allUniqueSubSeq.add(ans);
                }
            return;
        }

        // Recursion call, if the S[index]
        // is inserted in ans
        uniqueSubSeq(S, N, ans + S.charAt(index),
                     index + 1);

        // Recursion call, if S[index] is
        // not inserted in ans
        uniqueSubSeq(S, N, ans, index + 1);
    }

    // Function to find count of all the unique
    // subsequences of a string that are the
    // power of 2
    static int Countsubsequneces(String S, int N)
    {
        // Function Call
        uniqueSubSeq(S, N, "", 0);

        // Return the length of set
        // allUniqueSubSeq
        return allUniqueSubSeq.size();
    }

    // Driver Code
    public static void main(String[] args)
    {

        // Given Input
        String S = "1216389";
        int N = S.length();

        // Function call
        System.out.println(Countsubsequneces(S, N));
    }
}
```

## 蟒蛇 3

```
# Python program for the above approach

# Set to store subsequences that are
# power of 2
allUniqueSubSeq = set()

# Function to check whether the number
# is power of 2 or not
def checkpower(n):
    if(n & (n-1) == 0):
        return True
    return False

# Auxiliary recursive Function to find
# all the unique subsequences of a string
# that are the power of 2
def uniqueSubSeq(S, N, ans, index):

    # If index is equal to N
    if (index == N):
        if (len(ans) != 0):

            # If the number is
            # power of 2
            if(checkpower(int(ans))):
                allUniqueSubSeq.add(ans)
        return

    # Recursion call, if the S[index]
    # is inserted in ans
    uniqueSubSeq(S, N, ans+S[index], index+1)

    # Recursion call, if the S[index]
    # is not inserted in ans
    uniqueSubSeq(S, N, ans, index+1)

# Function to find count of all the unique
# subsequences of a string that are
# the power of 2
def countSubsequences(S, N):

    # Function call
    uniqueSubSeq(S, N, "", 0)

    # Return the length of set
    # allUniqueSubSeq
    return len(allUniqueSubSeq)

# Driver code
if __name__ == '__main__':

    # Given Input
    S = "1216389"
    N = len(S)

    # Function call
    print(countSubsequences(S, N))

# This code is contributed by MuskanKalra1
```

## C#

```
using System;
using System.Collections.Generic;
public class GFG {

    // Set to store subsequences that are
    // power of 2
    static HashSet<String> allUniqueSubSeq
        = new HashSet<String>();

    // Function to check whether the number
    // is power of 2 or not
    static bool checkpower(int n)
    {
        if ((n & (n - 1)) == 0) {
            return true;
        }
        return false;
    }

    // Auxiliary recursive Function to find
    // all the unique subsequences of a string
    // that are the power of 2
    static void uniqueSubSeq(String S, int N, String ans,
                             int index)
    {

        // If index is equal to N
        if (index == N) {

            if (ans.Length != 0)

                // If the number is
                // power of 2
                if (checkpower(
                        int.Parse(ans))) {

                    // Insert the String
                    // in the set
                    allUniqueSubSeq.Add(ans);
                }
            return;
        }

        // Recursion call, if the S[index]
        // is inserted in ans
        uniqueSubSeq(S, N, ans + S[index],
                     index + 1);

        // Recursion call, if S[index] is
        // not inserted in ans
        uniqueSubSeq(S, N, ans, index + 1);
    }

    // Function to find count of all the unique
    // subsequences of a string that are the
    // power of 2
    static int Countsubsequeneces(String S, int N)
    {
        // Function Call
        uniqueSubSeq(S, N, "", 0);

        // Return the length of set
        // allUniqueSubSeq
        return allUniqueSubSeq.Count;
    }

    // Driver Code

    static public void Main()
    {
        String S = "1216389";
        int N = S.Length;

        // Function call
        Console.WriteLine(Countsubsequeneces(S, N));
    }
}

// This code is contributed by maddler.
```

## java 描述语言

```
<script>
       // Javascript program for above approach

       // Set to store subsequences that are
       // power of 2
       const allUniqueSubSeq
           = new Set();

       // Function to check whether the number
       // is power of 2 or not
       function checkpower(n) {
           if ((n & (n - 1)) == 0) {
               return true;
           }
           return false;
       }

       // Auxiliary recursive Function to find
       // all the unique subsequences of a string
       // that are the power of 2
       function uniqueSubSeq(S, N, ans, index) {

           // If index is equal to N
           if (index == N) {

               if (ans.length != 0)

                   // If the number is
                   // power of 2
                   if (checkpower(parseInt(ans.trim()))) {

                       // Insert the String
                       // in the set
                       allUniqueSubSeq.add(ans);
                   }
               return;
           }

           // Recursion call, if the S[index]
           // is inserted in ans
           uniqueSubSeq(S, N, ans + S.charAt(index),
               index + 1);

           // Recursion call, if S[index] is
           // not inserted in ans
           uniqueSubSeq(S, N, ans, index + 1);
       }

       // Function to find count of all the unique
       // subsequences of a string that are the
       // power of 2
       function Countsubsequneces(S, N) {
           // Function Call
           uniqueSubSeq(S, N, "", 0);

           // Return the length of set
           // allUniqueSubSeq
           return allUniqueSubSeq.size;
       }

       // Driver Code

       // Given Input
       let S = "1216389";
       let N = S.length;

       // Function call
       document.write(Countsubsequneces(S, N));

       // This code is contributed by Hritik
   </script>
```

**Output**

```
5
```

***时间复杂度:**O(2<sup>N</sup>)*
***辅助空间:** O(2 <sup>N</sup> )*
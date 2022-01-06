# 字典上最小的字符串，与给定字符串在精确的 K 个索引处不同

> 原文:[https://www . geeksforgeeks . org/按字典顺序排列的与给定字符串不同的最小字符串索引/](https://www.geeksforgeeks.org/lexicographically-smallest-string-which-differs-from-given-strings-at-exactly-k-indices/)

给定两个长度为 **N** 的字符串 **S <sub>1</sub>** 和 **S <sub>2</sub>** 和一个正整数 **K** ，任务是找到字典上最小的字符串，使其与给定的两个字符串 **S <sub>1</sub>** 和 **S <sub>2</sub>** 在精确的 **K** 位置不同。如果不存在这样的字符串，则打印**-1”**。
**举例:**

> **输入:** N = 4，K = 3，S<sub>1</sub>=“ccbb”，S<sub>2</sub>=“caab”
> **输出:** abcb
> **说明:**
> 字符串“abcb”与 S <sub>1</sub> 恰好在 3 个位置不同，即位置 1、2 和 3 处，而
> 字符串“abcb”与 S <sub>2</sub> 不同
> **输入:** N = 5，K = 1，S<sub>1</sub>=“cbabb”，S<sub>2</sub>=“babaa”
> **输出:** -1
> **说明:**
> 不存在同时不同于 S <sub>1</sub> 和 S <sub>2</sub> 的字符串，只在 1 个位置。

**进场:**

1.  不要从头开始构建 S <sub>3</sub> ，而是选择 S <sub>2</sub> 作为合成字符串 S <sub>3</sub> ，并尝试根据给定的约束对其进行修改。
2.  找出答案串 S <sub>3</sub> 和 S <sub>1</sub> 有多少个位置不同。
3.  让它们在精确的 **d** 位置上彼此不同。那么答案串 S <sub>3</sub> 与两个串可以不同的最小位数是**上限(d/2)** ，最大位数可以是 **N** 。
4.  如果 **K** 在**【上限(d/2)，N】**范围内，则 S <sub>3</sub> 存在，否则 S <sub>3</sub> 不存在，打印**-1”**。
5.  对于串 S <sub>3</sub> ，以下是几种情况:
    *   **T1】KT3<u>大于</u>T6<u>d</u>T9】**
        1.  如果 K 大于 d，则修改 S <sub>1</sub> 与 S <sub>3</sub> 不同的所有位置，这样修改后，该位置的 S <sub>3</sub> 将与 S <sub>1</sub> 和 S <sub>2</sub> 不同。减量 k。
        2.  修改 S <sub>1</sub> 与 S <sub>3</sub> 相同的位置，这样修改后，该位置的 S <sub>3</sub> 将与 S <sub>1</sub> 和 S <sub>2</sub> 不同。减量 k。
    *   **<u>K</u>** <u>小于或等于</u> **<u>d</u>**
        1.  在这种情况下，只修改 S <sub>3</sub> 位置，在该位置 S <sub>1</sub> 和 S <sub>3</sub> 不同。
        2.  修改后让 **X** 为只有 S <sub>1</sub> 与 S <sub>3</sub> 不同，S <sub>2</sub> 与 S <sub>3</sub> 不同的位置数。
        3.  设 **T** 为 S <sub>1</sub> 和 S <sub>2</sub> 与 S <sub>3</sub> 不同的位置数。那么方程将是:

> (2 * X) + T = d
> X + T = K

1.  求解这些方程，就可以得到 X 和 T 的值，并相应地修改答案串 S <sub>3</sub> 。

以下是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

char arr[] = { 'a', 'b', 'c' };

// Function to find the string which
// differ at exactly K positions
void findString(int n, int k,
                string s1, string s2)
{
    // Initialise s3 as s2
    string s3 = s2;

    // Number of places at which
    // s3 differ from s2
    int d = 0;
    for (int i = 0;
         i < s1.size(); i++) {
        if (s1[i] != s2[i])
            d++;
    }

    // Minimum possible value
    // is ceil(d/2) if it is
    // not possible then -1
    if ((d + 1) / 2 > k) {
        cout << "-1" << endl;
        return;
    }

    else {

        // Case 2 when K is
        // less equal d
        if (k <= d) {

            // value of X and T
            // after solving
            // equations

            // T shows the number
            // of modification
            // such that position
            // differ from both

            // X show the modification
            // such that this position
            // only differ from only
            // one string
            int X = d - k;
            int T = 2 * k - d;

            for (int i = 0;
                 i < s3.size(); i++) {

                if (s1[i] != s2[i]) {

                    // modify the position
                    // such that this
                    // differ from both
                    // S1 & S2 & decrease
                    // the T at each step
                    if (T > 0) {

                        // Finding the character
                        // which is different
                        // from both S1 and S2
                        for (int j = 0;
                             j < 3; j++) {

                            if (arr[j] != s1[i]
                                && arr[j] != s2[i]) {
                                s3[i] = arr[j];
                                T--;
                                break;
                            }
                        }
                    }

                    // After we done T
                    // start modification
                    // to meet our
                    // requirement
                    // for X type
                    else if (X > 0) {

                        s3[i] = s1[i];
                        X--;
                    }
                }
            }

            // Resultant string
            cout << s3 << endl;
        }
        else {

            // Case 1 when K > d
            // In first step, modify all
            // the character which are
            // not same in S1 and S3
            for (int i = 0;
                 i < s1.size(); i++) {

                if (s1[i] != s3[i]) {
                    for (int j = 0;
                         j < 3; j++) {

                        // Finding character
                        // which is
                        // different from
                        // both S1 and S2
                        if (arr[j] != s1[i]
                            && arr[j] != s3[i]) {
                            s3[i] = arr[j];
                            k--;
                            break;
                        }
                    }
                }
            }

            // Our requirement not
            // satisfied by performing
            // step 1\. We need to
            // modify the position
            // which matches in
            // both string
            for (int i = 0;
                 i < s1.size(); i++) {

                if (s1[i] == s3[i] && k) {

                    // Finding the character
                    // which is different
                    // from both S1 and S2
                    for (int j = 0; j < 3; j++) {

                        if (arr[j] != s1[i]
                            && arr[j] != s3[i]) {
                            s3[i] = arr[j];
                            k--;
                            break;
                        }
                    }
                }
            }

            // Resultant string
            cout << s3 << endl;
        }
    }
}

// Driver Code
int main()
{
    int N = 4, k = 2;

    // Given two strings
    string S1 = "zzyy";
    string S2 = "zxxy";

    // Function Call
    findString(N, k, S1, S2);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
class GFG{

static char arr[] = { 'a', 'b', 'c' };

// Function to find the String which
// differ at exactly K positions
static void findString(int n, int k,
                       char []s1,
                       char []s2)
{
    // Initialise s3 as s2
    char []s3 = s2;

    // Number of places at which
    // s3 differ from s2
    int d = 0;
    for (int i = 0;
             i < s1.length; i++)
    {
        if (s1[i] != s2[i])
            d++;
    }

    // Minimum possible value
    // is Math.ceil(d/2) if it is
    // not possible then -1
    if ((d + 1) / 2 > k)
    {
        System.out.print("-1" + "\n");
        return;
    }

    else
    {

        // Case 2 when K is
        // less equal d
        if (k <= d)
        {

            // value of X and T
            // after solving
            // equations

            // T shows the number
            // of modification
            // such that position
            // differ from both

            // X show the modification
            // such that this position
            // only differ from only
            // one String
            int X = d - k;
            int T = 2 * k - d;

            for (int i = 0; i < s3.length; i++)
            {
                if (s1[i] != s2[i])
                {

                    // modify the position
                    // such that this
                    // differ from both
                    // S1 & S2 & decrease
                    // the T at each step
                    if (T > 0)
                    {

                        // Finding the character
                        // which is different
                        // from both S1 and S2
                        for (int j = 0; j < 3; j++)
                        {

                            if (arr[j] != s1[i] &&
                                arr[j] != s2[i])
                            {
                                s3[i] = arr[j];
                                T--;
                                break;
                            }
                        }
                    }

                    // After we done T
                    // start modification
                    // to meet our
                    // requirement
                    // for X type
                    else if (X > 0)
                    {
                        s3[i] = s1[i];
                        X--;
                    }
                }
            }

            // Resultant String
            System.out.print(new String(s3) + "\n");
        }
        else
        {

            // Case 1 when K > d
            // In first step, modify all
            // the character which are
            // not same in S1 and S3
            for (int i = 0;
                     i < s1.length; i++)
            {

                if (s1[i] != s3[i])
                {
                    for (int j = 0;
                             j < 3; j++)
                    {

                        // Finding character
                        // which is
                        // different from
                        // both S1 and S2
                        if (arr[j] != s1[i] &&
                            arr[j] != s3[i])
                        {
                            s3[i] = arr[j];
                            k--;
                            break;
                        }
                    }
                }
            }

            // Our requirement not
            // satisfied by performing
            // step 1\. We need to
            // modify the position
            // which matches in
            // both String
            for (int i = 0;
                     i < s1.length; i++)
            {
                if (s1[i] == s3[i] && k > 0)
                {

                    // Finding the character
                    // which is different
                    // from both S1 and S2
                    for (int j = 0; j < 3; j++)
                    {
                        if (arr[j] != s1[i] &&
                            arr[j] != s3[i])
                        {
                            s3[i] = arr[j];
                            k--;
                            break;
                        }
                    }
                }
            }

            // Resultant String
            System.out.print(new String(s3) + "\n");
        }
    }
}

// Driver Code
public static void main(String[] args)
{
    int N = 4, k = 2;

    // Given two Strings
    String S1 = "zzyy";
    String S2 = "zxxy";

    // Function Call
    findString(N, k, S1.toCharArray(), S2.toCharArray());
}
}

// This code is contributed by amal kumar choubey
```

## 蟒蛇 3

```
# Python3 program for the above approach
arr = [ 'a', 'b', 'c' ]

# Function to find the string which
# differ at exactly K positions
def findString(n, k, s1, s2):

    # Initialise s3 as s2
    s3 = s2
    s3 = list(s3)

    # Number of places at which
    # s3 differ from s2
    d = 0
    for i in range(len(s1)):
        if (s1[i] != s2[i]):
            d += 1

    # Minimum possible value
    # is ceil(d/2) if it is
    # not possible then -1
    if ((d + 1) // 2 > k):
        print ("-1")
        return

    else:

        # Case 2 when K is
        # less equal d
        if (k <= d):

            # Value of X and T
            # after solving
            # equations

            # T shows the number
            # of modification
            # such that position
            # differ from both

            # X show the modification
            # such that this position
            # only differ from only
            # one string
            X = d - k
            T = 2 * k - d

            for i in range(len(s3)):
                if (s1[i] != s2[i]):

                    # Modify the position
                    # such that this
                    # differ from both
                    # S1 & S2 & decrease
                    # the T at each step
                    if (T > 0):

                        # Finding the character
                        # which is different
                        # from both S1 and S2
                        for j in range(3):
                            if (arr[j] != s1[i] and
                                arr[j] != s2[i]):
                                s3[i] = arr[j]
                                T -= 1
                                break

                    # After we done T
                    # start modification
                    # to meet our
                    # requirement
                    # for X type
                    elif (X > 0):
                        s3[i] = s1[i]
                        X -= 1

            # Resultant string
            print("".join(s3))

        else:

            # Case 1 when K > d
            # In first step, modify all
            # the character which are
            # not same in S1 and S3
            for i in range(len(s1)):
                if (s1[i] != s3[i]):
                    for j in range(3):

                        # Finding character
                        # which is
                        # different from
                        # both S1 and S2
                        if (arr[j] != s1[i] and
                            arr[j] != s3[i]):
                            s3[i] = arr[j]
                            k -= 1
                            break

            # Our requirement not
            # satisfied by performing
            # step 1\. We need to
            # modify the position
            # which matches in
            # both string
            for i in range(len(s1)):
                if (s1[i] == s3[i] and k):

                    # Finding the character
                    # which is different
                    # from both S1 and S2
                    for j in range (3):
                        if (arr[j] != s1[i] and
                            arr[j] != s3[i]):
                            s3[i] = arr[j]
                            k -= 1
                            break

            # Resultant string
            print("".join(s3))

# Driver Code
if __name__ == "__main__":

    N = 4
    k = 2

    # Given two strings
    S1 = "zzyy"
    S2 = "zxxy"

    # Function call
    findString(N, k, S1, S2)

# This code is contributed by chitranayal
```

## C#

```
// C# program for the above approach
using System;

class GFG{

static char []arr = { 'a', 'b', 'c' };

// Function to find the String which
// differ at exactly K positions
static void findString(int n, int k,
                       char []s1,
                       char []s2)
{

    // Initialise s3 as s2
    char []s3 = s2;

    // Number of places at which
    // s3 differ from s2
    int d = 0;
    for(int i = 0;
            i < s1.Length; i++)
    {
       if (s1[i] != s2[i])
           d++;
    }

    // Minimum possible value
    // is Math.Ceiling(d/2) if it is
    // not possible then -1
    if ((d + 1) / 2 > k)
    {
        Console.Write("-1" + "\n");
        return;
    }
    else
    {

        // Case 2 when K is
        // less equal d
        if (k <= d)
        {

            // Value of X and T
            // after solving
            // equations

            // T shows the number
            // of modification
            // such that position
            // differ from both

            // X show the modification
            // such that this position
            // only differ from only
            // one String
            int X = d - k;
            int T = 2 * k - d;

            for(int i = 0; i < s3.Length; i++)
            {
               if (s1[i] != s2[i])
               {

                   // Modify the position
                   // such that this
                   // differ from both
                   // S1 & S2 & decrease
                   // the T at each step
                   if (T > 0)
                   {

                       // Finding the character
                       // which is different
                       // from both S1 and S2
                       for(int j = 0; j < 3; j++)
                       {
                          if (arr[j] != s1[i] &&
                              arr[j] != s2[i])
                          {
                              s3[i] = arr[j];
                              T--;
                              break;
                          }
                       }
                   }

                   // After we done T start
                   // modification to meet our
                   // requirement for X type
                   else if (X > 0)
                   {
                       s3[i] = s1[i];
                       X--;
                   }
               }
            }

            // Resultant String
            Console.Write(new String(s3) + "\n");
        }
        else
        {

            // Case 1 when K > d
            // In first step, modify all
            // the character which are
            // not same in S1 and S3
            for(int i = 0; i < s1.Length; i++)
            {
               if (s1[i] != s3[i])
               {
                   for(int j = 0; j < 3; j++)
                   {

                      // Finding character
                      // which is different
                      // from both S1 and S2
                      if (arr[j] != s1[i] &&
                          arr[j] != s3[i])
                      {
                          s3[i] = arr[j];
                          k--;
                          break;
                      }
                   }
               }
            }

            // Our requirement not
            // satisfied by performing
            // step 1\. We need to
            // modify the position
            // which matches in
            // both String
            for(int i = 0; i < s1.Length; i++)
            {
               if (s1[i] == s3[i] && k > 0)
               {

                   // Finding the character
                   // which is different
                   // from both S1 and S2
                   for(int j = 0; j < 3; j++)
                   {
                      if (arr[j] != s1[i] &&
                          arr[j] != s3[i])
                      {
                          s3[i] = arr[j];
                          k--;
                          break;
                      }
                   }
               }
            }

            // Resultant String
            Console.Write(new String(s3) + "\n");
        }
    }
}

// Driver Code
public static void Main(String[] args)
{
    int N = 4, k = 2;

    // Given two Strings
    String S1 = "zzyy";
    String S2 = "zxxy";

    // Function Call
    findString(N, k, S1.ToCharArray(),
                     S2.ToCharArray());
}
}

// This code is contributed by amal kumar choubey
```

## java 描述语言

```
<script>

// javascript program for the above approach
var arr = [ 'a', 'b', 'c' ];

// Function to find the String which
// differ at exactly K positions
function findString(n , k,s1,s2)
{
    // Initialise s3 as s2
    var s3 = s2;

    // Number of places at which
    // s3 differ from s2
    var d = 0;
    for (i = 0;
             i < s1.length; i++)
    {
        if (s1[i] != s2[i])
            d++;
    }

    // Minimum possible value
    // is Math.ceil(d/2) if it is
    // not possible then -1
    if ((d + 1) / 2 > k)
    {
        document.write("-1" + "<br>");
        return;
    }

    else
    {

        // Case 2 when K is
        // less equal d
        if (k <= d)
        {

            // value of X and T
            // after solving
            // equations

            // T shows the number
            // of modification
            // such that position
            // differ from both

            // X show the modification
            // such that this position
            // only differ from only
            // one String
            var X = d - k;
            var T = 2 * k - d;

            for (i = 0; i < s3.length; i++)
            {
                if (s1[i] != s2[i])
                {

                    // modify the position
                    // such that this
                    // differ from both
                    // S1 & S2 & decrease
                    // the T at each step
                    if (T > 0)
                    {

                        // Finding the character
                        // which is different
                        // from both S1 and S2
                        for (j = 0; j < 3; j++)
                        {

                            if (arr[j] != s1[i] &&
                                arr[j] != s2[i])
                            {
                                s3[i] = arr[j];
                                T--;
                                break;
                            }
                        }
                    }

                    // After we done T
                    // start modification
                    // to meet our
                    // requirement
                    // for X type
                    else if (X > 0)
                    {
                        s3[i] = s1[i];
                        X--;
                    }
                }
            }

            // Resultant String
            document.write(s3.join('') + "<br>");
        }
        else
        {

            // Case 1 when K > d
            // In first step, modify all
            // the character which are
            // not same in S1 and S3
            for (i = 0;
                     i < s1.length; i++)
            {

                if (s1[i] != s3[i])
                {
                    for (j = 0;
                             j < 3; j++)
                    {

                        // Finding character
                        // which is
                        // different from
                        // both S1 and S2
                        if (arr[j] != s1[i] &&
                            arr[j] != s3[i])
                        {
                            s3[i] = arr[j];
                            k--;
                            break;
                        }
                    }
                }
            }

            // Our requirement not
            // satisfied by performing
            // step 1\. We need to
            // modify the position
            // which matches in
            // both String
            for (i = 0;
                     i < s1.length; i++)
            {
                if (s1[i] == s3[i] && k > 0)
                {

                    // Finding the character
                    // which is different
                    // from both S1 and S2
                    for (j = 0; j < 3; j++)
                    {
                        if (arr[j] != s1[i] &&
                            arr[j] != s3[i])
                        {
                            s3[i] = arr[j];
                            k--;
                            break;
                        }
                    }
                }
            }

            // Resultant String
            document.write(s3.join('') + "<br>");
        }
    }
}

// Driver Code
var N = 4, k = 2;

// Given two Strings
var S1 = "zzyy";
var S2 = "zxxy";

// Function Call
findString(N, k, S1.split(''), S2.split(''));

// This code is contributed by 29AjayKumar
</script>
```

**Output:** 

```
zaay
```

**时间复杂度:**T2【O(N)T4】
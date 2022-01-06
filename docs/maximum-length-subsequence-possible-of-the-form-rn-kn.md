# r^n k^n 形式的最大可能长度子序列

> 原文:[https://www . geesforgeks . org/最大长度-子序列-可能的形式-rn-kn/](https://www.geeksforgeeks.org/maximum-length-subsequence-possible-of-the-form-rn-kn/)

给定一个只包含两个字符的字符串，即 R 和 K(如 RRKRRKKKKK)。任务是为形式为 r-n 次然后 k-n 次(即形式为 R^N K^N).)的可能子序列找到 n 的最大值
**注意:**K 的字符串应该在 R 的字符串之后开始，即被认为是“K”字符串的第一个 K 必须出现在给定字符串中“R”字符串的最后一个 R 之后。此外，结果子序列的长度将为 2*N.
**示例** :

> **输入** : RRRKRRKKRRKKK
> **输出** : 5
> 如果我们在索引 0、1、2、4、5 取 r，在索引 6、7、10、11、12
> 取 k，那么我们得到形式 R^N K^N 的最大子序列，其中 N = 5。
> **输入** : KKKKRRRRK
> **输出** : 1
> 如果我们在索引 4(或 5 或 6 或 7)取 R，在索引 8
> 取 K，那么我们得到 N = 1 的期望子序列。

**进场:**

1.  计算一个 K 之前的 R 的个数。
2.  计算一个 K 之后的 K 的个数，包括那个 K。
3.  将它们存储在一个表中，表[x][0]中有若干个 R，表[x][1]中有若干个 K。
4.  两者中的最小值给出了每个 K 的 n 值，我们将返回最大值 n。

以下是上述方法的实现:

## C++

```
// C++ program to find the maximum
// length of a substring of form R^nK^n
#include<bits/stdc++.h>
using namespace std;

    // function to calculate the maximum
    // length of substring of the form R^nK^n
    int find(string s)
    {
        int max = 0, i, j = 0, countk = 0, countr = 0;
        int table[s.length()][2];

        // Count no. Of R's before a K
        for (i = 0; i < s.length(); i++) {
            if (s[i] == 'R')
                countr++;
            else
                table[j++][0] = countr;
        }
        j--;

        // Count no. Of K's after a K
        for (i = s.length() - 1; i >= 0; i--) {
            if (s[i] == 'K') {
                countk++;
                table[j--][1] = countk;
            }

            // Update maximum length
            if (min(table[j + 1][0], table[j + 1][1]) > max)
                max = min(table[j + 1][0], table[j + 1][1]);
        }

        return max;
    }

    // Driver code
    int main()
    {
        string s = "RKRRRKKRRKKKKRR";
        int n = find(s);
        cout<<(n);
    }
// This code is contributed by
// Surendra_Gangwar
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the maximum
// length of a substring of form R^nK^n
public class gfg {

    // function to calculate the maximum
    // length of substring of the form R^nK^n
    int find(String s)
    {
        int max = 0, i, j = 0, countk = 0, countr = 0;
        int table[][] = new int[s.length()][2];

        // Count no. Of R's before a K
        for (i = 0; i < s.length(); i++) {
            if (s.charAt(i) == 'R')
                countr++;
            else
                table[j++][0] = countr;
        }
        j--;

        // Count no. Of K's after a K
        for (i = s.length() - 1; i >= 0; i--) {
            if (s.charAt(i) == 'K') {
                countk++;
                table[j--][1] = countk;
            }

            // Update maximum length
            if (Math.min(table[j + 1][0], table[j + 1][1]) > max)
                max = Math.min(table[j + 1][0], table[j + 1][1]);
        }

        return max;
    }

    // Driver code
    public static void main(String srgs[])
    {
        String s = "RKRRRKKRRKKKKRR";
        gfg ob = new gfg();
        int n = ob.find(s);
        System.out.println(n);
    }
}
```

## 蟒蛇 3

```
# Python3 program to find the maximum
# length of a substring of form R^nK^n

# Function to calculate the maximum
# length of substring of the form R^nK^n
def find(s):

    Max = j = countk = countr = 0
    table = [[0, 0] for i in range(len(s))]

    # Count no. Of R's before a K
    for i in range(0, len(s)): 
        if s[i] == 'R':
            countr += 1
        else:
            table[j][0] = countr
            j += 1

    j -= 1

    # Count no. Of K's after a K
    for i in range(len(s) - 1, -1, -1): 
        if s[i] == 'K': 
            countk += 1
            table[j][1] = countk
            j -= 1

        # Update maximum length
        if min(table[j + 1][0], table[j + 1][1]) > Max:
            Max = min(table[j + 1][0], table[j + 1][1])

    return Max

# Driver code
if __name__ == "__main__":

    s = "RKRRRKKRRKKKKRR"
    print(find(s))

# This code is contributed by Rituraj Jain
```

## C#

```
// C# program to find the maximum
// length of a substring of
// form R^nK^n
using System;

class GFG
{

// function to calculate the
// maximum length of substring
// of the form R^nK^n
static int find(String s)
{
    int max = 0, i, j = 0,
        countk = 0, countr = 0;
    int [,]table= new int[s.Length, 2];

    // Count no. Of R's before a K
    for (i = 0; i < s.Length; i++)
    {
        if (s[i] == 'R')
            countr++;
        else
            table[(j++),0] = countr;
    }
    j--;

    // Count no. Of K's after a K
    for (i = s.Length - 1; i >= 0; i--)
    {
        if (s[i] == 'K')
        {
            countk++;
            table[j--, 1] = countk;
        }

        // Update maximum length
        if (Math.Min(table[j + 1, 0],
                     table[j + 1, 1]) > max)
            max = Math.Min(table[j + 1, 0],
                           table[j + 1, 1]);
    }

    return max;
}

// Driver code
static public void Main(String []srgs)
{
    String s = "RKRRRKKRRKKKKRR";
    int n = find(s);
    Console.WriteLine(n);
}
}

// This code is contributed
// by Arnab Kundu
```

## java 描述语言

```
<script>

// JavaScript program to find the maximum
// length of a substring of form R^nK^n

// function to calculate the maximum
    // length of substring of the form R^nK^n
function find(s)
{
    let max = 0, i, j = 0, countk = 0, countr = 0;
        let table = new Array(s.length);
        for(let i=0;i<s.length;i++)
        {
            table[i]=new Array(2);
        }

        // Count no. Of R's before a K
        for (i = 0; i < s.length; i++) {
            if (s[i] == 'R')
                countr++;
            else
                table[j++][0] = countr;
        }
        j--;

        // Count no. Of K's after a K
        for (i = s.length - 1; i >= 0; i--) {
            if (s[i] == 'K') {
                countk++;
                table[j--][1] = countk;
            }

            // Update maximum length
            if (Math.min(table[j + 1][0], table[j + 1][1]) > max)
                max = Math.min(table[j + 1][0], table[j + 1][1]);
        }

        return max;
}

// Driver code
let s = "RKRRRKKRRKKKKRR";
let n=find(s);
document.write(n);

// This code is contributed by avanitrachhadiya2155

</script>
```

**Output:** 

```
4
```

**时间复杂度:** O(n)，其中 ln 为子串的长度。
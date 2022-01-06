# 从子串 10

中重复删除字符形成的字典最小串

> 原文:[https://www . geesforgeks . org/按字典顺序排列-最小-字符串形式-重复-从子字符串中删除-字符-10/](https://www.geeksforgeeks.org/lexicographically-smallest-string-formed-repeatedly-deleting-character-from-substring-10/)

给定一个长度为 **N** 的[二进制字符串](https://www.geeksforgeeks.org/tag/binary-string/) [](https://www.geeksforgeeks.org/string-data-structure/)**S** ，任务是通过选择任意[子字符串](https://www.geeksforgeeks.org/substring-in-java/)**【10】**并从该[子字符串](https://www.geeksforgeeks.org/substring-in-java/)中删除任意一个字符任意次数，来从字典中找到修改该字符串后形成的最小字符串。

**示例:**

> **输入:**S =“0101”
> T3】输出: 001
> **解释:**
> 从子串中去掉 S[1](=1)，范围[1，2]内的“10”将字符串 S 修改为最小的“001”。
> 
> **输入:**S = " 11001101 "
> **输出:** 0001
> **解释:**
> 获取字典上最小字符串的一种可能方法是:
> 
> 1.  从子串[1，2]中删除 S[1](=1)，范围[1，2]上的“10”将字符串 S 修改为 S =“1001101”。
> 2.  从子字符串中删除 S[0](=1)，范围[0，1]内的“10”将字符串 S 修改为 S =“001101”。
> 3.  从子串[3，4]中删除 S[3](=1)，范围[3，4]上的“10”将字符串 S 修改为 S =“00101”。
> 4.  从子串[2，3]中删除 S[2](=1)，范围[2，3]中的“10”将字符串 S 修改为 S =“0001”。
> 5.  现在任何字符都不能删除。
> 
> 因此，从字典序上获得的最小字符串是“0001”。

**方法:**给定的问题可以基于以下观察来解决:

*   可以观察到，最后一个零之后的字符“ **1** ”不能被移除，因为人们将找不到任何“ **10** ”子串。
*   从词典的角度来看，最小的字符串在第一个字符串之前会包含尽可能多的零。
*   可以观察到，如果后面至少有一个“ **0** ，则每个“ **1** ”都可以删除。
*   因此，想法是从字符串中删除最后出现的“ **0** ”之前的所有。

按照以下步骤解决问题:

*   初始化两个变量，比如 **ans** 和 **LastZe，**来存储结果字符串和最后出现的索引' **0** 。
*   [使用变量 **i** 迭代字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/) **S** 的字符，然后如果**S【I】**是“ **0** ，则将 **i** 分配给 **LastZe。**
*   [使用变量 **i** 迭代字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/) **S** 的字符，并执行以下操作:
    *   如果 **S[i] = '0'** 和 **i ≤ LastZe，**则在 **ans 后追加 **S[i]** 。**
    *   否则，如果 **i >** **LastZe，**则追加**S【I】**到 **ans** 。
*   最后，完成上述步骤后，将结果打印为**和**。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find smallest lexicogra-
// phically smallest string
string lexicographicallySmallestString(string S, int N)
{
    // Stores the index of last
    // occuring 0
    int LastZe = -1;

    // Stores the lexicographically
    // smallest string
    string ans;

    // Traverse the string S
    for (int i = N - 1; i >= 0; i--) {

        // If str[i] is 0
        if (S[i] == '0') {

            // Assign i to lastZe
            LastZe = i;
            break;
        }
    }

    // Traverse the string str
    for (int i = 0; i < N; i++) {

        // If i is less than or equal
        // to lastZe and str[i] is 0
        if (i <= LastZe && S[i] == '0')
            ans += S[i];

        // If i is greater than lastZe
        else if (i > LastZe)
            ans += S[i];
    }

    // Return ans
    return ans;
}

// Driver Code
int main()
{
    // Input
    string S = "11001101";
    int N = S.size();

    // Function Call
    cout << lexicographicallySmallestString(S, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.lang.*;
import java.util.*;

class GFG{

// Function to find smallest lexicogra-
// phically smallest string
static String lexicographicallySmallestString(String S,
                                              int N)
{

    // Stores the index of last
    // occuring 0
    int LastZe = -1;

    // Stores the lexicographically
    // smallest string
    String ans = "";

    // Traverse the string S
    for(int i = N - 1; i >= 0; i--)
    {

        // If str[i] is 0
        if (S.charAt(i) == '0')
        {

            // Assign i to lastZe
            LastZe = i;
            break;
        }
    }

    // Traverse the string str
    for(int i = 0; i < N; i++)
    {

        // If i is less than or equal
        // to lastZe and str[i] is 0
        if (i <= LastZe && S.charAt(i) == '0')
            ans += S.charAt(i);

        // If i is greater than lastZe
        else if (i > LastZe)
            ans += S.charAt(i);
    }

    // Return ans
    return ans;
}

// Driver code
public static void main(String[] args)
{

    // Input
    String S = "11001101";
    int N = S.length();

    // Function Call
    System.out.println(
        lexicographicallySmallestString(S, N));
}
}

// This code is contributed by avijitmondal1998
```

## 蟒蛇 3

```
# Python program for the above approach

# Function to find smallest lexicogra-
# phically smallest string
def lexicographicallySmallestString(S, N):

    # Stores the index of last
    # occuring 0
    LastZe = -1

    # Stores the lexicographically
    # smallest string
    ans = ""

    # Traverse the S
    for i in range(N - 1, -1, -1):

        # If str[i] is 0
        if (S[i] == '0'):

            # Assign i to lastZe
            LastZe = i
            break

    # Traverse the str
    for  i in range(N):
        # If i is less than or equal
        # to lastZe and str[i] is 0
        if (i <= LastZe and S[i] == '0'):
            ans += S[i]

        # If i is greater than lastZe
        elif (i > LastZe):
            ans += S[i]

    # Return ans
    return ans

# Driver Code
if __name__ == '__main__':
    # Input
    S = "11001101"
    N = len(S)

    # Function Call
    print (lexicographicallySmallestString(S, N))

# This code is contributed by mohit kumar 29.
```

## C#

```
// C# program for the above approach
using System;
class GFG {
    // Function to find smallest lexicogra-
    // phically smallest string
    static string lexicographicallySmallestString(string S,
                                                  int N)
    {
        // Stores the index of last
        // occuring 0
        int LastZe = -1;

        // Stores the lexicographically
        // smallest string
        string ans = "";

        // Traverse the string S
        for (int i = N - 1; i >= 0; i--) {

            // If str[i] is 0
            if (S[i] == '0') {

                // Assign i to lastZe
                LastZe = i;
                break;
            }
        }

        // Traverse the string str
        for (int i = 0; i < N; i++) {

            // If i is less than or equal
            // to lastZe and str[i] is 0
            if (i <= LastZe && S[i] == '0')
                ans += S[i];

            // If i is greater than lastZe
            else if (i > LastZe)
                ans += S[i];
        }

        // Return ans
        return ans;
    }

    // Driver Code
    public static void Main()
    {
        // Input
        string S = "11001101";
        int N = S.Length;

        // Function Call
        Console.Write(
            lexicographicallySmallestString(S, N));
    }
}

// This code is contributed by ukasp.
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to find smallest lexicogra-
// phically smallest string
function lexicographicallySmallestString(S, N)
{

    // Stores the index of last
    // occuring 0
    var LastZe = -1;

    // Stores the lexicographically
    // smallest string
    var ans = "";

    // Traverse the string S
    for(var i = N - 1; i >= 0; i--)
    {

        // If str[i] is 0
        if (S.charAt(i) == '0')
        {

            // Assign i to lastZe
            LastZe = i;
            break;
        }
    }

    // Traverse the string str
    for(var i = 0; i < N; i++)
    {

        // If i is less than or equal
        // to lastZe and str[i] is 0
        if (i <= LastZe && S.charAt(i) == '0')
            ans += S.charAt(i);

        // If i is greater than lastZe
        else if (i > LastZe)
            ans += S.charAt(i);
    }

    // Return ans
    return ans;
}

// Driver code

// Input
var S = "11001101";
var N = S.length;

// Function Call
document.write(lexicographicallySmallestString(S, N));

// This code is contributed by shivanisinghss2110

</script>
```

**Output**

```
0001
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)
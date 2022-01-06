# 需要安装的最小灯具数量

> 原文:[https://www . geesforgeks . org/需要安装的最小灯具数量/](https://www.geeksforgeeks.org/minimum-amount-of-lamps-needed-to-be-installed/)

给定的字符串只包含点和星号。点代表自由空间，![*        ](img/9e6d0cc27aee54ccaa164e0e4bc2b52d.png "Rendered by QuickLaTeX.com")代表灯。位置![i        ](img/7feee5adee861af01dd30cde7ea9f34a.png "Rendered by QuickLaTeX.com")的灯可以在位置 **i-1、i** 、**和 i+1** 处发光。确定照亮整个灯串所需的最小灯数。

**示例:**

> **输入:**str = "……"
> T3】输出: 2
> 最初没有灯，所以整条线都是黑暗的。我们将在位置 2 和 5 安装灯。位置 2 的灯将点亮 1、2、3，位置 5 的灯将点亮 4、5、6，因此整个灯串都点亮。
> 
> **输入:**str =“*”。*
> **输出:** 0

**方法:**如果我们没有星号![*        ](img/9e6d0cc27aee54ccaa164e0e4bc2b52d.png "Rendered by QuickLaTeX.com")，那么每 3 个点我们需要一盏灯，所以答案是 **ceil(D/3)** ，其中 D 是点的数量。这个问题可以通过创建给定字符串的副本来解决，对于第一个字符串中的每个星号，我们在第二个字符串的相邻索引处放置一个星号。
所以如果给定的字符串是**“…* *”**那么第二串就是**..****."**。
之后，我们统计每块连续点的点数，找到该块需要的灯数，对于每块，答案将是 **ceil(D/3)** ，这些灯的总和将是完整串的答案。

下面是上述方法的实现:

## C++

```
// C++ implementation of the above approach
#include <bits/stdc++.h>
using namespace std;

void check(int n, string s)
{

    // Create the modified string with
    // v[i-1] = v[i + 1] = * where s[i] = *
    char v[n];
    for(int i = 0; i < n; i++)
    {
        if (s[i] == '*')
        {
            v[i] = '*';

            // Checking valid index and then replacing
            // "." with "*" on the surrounding of a *
            if (i > 0 && i < n - 1)
            {
                v[i + 1] = '*';
                v[i - 1] = '*';
            }
            if (i == 0 && n != 1)
            {
                v[i + 1] = '*';
            }
            if (i == n - 1 && n != 1)
            {
                v[i - 1] = '*';
            }
        }
        else
        {

            // Just copying if the character is a "."
            if (v[i] != '*')
            {
                v[i] = '.';
            }
        }
    }

    // Creating the string with the list v
    string str(v);

    string word = "";
    char dl = '*';

    // to count the number of split strings
    int num = 0;

    // adding delimiter character at the end
    // of 'str'
    str = str + dl;

    // length of 'str'
    int l = str.size();

    // traversing 'str' from left to right
    vector<string> res;
    for (int i = 0; i < l; i++) {

        // if str[i] is not equal to the delimiter
        // character then accumulate it to 'word'
        if (str[i] != dl)
            word = word + str[i];

        else {

            // if 'word' is not an empty string,
            // then add this 'word' to the array
            // 'substr_list[]'
            if ((int)word.size() != 0)
                res.push_back(word);

            // reset 'word'
            word = "";
        }
    }

    int ans = 0;
    for(auto x : res)
    {

        // Continuing if the string length is 0
        if (x.length() == 0)
        {
            continue;
        }

        // Adding number of lamps for each block of "."
        ans += ceil(x.length() * 1.0 / 3);
    }
    cout << ans << "\n";
}

int main() {
    string s = ".....";
    int n = s.length();
    check(n, s);
    return 0;
}

// This code is contributed by NishaBharti.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
import java.io.*;
import java.lang.*;
import java.util.*;

class GFG{

// Function to print minimum amount
// of lamps needed to be installed
static void check(int n, String s)
{

    // Create the modified string with
    // v[i-1] = v[i + 1] = * where s[i] = *
    char v[] = new char[n];
    for(int i = 0; i < n; i++)
    {
        if (s.charAt(i) == '*')
        {
            v[i] = '*';

            // Checking valid index and then replacing
            // "." with "*" on the surrounding of a *
            if (i > 0 && i < n - 1)
            {
                v[i + 1] = '*';
                v[i - 1] = '*';
            }
            if (i == 0 && n != 1)
            {
                v[i + 1] = '*';
            }
            if (i == n - 1 && n != 1)
            {
                v[i - 1] = '*';
            }
        }
        else
        {

            // Just copying if the character is a "."
            if (v[i] != '*')
            {
                v[i] = '.';
            }
        }
    }

    // Creating the string with the list v
    String xx = new String(v);

    // Splitting the string into blocks
    // with "*" as delimiter
    String x[] = xx.split("\\*");

    int ans = 0;
    for(String xi : x)
    {

        // Continuing if the string length is 0
        if (xi.length() == 0)
        {
            continue;
        }

        // Adding number of lamps for each block of "."
        ans += Math.ceil(xi.length() * 1.0 / 3);
    }
    System.out.println(ans);
}

// Driver Code
public static void main(String[] args)
{
    String s = "......";
    int n = s.length();

    check(n, s);
}
}

// This code is contributed by Kingash
```

## 蟒蛇 3

```
# Python3 implementation of the above approach
import math

# Function to print minimum amount
# of lamps needed to be installed
def check(n, s):

    # Create the modified string with
    # v[i-1] = v[i + 1] = * where s[i] = *
    v = [""] * n
    for i in range(n):
        if (s[i] == "*"):
            v[i] = "*"

            # Checking valid index and then replacing
            # "." with "*" on the surrounding of a *
            if (i > 0 and i < n - 1):
                v[i + 1] = "*"
                v[i - 1] = "*"
            if (i == 0 and n != 1):
                v[i + 1] = "*"
            if (i == n - 1 and n != 1):
                v[i - 1] = "*"
        else:

            # Just copying if the character is a "."
            if (v[i] != "*"):
                v[i] = "."

    # Creating the string with the list v
    xx = ''.join(v)

    # Splitting the string into blocks
    # with "*" as delimiter
    x = xx.split("*")
    s = 0
    for i in range(len(x)):

        # Continuing if the string length is 0
        if (x[i] == ""):
            continue

        # Adding number of lamps for each block of "."
        s += math.ceil(len(x[i]) / 3)
    print(s)

# Driver code
s = "......"
n = len(s)
check(n, s)
```

**Output:** 

```
2
```
# 给定字符串中出现的驼色字符数

> 原文:[https://www . geeksforgeeks . org/count-of-camel-case-characters-present-in-给定字符串/](https://www.geeksforgeeks.org/count-of-camel-case-characters-present-in-a-given-string/)

给定一个[字符串](https://www.geeksforgeeks.org/string-data-structure/) **S** ，任务是统计给定字符串中出现的[骆驼格字符](https://www.geeksforgeeks.org/camel-case-given-sentence/)的数量。

> camel 大小写字符被定义为给定字符串中大写字符的数量。

**示例:**

> **输入:**S = " ckjkuuyi "
> **输出:** 5
> **说明:**
> 出现的驼色格字符为 U、U、Y、I、I
> 
> **输入:**S = " ABCD "
> T3】输出: 0

**方法:**给定的问题可以通过[遍历给定的字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/) **S** 和[计算那些](https://www.geeksforgeeks.org/c-program-to-count-the-number-of-characters-in-a-file/)的 [ASCII 值](https://www.geeksforgeeks.org/program-print-ascii-value-character/)位于**【65，91】**范围内的字符来解决。检查所有字符后，打印获得的总计数作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to count all the camelcase
// characters in the string S
int countCamelCase(string& S)
{
    // Stores the total count of
    // camelcase characters
    int count = 0;

    // Traverse the string S
    for (int i = 0; S[i]; i++) {

        // If ASCII value of character
        // lies over the range [65, 91]
        // then increment the count
        if (S[i] >= 65 && S[i] <= 91) {
            count++;
        }
    }

    // Print the total count obtained
    cout << count;
}

// Driver Code
int main()
{
    string S = "ckjkUUYII";
    countCamelCase(S);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;

class GFG{

// Function to count all the camelcase
// characters in the string S
static void countCamelCase(String S)
{

    // Stores the total count of
    // camelcase characters
    int count = 0;

    // Traverse the string S
    for(int i = 0; i < S.length(); i++)
    {

        // If ASCII value of character
        // lies over the range [65, 91]
        // then increment the count
        if (S.charAt(i) >= 65 && S.charAt(i) <= 91)
        {
            count++;
        }
    }

    // Print the total count obtained
    System.out.println(count);
}

// Driver code
public static void main(String[] args)
{
    String S = "ckjkUUYII";

    countCamelCase(S);
}
}

// This code is contributed by Potta Lokesh
```

## 蟒蛇 3

```
# Python 3 program for the above approach

# Function to count all the camelcase
# characters in the string S
def countCamelCase(S):

    # Stores the total count of
    # camelcase characters
    count = 0

    # Traverse the string S
    for i in range(len(S)):
        # If ASCII value of character
        # lies over the range [65, 91]
        # then increment the count
        if (ord(S[i]) >= 65 and ord(S[i]) <= 91):
            count += 1

    # Print the total count obtained
    print(count)

# Driver Code
if __name__ == '__main__':
    S = "ckjkUUYII"
    countCamelCase(S)

    # This code is contributed by ipg2016107.
```

**Output:** 

```
5
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)

**替代方法:**想法是使用内置的库函数 [isupper()](https://www.geeksforgeeks.org/isupper-islower-application-c/) 来检查字符是否是大写字母。按照以下步骤解决问题:

*   初始化一个变量，比如说**计数**为 **0** ，它存储给定字符串中大写字母数量的[计数。](https://www.geeksforgeeks.org/count-uppercase-lowercase-special-character-numeric-values/)
*   [遍历字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/)并检查每个字符的**是否为真(s[i])** ，然后增加**计数**。
*   打印**数**作为答案。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to count the number of
// camelcase characters
int countCamelCase(string s)
{
    // Stores the count of all the
    // camelcase characters
    int count = 0;

    // Traverse the string S
    for (int i = 0; s[i]; i++) {

        // Check if the character is
        // an uppercase letter or
        // not using isupper()
        if (isupper(s[i])) {

            // Increment the count
            count++;
        }
    }

    // Print the total count
    cout << count;
}

// Driver Code
int main()
{
    string str = "ckjkUUYII";
    countCamelCase(str);

    return 0;
}
```

**Output:** 

```
5
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)
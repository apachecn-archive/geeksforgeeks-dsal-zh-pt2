# 最大长度的字典最小字符串，由不包含任何重复子串的前 K 个字母组成

> 原文:[https://www . geesforgeks . org/按字典顺序排列的最大长度最小字符串由不包含任何重复子字符串的首字母 k 组成/](https://www.geeksforgeeks.org/lexicographically-smallest-string-of-maximum-length-made-up-of-first-k-alphabets-that-does-not-contain-any-repeating-substring/)

给定一个正整数 **K** ，任务是找到[字典上最小的](https://www.geeksforgeeks.org/lexicographically-smallest-string-obtained-concatenating-array/) [字符串](https://www.geeksforgeeks.org/string-data-structure/)，该字符串可以通过使用第一个 **K** 小写字母生成，使得在生成的字符串中没有长度为**的[子字符串](https://www.geeksforgeeks.org/substring-in-cpp/)重复至少 2 个**。

**示例:**

> **输入:** K = 3
> **输出:** aabacbbcca
> **解释:**
> 在字符串“aabacbbcca”中，长度至少为 2 的所有可能的子串被重复多次。
> 
> **输入:**K = 4
> T3】输出: aabacadbbcbdccdda

**方法:**给定的问题可以基于以下观察来解决:

*   如果**长度为 2** 的所有子串都是唯一的，那么长度大于 2 的所有子串也将是唯一的。
*   因此，最大长度字符串应该[包含长度为 2](https://www.geeksforgeeks.org/program-print-substrings-given-string/) 的所有唯一子字符串，按照字典顺序排列，使得字符串中没有 **3 个连续字符**相同。

按照以下步骤解决问题:

*   初始化一个[字符串](https://www.geeksforgeeks.org/string-data-structure/)，比如说 **S** 作为存储结果字符串的空字符串。
*   使用变量遍历小写字母的所有第一个 **K** 字符，说出 **i** 并执行以下步骤:
    *   将当前字符 **i** 附加到字符串 **S** 中。
    *   从 **(i + 1) <sup>第</sup>个字符**迭代到 **K <sup>第</sup>个字符**，并将字符 **i** 后跟字符 **j** 追加到字符串 **S** 中。
    *   将字符**‘a’**添加到字符串 **S** 中，这样由最后一个字母和第一个字母组成的子字符串也会出现在结果字符串中。
*   完成上述步骤后，打印字符串 **S** 作为结果字符串。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the lexicographically
// smallest string of the first K lower
// case alphabets having unique substrings
void generateString(int K)
{
    // Stores the resultant string
    string s = "";

    // Iterate through all the characters
    for (int i = 97; i < 97 + K; i++) {

        s = s + char(i);

        // Inner Loop for making pairs
        // and adding them into string
        for (int j = i + 1;
             j < 97 + K; j++) {
            s += char(i);
            s += char(j);
        }
    }

    // Adding first character so that
    // substring consisting of the last
    // the first alphabet is present
    s += char(97);

    // Print the resultant string
    cout << s;
}

// Driver Code
int main()
{
    int K = 4;
    generateString(K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to find the lexicographically
// smallest string of the first K lower
// case alphabets having unique substrings
static void generateString(int K)
{

    // Stores the resultant string
    String s = "";

    // Iterate through all the characters
    for(int i = 97; i < 97 + K; i++)
    {
        s = s + (char)(i);

        // Inner Loop for making pairs
        // and adding them into string
        for(int j = i + 1; j < 97 + K; j++)
        {
            s += (char)(i);
            s += (char)(j);
        }
    }

    // Adding first character so that
    // substring consisting of the last
    // the first alphabet is present
    s += (char)(97);

    // Print the resultant string
    System.out.println(s);
}

// Driver code
public static void main(String []args)
{
    int K = 4;

    generateString(K);
}
}

// This code is contributed by sanjoy_62
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to find the lexicographically
// smallest string of the first K lower
// case alphabets having unique substrings
static void generateString(int K)
{

    // Stores the resultant string
    string s = "";

    // Iterate through all the characters
    for(int i = 97; i < 97 + K; i++)
    {
        s = s + (char)(i);

        // Inner Loop for making pairs
        // and adding them into string
        for(int j = i + 1; j < 97 + K; j++)
        {
            s += (char)(i);
            s += (char)(j);
        }
    }

    // Adding first character so that
    // substring consisting of the last
    // the first alphabet is present
    s += (char)(97);

    // Print the resultant string
    Console.Write(s);
}

// Driver Code
public static void Main()
{
    int K = 4;
    generateString(K);
}
}

// This code is contributed by ukasp
```

## 蟒蛇 3

```
# python 3 program for the above approach

# Function to find the lexicographically
# smallest string of the first K lower
# case alphabets having unique substrings
def generateString(K):

    # Stores the resultant string
    s = ""

    # Iterate through all the  characters
    for i in range(97,97 + K,1):
        s = s + chr(i);

        # Inner Loop for making pairs
        # and adding them into string
        for j in range(i + 1,97 + K,1):
            s += chr(i)
            s += chr(j)

    # Adding first character so that
    # substring consisting of the last
    # the first alphabet is present
    s += chr(97)

    # Print the resultant string
    print(s)

# Driver Code
if __name__ == '__main__':
    K = 4
    generateString(K)

    # This code is contributed by SURENDRA_GANGWAR.
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to find the lexicographically
// smallest string of the first K lower
// case alphabets having unique substrings
function generateString(K)
{

    // Stores the resultant string
    var s = "";

    // Iterate through all the characters
    for(var i = 97; i < 97 + K; i++)
    {
        s = s + String.fromCharCode(i);

        // Inner Loop for making pairs
        // and adding them into string
        for(var j = i + 1; j < 97 + K; j++)
        {
            s += String.fromCharCode(i);
            s += String.fromCharCode(j);
        }
    }

    // Adding first character so that
    // substring consisting of the last
    // the first alphabet is present
    s += String.fromCharCode(97);

    // Print the resultant string
    document.write(s);
}

// Driver code
var K = 4;

generateString(K);

// This code is contributed by 29AjayKumar

</script>
```

**Output:** 

```
aabacadbbcbdccdda
```

***时间复杂度:**O(K<sup>2</sup>)*
***辅助空间:** O(K <sup>2</sup> )*
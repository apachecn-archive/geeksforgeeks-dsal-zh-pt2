# 形成给定二进制字符串所需的最小翻转次数，每次翻转都会将所有位更改到其右侧

> 原文:[https://www . geesforgeks . org/minimum-flips-required-to-form-给定-binary-string-凡-flip-change-all-bit-to-it-right-well/](https://www.geeksforgeeks.org/minimum-flips-required-to-form-given-binary-string-where-every-flip-changes-all-bits-to-its-right-as-well/)

给定一个字符串 **S** ，任务是找到将仅由零组成的初始二进制字符串转换为 S 所需的最小翻转次数，其中一个字符的每次翻转也会翻转所有后续字符。
**例:**

> **输入:**S =“01011”
> **输出:** 3
> **解释:**
> 初始字符串–“00000”
> 翻转第二位–“01111”
> 翻转第三位–“01000”
> 翻转第四位–“01011”
> 总翻转数= 3
> **输入:**S =“010101”

**进场:**
为了解决问题，按照以下步骤进行:

*   最初将**‘1’**存放在**币**中。
*   遍历 S，找到第一个出现的 **curr** 。遇到**币**时增加计数。如果 **curr** 为**【1】**，则存储**“0”**，反之亦然。
*   对 s 的整个遍历重复上述步骤。
*   **计数的最终值**给出所需答案。

下面是上述方法的实现。

## C++

```
// C++ program for the above approach
#include<bits/stdc++.h>
using namespace std;

// Function to return the count
// of minimum flips required
int minFlips(string target)
{
    char curr = '1';
    int count = 0;
    for(int i = 0; i < target.length(); i++)
    {

       // If curr occurs in the final string
       if (target[i] == curr)
       {
           count++;

           // Switch curr to '0' if '1'
           // or vice-versa
           curr = (char)(48 + (curr + 1) % 2);
       }
    }
    return count;
}

// Driver Code
int main()
{
    string S = "011000";

    cout << (minFlips(S));
}

// This code is contributed by rock_cool
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.Arrays;

public class GFG {
    // Function to return the count of
    // minimum flips required
    public static int minFlips(String target)
    {

        char curr = '1';
        int count = 0;
        for (int i = 0; i < target.length(); i++) {

            // If curr occurs in the final string
            if (target.charAt(i) == curr) {

                count++;

                // Switch curr to '0' if '1'
                // or vice-versa
                curr = (char)(48 + (curr + 1) % 2);
            }
        }

        return count;
    }

    // Driver Code
    public static void main(String args[])
    {

        String S = "011000";
        System.out.println(minFlips(S));
    }
}
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to return the count
# of minimum flips required
def minFlips(target):

    curr = '1'
    count = 0

    for i in range(len(target)):

        # If curr occurs in the final string
        if (target[i] == curr):
            count += 1

            # Switch curr to '0' if '1'
            # or vice-versa
            curr = chr(48 + (ord(curr) + 1) % 2)

    return count

# Driver Code
if __name__ == "__main__":

    S = "011000"

    print(minFlips(S))

# This code is contributed by chitranayal
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to return the count of
// minimum flips required
public static int minFlips(String target)
{
    char curr = '1';
    int count = 0;
    for(int i = 0; i < target.Length; i++)
    {

       // If curr occurs in the readonly string
       if (target[i] == curr)
       {
           count++;

           // Switch curr to '0' if '1'
           // or vice-versa
           curr = (char)(48 + (curr + 1) % 2);
       }
    }
    return count;
}

// Driver code
public static void Main(String []args)
{
    String S = "011000";
    Console.WriteLine(minFlips(S));
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

    // Javascript program for the above approach

    // Function to return the count
    // of minimum flips required
    function minFlips(target)
    {
        let curr = '1';
        let count = 0;
        for(let i = 0; i < target.length; i++)
        {

           // If curr occurs in the final string
           if (target[i] == curr)
           {
               count++;

               // Switch curr to '0' if '1'
               // or vice-versa
               curr = String.fromCharCode(48 + (curr.charCodeAt() + 1) % 2);
           }
        }
        return count;
    }

    let S = "011000";

    document.write(minFlips(S));

</script>
```

**Output:** 

```
2
```

***时间复杂度:**O(N)*T4】
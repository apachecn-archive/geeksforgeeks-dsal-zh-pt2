# 使密码强大所需的最少字符数

> 原文:[https://www . geeksforgeeks . org/需要最少字符才能制作密码-strong/](https://www.geeksforgeeks.org/minimum-characters-required-to-make-a-password-strong/)

给定表示密码的字符串 **str** ，任务是计算使[密码强](https://www.geeksforgeeks.org/program-check-strength-password/)所需添加的最少字符。
如果密码满足以下条件，则称其为**强**:

*   它至少包含 8 个字符。
*   它至少包含一个数字。
*   它至少包含一个小写字母。
*   它至少包含一个大写字母。
*   它至少包含一个特殊字符，包括**！@#$%^ & *()-+**

**示例:**

> **输入:** str = "Geeksforgeeks"
> **输出:** 2
> **解释:**
> 通过增加一个数字和一个特殊字符，我们可以使密码变得强大。
> **输入:** str = "Geeks1"
> **输出:** 2
> **说明:**
> 需要加上一个特殊字符以及多一个字符，使密码更强。

**方法:**这个问题可以用[正则表达式](https://www.geeksforgeeks.org/write-regular-expressions/)解决:

*   创建[正则表达式](https://www.geeksforgeeks.org/write-regular-expressions/)来检查数字、特殊字符、大写字母和小写字母。
*   编译正则表达式，找到与密码字符串匹配的**。**
*   **增加计数器，比如说**计数**，每当任何正则表达式不匹配时就添加字符。**
*   **在密码字符串中添加**计数**字符后，检查字符串长度是否小于 8。如果是，将差额加到**计数**并打印。**

**下面是上述方法的实现。** 

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java program to find minimum number
// of characters required to be added
// to make a password strong

import java.util.regex.Pattern;
import java.util.regex.Matcher;

class GFG {

    // Function to count minimum
    // number of characters
    static int countCharacters(
        String password)
    {

        int count = 0;

        // Create the patterns to search digit,
        // upper case alphabet, lower case
        // alphabet and special character
        Pattern digit = Pattern.compile("(\\d)");
        Pattern upper = Pattern.compile("([A-Z])");
        Pattern lower = Pattern.compile("([a-z])");
        Pattern spChar = Pattern.compile("(\\W)");

        // Search the above patterns in password.
        Matcher Digit = digit.matcher(password);
        Matcher Upper = upper.matcher(password);
        Matcher Lower = lower.matcher(password);
        Matcher Special = spChar.matcher(password);

        // If no digits are present
        if (!Digit.find()) {
            count++;
        }
        // If no upper case alphabet is present
        if (!Upper.find()) {
            count++;
        }
        // If no lower case alphabet is present
        if (!Lower.find()) {
            count++;
        }
        // If no special character is is present
        if (!Special.find()) {
            count++;
        }

        // Check if the string length after adding
        // the required characters is less than 8
        if ((count + password.length()) < 8) {

            // Add the number of
            // characters to be added
            count = count + 8
                    - (count + password.length());
        }

        return count;
    }

    // Driver Code
    public static void main(String args[])
    {

        String password1 = "Geeksforgeeks";
        System.out.println(
            countCharacters(password1));

        String password2 = "Geeks1";
        System.out.println(
            countCharacters(password2));
    }
}
```

## **蟒蛇 3**

```
# Python3 program to find
# minimum number of characters
# required to be added to make
# a password strong
import re

# Function to count minimum
# number of characters
def countCharacters(password):

    count = 0

    # Create the patterns to search digit,
    # upper case alphabet, lower case
    # alphabet and special character
    digit = re.compile("(\\d)")
    upper = re.compile("([A-Z])")
    lower = re.compile("([a-z])")
    spChar = re.compile("(\\W)")

    # Search the above patterns
    # in password.

    # If no digits are present
    if(not re.search(digit,
                     password)):
        count += 1

    # If no upper case alphabet
    # is present
    if(not re.search(upper,
                     password)):
        count += 1

    # If no lower case alphabet
    # is present
    if(not re.search(lower,
                     password)):
        count += 1

    # If no special character
    # is is present
    if(not re.search(spChar,
                     password)):
        count += 1

    # Check if the string length
    # after adding the required
    # characters is less than 8
    if((count +
        len(password)) < 8):

        # Add the number of
        # characters to be added
        count = count + 8 - (count +
                             len(password))

    return count

# Driver code
password1 = "Geeksforgeeks"
print(countCharacters(password1))

password2 = "Geeks1"
print(countCharacters(password2))

# This code is contributed by avanitrachhadiya2155
```

****Output:** 

```
2
2

```**
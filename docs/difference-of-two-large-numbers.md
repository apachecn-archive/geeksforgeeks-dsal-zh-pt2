# 两个大数之差

> 原文:[https://www . geesforgeks . org/两个大数之差/](https://www.geeksforgeeks.org/difference-of-two-large-numbers/)

给定两个数字作为字符串。这些数字可能非常大(可能不适合 long long int)，任务是找出这两个数字之间的差异。

**示例:**

```
Input : str1 = "11443333311111111100", 
        str2 =     "1144422222221111"
Output : 11442188888888889989

Input :str1 = "122387876566565674",
       str2 =     "31435454654554"
Output : 122356441111911120
```

这只是基于学校的数学。我们从头到尾遍历这两个字符串，一个接一个地减去数字。

1.  反转两个字符串。
2.  继续从第 0 个索引(在反向字符串中)中一个接一个地减去数字到一个较小字符串的末尾，如果结果的末尾是正数，则追加 diff。如果差值(diff)为负，则加 10，并记录进位为 1。如果差值为正，则进位为 0。
3.  最后，扭转结果。

下面是上述想法的实现:

## C++

```
// C++ program to find difference of two large numbers.
#include <bits/stdc++.h>
using namespace std;

// Returns true if str1 is smaller than str2.
bool isSmaller(string str1, string str2)
{
    // Calculate lengths of both string
    int n1 = str1.length(), n2 = str2.length();

    if (n1 < n2)
        return true;
    if (n2 < n1)
        return false;

    for (int i = 0; i < n1; i++)
        if (str1[i] < str2[i])
            return true;
        else if (str1[i] > str2[i])
            return false;

    return false;
}

// Function for find difference of larger numbers
string findDiff(string str1, string str2)
{
    // Before proceeding further, make sure str1
    // is not smaller
    if (isSmaller(str1, str2))
        swap(str1, str2);

    // Take an empty string for storing result
    string str = "";

    // Calculate length of both string
    int n1 = str1.length(), n2 = str2.length();

    // Reverse both of strings
    reverse(str1.begin(), str1.end());
    reverse(str2.begin(), str2.end());

    int carry = 0;

    // Run loop till small string length
    // and subtract digit of str1 to str2
    for (int i = 0; i < n2; i++) {
        // Do school mathematics, compute difference of
        // current digits

        int sub
            = ((str1[i] - '0') - (str2[i] - '0') - carry);

        // If subtraction is less then zero
        // we add then we add 10 into sub and
        // take carry as 1 for calculating next step
        if (sub < 0) {
            sub = sub + 10;
            carry = 1;
        }
        else
            carry = 0;

        str.push_back(sub + '0');
    }

    // subtract remaining digits of larger number
    for (int i = n2; i < n1; i++) {
        int sub = ((str1[i] - '0') - carry);

        // if the sub value is -ve, then make it positive
        if (sub < 0) {
            sub = sub + 10;
            carry = 1;
        }
        else
            carry = 0;

        str.push_back(sub + '0');
    }

    // reverse resultant string
    reverse(str.begin(), str.end());

    return str;
}

// Driver code
int main()
{
    string str1 = "978";
    string str2 = "12977";

    // Function call
    cout << findDiff(str1, str2) << endl;

    string s1 = "100";
    string s2 = "1000000";

    // Function call
    cout << findDiff(s1, s2);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find difference of two large numbers.
import java.util.*;

class GFG {

    // Returns true if str1 is smaller than str2.
    static boolean isSmaller(String str1, String str2)
    {
        // Calculate lengths of both string
        int n1 = str1.length(), n2 = str2.length();
        if (n1 < n2)
            return true;
        if (n2 < n1)
            return false;

        for (int i = 0; i < n1; i++)
            if (str1.charAt(i) < str2.charAt(i))
                return true;
            else if (str1.charAt(i) > str2.charAt(i))
                return false;

        return false;
    }

    // Function for find difference of larger numbers
    static String findDiff(String str1, String str2)
    {
        // Before proceeding further, make sure str1
        // is not smaller
        if (isSmaller(str1, str2)) {
            String t = str1;
            str1 = str2;
            str2 = t;
        }

        // Take an empty string for storing result
        String str = "";

        // Calculate length of both string
        int n1 = str1.length(), n2 = str2.length();

        // Reverse both of strings
        str1 = new StringBuilder(str1).reverse().toString();
        str2 = new StringBuilder(str2).reverse().toString();

        int carry = 0;

        // Run loop till small string length
        // and subtract digit of str1 to str2
        for (int i = 0; i < n2; i++) {
            // Do school mathematics, compute difference of
            // current digits
            int sub
                = ((int)(str1.charAt(i) - '0')
                   - (int)(str2.charAt(i) - '0') - carry);

            // If subtraction is less then zero
            // we add then we add 10 into sub and
            // take carry as 1 for calculating next step
            if (sub < 0) {
                sub = sub + 10;
                carry = 1;
            }
            else
                carry = 0;

            str += (char)(sub + '0');
        }

        // subtract remaining digits of larger number
        for (int i = n2; i < n1; i++) {
            int sub = ((int)(str1.charAt(i) - '0') - carry);

            // if the sub value is -ve, then make it
            // positive
            if (sub < 0) {
                sub = sub + 10;
                carry = 1;
            }
            else
                carry = 0;

            str += (char)(sub + '0');
        }

        // reverse resultant string
        return new StringBuilder(str).reverse().toString();
    }

    // Driver code
    public static void main(String[] args)
    {
        String str1 = "978";
        String str2 = "12977";

        // Function call
        System.out.println(findDiff(str1, str2));

        String s1 = "100";
        String s2 = "1000000";

        // Function call
        System.out.println(findDiff(s1, s2));
    }
}

// This code is contributed by mits
```

## 蟒蛇 3

```
# Python 3 program to find difference of two large numbers.

# Returns true if str1 is smaller than str2.

def isSmaller(str1, str2):

    # Calculate lengths of both string
    n1 = len(str1)
    n2 = len(str2)

    if (n1 < n2):
        return True
    if (n2 < n1):
        return False

    for i in range(n1):
        if (str1[i] < str2[i]):
            return True
        elif (str1[i] > str2[i]):
            return False

    return False

# Function for find difference of larger numbers

def findDiff(str1, str2):

    # Before proceeding further, make sure str1
    # is not smaller
    if (isSmaller(str1, str2)):
        temp = str1
        str1 = str2
        str2 = temp

    # Take an empty string for storing result
    str3 = ""

    # Calculate length of both string
    n1 = len(str1)
    n2 = len(str2)

    # Reverse both of strings
    str1 = str1[::-1]
    str2 = str2[::-1]

    carry = 0

    # Run loop till small string length
    # and subtract digit of str1 to str2
    for i in range(n2):

        # Do school mathematics, compute difference of
        # current digits

        sub = ((ord(str1[i])-ord('0'))-(ord(str2[i])-ord('0'))-carry)

        # If subtraction is less then zero
        # we add then we add 10 into sub and
        # take carry as 1 for calculating next step
        if (sub < 0):

            sub = sub + 10
            carry = 1

        else:
            carry = 0

        str3 = str3+str(sub)

    # subtract remaining digits of larger number
    for i in range(n2, n1):

        sub = ((ord(str1[i])-ord('0')) - carry)

        # if the sub value is -ve, then make it positive
        if (sub < 0):

            sub = sub + 10
            carry = 1

        else:
            carry = 0

        str3 = str3+str(sub)

    # reverse resultant string
    str3 = str3[::-1]

    return str3

# Driver code
if __name__ == "__main__":
    str1 = "978"
    str2 = "12977"

    # Function call
    print(findDiff(str1, str2))

    s1 = "100"
    s2 = "1000000"

    # Function call
    print(findDiff(s1, s2))

# This code is contributed by ChitraNayal
```

## C#

```
// C# program to find difference of two large numbers.
using System;
using System.Collections;

class GFG {

    // Returns true if str1 is smaller than str2.
    static bool isSmaller(string str1, string str2)
    {
        // Calculate lengths of both string
        int n1 = str1.Length, n2 = str2.Length;
        if (n1 < n2)
            return true;
        if (n2 < n1)
            return false;

        for (int i = 0; i < n1; i++)
            if (str1[i] < str2[i])
                return true;
            else if (str1[i] > str2[i])
                return false;

        return false;
    }

    // Function for find difference of larger numbers
    static string findDiff(string str1, string str2)
    {
        // Before proceeding further, make sure str1
        // is not smaller
        if (isSmaller(str1, str2)) {
            string t = str1;
            str1 = str2;
            str2 = t;
        }

        // Take an empty string for storing result
        string str = "";

        // Calculate length of both string
        int n1 = str1.Length, n2 = str2.Length;

        // Reverse both of strings
        char[] ch1 = str1.ToCharArray();
        Array.Reverse(ch1);
        str1 = new string(ch1);
        char[] ch2 = str2.ToCharArray();
        Array.Reverse(ch2);
        str2 = new string(ch2);

        int carry = 0;

        // Run loop till small string length
        // and subtract digit of str1 to str2
        for (int i = 0; i < n2; i++) {
            // Do school mathematics, compute difference of
            // current digits
            int sub = ((int)(str1[i] - '0')
                       - (int)(str2[i] - '0') - carry);

            // If subtraction is less then zero
            // we add then we add 10 into sub and
            // take carry as 1 for calculating next step
            if (sub < 0) {
                sub = sub + 10;
                carry = 1;
            }
            else
                carry = 0;

            str += (char)(sub + '0');
        }

        // subtract remaining digits of larger number
        for (int i = n2; i < n1; i++) {
            int sub = ((int)(str1[i] - '0') - carry);

            // if the sub value is -ve, then make it
            // positive
            if (sub < 0) {
                sub = sub + 10;
                carry = 1;
            }
            else
                carry = 0;

            str += (char)(sub + '0');
        }

        // reverse resultant string
        char[] ch3 = str.ToCharArray();
        Array.Reverse(ch3);
        return new string(ch3);
    }

    // Driver code
    public static void Main()
    {
        string str1 = "978";
        string str2 = "12977";

        // Function call
        Console.WriteLine(findDiff(str1, str2));

        string s1 = "100";
        string s2 = "1000000";

        // Function call
        Console.WriteLine(findDiff(s1, s2));
    }
}

// This code is contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find difference of two large numbers.

// Returns true if str1 is smaller than str2.
function isSmaller($str1, $str2)
{
    // Calculate lengths of both string
    $n1 = strlen($str1);
    $n2 = strlen($str2);

    if ($n1 < $n2)
    return true;
    if ($n2 < $n1)
    return false;

    for ($i=0; $i<$n1; $i++)
    if ($str1[$i] < $str2[$i])
        return true;
    else if ($str1[$i] > $str2[$i])
        return false;

    return false;
}

// Function for find difference of larger numbers
function findDiff($str1, $str2)
{
    // Before proceeding further, make sure str1
    // is not smaller
    if (isSmaller($str1, $str2)){
        $t=$str1;
        $str1=$str2;
        $str2=$t;
    }

    // Take an empty string for storing result
    $str = "";

    // Calculate length of both string
    $n1 = strlen($str1);
    $n2 = strlen($str2);

    // Reverse both of strings
    $str1=strrev($str1);
    $str2=strrev($str2);

    $carry = 0;

    // Run loop till small string length
    // and subtract digit of str1 to str2
    for ($i=0; $i<$n2; $i++)
    {
        // Do school mathematics, compute difference of
        // current digits

        $sub=((ord($str1[$i])-ord('0'))-(ord($str2[$i])-ord('0'))-$carry);

        // If subtraction is less then zero
        // we add then we add 10 into sub and
        // take carry as 1 for calculating next step
        if ($sub < 0)
        {
            $sub = $sub + 10;
            $carry = 1;
        }
        else
            $carry = 0;

        $str.=chr($sub+48);
    }

    // subtract remaining digits of larger number
    for ($i=$n2; $i<$n1; $i++)
    {
        $sub = ((ord($str1[$i])-ord('0')) - $carry);

        // if the sub value is -ve, then make it positive
        if ($sub < 0)
        {
            $sub = $sub + 10;
            $carry = 1;
        }
        else
            $carry = 0;

        $str.=chr($sub+48);
    }

    // reverse resultant string
    $str=strrev($str);

    return $str;
}

// Driver code

    $str1 = "978";
    $str2 = "12977";

    // Function call
    echo findDiff($str1, $str2)."\n";

    $s1 = "100";
    $s2 = "1000000";

    // Function call
    echo findDiff($s1,$s2);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// Javascript program to find difference
// of two large numbers.

    // Returns true if str1 is smaller than str2.
    function isSmaller(str1,str2)
    {
        // Calculate lengths of both string
        let n1 = str1.length, n2 = str2.length;
        if (n1 < n2)
            return true;
        if (n2 < n1)
            return false;

        for (let i = 0; i < n1; i++)
            if (str1[i] < str2[i])
                return true;
            else if (str1[i] > str2[i])
                return false;

        return false;
    }

     // Function for find difference
     // of larger numbers
    function findDiff(str1,str2)
    {
        // Before proceeding further,
        // make sure str1
        // is not smaller
        if (isSmaller(str1, str2)) {
            let t = str1;
            str1 = str2;
            str2 = t;
        }

        // Take an empty string for storing result
        let str = "";

        // Calculate length of both string
        let n1 = str1.length, n2 = str2.length;

        // Reverse both of strings
        str1 = str1.split("").reverse().join("")
        str2 = str2.split("").reverse().join("")

        let carry = 0;

        // Run loop till small string length
        // and subtract digit of str1 to str2
        for (let i = 0; i < n2; i++)
        {
            // Do school mathematics,
            // compute difference of
            // current digits
            let sub
                = ((str1[i].charCodeAt(0) -
                '0'.charCodeAt(0))
                   - (str2[i].charCodeAt(0) -
                   '0'.charCodeAt(0)) - carry);

            // If subtraction is less then zero
            // we add then we add 10 into sub and
            // take carry as 1 for calculating next step
            if (sub < 0) {
                sub = sub + 10;
                carry = 1;
            }
            else
                carry = 0;

            str += String.fromCharCode(sub +
            '0'.charCodeAt(0));
        }

        // subtract remaining digits of larger number
        for (let i = n2; i < n1; i++) {
            let sub = ((str1[i].charCodeAt(0) -
            '0'.charCodeAt(0)) - carry);

            // if the sub value is -ve, then make it
            // positive
            if (sub < 0) {
                sub = sub + 10;
                carry = 1;
            }
            else
                carry = 0;

            str += String.fromCharCode(sub +
            '0'.charCodeAt(0));
        }

        // reverse resultant string
        return str.split("").reverse().join("")
    }

    // Driver code

    let str1 = "978";
    let str2 = "12977";

    document.write(findDiff(str1, str2)+"<br>");

    let s1 = "100";
    let s2 = "1000000";
    document.write(findDiff(s1, s2)+"<br>");

    // This code is contributed by rag2127

</script>
```

**Output**

```
11999
0999900
```

**时间复杂度:** O(n1 + n2)

**辅助空间:** O(max(n1，n2))
**优化解:**
我们可以通过从末尾遍历来避免前两个字符串反向操作。

下面是优化后的解决方案。

## C++

```
// C++ program to find difference of two large numbers.
#include <bits/stdc++.h>
using namespace std;

// Returns true if str1 is smaller than str2,
// else false.
bool isSmaller(string str1, string str2)
{
    // Calculate lengths of both string
    int n1 = str1.length(), n2 = str2.length();

    if (n1 < n2)
        return true;
    if (n2 < n1)
        return false;

    for (int i = 0; i < n1; i++) {
        if (str1[i] < str2[i])
            return true;
        else if (str1[i] > str2[i])
            return false;
    }
    return false;
}

// Function for finding difference of larger numbers
string findDiff(string str1, string str2)
{
    // Before proceeding further, make sure str1
    // is not smaller
    if (isSmaller(str1, str2))
        swap(str1, str2);

    // Take an empty string for storing result
    string str = "";

    // Calculate lengths of both string
    int n1 = str1.length(), n2 = str2.length();
    int diff = n1 - n2;

    // Initially take carry zero
    int carry = 0;

    // Traverse from end of both strings
    for (int i = n2 - 1; i >= 0; i--) {
        // Do school mathematics, compute difference of
        // current digits and carry
        int sub = ((str1[i + diff] - '0') - (str2[i] - '0')
                   - carry);
        if (sub < 0) {
            sub = sub + 10;
            carry = 1;
        }
        else
            carry = 0;

        str.push_back(sub + '0');
    }

    // subtract remaining digits of str1[]
    for (int i = n1 - n2 - 1; i >= 0; i--) {
        if (str1[i] == '0' && carry) {
            str.push_back('9');
            continue;
        }
        int sub = ((str1[i] - '0') - carry);
        if (i > 0 || sub > 0) // remove preceding 0's
            str.push_back(sub + '0');
        carry = 0;
    }

    // reverse resultant string
    reverse(str.begin(), str.end());

    return str;
}

// Driver code
int main()
{
    string str1 = "88";
    string str2 = "1079";

    // Function call
    cout << findDiff(str1, str2);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find difference of two large numbers.

class GFG {

    // Returns true if str1 is smaller than str2,
    // else false.
    static boolean isSmaller(String str1, String str2)
    {
        // Calculate lengths of both string
        int n1 = str1.length(), n2 = str2.length();

        if (n1 < n2)
            return true;
        if (n2 < n1)
            return false;

        for (int i = 0; i < n1; i++) {
            if (str1.charAt(i) < str2.charAt(i))
                return true;
            else if (str1.charAt(i) > str2.charAt(i))
                return false;
        }
        return false;
    }

    // Function for finding difference of larger numbers
    static String findDiff(String str1, String str2)
    {
        // Before proceeding further, make sure str1
        // is not smaller
        if (isSmaller(str1, str2)) {
            String t = str1;
            str1 = str2;
            str2 = t;
        }

        // Take an empty string for storing result
        String str = "";

        // Calculate lengths of both string
        int n1 = str1.length(), n2 = str2.length();
        int diff = n1 - n2;

        // Initially take carry zero
        int carry = 0;

        // Traverse from end of both strings
        for (int i = n2 - 1; i >= 0; i--) {
            // Do school mathematics, compute difference of
            // current digits and carry
            int sub
                = (((int)str1.charAt(i + diff) - (int)'0')
                   - ((int)str2.charAt(i) - (int)'0')
                   - carry);
            if (sub < 0) {
                sub = sub + 10;
                carry = 1;
            }
            else
                carry = 0;

            str += String.valueOf(sub);
        }

        // subtract remaining digits of str1[]
        for (int i = n1 - n2 - 1; i >= 0; i--) {
            if (str1.charAt(i) == '0' && carry > 0) {
                str += "9";
                continue;
            }
            int sub = (((int)str1.charAt(i) - (int)'0')
                       - carry);
            if (i > 0 || sub > 0) // remove preceding 0's
                str += String.valueOf(sub);
            carry = 0;
        }

        // reverse resultant string
        return new StringBuilder(str).reverse().toString();
    }

    // Driver code
    public static void main(String[] args)
    {
        String str1 = "88";
        String str2 = "1079";

        // Function call
        System.out.println(findDiff(str1, str2));
    }
}

// This code is contributed by mits
```

## 蟒蛇 3

```
# Python3 program to find difference
# of two large numbers.

# Returns true if str1 is smaller than
# str2, else false.
def isSmaller(str1, str2):

    # Calculate lengths of both string
    n1 = len(str1)
    n2 = len(str2)

    if (n1 < n2):
        return True
    if (n2 < n1):
        return False

    for i in range(n1):
        if (str1[i] < str2[i]):
            return True
        elif (str1[i] > str2[i]):
            return False

    return False

# Function for finding difference
# of larger numbers
def findDiff(str1, str2):

    # Before proceeding further,
    # make sure str1 is not smaller
    if (isSmaller(str1, str2)):
        str1, str2 = str2, str1

    # Take an empty string for
    # storing result
    Str = ""

    # Calculate lengths of both string
    n1 = len(str1)
    n2 = len(str2)
    diff = n1 - n2

    # Initially take carry zero
    carry = 0

    # Traverse from end of both strings
    for i in range(n2 - 1, -1, -1):

        # Do school mathematics, compute
        # difference of current digits
        # and carry
        sub = ((ord(str1[i + diff]) - ord('0')) -
               (ord(str2[i]) - ord('0')) - carry)

        if (sub < 0):
            sub += 10
            carry = 1
        else:
            carry = 0

        Str += chr(sub + ord('0'))

    # Subtract remaining digits of str1[]
    for i in range(n1 - n2 - 1, -1, -1):
        if (str1[i] == '0' and carry):
            Str += '9'
            continue

        sub = (ord(str1[i]) - ord('0')) - carry

        # Remove preceding 0's
        if (i > 0 or sub > 0):
            Str += chr(sub + ord('0'))

        carry = 0

    # Reverse resultant string
    Str = Str[::-1]

    return Str

# Driver code
str1 = "88"
str2 = "1079"

# Function call
print(findDiff(str1, str2))

# This code is contributed by avanitrachhadiya2155
```

## C#

```
// C# program to find difference of
// two large numbers.
using System;

class GFG {

    // Returns true if str1 is smaller
    // than str2, else false.
    static bool isSmaller(string str1, string str2)
    {
        // Calculate lengths of both string
        int n1 = str1.Length, n2 = str2.Length;

        if (n1 < n2)
            return true;
        if (n2 < n1)
            return false;

        for (int i = 0; i < n1; i++) {
            if (str1[i] < str2[i])
                return true;
            else if (str1[i] > str2[i])
                return false;
        }
        return false;
    }

    // Function for finding difference of
    // larger numbers
    static string findDiff(string str1, string str2)
    {
        // Before proceeding further,
        // make sure str1 is not smaller
        if (isSmaller(str1, str2)) {
            string t = str1;
            str1 = str2;
            str2 = t;
        }

        // Take an empty string for
        // storing result
        String str = "";

        // Calculate lengths of both string
        int n1 = str1.Length, n2 = str2.Length;
        int diff = n1 - n2;

        // Initially take carry zero
        int carry = 0;

        // Traverse from end of both strings
        for (int i = n2 - 1; i >= 0; i--) {
            // Do school mathematics, compute
            // difference of current digits and carry
            int sub = (((int)str1[i + diff] - (int)'0')
                       - ((int)str2[i] - (int)'0') - carry);
            if (sub < 0) {
                sub = sub + 10;
                carry = 1;
            }
            else
                carry = 0;

            str += sub.ToString();
        }

        // subtract remaining digits of str1[]
        for (int i = n1 - n2 - 1; i >= 0; i--) {
            if (str1[i] == '0' && carry > 0) {
                str += "9";
                continue;
            }
            int sub = (((int)str1[i] - (int)'0') - carry);
            if (i > 0 || sub > 0) // remove preceding 0's
                str += sub.ToString();
            carry = 0;
        }

        // reverse resultant string
        char[] aa = str.ToCharArray();
        Array.Reverse(aa);
        return new string(aa);
    }

    // Driver code
    public static void Main()
    {
        String str1 = "88";
        String str2 = "1079";

        // Function call
        Console.WriteLine(findDiff(str1, str2));
    }
}

// This code is contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find difference of two
// large numbers.

// Returns true if str1 is smaller than
// str2, else false.
function isSmaller($str1, $str2)
{
    // Calculate lengths of both string
    $n1 = strlen($str1);
    $n2 = strlen($str2);

    if ($n1 < $n2)
        return true;
    if ($n2 < $n1)
        return false;

    for ($i = 0; $i < $n1; $i++)
    {
        if ($str1[$i] < $str2[$i])
            return true;
        else if ($str1[$i] > $str2[$i])
            return false;
    }
    return false;
}

// Function for finding difference
// of larger numbers
function findDiff($str1, $str2)
{
    // Before proceeding further, make
    // sure str1 is not smaller
    if (isSmaller($str1, $str2))
    {
        $t = $str1;
        $str1 = $str2;
        $str2 = $t;
    }

    // Take an empty string for storing result
    $str = "";

    // Calculate lengths of both string
    $n1 = strlen($str1);
    $n2 = strlen($str2);
    $diff = $n1 - $n2;

    // Initially take carry zero
    $carry = 0;

    // Traverse from end of both strings
    for ($i = $n2 - 1; $i >= 0; $i--)
    {
        // Do school mathematics, compute
        // difference of current digits and carry
        $sub = ((ord($str1[$i + $diff]) - ord('0')) -
                (ord($str2[$i]) - ord('0')) - $carry);
        if ($sub < 0)
        {
            $sub = $sub + 10;
            $carry = 1;
        }
        else
            $carry = 0;

        $str.=chr($sub + ord("0"));
    }

    // subtract remaining digits of str1[]
    for ($i = $n1 - $n2 - 1; $i >= 0; $i--)
    {
        if ($str1[$i] == '0' && $carry > 0)
        {
            $str.="9";
            continue;
        }
        $sub = (ord($str1[$i]) - ord('0') - $carry);
        if ($i > 0 || $sub > 0) // remove preceding 0's
            $str.=chr($sub + ord("0"));
        $carry = 0;

    }

    // reverse resultant string
    return strrev($str);

}

// Driver code
$str1 = "88";
$str2 = "1079";

// Function call
print(findDiff($str1, $str2));

// This code is contributed by chandan_jnu
?>
```

## java 描述语言

```
<script>

    // JavaScript program to find difference
    // of two large numbers.

    // Returns true if str1 is smaller
    // than str2, else false.
    function isSmaller(str1, str2)
    {
        // Calculate lengths of both string
        let n1 = str1.length, n2 = str2.length;

        if (n1 < n2)
            return true;
        if (n2 < n1)
            return false;

        for (let i = 0; i < n1; i++) {
            if (str1[i].charCodeAt() < str2[i].charCodeAt())
                return true;
            else if (str1[i].charCodeAt() > str2[i].charCodeAt())
                return false;
        }
        return false;
    }

    // Function for finding difference of
    // larger numbers
    function findDiff(str1, str2)
    {
        // Before proceeding further,
        // make sure str1 is not smaller
        if (isSmaller(str1, str2)) {
            let t = str1;
            str1 = str2;
            str2 = t;
        }

        // Take an empty string for
        // storing result
        let str = "";

        // Calculate lengths of both string
        let n1 = str1.length, n2 = str2.length;
        let diff = n1 - n2;

        // Initially take carry zero
        let carry = 0;

        // Traverse from end of both strings
        for (let i = n2 - 1; i >= 0; i--) {
            // Do school mathematics, compute
            // difference of current digits and carry
            let sub = ((str1[i + diff].charCodeAt() -
                       '0'.charCodeAt())
                   - (str2[i].charCodeAt() -
                     '0'.charCodeAt()) - carry);
            if (sub < 0) {
                sub = sub + 10;
                carry = 1;
            }
            else
                carry = 0;

            str += sub.toString();
        }

        // subtract remaining digits of str1[]
        for (let i = n1 - n2 - 1; i >= 0; i--) {
            if (str1[i] == '0' && carry > 0) {
                str += "9";
                continue;
            }
            let sub = ((str1[i].charCodeAt() -
                       '0'.charCodeAt()) - carry);
            if (i > 0 || sub > 0) // remove preceding 0's
                str += sub.toString();
            carry = 0;
        }

        // reverse resultant string
        let aa = str.split('');
        aa.reverse();
        return aa.join("");
    }

    let str1 = "88";
    let str2 = "1079";

    // Function call
    document.write(findDiff(str1, str2));

</script>
```

**Output**

```
991
```

**时间复杂度:** O(n1 + n2)

**辅助空间:** O(最大值(n1，n2))

本文由 [**丹麦语 _RAZA**](https://www.facebook.com/danish.raza.98096721) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。
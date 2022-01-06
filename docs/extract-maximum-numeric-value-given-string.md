# 从给定字符串中提取最大数值|设置 1(一般方法)

> 原文:[https://www . geesforgeks . org/extract-maximum-numeric-value-given-string/](https://www.geeksforgeeks.org/extract-maximum-numeric-value-given-string/)

给定一个字母数字字符串，从该字符串中提取最大数值。字母只会用小写字母。
这里讨论了一种解决问题的方法，其他使用正则表达式的方法在[集合 2](https://www.geeksforgeeks.org/extract-maximum-numeric-value-given-string-set-2-regex-approach/)
**中给出示例:**

```
Input : 100klh564abc365bg
Output : 564
Maximum numeric value among 100, 564 
and 365 is 564.

Input : abchsd0sdhs
Output : 0
```

它的解决方案很简单，即开始遍历字符串并执行两个操作:

1.  如果当前索引中有一个数值，那么将其转换成一个整数

    ```
     num = num*10 + (str[i]-'0') 
    ```

2.  否则，更新最大值并重置 num = 0。

最后返回最大值。

## C++

```
// C++ program to extract the maximum value
#include<bits/stdc++.h>
using namespace std;

// Function to extract the maximum value
int extractMaximum(string str)
{
    int num = 0, res = 0;

    // Start traversing the given string
    for (int i = 0; i<str.length(); i++)
    {
        // If a numeric value comes, start converting
        // it into an integer till there are consecutive
        // numeric digits
        if (str[i] >= '0' && str[i] <= '9')
            num = num * 10 + (str[i]-'0');

        // Update maximum value
        else
        {
            res = max(res, num);

            // Reset the number
            num = 0;
        }
    }

    // Return maximum value
    return max(res, num);
}

// Driver program
int main()
{
    string str = "100klh564abc365bg";
    cout << extractMaximum(str);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to extract the maximum value

class GFG 
{
    // Method to extract the maximum value
    static int extractMaximum(String str)
    {
        int num = 0, res = 0;

        // Start traversing the given string
        for (int i = 0; i<str.length(); i++)
        {
            // If a numeric value comes, start converting
            // it into an integer till there are consecutive
            // numeric digits
            if (Character.isDigit(str.charAt(i)))
                num = num * 10 + (str.charAt(i)-'0');

            // Update maximum value
            else
            {
                res = Math.max(res, num);

                // Reset the number
                num = 0;
            }
        }

        // Return maximum value
        return Math.max(res, num);
    }

    // Driver method
    public static void main(String[] args) 
    {
        String str = "100klh564abc365bg";
        System.out.println(extractMaximum(str));
    }    
}
```

## 蟒蛇 3

```
# Python 3 program to extract
# the maximum value
def extractMaximum(ss):
    num, res = 0, 0

    # start traversing the given string 
    for i in range(len(ss)):

        if ss[i] >= "0" and ss[i] <= "9":
            num = num * 10 + int(int(ss[i]) - 0)
        else:
            res = max(res, num)
            num = 0

    return max(res, num)

# Driver Code
ss = "100klh564abc365bg"

print(extractMaximum(ss))

# This code is contributed
# by mohit kumar 29
```

## C#

```
// C# program to extract the maximum value
using System;

class GFG {

    // Method to extract the maximum value
    static int extractMaximum(String str)
    {
        int num = 0, res = 0;

        // Start traversing the given string
        for (int i = 0; i < str.Length; i++)
        {

            // If a numeric value comes, start 
            // converting it into an integer 
            // till there are consecutive
            // numeric digits
            if (char.IsDigit(str[i]))
                num = num * 10 + (str[i]-'0');

            // Update maximum value
            else
            {
                res = Math.Max(res, num);

                // Reset the number
                num = 0;
            }
        }

        // Return maximum value
        return Math.Max(res, num);
    }

    // Driver method
    public static void Main() 
    {
        String str = "100klh564abc365bg";

        Console.Write(extractMaximum(str));
    } 
}

// This code is contributed by nitin mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to extract the maximum value

// Function to extract the maximum value
function extractMaximum($str)
{
    $num = 0;
    $res = 0;

    // Start traversing the given string
    for ($i = 0; $i<strlen($str); $i++)
    {

        // If a numeric value comes,
        // start converting it into 
        // an integer till there are
        // consecutive numeric digits
        if ($str[$i] >= '0' && $str[$i] <= '9')
            $num = $num * 10 + ($str[$i]-'0');

        // Update maximum value
        else
        {
            $res = max($res, $num);

            // Reset the number
            $num = 0;
        }
    }

    // Return maximum value
    return max($res, $num);
}

    // Driver Code
    $str = "100klh564abc365bg";
    echo extractMaximum($str);

// This code is contributed by nitin mittal.
?>
```

## java 描述语言

```
<script>

// JavaScript program to extract
// the maximum value

// Method to extract the maximum value
function extractMaximum(str)
{
    var num = 0, res = 0;

    // Start traversing the given string
    for (i = 0; i<str.length; i++)
    {
        // If a numeric value comes,
        // start converting
        // it into an integer till
        // there are consecutive
        // numeric digits
        if (isDigit(str.charAt(i)))
            num = num * 10 + 
            (str.charAt(i).charCodeAt(0)-
            '0'.charCodeAt(0));

        // Update maximum value
        else
        {
            res = Math.max(res, num);

            // Reset the number
            num = 0;
        }
    }

    // Return maximum value
    return Math.max(res, num);
}

function isDigit(c) {
      return c >= '0' && c <= '9';
    }

// Driver method
var str = "100klh564abc365bg";
document.write(extractMaximum(str));

// This code is contributed by Amit Katiyar

</script>
```

**输出:**

```
564
```

但是在大数的情况下，由于 C 和 C++中的整数范围，上面的程序将无法工作。因此，为了处理大数的情况，我们必须将每个数值作为一个单独的字符串，然后找到最大值。

```

1) Start traversing the given string.
   Continue traversing if there are any 
   leading zeroes or any lowercase character.
  b) Form a string of integer values.
  c) Update the maximum string.
    i) If the maximum string and current 
       string are having equal lengths then 
       on the basis of the first unmatched 
       value return maximum string.
    ii) If both are having different lengths 
        then return the string with greater 
        length.

2) Return maximum string.
```

## C++

```
// C++ program for above implementation
#include<bits/stdc++.h>
using namespace std;

// Utility function to find maximum string
string maximumNum(string curr_num, string res)
{
    int len1 = curr_num.length();
    int len2 = res.length();

    // If both having equal lengths
    if (len1 == len2)
    {
        // Reach first unmatched character / value
        int i = 0;
        while (curr_num[i]== res[i])
            i++;

        // Return string with maximum value
        if (curr_num[i] < res[i])
            return res;
        else
            return curr_num;
    }

    // If different lengths
    // return string with maximum length
    return len1 < len2 ? res: curr_num;
}

// Function to extract the maximum value
string extractMaximum(string str)
{
    int n = str.length();
    string curr_num ="";
    string res;

    // Start traversing the string
    for (int i = 0; i<n; i++)
    {
        // Ignore leading zeroes
        while (i<n && str[i]=='0')
            i++;

        // Store numeric value into a string
        while (i<n && str[i]>='0' && str[i]<='9')
        {
            curr_num = curr_num + str[i];
            i++;
        }

        if (i == n)
            break;

        if (curr_num.size() > 0)
            i--;

        // Update maximum string
        res = maximumNum(curr_num, res);

        curr_num = "";
    }

    // To handle the case if there is only
    // 0 numeric value
    if (curr_num.size()== 0 && res.size()== 0)
        res = res + '0';

    // Return maximum string
    return maximumNum(curr_num, res);
}

// Drivers program
int main()
{
    string str ="100klh564abc365bg";
    cout << extractMaximum(str) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for above implementation

class GFG 
{
    // Utility method to find maximum string
    static String maximumNum(String curr_num, String res)
    {
        int len1 = curr_num.length();
        int len2 = res.length();

        // If both having equal lengths
        if (len1 == len2)
        {
            // Reach first unmatched character / value
            int i = 0;
            while (curr_num.charAt(i) == res.charAt(i))
                i++;

            // Return string with maximum value
            if (curr_num.charAt(i) < res.charAt(i))
                return res;
            else
                return curr_num;
        }

        // If different lengths
        // return string with maximum length
        return len1 < len2 ? res: curr_num;
    }

    // Method to extract the maximum value
    static String extractMaximum(String str)
    {
        int n = str.length();
        String curr_num ="";
        String res="";

        // Start traversing the string
        for (int i = 0; i<n; i++)
        {
            // Ignore leading zeroes
            while (i<n && str.charAt(i)=='0')
                i++;

            // Store numeric value into a string
            while (i<n && Character.isDigit(str.charAt(i)))
            {
                curr_num = curr_num + str.charAt(i);
                i++;
            }

            if (i == n)
                break;

            if (curr_num.length() > 0)
                i--;

            // Update maximum string
            res = maximumNum(curr_num, res);

            curr_num = "";
        }

        // To handle the case if there is only
        // 0 numeric value
        if (curr_num.length() == 0 && res.length() == 0)
            res = res + '0';

        // Return maximum string
        return maximumNum(curr_num, res);
    }

    // Driver method
    public static void main(String[] args) 
    {
        String str = "100klh564abc365bg";
        System.out.println(extractMaximum(str));
    }    
}
```

## 蟒蛇 3

```
# Python3 program for above implementation

# Utility function to find maximum string
def maximumNum(curr_num, res):

    len1 = len(curr_num);
    len2 = len(res);

    # If both having equal lengths
    if (len1 == len2):

        # Reach first unmatched character / value
        i = 0;
        while (curr_num[i]== res[i]):
            i += 1;

        # Return string with maximum value
        if (curr_num[i] < res[i]):
            return res;
        else:
            return curr_num;

    # If different lengths
    # return string with maximum length
    return res if(len1 < len2) else curr_num;

# Function to extract the maximum value
def extractMaximum(str):

    n = len(str);
    curr_num = "";
    res = "";

    # Start traversing the string
    for i in range(n):

        # Ignore leading zeroes
        while (i < n and str[i]=='0'):
            i += 1;

        # Store numeric value into a string
        while (i < n and str[i] >= '0' and 
                         str[i] <= '9'):
            curr_num += str[i];
            i += 1;

        if (i == n):
            break;

        if (len(curr_num) > 0):
            i -= 1;

        # Update maximum string
        res = maximumNum(curr_num, res);

        curr_num = "";

    # To handle the case if there is only
    # 0 numeric value
    if (len(curr_num) == 0 and len(res) == 0):
        res += '0';

    # Return maximum string
    return maximumNum(curr_num, res);

# Driver Code
str ="100klh564abc365bg";
print(extractMaximum(str));

# This code is contributed by mits
```

## C#

```
// C# program for above implementation 
using System;
class GFG 
{ 
    // Utility method to find maximum string 
    static String maximumNum(string curr_num, string res) 
    { 
        int len1 = curr_num.Length; 
        int len2 = res.Length; 

        // If both having equal lengths 
        if (len1 == len2) 
        { 
            // Reach first unmatched character / value 
            int i = 0; 
            while (curr_num[i] == res[i]) 
                i++; 

            // Return string with maximum value 
            if (curr_num[i] < res[i]) 
                return res; 
            else
                return curr_num; 
        } 

        // If different lengths 
        // return string with maximum length 
        return len1 < len2 ? res: curr_num; 
    } 

    // Method to extract the maximum value 
    static string extractMaximum(string str) 
    { 
        int n = str.Length; 
        string curr_num =""; 
        string res=""; 

        // Start traversing the string 
        for (int i = 0; i<n; i++) 
        { 
            // Ignore leading zeroes 
            while (i<n && str[i]=='0') 
                i++; 

            // Store numeric value into a string 
            while (i<n && Char.IsDigit(str[i])) 
            { 
                curr_num = curr_num + str[i]; 
                i++; 
            } 

            if (i == n) 
                break; 

            if (curr_num.Length > 0) 
                i--; 

            // Update maximum string 
            res = maximumNum(curr_num, res); 

            curr_num = ""; 
        } 

        // To handle the case if there is only 
        // 0 numeric value 
        if (curr_num.Length == 0 && res.Length == 0) 
            res = res + '0'; 

        // Return maximum string 
        return maximumNum(curr_num, res); 
    } 

    // Driver method 
    public static void Main() 
    { 
        string str = "100klh564abc365bg"; 
        Console.WriteLine(extractMaximum(str)); 
    }     
} 
// This code is contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program for above implementation

// Utility function to find maximum string
function maximumNum($curr_num, $res)
{
    $len1 = strlen($curr_num);
    $len2 = strlen($res);

    // If both having equal lengths
    if ($len1 == $len2)
    {
        // Reach first unmatched character / value
        $i = 0;
        while ($curr_num[$i]== $res[$i])
            $i++;

        // Return string with maximum value
        if ($curr_num[$i] < $res[$i])
            return $res;
        else
            return $curr_num;
    }

    // If different lengths
    // return string with maximum length
    return $len1 < $len2 ? $res: $curr_num;
}

// Function to extract the maximum value
function extractMaximum($str)
{
    $n = strlen($str);
    $curr_num ="";
    $res="";

    // Start traversing the string
    for ($i = 0; $i<$n; $i++)
    {
        // Ignore leading zeroes
        while ($i<$n && $str[$i]=='0')
            $i++;

        // Store numeric value into a string
        while ($i<$n && $str[$i]>='0' && $str[$i]<='9')
        {
            $curr_num .= $str[$i];
            $i++;
        }

        if ($i == $n)
            break;

        if (strlen($curr_num) > 0)
            $i--;

        // Update maximum string
        $res = maximumNum($curr_num, $res);

        $curr_num = "";
    }

    // To handle the case if there is only
    // 0 numeric value
    if (strlen($curr_num)== 0 && strlen($res)== 0)
        $res .= '0';

    // Return maximum string
    return maximumNum($curr_num, $res);
}

// Drivers program

    $str ="100klh564abc365bg";
    echo extractMaximum($str);

// this code is contributed by mits
?>
```

## java 描述语言

```
<script>

// JavaScript program for above implementation

    // Utility method to find maximum string
    function maximumNum(curr_num,res)
    {
        let len1 = curr_num.length;
        let len2 = res.length;

        // If both having equal lengths
        if (len1 == len2)
        {
            // Reach first unmatched character / value
            let i = 0;
            while (curr_num[i] == res[i])
                i++;

            // Return string with maximum value
            if (curr_num[i] < res[i])
                return res;
            else
                return curr_num;
        }

        // If different lengths
        // return string with maximum length
        return len1 < len2 ? res: curr_num;
    }

    // Method to extract the maximum value
    function extractMaximum(str)
    {
        let n = str.length;
        let curr_num ="";
        let res="";

        // Start traversing the string
        for (let i = 0; i<n; i++)
        {
            // Ignore leading zeroes
            while (i<n && str[i]=='0')
                i++;

            // Store numeric value into a string
            while (i<n && !isNaN(String(str[i]) * 1))
            {
                curr_num = curr_num + str[i];
                i++;
            }

            if (i == n)
                break;

            if (curr_num.length > 0)
                i--;

            // Update maximum string
            res = maximumNum(curr_num, res);

            curr_num = "";
        }

        // To handle the case if there is only
        // 0 numeric value
        if (curr_num.length == 0 && res.length == 0)
            res = res + '0';

        // Return maximum string
        return maximumNum(curr_num, res);
    }

    // Driver method
    let str = "100klh564abc365bg";
    document.write(extractMaximum(str));

// This code is contributed by unknown2108

</script>
```

**输出:**

```
564
```

本文由 [**萨哈布拉**](https://www.facebook.com/sahil.chhabra.965) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。
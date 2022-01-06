# 迷人的数字

> 原文:[https://www.geeksforgeeks.org/fascinating-number/](https://www.geeksforgeeks.org/fascinating-number/)

给定一个数字 N，任务是检查它是否迷人。
**迷人的数字**:当一个数字(3 位数或更多)乘以 2 和 3，并且当这两个乘积都与原始数字串联时，那么它导致从 1 到 9 的所有数字恰好出现一次。可以有任意数量的零，并被忽略。
**示例:**

> **输入:** 192
> **输出:**是
> 与 2 和 3 相乘，并与原数串联后，结果数为 192384576，包含 1 到 9 的所有数字。
> **输入:** 853
> **输出:**否
> 与 2、3 相乘，并与原数串接后，结果数为 85317062559。这里面，数字 4 不见了，数字 5 出现了多次。

**接近** :

1.  检查给定的数字是否有三位数或更多。如果没有，打印否。
2.  否则，给定的数字乘以 2 和 3。
3.  将这些产品与给定的数字连接起来形成一个字符串。
4.  遍历这个字符串，保持数字的频率计数。
5.  如果任何数字丢失或多次出现，则打印否。
6.  否则，打印“是”。

以下是上述方法的实现:

## C++14

```
// C++ program to implement
// fascinating number
#include <bits/stdc++.h>
using namespace std;

// function to check if number
// is fascinating or not
bool isFascinating(int num)
{
    // frequency count array
    // using 1 indexing
    int freq[10] = {0};

    // obtaining the resultant number
    // using string concatenation
    string val = "" + to_string(num) +
                      to_string(num * 2) +
                      to_string(num * 3);

    // Traversing the string
    // character by character
    for (int i = 0; i < val.length(); i++)
    {

        // gives integer value of
        // a character digit
        int digit = val[i] - '0';

        // To check if any digit has
        // appeared multiple times
        if (freq[digit] and digit != 0 > 0)
            return false;
        else
            freq[digit]++;
    }

    // Traversing through freq array to
    // check if any digit was missing
    for (int i = 1; i < 10; i++)
    {
        if (freq[i] == 0)
            return false;
    }
    return true;
}

// Driver code
int main()
{
    // Input number
    int num = 192;

    // Not a valid number
    if (num < 100)
        cout << "No" << endl;

    else
    {
        // Calling the function to
        // check if input number
        // is fascinating or not
        bool ans = isFascinating(num);
        if (ans)
            cout << "Yes";
        else
            cout << "No";
    }
}

// This code is contributed
// by Subhadeep
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// fascinating number
import java.io.*;
import java.util.*;

public class GFG {

    // function to check if number
    // is fascinating or not
    public static boolean isFascinating(
                                int num)
    {

        // frequency count array
        //using 1 indexing
        int[] freq = new int[10];

        // obtaining the resultant number
        // using string concatenation
        String val = "" + num + num * 2 +
                                num * 3;

        // Traversing the string character //by character
        for (int i = 0; i < val.length(); i++)
        {

            // gives integer value of //a character digit
            int digit = val.charAt(i) - '0';

            // To check if any digit has
            // appeared multiple times
            if (freq[digit]>0 && digit != 0)
                return false;
            else
                freq[digit]++;
        }

        // Traversing through freq array to
        // check if any digit was missing
        for (int i = 1; i < freq.length; i++)
        {
            if (freq[i] == 0)
                return false;
        }
        return true;
    }

    // Driver code
    public static void main(String args[])
    {

        // Input number
        int num = 192;

        // Not a valid number
        if (num < 100)
            System.out.println("No");

        else
        {

            // Calling the function to check
            // if input number is fascinating or not
            boolean ans = isFascinating(num);
            if (ans)
                System.out.println("Yes");
            else
                System.out.println("No");
        }
    }
}
```

## 蟒蛇 3

```
# Python 3 program to implement
# fascinating number

# function to check if number
# is fascinating or not
def isFascinating(num) :

    # frequency count array
    # using 1 indexing
    freq = [0] * 10

    # obtaining the resultant number
    # using string concatenation
    val = (str(num) + str(num * 2) +
                      str(num * 3))

    # Traversing the string
    # character by character
    for i in range(len(val)) :

        # gives integer value of
        # a character digit
        digit = int(val[i])

        # To check if any digit has
        # appeared multiple times
        if freq[digit] and digit != 0 > 0 :
            return False
        else :
            freq[digit] += 1

    # Traversing through freq array to
    # check if any digit was missing
    for i in range(1, 10) :

        if freq[i] == 0 :
            return False

    return True

# Driver Code
if __name__ == "__main__" :

    # Input number
    num = 192

    # Not a valid number
    if num < 100 :
        print("No")

    else :

        # Calling the function to
        # check if input number
        # is fascinating or not
        ans = isFascinating(num)

        if ans :
            print("Yes")
        else :
            print("No")

# This code is contributed by ANKITRAI1
```

## C#

```
// C# program to implement
// fascinating number
using System;

class GFG
{

// function to check if number
// is fascinating or not
public static bool isFascinating(int num)
{
    // frequency count array
    // using 1 indexing
    int[] freq = new int[10];

    // obtaining the resultant number
    // using string concatenation
    String val = "" + num.ToString() +
                     (num * 2).ToString() +
                     (num * 3).ToString();

    // Traversing the string
    // character by character
    for (int i = 0; i < val.Length; i++)
    {

        // gives integer value of
        // a character digit
        int digit = val[i] - '0';

        // To check if any digit has
        // appeared multiple times
        if (freq[digit] && digit != 0 > 0 )
            return false;
        else
            freq[digit]++;
    }

    // Traversing through freq array to
    // check if any digit was missing
    for (int i = 1; i < freq.Length; i++)
    {
        if (freq[i] == 0)
            return false;
    }
    return true;
}

// Driver code
static void Main()
{
    // Input number
    int num = 192;

    // Not a valid number
    if (num < 100)
        Console.WriteLine("No");

    else
    {
        // Calling the function to check
        // if input number is fascinating or not
        bool ans = isFascinating(num);
        if (ans)
            Console.WriteLine("Yes");
        else
            Console.WriteLine("No");
    }
}
}

// This code is contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to implement
// fascinating number

// function to check if number
// is fascinating or not
function isFascinating($num)
{
    // frequency count array
    // using 1 indexing
    $freq = array_fill(0, 10, NULL);

    // obtaining the resultant number
    // using string concatenation
    $val = "" . $num . ($num * 2).
                       ($num * 3);

    // Traversing the string
    // character by character
    for ($i = 0; $i < strlen($val); $i++)
    {

        // gives integer value of
        // a character digit
        $digit = $val[$i] - '0';

        // To check if any digit has
        // appeared multiple times
        if ($freq[$digit] > 0 && $digit != 0)
            return false;
        else
            $freq[$digit]++;
    }

    // Traversing through freq array to
    // check if any digit was missing
    for ($i = 1; $i < 10; $i++)
    {
        if ($freq[$i] == 0)
            return false;
    }
    return true;
}

// Driver code

// Input number
$num = 192;

// Not a valid number
if ($num < 100)
    echo "No" ;

else
{
    // Calling the function to
    // check if input number
    // is fascinating or not
    $ans = isFascinating($num);
    if ($ans)
        echo "Yes";
    else
        echo "No";
}

// This code is contributed
// by ChitraNayal
?>
```

## java 描述语言

```
<script>

// Javascript program to implement
// fascinating number

    // function to check if number
    // is fascinating or not
    function isFascinating(num)
    {
        // frequency count array
        //using 1 indexing
        let freq = new Array(10);
        for(let i=0;i<freq.length;i++)
        {
            freq[i]=0;
        }

        // obtaining the resultant number
        // using string concatenation
        let val = "" + num + num * 2 +
                                num * 3;

        // Traversing the string character //by character
        for (let i = 0; i < val.length; i++)
        {

            // gives integer value of //a character digit
            let digit = val[i].charCodeAt(0) -
            '0'.charCodeAt(0);

            // To check if any digit has
            // appeared multiple times
            if (freq[digit]>0 && digit != 0)
                return false;
            else
                freq[digit]++;
        }

        // Traversing through freq array to
        // check if any digit was missing
        for (let i = 1; i < freq.length; i++)
        {
            if (freq[i] == 0)
                return false;
        }
        return true;
    }

    // Driver code

    // Input number
    let num = 192;
    // Not a valid number
    if (num < 100)
        document.write("No");

    else
    {

        // Calling the function to check
        // if input number is fascinating or not
        let ans = isFascinating(num);
        if (ans)
            document.write("Yes");
        else
            document.write("No");
    }

// This code is contributed by rag2127

</script>
```

**Output:** 

```
Yes
```
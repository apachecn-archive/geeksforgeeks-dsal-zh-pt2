# 最多换 K 位数字

最小化数字

> 原文:[https://www . geesforgeks . org/通过最多改变 k 位数来最小化数字/](https://www.geeksforgeeks.org/minimize-the-number-by-changing-at-most-k-digits/)

给定一个数字 **N** ，任务是通过最多改变 **K** 位数来最小化该数字。请注意，该数字不应包含任何前导零。
**例:**

> **输入:** N = 91945，K = 3
> **输出:** 10045
> **输入:** N = 1，K = 0
> **输出:** 1

**进场:**

*   如果第一个数字还没有 **1** 替换为 **1** ，并相应更新 **K** 。
*   现在剩下的数字，用 **0** 替换下一个**K–1**非零数字。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <iostream>
using namespace std;

// Function to return the minimized number
string minNum(string num, int k)
{

    // Total digits in the number
    int len = num.length();

    // If the string is empty or there
    // are no operations to perform
    if (len == 0 || k == 0)
        return num;

    // "0" is a valid number
    if (len == 1)
        return "0";

    // If the first digit is not already 1 then
    // update it to 1 and decrement k
    if (num[0] != '1') {
        num[0] = '1';
        k--;
    }

    int i = 1;
    // While there are operations left
    // and the number can still be updated
    while (k > 0 && i < len) {

        // If the current digit is not already 0
        // then update it to 0 and decrement k
        if (num[i] != '0') {
            num[i] = '0';
            k--;
        }

        i++;
    }

    // Return the minimised number
    return num;
}

// Driver code
int main()
{
    string num = "91945";
    int k = 3;

    cout << minNum(num, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

    // Function to return the minimized number
    static String minNum(char num[], int k)
    {

        // Total digits in the number
        int len = num.length;

        // If the string is empty or there
        // are no operations to perform
        if (len == 0 || k == 0)
        {
            String num_str = new String(num);
            return num_str;
        }

        // "0" is a valid number
        if (len == 1)
            return "0";

        // If the first digit is not already 1 then
        // update it to 1 and decrement k
        if (num[0] != '1')
        {
            num[0] = '1';
            k--;
        }

        int i = 1;

        // While there are operations left
        // and the number can still be updated
        while (k > 0 && i < len)
        {

            // If the current digit is not already 0
            // then update it to 0 and decrement k
            if (num[i] != '0')
            {
                num[i] = '0';
                k--;
            }
            i++;
        }

        String num_str = new String(num);

        // Return the minimised number
        return num_str;
    }

    // Driver code
    public static void main(String args[])
    {
        String num = "91945";
        int k = 3;

        System.out.println(minNum(num.toCharArray(), k));
    }
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python 3 implementation of the approach

# Function to return the minimized number
def minNum(num, k) :

    # Total digits in the number
    len_ = len(num)

    # If the string is empty or there
    # are no operations to perform
    if len_ == 0 or k == 0 :
        return num

    # "0" is a valid number
    if len_ == 1:
        return "0"

    # If the first digit is not already 1 then
    # update it to 1 and decrement k
    if num[0] != '1' :
        num = '1' + num[1:]
        k -= 1

    i = 1

    # While there are operations left
    # and the number can still be updated
    while k > 0 and i < len_ :

        # If the current digit is not already 0
        # then update it to 0 and decrement k
        if num[i] != '0' :
            num = num[:i] + '0' + num[i + 1:]
            k -= 1

        i += 1

    # Return the minimised number
    return num

# Driver code
num = "91945"
k = 3

print(minNum(num, k))

# This code is contributed by divyamohan123
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Function to return the minimized number
    static String minNum(char []num, int k)
    {

        // Total digits in the number
        int len = num.Length;

        // If the string is empty or there
        // are no operations to perform
        if (len == 0 || k == 0)
        {
            return String.Join("", num);
        }

        // "0" is a valid number
        if (len == 1)
            return "0";

        // If the first digit is not already 1 then
        // update it to 1 and decrement k
        if (num[0] != '1')
        {
            num[0] = '1';
            k--;
        }

        int i = 1;

        // While there are operations left
        // and the number can still be updated
        while (k > 0 && i < len)
        {

            // If the current digit is not already 0
            // then update it to 0 and decrement k
            if (num[i] != '0')
            {
                num[i] = '0';
                k--;
            }
            i++;
        }

        // Return the minimised number
        return String.Join("", num);
    }

    // Driver code
    public static void Main(String []args)
    {
        String num = "91945";
        int k = 3;

        Console.WriteLine(minNum(num.ToCharArray(), k));
    }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// Javascript implementation of the approach

// Function to return the minimized number
function minNum(num, k)
{

    // Total digits in the number
    let len = num.length;

    // If the string is empty or there
    // are no operations to perform
    if (len == 0 || k == 0) {
        let num_str = num.join("");
        return num_str;
    }

    // "0" is a valid number
    if (len == 1)
        return "0";

    // If the first digit is not already 1 then
    // update it to 1 and decrement k
    if (num[0] != '1') {
        num[0] = '1';
        k--;
    }

    let i = 1;

    // While there are operations left
    // and the number can still be updated
    while (k > 0 && i < len) {

        // If the current digit is not already 0
        // then update it to 0 and decrement k
        if (num[i] != '0') {
            num[i] = '0';
            k--;
        }
        i++;
    }

    let num_str = num.join("");

    // Return the minimised number
    return num_str;
}

// Driver code
let num = "91945";
let k = 3;

document.write(minNum(num.split(""), k));

// This code is contributed by _saurabh_jaiswal.
</script>
```

**Output:** 

```
10045
```
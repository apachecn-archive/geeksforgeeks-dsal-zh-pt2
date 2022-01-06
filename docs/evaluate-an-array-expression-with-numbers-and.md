# 用数字、+和–

计算数组表达式

> 原文:[https://www . geesforgeks . org/evaluate-a-array-expression-with-numbers-and/](https://www.geeksforgeeks.org/evaluate-an-array-expression-with-numbers-and/)

给定由字符串“+”、“-”和数字组成的字符串类型的数组 arr[]。求给定数组的和。
**例:**

```
Input : arr[] = {"3", "+", "4", "-", "7", "+", "13"}
Output : Value = 13
The value of expression 3+4-7+13 is 13.

Input : arr[] = { "2", "+", "1", "-8", "+", "13"}
Output : Value = 8
```

**进场:**
**1)** 首先初始化和即和= 0。
**2)** 开始穿越阵列。
**3)** 由于数组的每一个偶数位置都有一串数字，所以使用 C++中的 [stoi 函数](https://www.geeksforgeeks.org/converting-strings-numbers-cc/)将这个字符串转换为整数并存储在变量*值*中。
**(4)**由于每个奇数位置都有一个运算符，请检查运算符是“+”还是“-”。如果是“+”，则将*值*加到和上，否则从和上减去。
**5)** 最后，返回得到的和。
以下是上述方法的实施:

## C++

```
// C++ program to find sum of given array of
// string type in integer form
#include <bits/stdc++.h>
using namespace std;

// Function to find the sum of given array
int calculateSum(string arr[], int n)
{  
    // if string is empty
    if (n == 0)
       return 0;

    string s = arr[0];

    // stoi function to convert
    // string into integer
    int value = stoi(s);
    int sum = value;

    for (int i = 2; i < n; i = i + 2)
    {
        s = arr[i];

        // stoi function to convert
        // string into integer
        int value = stoi(s);

        // Find operator
        char operation = arr[i - 1][0];

        // If operator is equal to '+',
        // add value in sum variable
        // else subtract
        if (operation == '+')
            sum += value;
        else
            sum -= value;
    }
    return sum;
}

// Driver Function
int main()
{
    string arr[] = { "3", "+", "4", "-",
                     "7", "+", "13" };
    int n = sizeof(arr) / sizeof(arr[0]);  
    cout << calculateSum(arr, n);  
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find sum of given array of
// string type in integer form
import java.io.*;

class GFG {

    // Function to find the sum of given array
    public static int calculateSum(String arr[], int n)
    {
        // if string is empty
        if (n == 0)
        return 0;
        String s = arr[0];

        // parseInt function to convert
        // string into integer
        int value = Integer.parseInt(s);
        int sum = value;

        for (int i = 2; i < n; i = i + 2)
        {
            s = arr[i];

            // parseInt function to convert
            // string into integer
            value = Integer.parseInt(s);

            // Find operator
            char operation = arr[i - 1].charAt(0);

            // If operator is equal to '+',
            // add value in sum variable
            // else subtract
            if (operation == '+')
                sum += value;
            else
                sum -= value;
        }
        return sum;
    }

    // Driver code
    public static void main (String[] args)
    {
        String arr[] = { "3", "+", "4", "-",
                        "7", "+", "13" };
        int n = arr.length;
        System.out.println( calculateSum(arr, n));
    }
}

// This code in contributed by Upendra bartwal
```

## 蟒蛇 3

```
# Python3 program to find sum of given
# array of string type in integer form

# Function to find the sum of given array
def calculateSum(arr, n):

    # if string is empty
    if (n == 0):
        return 0

    s = arr[0]

    # stoi function to convert
    # string into integer
    value = int(s)
    sum = value

    for i in range(2 , n, 2):

        s = arr[i]

        # stoi function to convert
        # string into integer
        value = int(s)

        # Find operator
        operation = arr[i - 1][0]

        # If operator is equal to '+',
        # add value in sum variable
        # else subtract
        if (operation == '+'):
            sum += value
        else:
            sum -= value

    return sum

# Driver Function
arr = ["3", "+", "4", "-","7", "+", "13"]
n = len(arr)
print(calculateSum(arr, n))

# This code is contributed by Smitha
```

## C#

```
// C# program to find sum of given array of
// string type in integer form
using System;

class GFG {

    // Function to find the sum of given array
    public static int calculateSum(string []arr,
                                          int n)
    {

        // if string is empty
        if (n == 0)
            return 0;
        string s = arr[0];

        // parseInt function to convert
        // string into integer
        int value = int.Parse(s);
        int sum = value;

        for (int i = 2; i < n; i = i + 2)
        {
            s = arr[i];

            // parseInt function to convert
            // string into integer
            value = int.Parse(s);

            // Find operator
            char operation = arr[i - 1][0];

            // If operator is equal to '+',
            // add value in sum variable
            // else subtract
            if (operation == '+')
                sum += value;
            else
                sum -= value;
        }

        return sum;
    }

    // Driver code
    public static void Main ()
    {
        string []arr = { "3", "+", "4", "-",
                           "7", "+", "13" };
        int n = arr.Length;

        Console.Write(calculateSum(arr, n));
    }
}

// This code in contributed by nitin mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// php program to find sum of given
// array of string type in integer form

// Function to find the
// sum of given array
function calculateSum($arr,$n)
{

    // if string is empty
    if ($n == 0)
    return 0;

    $s = $arr[0];

    // stoi function to convert
    // string into integer
    $value = (int)$s;
    $sum = $value;
    for ($i = 2; $i < $n; $i = $i + 2)
    {
        $s = $arr[$i];

        // cast to convert
        // string into integer
        $value = (int)$s;

        // Find operator
        $operation = $arr[$i - 1];

        // If operator is equal to '+',
        // add value in sum variable
        // else subtract
        if ($operation == '+')
            $sum += $value;
        else if ($operation == '-')
            $sum -= $value;
    }
    return $sum;
}

    // Driver code
    $arr = array("3", "+", "4", "-",
                 "7", "+", "13" );
    $n = sizeof($arr) / sizeof($arr[0]);
    echo calculateSum($arr, $n);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>
    // Javascript program to find sum of given array of
    // string type in integer form   

    // Function to find the sum of given array
    function calculateSum(arr, n)
    {

        // if string is empty
        if (n == 0)
            return 0;
        let s = arr[0];

        // parseInt function to convert
        // string into integer
        let value = parseInt(s);
        let sum = value;

        for (let i = 2; i < n; i = i + 2)
        {
            s = arr[i];

            // parseInt function to convert
            // string into integer
            value = parseInt(s);

            // Find operator
            let operation = arr[i - 1][0];

            // If operator is equal to '+',
            // add value in sum variable
            // else subtract
            if (operation == '+')
                sum += value;
            else
                sum -= value;
        }

        return sum;
    }

    let arr = [ "3", "+", "4", "-", "7", "+", "13" ];
    let n = arr.length;

    document.write(calculateSum(arr, n));

    // This code is contributed by vaibhavrabadiya117.
</script>
```

输出:

```
13 
```

**时间复杂度:** O(n)
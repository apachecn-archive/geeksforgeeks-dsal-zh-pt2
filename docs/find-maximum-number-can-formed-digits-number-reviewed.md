# 用给定数字的数字找到可以形成的最大数字

> 原文:[https://www . geesforgeks . org/find-最大数字-可形成数字-数字-已审核/](https://www.geeksforgeeks.org/find-maximum-number-can-formed-digits-number-reviewed/)

给定一个数字，编写一个程序，找出这个数字的所有数字所能构成的最大数字。
**例:**

```
Input : 38293367
Output : 98763332

Input : 1203465
Output: 6543210
```

**简单方法**:解决这个问题的简单方法是将给定数字的位数提取并存储在一个整数数组中，并对这个数组进行降序排序。对数组进行排序后，打印数组的元素。
**时间复杂度** : O( N log N)，其中 N 为给定数字中的位数。
**高效方法:**我们知道一个数字中的位数将在 0-9 的范围内，所以想法是创建一个大小为 10 的散列数组，并存储该数字中出现的散列数组中每个位数的计数。然后遍历从索引 9 到 0 的散列数组，并相应地计算数字。
以下是上述高效方法的实现:

## C++

```
// CPP program to print the maximum number
// from the set of digits of a given number
#include <bits/stdc++.h>
using namespace std;

// Function to print the maximum number
int printMaxNum(int num)
{
    // hashed array to store count of digits
    int count[10] = {0};

    // Converting given number to string
    string str = to_string(num);

    // Updating the count array
    for (int i=0; i<str.length(); i++)
        count[str[i]-'0']++;

    // result is to store the final number
    int result = 0, multiplier = 1;

    // Traversing the count array
    // to calculate the maximum number
    for (int i = 0; i <= 9; i++)
    {
        while (count[i] > 0)
        {
            result = result + (i * multiplier);
            count[i]--;
            multiplier = multiplier * 10;
        }
    }

    // return the result
    return result;
}

// Driver program to test above function
int main()
{
    int num = 38293367;
    cout << printMaxNum(num);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print the maximum number
// from the set of digits of a given number
public class GFG
{
    // Function to print the maximum number
    static int printMaxNum(int num)
    {
        // hashed array to store count of digits
        int count[] = new int[10];

        // Converting given number to string
        String str = Integer.toString(num);

        // Updating the count array
        for(int i=0; i < str.length(); i++)
            count[str.charAt(i)-'0']++;

        // result is to store the final number
        int result = 0, multiplier = 1;

        // Traversing the count array
        // to calculate the maximum number
        for (int i = 0; i <= 9; i++)
        {
            while (count[i] > 0)
            {
                result = result + (i * multiplier);
                count[i]--;
                multiplier = multiplier * 10;
            }
        }

        // return the result
        return result;
    }

    // Driver program to test above function
    public static void main(String[] args)
    {
        int num = 38293367;
        System.out.println(printMaxNum(num));
    }
}
// This code is contributed by Sumit Ghosh
```

## 计算机编程语言

```
# Python program to print the maximum number
# from the set of digits of a given number

# Function to print maximum number
def printMaximum(inum):

    # Hashed array to store count of digits
    count = [0 for x in range(10)]

    # Converting given number to string
    string = str(num)

    # Updating the count array
    for i in range(len(string)):
        count[int(string[i])] = count[int(string[i])] +  1

    # Result stores final number
    result = 0
    multiplier = 1

    # traversing the count array
    # to calculate the maximum number

    for i in range(10):
        while count[i] > 0:
            result = result + ( i * multiplier )
            count[i] = count[i] - 1
            multiplier = multiplier * 10

    # return the result
    return result

# Driver code
num = 38293367
print printMaximum(num)

# This code is contributed by Harshit Agrawal
```

## C#

```
// C# program to print the maximum number
// from the set of digits of a given number
using System;

class GFG
{

// Function to print the maximum number
static int printMaxNum(int num)
{
    // hashed array to store
    // count of digits
    int []count = new int[10];

    // Converting given number
    // to string
    String str = num.ToString();

    // Updating the count array
    for(int i = 0; i < str.Length; i++)
        count[str[i] - '0']++;

    // result is to store the
    // final number
    int result = 0, multiplier = 1;

    // Traversing the count array
    // to calculate the maximum number
    for (int i = 0; i <= 9; i++)
    {
        while (count[i] > 0)
        {
            result = result + (i * multiplier);
            count[i]--;
            multiplier = multiplier * 10;
        }
    }

    // return the result
    return result;
}

// Driver Code
public static void Main()
{
    int num = 38293367;
    Console.Write(printMaxNum(num));
}
}

// This code is contributed
// by PrinciRaj1992
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php

// Php program to print the maximum number
// from the set of digits of a given number

// Function to print the maximum number
function printMaxNum($num)
{
    // hashed array to store count of digits
    $count = array_fill(0,10, NULL);

    // Converting given number to string
    $str = (string)$num;

    // Updating the count array
    for ($i=0; $i<strlen($str); $i++)
        $count[ord($str[$i])-ord('0')]++;

    // result is to store the final number
    $result = 0;
    $multiplier = 1;

    // Traversing the count array
    // to calculate the maximum number
    for ($i = 0; $i <= 9; $i++)
    {
        while ($count[$i] > 0)
        {
            $result = $result + ($i * $multiplier);
            $count[$i]--;
            $multiplier = $multiplier * 10;
        }
    }

    // return the result
    return $result;
}

// Driver program to test above function

    $num = 38293367;
    echo printMaxNum($num);
?>
```

## java 描述语言

```
<script>
// Javascript program to print the maximum number
// from the set of digits of a given number

    // Function to print the maximum number
    function printMaxNum(num)
    {
        // hashed array to store count of digits
        let count = new Array(10);
        for(let i=0;i<count.length;i++)
        {
            count[i]=0;
        }

        // Converting given number to string
        let str = num.toString();

        // Updating the count array
        for(let i=0; i < str.length; i++)
            count[str[i]-'0']++;

        // result is to store the final number
        let result = 0, multiplier = 1;

        // Traversing the count array
        // to calculate the maximum number
        for (let i = 0; i <= 9; i++)
        {
            while (count[i] > 0)
            {
                result = result + (i * multiplier);
                count[i]--;
                multiplier = multiplier * 10;
            }
        }

        // return the result
        return result;
    }

    // Driver program to test above function
    let num = 38293367;
    document.write(printMaxNum(num));

    //This code is contributed by avanitrachhadiya2155

</script>
```

**输出:**

```
98763332
```

**时间复杂度:** O( N)，其中 N 为给定数字中的位数。
**注**:对于非常大的数字，我们可以使用字符串进行输入，而不是将输入存储为整数数据类型。

本文由 **Rohit Thapliyal** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。
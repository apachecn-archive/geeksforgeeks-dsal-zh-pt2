# 计算给定字符串中长度为 3 的子序列

> 原文:[https://www . geesforgeks . org/count-给定字符串中长度为三的子序列/](https://www.geeksforgeeks.org/count-subsequence-of-length-three-in-a-given-string/)

给定长度为 n 的字符串和长度为 3 的子序列。查找该字符串中子序列出现的总次数。

**示例:**

```
Input : string = "GFGFGYSYIOIWIN", 
        subsequence = "GFG"
Output : 4
Explanation : There are 4 such subsequences as shown:
              GFGFGYSYIOIWIN
              GFGFGYSYIOIWIN
              GFGFGYSYIOIWIN
              GFGFGYSYIOIWIN

Input : string = "GFGGGZZYNOIWIN", 
        subsequence = "GFG"
Output : 3
```

**蛮力法**:解决这个问题最简单的方法就是对给定子序列的树型字符运行三个循环。它启动一个循环来查找字符串中子序列的第一个字符，一旦找到这个字符，就在这个索引之后启动一个循环来查找第二个字符，一旦找到这个字符，就在这个索引之后启动一个循环来查找第三个字符。维护一个变量来存储第三个字符的出现次数，即子序列的出现次数。

下面是上述方法的实现:

## C++

```
// C++ program to find number of occurrences of
// a subsequence of length 3
#include<iostream>
using namespace std;

// Function to find number of occurrences of
// a subsequence of length three in a string
int findOccurrences(string str, string substr)
{   
    // variable to store no of occurrences
    int counter = 0;

    // loop to find first character
    for (int i=0;i<str.length();i++)
    {
        if (str[i]==substr[0])
        {   
            // loop to find 2nd character
            for (int j=i+1;j<str.length();j++)
            {
                if (str[j]==substr[1])
                {   
                    // loop to find 3rd character
                    for (int k = j+1; k<str.length(); k++)
                    {   
                        // increment count if subsequence
                        // is found
                        if (str[k]==substr[2])
                            counter++;
                    }
                }
            }
        }
    }

    return counter;
}

// Driver code
int main()
{
    string str = "GFGFGYSYIOIWIN";
    string substr = "GFG";
    cout << findOccurrences(str, substr);   
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find number of occurrences of
// a subsequence of length 3
import java.util.*;
import java.lang.*;

public class GfG{

    // Function to find number of occurrences of
    // a subsequence of length three in a string
    public static int findOccurrences(String str1, String substr1)
    {
        // variable to store no of occurrences
        int counter = 0;

        char[] str = str1.toCharArray();
        char[] substr = substr1.toCharArray();

        // loop to find first character
        for (int i=0; i < str1.length(); i++)
        {
            if (str[i] == substr[0])
            {
                // loop to find 2nd character
                for (int j = i+1; j < str1.length(); j++)
                {
                    if (str[j] == substr[1])
                    {
                        // loop to find 3rd character
                        for (int k = j+1; k < str1.length(); k++)
                        {
                            // increment count if subsequence
                            // is found
                            if (str[k] == substr[2])
                                counter++;
                        }
                    }
                }
            }
        }

        return counter;
    }

    // Driver function
    public static void main(String argc[]){
        String str = "GFGFGYSYIOIWIN";
        String substr = "GFG";

        System.out.println(findOccurrences(str, substr));
    }

}
/* This code is contributed by Sagar Shukla */
```

## 蟒蛇 3

```
# Python program to find
# number of occurrences
# of a subsequence of
# length 3

# Function to find number
# of occurrences of a
# subsequence of length
# three in a string
def findOccurrences(str, substr) :

    # variable to store
    # no of occurrences
    counter = 0

    # loop to find
    # first character
    for i in range(0, len(str)) :

        if (str[i] == substr[0]) :

            # loop to find
            # 2nd character
            for j in range(i + 1,
                           len(str)) :

                if (str[j] == substr[1]) :

                    # loop to find
                    # 3rd character
                    for k in range(j + 1,
                                   len(str)) :

                        # increment count if
                        # subsequence is found
                        if (str[k] == substr[2]) :
                            counter = counter + 1

    return counter

# Driver Code
str = "GFGFGYSYIOIWIN"
substr = "GFG"
print (findOccurrences(str, substr))

# This code is contributed by
# Manish Shaw(manishshaw1)
```

## C#

```
// C# program to find number of occurrences of
// a subsequence of length 3
using System;

public class GfG {

    // Function to find number of occurrences of
    // a subsequence of length three in a string
    public static int findOccurrences(string str1,
                                   string substr1)
    {

        // variable to store no of occurrences
        int counter = 0;

        //char[] str = str1.toCharArray();
        //char[] substr = substr1.toCharArray();

        // loop to find first character
        for (int i=0; i < str1.Length; i++)
        {
            if (str1[i] == substr1[0])
            {

                // loop to find 2nd character
                for (int j = i+1; j < str1.Length; j++)
                {
                    if (str1[j] == substr1[1])
                    {

                        // loop to find 3rd character
                        for (int k = j+1; k < str1.Length; k++)
                        {

                            // increment count if subsequence
                            // is found
                            if (str1[k] == substr1[2])
                                counter++;
                        }
                    }
                }
            }
        }

        return counter;
    }

    // Driver function
    public static void Main()
    {
        string str1 = "GFGFGYSYIOIWIN";
        string substr1 = "GFG";

        Console.WriteLine(findOccurrences(str1, substr1));
    }
}

/* This code is contributed by vt_m */
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find number
// of occurrences of a
// subsequence of length 3

// Function to find number of
// occurrences of a subsequence
// of length three in a string
function findOccurrences($str, $substr)
{
    // variable to store
    // no of occurrences
    $counter = 0;

    // loop to find first character
    for ($i = 0;$i < strlen($str); $i++)
    {
        if ($str[$i] == $substr[0])
        {
            // loop to find 2nd character
            for ($j = $i + 1; $j < strlen($str); $j++)
            {
                if ($str[$j] == $substr[1])
                {
                    // loop to find 3rd character
                    for ($k = $j + 1; $k < strlen($str); $k++)
                    {
                        // increment count if
                        // subsequence is found
                        if ($str[$k] == $substr[2])
                            $counter++;
                    }
                }
            }
        }
    }

    return $counter;
}

// Driver Code
$str = "GFGFGYSYIOIWIN";
$substr = "GFG";
echo findOccurrences($str, $substr);

// This code is contributed by aj_36
?>
```

## java 描述语言

```
<script>

// Javascript program to find number
// of occurrences of a subsequence of length 3

// Function to find number of occurrences of
// a subsequence of length three in a string
function findOccurrences(str1, substr1)
{

    // Variable to store no of occurrences
    let counter = 0;

    //char[] str = str1.toCharArray();
    //char[] substr = substr1.toCharArray();

    // Loop to find first character
    for(let i = 0; i < str1.length; i++)
    {
        if (str1[i] == substr1[0])
        {

            // Loop to find 2nd character
            for(let j = i + 1; j < str1.length; j++)
            {
                if (str1[j] == substr1[1])
                {

                    // Loop to find 3rd character
                    for (let k = j + 1; k < str1.length; k++)
                    {

                        // Increment count if subsequence
                        // is found
                        if (str1[k] == substr1[2])
                            counter++;
                    }
                }
            }
        }
    }
    return counter;
}

// Driver code
let str1 = "GFGFGYSYIOIWIN";
let substr1 = "GFG";

document.write(findOccurrences(str1, substr1));

// This code is contributed by suresh07 

</script>
```

**输出:**

```
4
```

**时间复杂度** : O(n^3)
**辅助空间** : O(1)

**高效方法**:解决这个问题的有效方法是使用预计算的概念。这个想法是，对于字符串中子序列中间字符的每次出现，预先计算两个值。也就是说，它前面的第一个字符的出现次数和它后面的第三个字符的出现次数，将这两个值相乘，生成中间字符每次出现的总次数。

下面是这个想法的实现:

## C++

```
// C++ program to find number of occurrences of
// a subsequence of length 3
#include<iostream>
using namespace std;

// Function to find number of occurrences of
// a subsequence of length three in a string
int findOccurrences(string str, string substr)
{   
    // calculate length of string
    int n = str.length();

    // auxiliary array to store occurrences of
    // first character
    int preLeft[n] = {0};

    // auxiliary array to store occurrences of
    // third character
    int preRight[n] = {0};

    if (str[0]==substr[0])
        preLeft[0]++;

    // calculate occurrences of first character
    // upto ith index from left
    for (int i=1;i<n;i++)
    {
        if (str[i]==substr[0])       
            preLeft[i] = preLeft[i-1] + 1;       
        else
            preLeft[i] = preLeft[i-1];       
    }

    if (str[n-1]==substr[2])
        preRight[n-1]++;

    // calculate occurrences of third character
    // upto ith index from right
    for(int i=n-2;i>=0;i--)
    {
        if (str[i]==substr[2])       
            preRight[i] = preRight[i+1] + 1;       
        else       
            preRight[i] = preRight[i+1];       
    }

    // variable to store total number of occurrences
    int counter = 0;

    // loop to find the occurrences of middle element
    for (int i=1; i<n-1;i++)
    {   
        // if middle character of subsequence is found
        // in the string
        if (str[i]==str[1])
        {   
            // multiply the total occurrences of first
            // character before middle character with
            // the total occurrences of third character
            // after middle character
            int total = preLeft[i-1]*preRight[i+1];
            counter += total;
        }
    }

    return counter;
}

// Driver code
int main()
{
    string str = "GFGFGYSYIOIWIN";
    string substr = "GFG";
    cout << findOccurrences(str,substr);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find number of occurrences of
// a subsequence of length 3
import java.util.*;
import java.lang.*;

public class GfG{

    // Function to find number of occurrences of
    // a subsequence of length three in a string
    public static int findOccurrences(String str1, String substr1)
    {
        // calculate length of string
        int n = str1.length();

        char[] str = str1.toCharArray();
        char[] substr = substr1.toCharArray();

        // auxiliary array to store occurrences of
        // first character
        int[] preLeft = new int[n];

        // auxiliary array to store occurrences of
        // third character
        int[] preRight = new int[n];

        if (str[0] == substr[0])
            preLeft[0]++;

        // calculate occurrences of first character
        // upto ith index from left
        for (int i = 1; i < n; i++)
        {
            if (str[i] == substr[0])    
                preLeft[i] = preLeft[i-1] + 1;    
            else
                preLeft[i] = preLeft[i-1];    
        }

        if (str[n-1] == substr[2])
            preRight[n-1]++;

        // calculate occurrences of third character
        // upto ith index from right
        for(int i = n-2; i >= 0; i--)
        {
            if (str[i] == substr[2])    
                preRight[i] = preRight[i+1] + 1;    
            else   
                preRight[i] = preRight[i+1];    
        }

        // variable to store total number of occurrences
        int counter = 0;

        // loop to find the occurrences of middle element
        for (int i = 1; i < n-1; i++)
        {
            // if middle character of subsequence is found
            // in the string
            if (str[i] == str[1])
            {
                // multiply the total occurrences of first
                // character before middle character with
                // the total occurrences of third character
                // after middle character
                int total = preLeft[i-1] * preRight[i+1];
                counter += total;
            }
        }

        return counter;
    }

    // Driver function
    public static void main(String argc[]){
        String str = "GFGFGYSYIOIWIN";
        String substr = "GFG";

        System.out.println(findOccurrences(str, substr));
    }

    /* This code is contributed by Sagar Shukla */
}
```

## 蟒蛇 3

```
# Python 3 program to find number of
# occurrences of a subsequence of length 3

# Function to find number of occurrences of
# a subsequence of length three in a string
def findOccurrences(str1, substr):

    # calculate length of string
    n = len(str1)

    # auxiliary array to store occurrences of
    # first character
    preLeft = [0 for i in range(n)]

    # auxiliary array to store occurrences of
    # third character
    preRight = [0 for i in range(n)]

    if (str1[0] == substr[0]):
        preLeft[0] += 1

    # calculate occurrences of first character
    # upto ith index from left
    for i in range(1, n):
        if (str1[i] == substr[0]):
            preLeft[i] = preLeft[i - 1] + 1   
        else:
            preLeft[i] = preLeft[i - 1]    

    if (str1[n - 1] == substr[2]):
        preRight[n - 1] += 1

    # calculate occurrences of third character
    # upto ith index from right
    i = n - 2
    while(i >= 0):
        if (str1[i] == substr[2]):
            preRight[i] = preRight[i + 1] + 1   
        else:    
            preRight[i] = preRight[i + 1]

        i -= 1

    # variable to store
    # total number of occurrences
    counter = 0

    # loop to find the occurrences
    # of middle element
    for i in range(1, n - 1):

        # if middle character of subsequence
        # is found in the string
        if (str1[i] == str1[1]):

            # multiply the total occurrences of first
            # character before middle character with
            # the total occurrences of third character
            # after middle character
            total = preLeft[i - 1] * preRight[i + 1]
            counter += total

    return counter

# Driver code
if __name__ == '__main__':
    str1 = "GFGFGYSYIOIWIN"
    substr = "GFG"
    print(findOccurrences(str1, substr))

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# program to find number of occurrences of
// a subsequence of length 3
using System;

public class GfG {

    // Function to find number of occurrences of
    // a subsequence of length three in a string
    public static int findOccurrences(string str1,
                                   string substr1)
    {

        // calculate length of string
        int n = str1.Length;

        // char[] str = str1.toCharArray();
        // char[] substr = substr1.toCharArray();

        // auxiliary array to store occurrences of
        // first character
        int[] preLeft = new int[n];

        // auxiliary array to store occurrences of
        // third character
        int[] preRight = new int[n];

        if (str1[0] == substr1[0])
            preLeft[0]++;

        // calculate occurrences of first character
        // upto ith index from left
        for (int i = 1; i < n; i++)
        {
            if (str1[i] == substr1[0])
                preLeft[i] = preLeft[i-1] + 1;
            else
                preLeft[i] = preLeft[i-1];
        }

        if (str1[n-1] == substr1[2])
            preRight[n-1]++;

        // calculate occurrences of third character
        // upto ith index from right
        for(int i = n-2; i >= 0; i--)
        {
            if (str1[i] == substr1[2])
                preRight[i] = preRight[i+1] + 1;    
            else
                preRight[i] = preRight[i+1];    
        }

        // variable to store total number of occurrences
        int counter = 0;

        // loop to find the occurrences of middle element
        for (int i = 1; i < n-1; i++)
        {

            // if middle character of subsequence is found
            // in the string
            if (str1[i] == str1[1])
            {

                // multiply the total occurrences of first
                // character before middle character with
                // the total occurrences of third character
                // after middle character
                int total = preLeft[i-1] * preRight[i+1];
                counter += total;
            }
        }

        return counter;
    }

    // Driver function
    public static void Main()
    {
        string str1 = "GFGFGYSYIOIWIN";
        string substr1 = "GFG";

        Console.WriteLine(findOccurrences(str1, substr1));
    }
}

/* This code is contributed by Vt_m */
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find number
// of occurrences of a
// subsequence of length 3

// Function to find number
// of occurrences of a
// subsequence of length
// three in a string
function findOccurrences($str,
                         $substr)
{
    // calculate length of string
    $n = strlen($str);

    // auxiliary array to store
    // occurrences of first character
    $preLeft = array(0);

    // auxiliary array to store
    // occurrences of third character
    $preRight = array(0);

    if ($str[0] == $substr[0])
        $preLeft[0]++;

    // calculate occurrences
    // of first character
    // upto ith index from left
    for ($i = 1; $i < $n; $i++)
    {
        if ($str[$i] == $substr[0])
            $preLeft[$i] = $preLeft[$i - 1] + 1;
        else
            $preLeft[$i] = $preLeft[$i - 1];
    }

    if ($str[$n - 1] == $substr[2])
        $preRight[$n - 1]++;

    // calculate occurrences
    // of third character
    // upto ith index from right
    for($i = $n - 2; $i >= 0; $i--)
    {
        if ($str[$i] == $substr[2])
            $preRight[$i] = ($preRight[$i + 1] + 1);
        else
            $preRight[$i] = $preRight[$i + 1];    
    }

    // variable to store total
    // number of occurrences
    $counter = 0;

    // loop to find the occurrences
    // of middle element
    for ($i = 1; $i < $n - 1; $i++)
    {
        // if middle character of
        // subsequence is found
        // in the string
        if ($str[$i] == $str[1])
        {
            // multiply the total occurrences
            // of first character before
            // middle character with the
            // total occurrences of third
            // character after middle character
            $total = $preLeft[$i - 1] *
                     $preRight[$i + 1];
            $counter += $total;
        }
    }

    return $counter;
}

// Driver Code
$str = "GFGFGYSYIOIWIN";
$substr = "GFG";
echo findOccurrences($str, $substr);

// This code is contributed by aj_36
?>
```

## java 描述语言

```
<script>

    // Javascript program to find
    // number of occurrences
    // of a subsequence of length 3

    // Function to find number of occurrences of
    // a subsequence of length three in a string
    function findOccurrences(str, substr)
    {

        // calculate length of string
        let n = str.length;

        // char[] str = str.toCharArray();
        // char[] substr = substr.toCharArray();

        // auxiliary array to store occurrences of
        // first character
        let preLeft = new Array(n);
        preLeft.fill(0);

        // auxiliary array to store occurrences of
        // third character
        let preRight = new Array(n);
        preRight.fill(0);

        if (str[0] == substr[0])
            preLeft[0]++;

        // calculate occurrences of first character
        // upto ith index from left
        for (let i = 1; i < n; i++)
        {
            if (str[i] == substr[0])
                preLeft[i] = preLeft[i-1] + 1;
            else
                preLeft[i] = preLeft[i-1];
        }

        if (str[n-1] == substr[2])
            preRight[n-1]++;

        // calculate occurrences of third character
        // upto ith index from right
        for(let i = n-2; i >= 0; i--)
        {
            if (str[i] == substr[2])
                preRight[i] = preRight[i+1] + 1;   
            else
                preRight[i] = preRight[i+1];   
        }

        // variable to store total
        // number of occurrences
        let counter = 0;

        // loop to find the occurrences
        // of middle element
        for (let i = 1; i < n-1; i++)
        {

            // if middle character of subsequence
            // is found
            // in the string
            if (str[i] == str[1])
            {

                // multiply the total
                // occurrences of first
                // character before middle
                // character with
                // the total occurrences
                // of third character
                // after middle character
                let total = preLeft[i-1] * preRight[i+1];
                counter += total;
            }
        }

        return counter;
    }

    let str = "GFGFGYSYIOIWIN";
    let substr = "GFG";

    document.write(findOccurrences(str, substr));

</script>
```

**输出:**

```
4
```

**时间复杂度**:O(n)
T3】辅助空间 : O(n)
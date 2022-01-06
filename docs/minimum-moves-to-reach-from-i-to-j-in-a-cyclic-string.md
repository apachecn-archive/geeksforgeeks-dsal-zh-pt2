# 循环字符串中从 I 到 j 的最小移动次数

> 原文:[https://www . geeksforgeeks . org/最小移动到达距离-从 I 到 j-in-a-cyclic-string/](https://www.geeksforgeeks.org/minimum-moves-to-reach-from-i-to-j-in-a-cyclic-string/)

给定一个循环字符串 **str** 和两个整数 **i** 和 **j** ，任务是计算从**str【I】**移动到**str【j】**所需的最小步数。移动是为了到达字符串中任何相邻的字符，只有在**字符串【开始】时，移动才算！= start[end]** 其中 **start** 是移动的起始索引， **end** 是结束索引(左侧或右侧相邻)。因为给定的字符串是圆形的，**字符串[0]** 和**字符串[n–1]**彼此相邻。

**示例:**

> **输入:** str = "SSNSS "，i = 0，j = 3
> **输出:** 0
> 从左到右:S - > S - > N - > S
> 从右到左:S - > S - > S
> 
> **输入:** str = "geeksforgeeks "，i = 0，j = 3
> T3】输出: 2

**进场:**

*   从索引 **i** 开始向右移动，直到索引 **j** 为止，对于访问的每个字符，如果当前字符不等于前一个字符，则递增**步长 1 =步长 1 + 1** 。
*   类似地，从 **i** 开始向左移动，直到索引 **0** 为止，对于访问的每个字符，如果当前字符不等于前一个字符，则递增**步长 2 =步长 2 + 1** 。一旦索引 **0** 被访问，开始从索引**n–1**到 **j** 的遍历，如果**str【0】则递增**步长 2** ！= str[n–1]**。
*   最后打印**分钟(第一步，第二步)**。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the count of steps
// required to move from i to j
int getSteps(string str, int i, int j, int n)
{
    // Starting from i + 1
    int k = i + 1;

    // Count of steps
    int steps = 0;

    // Current character
    char ch = str[i];
    while (k <= j) {

        // If current character is different from previous
        if (str[k] != ch) {

            // Increment steps
            steps++;

            // Update current character
            ch = str[k];
        }
        k++;
    }

    // Return total steps
    return steps;
}

// Function to return the minimum number of steps
// required to reach j from i
int getMinSteps(string str, int i, int j, int n)
{

    // Swap the values so that i <= j
    if (j < i) {
        int temp = i;
        i = j;
        j = temp;
    }

    // Steps to go from i to j (left to right)
    int stepsToRight = getSteps(str, i, j, n);

    // While going from i to j (right to left)
    // First go from i to 0
    // then from (n - 1) to j
    int stepsToLeft = getSteps(str, 0, i, n)
                      + getSteps(str, j, n - 1, n);

    // If first and last character is different
    // then it'll add a step to stepsToLeft
    if (str[0] != str[n - 1])
        stepsToLeft++;

    // Return the minimum of two paths
    return min(stepsToLeft, stepsToRight);
}

// Driver code
int main()
{
    string str = "SSNSS";
    int n = str.length();
    int i = 0, j = 3;
    cout << getMinSteps(str, i, j, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach

class GFG
{
    // Function to return the count of steps
    // required to move from i to j
    static int getSteps(String str, int i, int j, int n)
    {
        // Starting from i + 1
        int k = i + 1;

        // Count of steps
        int steps = 0;

        // Current character
        char ch = str.charAt(i);
        while (k <= j) 
        {

            // If current character is different from previous
            if (str.charAt(k) != ch)
            {

                // Increment steps
                steps++;

                // Update current character
                ch = str.charAt(k);
            }
            k++;
        }

        // Return total steps
        return steps;
    }

    // Function to return the minimum number of steps
    // required to reach j from i
    static int getMinSteps(String str, int i, int j, int n)
    {

        // Swap the values so that i <= j
        if (j < i) 
        {
            int temp = i;
            i = j;
            j = temp;
        }

        // Steps to go from i to j (left to right)
        int stepsToRight = getSteps(str, i, j, n);

        // While going from i to j (right to left)
        // First go from i to 0
        // then from (n - 1) to j
        int stepsToLeft = getSteps(str, 0, i, n)
                        + getSteps(str, j, n - 1, n);

        // If first and last character is different
        // then it'll add a step to stepsToLeft
        if (str.charAt(0) != str.charAt(n - 1))
            stepsToLeft++;

        // Return the minimum of two paths
        return Math.min(stepsToLeft, stepsToRight);
    }

    // Driver code
    public static void main(String []args)
    {
        String str = "SSNSS";
        int n = str.length();
        int i = 0, j = 3;
        System.out.println(getMinSteps(str, i, j, n));
    }
}

// This code is contributed by ihritik 
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the count of steps
# required to move from i to j
def getSteps( str,  i, j, n) :

    # Starting from i + 1
    k = i + 1

    # Count of steps
    steps = 0

    # Current character
    ch = str[i]
    while (k <= j): 

        # If current character is different from previous
        if (str[k] != ch): 

            # Increment steps
            steps = steps + 1

            # Update current character
            ch = str[k]

        k = k + 1

    # Return total steps
    return steps

# Function to return the minimum number of steps
# required to reach j from i
def getMinSteps( str, i, j, n):

    # Swap the values so that i <= j
    if (j < i):
        temp = i
        i = j
        j = temp

    # Steps to go from i to j (left to right)
    stepsToRight = getSteps(str, i, j, n)

    # While going from i to j (right to left)
    # First go from i to 0
    # then from (n - 1) to j
    stepsToLeft = getSteps(str, 0, i, n) + getSteps(str, j, n - 1, n)

    # If first and last character is different
    # then it'll add a step to stepsToLeft
    if (str[0] != str[n - 1]):
        stepsToLeft = stepsToLeft + 1

    # Return the minimum of two paths
    return min(stepsToLeft, stepsToRight)

# Driver code

str = "SSNSS"
n = len(str)
i = 0
j = 3
print(getMinSteps(str, i, j, n))

# This code is contributed by ihritik 
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{
    // Function to return the count of steps
    // required to move from i to j
    static int getSteps(string str, int i, int j, int n)
    {
        // Starting from i + 1
        int k = i + 1;

        // Count of steps
        int steps = 0;

        // Current character
        char ch = str[i];
        while (k <= j)
        {

            // If current character is different from previous
            if (str[k] != ch)
            {

                // Increment steps
                steps++;

                // Update current character
                ch = str[k];
            }
            k++;
        }

        // Return total steps
        return steps;
    }

    // Function to return the minimum number of steps
    // required to reach j from i
    static int getMinSteps(string str, int i, int j, int n)
    {

        // Swap the values so that i <= j
        if (j < i) 
        {
            int temp = i;
            i = j;
            j = temp;
        }

        // Steps to go from i to j (left to right)
        int stepsToRight = getSteps(str, i, j, n);

        // While going from i to j (right to left)
        // First go from i to 0
        // then from (n - 1) to j
        int stepsToLeft = getSteps(str, 0, i, n)
                        + getSteps(str, j, n - 1, n);

        // If first and last character is different
        // then it'll add a step to stepsToLeft
        if (str[0] != str[n - 1])
            stepsToLeft++;

        // Return the minimum of two paths
        return Math.Min(stepsToLeft, stepsToRight);
    }

    // Driver code
    public static void Main()
    {
        string str = "SSNSS";
        int n = str.Length;
        int i = 0, j = 3;
        Console.WriteLine(getMinSteps(str, i, j, n));
    }
}

// This code is contributed by ihritik 
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the above approach

// Function to return the count of steps 
// required to move from i to j 
function getSteps($str, $i, $j, $n) 
{ 
    // Starting from i + 1 
    $k = $i + 1; 

    // Count of steps 
    $steps = 0; 

    // Current character 
    $ch = $str[$i]; 
    while ($k <= $j)
    { 

        // If current character is different 
        // from previous 
        if ($str[$k] != $ch) 
        { 

            // Increment steps 
            $steps++; 

            // Update current character 
            $ch = $str[$k]; 
        } 
        $k++; 
    } 

    // Return total steps 
    return $steps; 
} 

// Function to return the minimum number 
// of steps required to reach j from i 
function getMinSteps($str, $i, $j, $n) 
{ 

    // Swap the values so that i <= j 
    if ($j < $i) 
    { 
        $temp = $i; 
        $i = $j; 
        $j = $temp; 
    } 

    // Steps to go from i to j (left to right) 
    $stepsToRight = getSteps($str, $i, $j, $n); 

    // While going from i to j (right to left) 
    // First go from i to 0 then 
    // from (n - 1) to j 
    $stepsToLeft = getSteps($str, 0, $i, $n) + 
                   getSteps($str, $j, $n - 1, $n); 

    // If first and last character is different 
    // then it'll add a step to stepsToLeft 
    if ($str[0] != $str[$n - 1]) 
        $stepsToLeft++; 

    // Return the minimum of two paths 
    return min($stepsToLeft, $stepsToRight); 
} 

// Driver code 
$str = "SSNSS"; 
$n = strlen($str); 
$i = 0;
$j = 3; 
echo getMinSteps($str, $i, $j, $n); 

// This code is contributed by aishwarya.27
?>
```

**Output:**

```
0

```
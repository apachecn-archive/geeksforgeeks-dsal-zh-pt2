# 小于 n 的立方自由数

> 原文:[https://www.geeksforgeeks.org/cube-free-numbers-smaller-n/](https://www.geeksforgeeks.org/cube-free-numbers-smaller-n/)

一个立方自由数[平方自由数](https://www.geeksforgeeks.org/square-free-number/)，其任何除数都不是立方数(一个整数的立方数)。给定一个整数 n，求所有小于或等于 n 的立方自由数。

**示例:**

```
Input :  n = 10
Output : 2 3 4 5 6 7 9 10
Note that only 1 and 8 are missing. 

Input : 20
Output : 2 3 4 5 6 7 9 10 11 12 13 14 
         15 17 18 19 20 
```

一个**简单的解决方案**是遍历从 1 到 n 的所有数字。对于每个数字，检查它是否是自由立方体。如果是，那就打印出来。

## C++

```
// Simple C++ Program to print all cube free
// numbers smaller than or equal to n.
#include <bits/stdc++.h>
using namespace std;

// Returns true if n is a cube free
// number, else returns false.
bool isCubeFree(int n)
{
    if (n == 1)
        return false;

    // check for all possible divisible cubes
    for (int i = 2; i * i * i <= n; i++)
        if (n % (i * i * i) == 0)
            return false;

    return true;
}

// Print all cube free numbers smaller
// than n.
void printCubeFree(int n)
{
    for (int i = 2; i <= n; i++)
        if (isCubeFree(i))
            cout << i << " ";
}

/* Driver program to test above function */
int main()
{
    int n = 20;
    printCubeFree(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to print all cube free
// numbers smaller than or equal to n.

class GFG
{
    // Returns true if n is a cube free
    // number, else returns false.
    public static boolean isCubeFree(int n)
    {
        if (n == 1)
            return false;

        // check for all possible divisible cubes
        for (int i = 2; i * i * i <= n; i++)
            if (n % (i * i * i) == 0)
                return false;

        return true;
    }

    // Print all cube free numbers smaller
    // than n.
    public static void printCubeFree(int n)
    {
        for (int i = 2; i <= n; i++)
        {
            if (isCubeFree(i))
            {
                System.out.print ( i + " ");
            }   
        }
    }

    // Driver program
    public static void main(String[] args)
    {
        int n = 20;
        printCubeFree(n);
    }
}

// Contributed by _omg
```

## 蟒蛇 3

```
# Python3 Program to print all cube free
# numbers smaller than or equal to n.

import math

# Returns true if n is a cube free
# number, else returns false.
def isCubeFree( n ):
    if n == 1:
        return False

    # check for all possible divisible cubes
    for i in range(2, int(n ** (1 / 3) + 1)):
        if (n % (i * i * i) == 0):
            return False;

    return True;

# Print all cube free numbers smaller
# than n.   
def printCubeFree( n ):
    for i in range(2, n+1):
        if (isCubeFree(i)):
            print ( i , end= " ")

n = 20
printCubeFree(n)

# Contributed by _omg
```

## C#

```
// C# Program to print all cube free
// numbers smaller than or equal to n.
using System;

class GFG
{
    // Returns true if n is a cube free
    // number, else returns false.
    static bool isCubeFree(int n)
    {
        if (n == 1)
            return false;

        // check for all possible divisible cubes
        for (int i = 2; i * i * i <= n; i++)
            if (n % (i * i * i) == 0)
                return false;

        return true;
    }

    // Print all cube free numbers smaller
    // than n.
    static void printCubeFree(int n)
    {
        for (int i = 2; i <= n; i++)
        {
            if (isCubeFree(i))
            {
                Console.Write ( i + " ");
            }
        }
    }

    public static void Main()
    {
        int n = 20;
        printCubeFree(n);
    }
}

// Contributed by _omg
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// Simple PHP Program to
// print all cube free
// numbers smaller than
// or equal to n.

// Returns true if n is
// a cube free number,
// else returns false.
function isCubeFree($n)
{
    if ($n == 1)
        return false;

    // check for all possible
    // divisible cubes
    for ($i = 2;
         $i * $i * $i <= $n; $i++)
        if ($n % ($i * $i * $i) == 0)
            return false;

    return true;
}

// Print all cube free
// numbers smaller than n.
function printCubeFree($n)
{
    for ($i = 2; $i <= $n; $i++)
        if (isCubeFree($i))
            echo $i . " ";
}

// Driver code
$n = 20;
printCubeFree($n);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// JavaScript program to print all cube free
// numbers smaller than or equal to n.

// Returns true if n is a cube free
// number, else returns false.
function isCubeFree(n)
{
    if (n == 1)
        return false;

    // Check for all possible divisible cubes
    for(let i = 2; i * i * i <= n; i++)
        if (n % (i * i * i) == 0)
            return false;

    return true;
}

// Print all cube free numbers smaller
// than n.
function prletCubeFree(n)
{
    for(let i = 2; i <= n; i++)
    {
        if (isCubeFree(i))
        {
            document.write ( i + " ");
        }   
    }
}

// Driver code
let N = 20;

prletCubeFree(N);

// This code is contributed by code_hunt

</script>
```

**Output:** 

```
2 3 4 5 6 7 9 10 11 12 13 14 15 17 18 19 20
```

一个**有效的解决方案**是使用厄拉多塞的[筛像技术，洗出非立方自由数。这里我们将创建布尔筛数组并用真值初始化它。现在，我们将从 2 开始迭代变量“div ”,并开始将 div 的立方倍数标记为假，因为它们将是非立方自由数。然后，剩下值为真的元素将是立方体自由数。](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)

## C++

```
// Efficient C++ Program to print all
// cube free numbers smaller than or
// equal to n.
#include <bits/stdc++.h>
using namespace std;

void printCubeFree(int n)
{
    // Initialize all numbers as not cube free
    bool cubFree[n + 1];
    for (int i = 0; i <= n; i++)
        cubFree[i] = true;

    // Traverse through all possible cube roots
    for (int i = 2; i * i * i <= n; i++) {

        // If i itself is cube free
        if (cubFree[i]) {

            // Mark all multiples of i as not cube free
            for (int multiple = 1; i * i * i * multiple <= n;
                                                  multiple++)
            {
                cubFree[i * i * i * multiple] = false;
            }
        }
    }

    // Print all cube free numbers
    for (int i = 2; i <= n; i++) {
        if (cubFree[i] == true)
            cout<<i<<" ";
    }
}

// Driver code
int main()
{
    printCubeFree(20);
    return 0;
}

// This code is contributed by Ajit.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Efficient Java Program to print all cube free
// numbers smaller than or equal to n.
class GFG {

    public static void printCubeFree(int n)
    {
        // Initialize all numbers as not cube free
        boolean[] cubFree = new boolean[n + 1];
        for (int i = 0; i <= n; i++)
            cubFree[i] = true;

        // Traverse through all possible cube roots
        for (int i = 2; i * i * i <= n; i++) {

            // If i itself is cube free
            if (cubFree[i]) {

                // Mark all multiples of i as not cube free
                for (int multiple = 1; i * i * i * multiple <= n;
                                                   multiple++) {

                    cubFree[i * i * i * multiple] = false;
                }
            }
        }

        // Print all cube free numbers
        for (int i = 2; i <= n; i++) {
            if (cubFree[i] == true)
                System.out.print(i + " ");
        }
    }

    public static void main(String[] args)
    {
        printCubeFree(20);
    }
}
```

## 蟒蛇 3

```
# Efficient Python3 Program to
# print all cube free
# numbers smaller than or
# equal to n.

def printCubeFree(n):
    # Initialize all numbers
    # as not cube free
    cubFree = [1]*(n + 1);

    # Traverse through all
    # possible cube roots
    i = 2;
    while(i * i * i <= n):

        # If i itself
        # is cube free
        if(cubFree[i]==1):

            # Mark all multiples of
            # i as not cube free
            multiple = 1;
            while(i * i * i * multiple <= n):
                cubFree[i * i * i * multiple] = 0;
                multiple+=1;
        i+=1;
    # Print all cube
    # free numbers
    for i in range(2,n+1):
        if (cubFree[i] == 1):
            print(i,end=" ");

# Driver Code
if __name__ == "__main__":
    printCubeFree(20);

# This code is contributed
# by mits
```

## C#

```
// Efficient C# Program to
// print all cube free
// numbers smaller than or
// equal to n.
using System;

class GFG
{
public static void printCubeFree(int n)
{

// Initialize all numbers
// as not cube free
bool[] cubFree = new bool[n + 1];
for (int i = 0;
         i <= n; i++)
    cubFree[i] = true;

// Traverse through all
// possible cube roots
for (int i = 2;
         i * i * i <= n; i++)
{

    // If i itself
    // is cube free
    if (cubFree[i])
    {

        // Mark all multiples of
        // i as not cube free
        for (int multiple = 1;
                 i * i * i * multiple <= n;
                 multiple++)
        {
            cubFree[i * i * i *
                    multiple] = false;
        }
    }
}

// Print all cube
// free numbers
for (int i = 2; i <= n; i++)
{
    if (cubFree[i] == true)
        Console.Write(i + " ");
}
}

// Driver Code
public static void Main()
{
    printCubeFree(20);
}
}

// This code is contributed
// by Akanksha Rai(Abby_akku)
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// Efficient PHP Program to
// print all cube free
// numbers smaller than or
// equal to n.

function printCubeFree($n)
{
    // Initialize all numbers
    // as not cube free
    $cubFree = array_fill(0,($n + 1), 1);

    // Traverse through all
    // possible cube roots
    $i = 2;
    while($i * $i * $i <= $n)
    {

        // If i itself
        // is cube free
        if($cubFree[$i] == 1)
        {
            // Mark all multiples of
            // i as not cube free
            $multiple = 1;
            while($i * $i * $i * $multiple <= $n)
                {
                    $cubFree[$i * $i *
                             $i * $multiple] = 0;
                    $multiple += 1;
                }
        }
        $i += 1;
    }

    // Print all cube
    // free numbers
    for($i = 2; $i < $n + 1; $i++)
        if ($cubFree[$i] == 1)
            echo $i . " ";
}

// Driver Code
printCubeFree(20);

// This code is contributed
// by mits
?>
```

## java 描述语言

```
<script>

// Efficient Javascript program to print
// all cube free numbers smaller than or
// equal to n.   
function printCubeFree(n)
{

    // Initialize all numbers as not
    // cube free
    var cubFree = Array(n + 1).fill(false);
    for(i = 0; i <= n; i++)
        cubFree[i] = true;

    // Traverse through all possible cube roots
    for(i = 2; i * i * i <= n; i++)
    {

        // If i itself is cube free
        if (cubFree[i])
        {

            // Mark all multiples of i as not cube free
            for(multiple = 1; i * i * i * multiple <= n;
                multiple++)
            {
                cubFree[i * i * i * multiple] = false;
            }
        }
    }

    // Print all cube free numbers
    for(i = 2; i <= n; i++)
    {
        if (cubFree[i] == true)
            document.write(i + " ");
    }
}

// Driver code
printCubeFree(20);

// This code is contributed by aashish1995

</script>
```

**Output:** 

```
2 3 4 5 6 7 9 10 11 12 13 14 15 17 18 19 20
```
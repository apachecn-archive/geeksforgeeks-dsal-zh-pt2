# 将 N 写成三个数之和的方式数

> 原文:[https://www . geeksforgeeks . org/写 n 作为三个数字之和的次数/](https://www.geeksforgeeks.org/count-of-ways-to-write-n-as-a-sum-of-three-numbers/)

给定一个**正整数 N** ，将 N 写成三个数之和的方式数。对于无法表达的数字，打印-1。
**例:**

> **输入:** N = 4
> **输出:** 3
> **解释:**
> (1+1+2)= 4
> (1+2+1)= 4
> (2+1+1)= 4。
> 所以总共有 3 种方式。
> **输入:** N = 5
> **输出:**6
> (1+1+3)= 5
> (1+3+1)= 5
> (3+1+1)= 5
> (1+2+2)= 5
> (2+2+1)= 5
> (2+1+2)= 5。
> 所以总共有 6 种方式

**方法:**为了解决上面提到的问题，如果我们仔细观察，我们会观察到问题解决方案中的一种模式。对于所有大于 2 的数，我们得到 3、6、10、15、25 等数列，这不过是**[**前 N-1 个自然数的和**](https://www.geeksforgeeks.org/sum-of-natural-numbers-using-recursion/) **。**
以下是上述方法的实施:** 

## **C++**

```
// C++ program to count the total number of
// ways to write N as a sum of three numbers

#include <bits/stdc++.h>
using namespace std;

// Function to find the number of ways
void countWays(int n)
{
    // Check if number is less than 2
    if (n <= 2)
        cout << "-1";

    else {
        // Calculate the sum
        int ans = (n - 1) * (n - 2) / 2;

        cout << ans;
    }
}

// Driver code
int main()
{
    int N = 5;

    countWays(N);

    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java program to count the total number of
// ways to write N as a sum of three numbers
class GFG{

// Function to find the number of ways
static void countWays(int n)
{

    // Check if number is less than 2
    if (n <= 2)
    {
        System.out.print("-1");
    }
    else
    {

        // Calculate the sum
        int ans = (n - 1) * (n - 2) / 2;
        System.out.print(ans);
    }
}

// Driver code
public static void main(String[] args)
{
    int N = 5;
    countWays(N);
}
}

// This code is contributed by Amit Katiyar
```

## **蟒蛇 3**

```
# Python3 program to count the total number of
# ways to write N as a sum of three numbers
def countWays(N):

    # Check if number is less than 2
    if (N <= 2):
        print("-1")
    else:

        # Calculate the sum
        ans = (N - 1) * (N - 2) / 2

    print(ans)

# Driver code
if __name__ == '__main__':

    N = 5
    countWays(N)

# This code is contributed by coder001
```

## **C#**

```
// C# program to count the total number of
// ways to write N as a sum of three numbers
using System;

class GFG{

// Function to find the number of ways
static void countWays(int n)
{

    // Check if number is less than 2
    if (n <= 2)
    {
        Console.WriteLine("-1");
    }
    else
    {

        // Calculate the sum
        int ans = (n - 1) * (n - 2) / 2;
        Console.WriteLine(ans);
    }
}

// Driver code    
static void Main()
{
    int N = 5;
    countWays(N);
}
}

// This code is contributed by divyeshrabadiya07   
```

## **java 描述语言**

```
<script>

// Javascript program to count the total number of
// ways to write N as a sum of three numbers

// Function to find the number of ways
function countWays(n)
{
    // Check if number is less than 2
    if (n <= 2)
        document.write( "-1");

    else {
        // Calculate the sum
        var ans = (n - 1) * (n - 2) / 2;

        document.write( ans);
    }
}

// Driver code

var N = 5;
countWays(N);

</script>
```

****Output:** 

```
6
```** 

*****时间复杂度:** O(1)***
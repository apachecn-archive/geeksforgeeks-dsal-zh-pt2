# 删除给定数的位数形成的唯一素数的个数

> 原文:[https://www . geeksforgeeks . org/唯一素数计数-通过删除给定数字的位数形成/](https://www.geeksforgeeks.org/count-of-unique-prime-numbers-formed-by-deleting-digits-of-given-number/)

给定一个数 **N，**的任务是统计唯一的[质数](https://www.geeksforgeeks.org/prime-numbers/)的个数，这个质数可以通过删除给定数的零个或多个数字而形成。

**示例:**

> **输入:** N = 132
> **输出:** 3
> **说明:**
> 给定数字 132 的零个或多个数字删除后形成的质数总数为 3 即[3，2，13]。
> 
> **输入:**N = 2222
> T3】输出: 1

**逼近**:这个问题可以用[递归](https://www.geeksforgeeks.org/recursion/)来解决，对于每个数字有两个选择，要么包含这个数字，要么不包含这个数字。对于每个选项，[检查形成的数字是否是质数](https://www.geeksforgeeks.org/python-program-to-check-whether-a-number-is-prime-or-not/)。按照以下步骤解决此问题:

*   初始化一个[哈希集](https://www.geeksforgeeks.org/hashset-in-java/)说**素数**来存储唯一的[素数](https://www.geeksforgeeks.org/primality-test-set-1-introduction-and-school-method/)数。
*   声明一个函数，比如说，**unique 素数(number，ans，index)** ，传递数字串 **N，ans** 为空[串](https://www.geeksforgeeks.org/string-data-structure/)和**索引 0** 为参数。
    *   **基本情况:**如果索引达到[字符串](https://www.geeksforgeeks.org/string-class-in-java/)的长度，则[将字符串转换为整数](https://www.geeksforgeeks.org/converting-strings-numbers-cc/)和[检查形成的数字是否为素数](https://www.geeksforgeeks.org/python-program-to-check-whether-a-number-is-prime-or-not/)如果[为素数](https://www.geeksforgeeks.org/primality-test-set-1-introduction-and-school-method/)，则在 [HashSet](https://www.geeksforgeeks.org/hashset-in-java/) 和 **Primes** 中添加数字。
    *   调用**unique 素数**函数进行两种选择，或者取字符即**unique 素数(数字，ans + number.charAt(index)，index + 1)** 或者留下字符即**unique 素数(数字，ans，index + 1)** 。
*   完成以上步骤后，打印 [HashSet](https://www.geeksforgeeks.org/hashset-in-java/) **Primes** 的**大小**作为所需答案。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check whether the number
// is prime or not
bool checkprime(int n)
{
    // If n is 1
    if (n == 1) {
        return false;
    }

    // If n is 2 or 3
    if (n == 2 || n == 3) {
        return true;
    }

    // If n is multiple of 2, 3 or 6
    else if (n % 2 == 0 || n % 3 == 0
             || n % 6 == 0) {
        return false;
    }

    // Traversing till sqrt(n)
    for (int i = 6; i * i <= n; i += 6) {
        if (n % (i - 1) == 0
            || n % (i + 1) == 0) {
            return false;
        }
    }
    return true;
}

// To store the unique prime numbers
set<int> Primes;

// Function to Count the total number
// of unique prime number formed by
// deleting zero or more digits of the
// given number
void uniquePrimeNums(string number, string ans, int index)
{
    // Base Case
    if (index == number.length()) {

        if (ans.length() != 0)

            // Check whether the number is
            // prime or not
            if (checkprime(stoi(ans))) {

                // Adding to the HashSet
                Primes.insert(stoi(ans));
            }

        return;
    }

    // Recursive call by taking the character
    // at index
    uniquePrimeNums(number,
                    ans + number[index],
                    index + 1);

    // Recursive call by not taking the
    // character
    uniquePrimeNums(number, ans, index + 1);
}

int main()
{
    // Given Input
    int number = 132;

    // Function Call
    uniquePrimeNums("" + to_string(number), "", 0);
    cout << Primes.size();

    return 0;
}

// This code is contributed by divyeshrabadiya07.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.util.*;

public class GFG {

    // Function to check whether the number
    // is prime or not
    static boolean checkprime(int n)
    {
        // If n is 1
        if (n == 1) {
            return false;
        }

        // If n is 2 or 3
        if (n == 2 || n == 3) {
            return true;
        }

        // If n is multiple of 2, 3 or 6
        else if (n % 2 == 0 || n % 3 == 0
                 || n % 6 == 0) {
            return false;
        }

        // Traversing till sqrt(n)
        for (int i = 6; i * i <= n; i += 6) {
            if (n % (i - 1) == 0
                || n % (i + 1) == 0) {
                return false;
            }
        }
        return true;
    }

    // To store the unique prime numbers
    static HashSet<Integer> Primes
        = new HashSet<>();

    // Function to Count the total number
    // of unique prime number formed by
    // deleting zero or more digits of the
    // given number
    static void uniquePrimeNums(
        String number, String ans, int index)
    {
        // Base Case
        if (index == number.length()) {

            if (ans.length() != 0)

                // Check whether the number is
                // prime or not
                if (checkprime(Integer.parseInt(ans))) {

                    // Adding to the HashSet
                    Primes.add(Integer.parseInt(ans));
                }

            return;
        }

        // Recursive call by taking the character
        // at index
        uniquePrimeNums(number,
                        ans + number.charAt(index),
                        index + 1);

        // Recursive call by not taking the
        // character
        uniquePrimeNums(number, ans, index + 1);
    }

    // Driver Code
    public static void main(String[] args)
    {
        // Given Input
        int number = 132;

        // Function Call
        uniquePrimeNums("" + number, "", 0);
        System.out.println(Primes.size());
    }
}
```

## 蟒蛇 3

```
# Python3 program for the above approach
import math

# Function to check whether the number
# is prime or not
def checkprime(n):

    # If n is 1
    if (n == 1):
        return False

    # If n is 2 or 3
    if (n == 2 or n == 3):
        return True

    # If n is multiple of 2, 3 or 6
    elif (n % 2 == 0 or n % 3 == 0 or
          n % 6 == 0):
        return False

    # Traversing till sqrt(n)
    k = int(math.sqrt(n))
    for i in range(6, k+1, 6):
        if (n % (i - 1) == 0 or n % (i + 1) == 0):
            return False

    return True

# Function to Count the total number
# of unique prime number formed by
# deleting zero or more digits of the
# given number
def uniquePrimeNums(number, ans, index):

    # Base Case
    length = len(list(number))

    if (index == length):
        if (len(ans) != 0):

            # Check whether the number is
            # prime or not
            if (checkprime(int(ans))):

                # Adding to the HashSet
                Primes.add(int(ans))
        return

    # Recursive call by taking the character
    # at index
    uniquePrimeNums(number, ans + number[index],
                          index + 1)

    # Recursive call by not taking the
    # character
    uniquePrimeNums(number, ans, index + 1)
    return

# To store the unique prime numbers
Primes = set()

# Driver code
if __name__ == '__main__':

    # Given Input
    number = 132

    # Function Call
    uniquePrimeNums(str(number), "", 0)
    print(len(Primes))

# This code is contributed by MuskanKalra1
```

## C#

```
using System;
using System.Collections.Generic;
public class GFG {
    static bool checkprime(int n)
    {
        // If n is 1
        if (n == 1) {
            return false;
        }

        // If n is 2 or 3
        if (n == 2 || n == 3) {
            return true;
        }

        // If n is multiple of 2, 3 or 6
        else if (n % 2 == 0 || n % 3 == 0 || n % 6 == 0) {
            return false;
        }

        // Traversing till sqrt(n)
        for (int i = 6; i * i <= n; i += 6) {
            if (n % (i - 1) == 0 || n % (i + 1) == 0) {
                return false;
            }
        }
        return true;
    }

    // To store the unique prime numbers
    static HashSet<int> Primes = new HashSet<int>();

    // Function to Count the total number
    // of unique prime number formed by
    // deleting zero or more digits of the
    // given number
    static void uniquePrimeNums(String number, String ans,
                                int index)
    {
        // Base Case
        if (index == number.Length) {

            if (ans.Length != 0)

                // Check whether the number is
                // prime or not
                if (checkprime(int.Parse(ans))) {

                    // Adding to the HashSet
                    Primes.Add(int.Parse(ans));
                }

            return;
        }

        // Recursive call by taking the character
        // at index
        uniquePrimeNums(number, ans + number[index],
                        index + 1);

        // Recursive call by not taking the
        // character
        uniquePrimeNums(number, ans, index + 1);
    }

    // Driver Code
    static public void Main()
    {
        int number = 132;

        // Function Call
        uniquePrimeNums("" + number, "", 0);
        Console.WriteLine(Primes.Count);
    }
}

// This code is contributed by maddler.
```

## java 描述语言

```
<script>

// JavaScript implementation of
// the above approach

    // Function to check whether the number
    // is prime or not
    function checkprime(n)
    {
        // If n is 1
        if (n == 1) {
            return false;
        }

        // If n is 2 or 3
        if (n == 2 || n == 3) {
            return true;
        }

        // If n is multiple of 2, 3 or 6
        else if (n % 2 == 0 || n % 3 == 0
                 || n % 6 == 0) {
            return false;
        }

        // Traversing till sqrt(n)
        for (let i = 6; i * i <= n; i += 6) {
            if (n % (i - 1) == 0
                || n % (i + 1) == 0) {
                return false;
            }
        }
        return true;
    }

    // To store the unique prime numbers
    var Primes
        = new Set();

    // Function to Count the total number
    // of unique prime number formed by
    // deleting zero or more digits of the
    // given number
    function uniquePrimeNums(
        number, ans, index)
    {
        // Base Case
        if (index == number.length) {

            if (ans.length != 0)

                // Check whether the number is
                // prime or not
                if (checkprime(parseInt(ans))) {

                    // Adding to the HashSet
                    Primes.add(parseInt(ans));
                }

            return;
        }

        // Recursive call by taking the character
        // at index
        uniquePrimeNums(number,
                        ans + number[index],
                        index + 1);

        // Recursive call by not taking the
        // character
        uniquePrimeNums(number, ans, index + 1);
    }

// Driver Code

    // Given Input
        let number = 132;

        // Function Call
        uniquePrimeNums("" + number, "", 0);
        document.write(Primes.size);

</script>
```

**Output**

```
3
```

***时间复杂度:**O(2<sup>N</sup>* sqrt(N))*
***辅助空间:** O(2 <sup>N</sup> )*
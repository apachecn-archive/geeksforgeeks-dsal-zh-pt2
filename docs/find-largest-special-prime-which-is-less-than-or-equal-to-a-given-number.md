# 求小于等于给定数的最大特殊素数

> 原文:[https://www . geesforgeks . org/find-最大-特殊-质数-小于或等于给定数/](https://www.geeksforgeeks.org/find-largest-special-prime-which-is-less-than-or-equal-to-a-given-number/)

给定一个数 n，任务是找到小于或等于 n 的最大特殊素数
A **特殊素数**是一个数，它可以通过一个接一个地放置数字来创建，这样得到的所有数都是素数。
T4【示例】T5:

```
Input : N = 379
Output : 379
Explanation: 379 can be created as => 3 => 37 => 379
Here, all the numbers ie. 3, 37, 379 are prime.

Input : N = 100
Output : 79
Explanation: 79 can be created as => 7 => 79, 
where both 7, 79 are prime numbers.
```

**方法:**想法是使用埃拉托斯特尼的[筛子。构建 N 的筛阵列。然后从 N 开始迭代，检查这个数是否是质数。如果它是质数，那么检查它是否是特殊质数。
现在，检查一个数是否是特殊素数。继续将数字除以 10，并在每一点检查剩余的数字是否是质数，这可以通过参考我们构建的筛数组来实现。
以下是上述方法的实施:](https://www.geeksforgeeks.org/sieve-of-eratosthenes/) 

## C++

```
// CPP program to find the Largest Special Prime
// which is less than or equal to a given number

#include <bits/stdc++.h>
using namespace std;

// Function to check whether the number
// is a special prime or not
bool checkSpecialPrime(bool* sieve, int num)
{
    // While number is not equal to zero
    while (num) {
        // If the number is not prime
        // return false.
        if (!sieve[num]) {
            return false;
        }

        // Else remove the last digit
        // by dividing the number by 10.
        num /= 10;
    }

    // If the number has become zero
    // then the number is special prime,
    // hence return true
    return true;
}

// Function to find the Largest Special Prime
// which is less than or equal to a given number
void findSpecialPrime(int N)
{
    bool sieve[N + 10];

    // Initially all numbers are considered Primes.
    memset(sieve, true, sizeof(sieve));
    sieve[0] = sieve[1] = false;
    for (long long i = 2; i <= N; i++) {
        if (sieve[i]) {

            for (long long j = i * i; j <= N; j += i) {
                sieve[j] = false;
            }
        }
    }

    // There is always an answer possible
    while (true) {
        // Checking if the number is a
        // special prime or not
        if (checkSpecialPrime(sieve, N)) {
            // If yes print the number
            // and break the loop.
            cout << N << '\n';
            break;
        }
        // Else decrement the number.
        else
            N--;
    }
}

// Driver code
int main()
{
    findSpecialPrime(379);
    findSpecialPrime(100);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the Largest Special Prime
// which is less than or equal to a given number

class GFG
{

        // Function to check whether the number
        // is a special prime or not
    static boolean checkSpecialPrime(boolean [] sieve, int num)
        {
            // While number is not equal to zero
            while (num!=0) {
                // If the number is not prime
                // return false.
                if (!sieve[num]) {
                    return false;
                }

                // Else remove the last digit
                // by dividing the number by 10.
                num /= 10;
            }

            // If the number has become zero
            // then the number is special prime,
            // hence return true
            return true;
        }

        // Function to find the Largest Special Prime
        // which is less than or equal to a given number
        static void findSpecialPrime(int N)
        {
            boolean []sieve=new boolean[N+10];
            sieve[0] = sieve[1] = false;

            // Initially all numbers are considered Primes.
            for(int i=0;i<N+10;i++)
                sieve[i]=true;

            for (int i = 2; i <= N; i++) {
                if (sieve[i]) {

                    for ( int j = i * i; j <= N; j += i) {
                        sieve[j] = false;
                    }
                }
            }

            // There is always an answer possible
            while (true) {
                // Checking if the number is a
                // special prime or not
                if (checkSpecialPrime(sieve, N)) {
                    // If yes print the number
                    // and break the loop.
                    System.out.println(N);
                    break;
                }
                // Else decrement the number.
                else
                    N--;
            }
        }

        // Driver code
        public static void main(String [] args)
        {
            findSpecialPrime(379);
            findSpecialPrime(100);

        }

// This code is contributed by ihritik

}
```

## 蟒蛇 3

```
# Python 3 program to find the Largest
# Special Prime which is less than or
# equal to a given number

# Function to check whether the number
# is a special prime or not
def checkSpecialPrime(sieve, num):

    # While number is not equal to zero
    while (num) :

        # If the number is not prime
        # return false.
        if (not sieve[num]) :
            return False

        # Else remove the last digit
        # by dividing the number by 10.
        num //= 10

    # If the number has become zero
    # then the number is special prime,
    # hence return true
    return True

# Function to find the Largest Special
# Prime which is less than or equal to
# a given number
def findSpecialPrime(N):

    # Initially all numbers are
    # considered Primes.
    sieve = [True] * (N + 10)
    sieve[0] = sieve[1] = False;
    for i in range(2, N + 1) :
        if (sieve[i]) :

            for j in range(i * i, N + 1, i) :
                sieve[j] = False

    # There is always an answer possible
    while (True) :

        # Checking if the number is
        # a special prime or not
        if (checkSpecialPrime(sieve, N)):

            # If yes print the number
            # and break the loop.
            print( N)
            break

        # Else decrement the number.
        else:
            N -= 1

# Driver code
if __name__ == "__main__":
    findSpecialPrime(379)
    findSpecialPrime(100)

# This code is contributed
# by ChitraNayal
```

## C#

```
// C# program to find the Largest Special Prime
// which is less than or equal to a given number

using System;
class GFG
{

        // Function to check whether the number
        // is a special prime or not
    static bool checkSpecialPrime(bool [] sieve, int num)
        {
            // While number is not equal to zero
            while (num!=0) {
                // If the number is not prime
                // return false.
                if (!sieve[num]) {
                    return false;
                }

                // Else remove the last digit
                // by dividing the number by 10.
                num /= 10;
            }

            // If the number has become zero
            // then the number is special prime,
            // hence return true
            return true;
        }

        // Function to find the Largest Special Prime
        // which is less than or equal to a given number
        static void findSpecialPrime(int N)
        {
            bool []sieve=new bool[N+10];

            // Initially all numbers are considered Primes.
            for(int i = 0; i < N + 10; i++)
                sieve[i] = true;

            sieve[0] = sieve[1] = false;
            for (int i = 2; i <= N; i++) {
                if (sieve[i]) {

                    for ( int j = i * i; j <= N; j += i) {
                        sieve[j] = false;
                    }
                }
            }

            // There is always an answer possible
            while (true) {
                // Checking if the number is a
                // special prime or not
                if (checkSpecialPrime(sieve, N)) {
                    // If yes print the number
                    // and break the loop.
                    Console.WriteLine(N);
                    break;
                }
                // Else decrement the number.
                else
                    N--;
            }
        }

        // Driver code
        public static void Main()
        {
            findSpecialPrime(379);
            findSpecialPrime(100);

        }

// This code is contributed by ihritik

}
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find the Largest
// Special Prime which is less than
// or equal to a given number

// Function to check whether the number
// is a special prime or not
function checkSpecialPrime(&$sieve, $num)
{
    // While number is not equal to zero
    while ($num)
    {
        // If the number is not prime
        // return false.
        if (!$sieve[$num])
        {
            return false;
        }

        // Else remove the last digit
        // by dividing the number by 10.
        $num = (int)($num / 10);
    }

    // If the number has become zero
    // then the number is special prime,
    // hence return true
    return true;
}

// Function to find the Largest Special Prime
// which is less than or equal to a given number
function findSpecialPrime($N)
{

    // Initially all numbers are
    // considered Primes.
    $sieve = array_fill(0, $N + 10, true);
    $sieve[0] = $sieve[1] = false;

    for ($i = 2; $i <= $N; $i++)
    {
        if ($sieve[$i])
        {
            for ($j = $i * $i; $j <= $N; $j += $i)
            {
                $sieve[$j] = false;
            }
        }
    }

    // There is always an answer possible
    while (true)
    {

        // Checking if the number is a
        // special prime or not
        if (checkSpecialPrime($sieve, $N))
        {
            // If yes print the number
            // and break the loop.

            echo $N . "\n";
            break;
        }

        // Else decrement the number.
        else
            $N--;
    }
}

// Driver code
findSpecialPrime(379);
findSpecialPrime(100);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>
// Javascript program to find the Largest Special Prime
// which is less than or equal to a given number

    // Function to check whether the number
        // is a special prime or not
    function checkSpecialPrime(sieve,num)
    {
         // While number is not equal to zero
            while (num!=0) {
                // If the number is not prime
                // return false.
                if (!sieve[num]) {
                    return false;
                }

                // Else remove the last digit
                // by dividing the number by 10.
                num =Math.floor(num/ 10);
            }

            // If the number has become zero
            // then the number is special prime,
            // hence return true
            return true;
    }

    // Function to find the Largest Special Prime
        // which is less than or equal to a given number
    function findSpecialPrime(N)
    {
        let sieve=new Array(N+10);
            sieve[0] = sieve[1] = false;

            // Initially all numbers are considered Primes.
            for(let i=0;i<N+10;i++)
                sieve[i]=true;

            for (let i = 2; i <= N; i++) {
                if (sieve[i]) {

                    for ( let j = i * i; j <= N; j += i) {
                        sieve[j] = false;
                    }
                }
            }

            // There is always an answer possible
            while (true) {
                // Checking if the number is a
                // special prime or not
                if (checkSpecialPrime(sieve, N)) {
                    // If yes print the number
                    // and break the loop.
                    document.write(N+"<br>");
                    break;
                }
                // Else decrement the number.
                else
                    N--;
            }
    }

    // Driver code
    findSpecialPrime(379);
    findSpecialPrime(100);

// This code is contributed by rag2127
</script>
```

**Output:** 

```
379
79
```

**时间复杂度:** O(N*log(log N))
# 费马因式分解法

> 原文:[https://www.geeksforgeeks.org/fermats-factorization-method/](https://www.geeksforgeeks.org/fermats-factorization-method/)

**费马因式分解法**是以奇数表示为两个平方之差。
对于整数 **n** ，我们需要 **a** 和 **b** ，如:

```
n = a<sup>2 - b2 = (a+b)(a-b)</sup> 

where (a+b) and (a-b) are
the factors of the number n
```

**例:**

```
Input: n = 6557
Output: [79,83]
Explanation: 
For the above value, 
the first try for a is ceil value 
of square root of 6557, which is 81.

Then, 
b2 = 812 - 6557 = 4,
as it is a perfect square.
So, b = 2

So, the factors of 6557 are:  
(a - b) = 81 -2  = 79 & 
(a + b) = 81 + 2 = 83.
```

**进场:**

1.  如果 n = pq 是 n 分解成两个正整数，那么，既然 n 是奇数，那么 p 和 q 都是奇数。
2.  设 a = 1/2 * (p+q)和 b = 1/2 * (q-p)。
3.  因为 a 和 b 都是整数，所以 p =(a–b)和 q = (a + b)。
4.  所以，**n = pq =(a–b)(a+b)= a<sup>2</sup>–b<sup>2</sup>T5】**
5.  对于质数，我们回到 b = 1，因为一个质数的一个因子是 1。
6.  while 循环确保了这一操作

以下是上述方法的实施

## C++

```
// C++ implementation of fermat's factorization
#include<bits/stdc++.h>

using namespace std;

    // This function finds the value of a and b
    // and returns a+b and a-b
    void FermatFactors(int n)
    {

        // since fermat's factorization applicable
        // for odd positive integers only
        if(n <= 0)
        {
            cout << "[" << n << "]";
            return;
        }

        // check if n is a even number
        if((n & 1) == 0)
        {
            cout << "[" << n / 2.0 << "," << 2 << "]";
            return;
        }

        int a = ceil(sqrt(n)) ;

        // if n is a perfect root,
        // then both its square roots are its factors
        if(a * a == n)
        {
            cout << "[" << a << "," << a << "]";
            return;
        }
        int b;
        while(true)
        {
            int b1 = a * a - n ;
            b = (int)sqrt(b1) ;

            if(b * b == b1)
                break;
            else
                a += 1;
        }
        cout << "[" << (a - b) << "," << (a + b) << "]" ;
        return;
    }

    // Driver Code
    int main()
    {
        FermatFactors(6557);
        return 0;
    }

// This code is contributed by AnkitRai01
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of fermat's factorization
class GFG
{

    // This function finds the value of a and b
    // and returns a+b and a-b
    static void FermatFactors(int n)
    {

        // since fermat's factorization applicable
        // for odd positive integers only
        if(n <= 0)
        {
            System.out.print("["+ n + "]");
            return;
        }

        // check if n is a even number
        if((n & 1) == 0)
        {
            System.out.print("[" + n / 2.0 + "," + 2 + "]");
            return;
        }

        int a = (int)Math.ceil(Math.sqrt(n)) ;

        // if n is a perfect root,
        // then both its square roots are its factors
        if(a * a == n)
        {
            System.out.print("[" + a + "," + a + "]");
            return;
        }
        int b;
        while(true)
        {
            int b1 = a * a - n ;
            b = (int)(Math.sqrt(b1)) ;

            if(b * b == b1)
                break;
            else
                a += 1;
        }
        System.out.print("[" + (a - b) +"," + (a + b) + "]" );
        return;
    }

    // Driver Code
    public static void main (String[] args)
    {
        FermatFactors(6557);
    }
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python 3 implementation of fermat's factorization

from math import ceil, sqrt

#This function finds the value of a and b
#and  returns a+b and a-b
def FermatFactors(n):

   # since fermat's factorization applicable
   # for odd positive integers only
    if(n<= 0):
        return [n] 

    # check if n is a even number
    if(n & 1) == 0: 
        return [n / 2, 2]

    a = ceil(sqrt(n))

    #if n is a perfect root,
    #then both its square roots are its factors
    if(a * a == n):
        return [a, a]

    while(True):
        b1 = a * a - n
        b = int(sqrt(b1))
        if(b * b == b1):
            break
        else:
            a += 1
    return [a-b, a + b]

# Driver Code
print(FermatFactors(6557))
```

## C#

```
// C# implementation of fermat's factorization
using System;

class GFG
{

    // This function finds the value of a and b
    // and returns a+b and a-b
    static void FermatFactors(int n)
    {

        // since fermat's factorization applicable
        // for odd positive integers only
        if(n <= 0)
        {
            Console.Write("["+ n + "]");
            return;
        }

        // check if n is a even number
        if((n & 1) == 0)
        {
            Console.Write("[" + n / 2.0 + "," + 2 + "]");
            return;
        }

        int a = (int)Math.Ceiling(Math.Sqrt(n)) ;

        // if n is a perfect root,
        // then both its square roots are its factors
        if(a * a == n)
        {
            Console.Write("[" + a + "," + a + "]");
            return;
        }
        int b;
        while(true)
        {
            int b1 = a * a - n ;
            b = (int)(Math.Sqrt(b1)) ;

            if(b * b == b1)
                break;
            else
                a += 1;
        }
        Console.Write("[" + (a - b) +"," + (a + b) + "]" );
        return;
    }

    // Driver Code
    public static void Main ()
    {
        FermatFactors(6557);
    }
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>

    // JavaScript implementation of fermat's factorization

    // This function finds the value of a and b
    // and returns a+b and a-b
    function FermatFactors(n)
    {

        // since fermat's factorization applicable
        // for odd positive integers only
        if(n <= 0)
        {
            document.write("["+ n + "]");
            return;
        }

        // check if n is a even number
        if((n & 1) == 0)
        {
            document.write("[" + (n / 2.0) + "," + (2) + "]");
            return;
        }

        let a = Math.ceil(Math.sqrt(n)) ;

        // if n is a perfect root,
        // then both its square roots are its factors
        if(a * a == n)
        {
            document.write("[" + a + "," + a + "]");
            return;
        }
        let b;
        while(true)
        {
            let b1 = a * a - n ;
            b = parseInt(Math.sqrt(b1), 10);

            if(b * b == b1)
                break;
            else
                a += 1;
        }
        document.write("[" + (a - b) +", " + (a + b) + "]");
        return;
    }

    FermatFactors(6557);

</script>
```

**Output:** 

```
[79, 83]
```
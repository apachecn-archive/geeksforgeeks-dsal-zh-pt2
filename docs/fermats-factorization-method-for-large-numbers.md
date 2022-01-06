# 费马大数因式分解法

> 原文:[https://www . geesforgeks . org/fermats-因式分解-大数方法/](https://www.geeksforgeeks.org/fermats-factorization-method-for-large-numbers/)

给定一个很大的数 **N** ，任务是使用[费马的因式分解法](https://www.geeksforgeeks.org/fermats-factorization-method/)将这个数分成两个因子的乘积。

**示例**

> **输入:**N = 105327569
> T3】输出: 10223，10303
> 
> **输入:**N = 249803
> T3】输出: 23，10861

**[费马因式分解](https://www.geeksforgeeks.org/fermats-factorization-method/) :** 费马因式分解法是将一个奇数表示为两个平方之差。
对于整数 N，我们需要 a 和 b，例如:

```
N = a2 - b2 = (a+b)(a-b) 

where (a+b) and (a-b) are 
the factors of the number N.

```

**进场:**

1.  获取数字作为[大整数类](https://www.geeksforgeeks.org/biginteger-class-in-java/)的对象
2.  求 **N** 的[平方根](https://www.geeksforgeeks.org/square-root-of-an-integer/)。
3.  保证 **a** 的值大于 sqrt(N)**b**的值小于 sqrt(N)。
4.  将 sqrt(n)的值作为 a，并递增该数，直到找到一个数 b，使得**n–a^2**是一个完美的正方形。

下面是上述方法的实现:

```
// Java program for Fermat's Factorization
// method for large numbers

import java.math.*;
import java.util.*;

class Solution {

    // Function to find the Floor
    // of square root of a number
    public static BigInteger sqrtF(BigInteger x)
        throws IllegalArgumentException
    {
        // if x is less than 0
        if (x.compareTo(BigInteger.ZERO) < 0) {
            throw new IllegalArgumentException(
                "Negative argument.");
        }

        // if x==0 or x==1
        if (x.equals(BigInteger.ZERO)
            || x.equals(BigInteger.ONE)) {
            return x;
        }

        BigInteger two
            = BigInteger.valueOf(2L);
        BigInteger y;

        // run a loop
        y = x.divide(two);
        while (y.compareTo(x.divide(y)) > 0)
            y = ((x.divide(y)).add(y))
                    .divide(two);
        return y;
    }

    // function to find the Ceil
    // of square root of a number
    public static BigInteger sqrtC(BigInteger x)
        throws IllegalArgumentException
    {
        BigInteger y = sqrtF(x);

        if (x.compareTo(y.multiply(y)) == 0) {
            return y;
        }

        else {
            return y.add(BigInteger.ONE);
        }
    }

    // Fermat factorisation
    static String FermatFactors(BigInteger n)
    {
        // constants
        BigInteger ONE = new BigInteger("1");
        BigInteger ZERO = new BigInteger("0");
        BigInteger TWO = new BigInteger("2");

        // if n%2 ==0 then return the factors
        if (n.mod(TWO).equals(ZERO)) {
            return n.divide(TWO)
                       .toString()
                + ", 2";
        }

        // find the square root
        BigInteger a = sqrtC(n);

        // if the number is a perfect square
        if (a.multiply(a).equals(n)) {
            return a.toString()
                + ", " + a.toString();
        }

        // else perform factorisation
        BigInteger b;
        while (true) {
            BigInteger b1 = a.multiply(a)
                                .subtract(n);
            b = sqrtF(b1);

            if (b.multiply(b).equals(b1))
                break;
            else
                a = a.add(ONE);
        }

        return a.subtract(b).toString()
            + ", " + a.add(b).toString();
    }

    // Driver code
    public static void main(String args[])
    {
        String N = "105327569";

        System.out.println(
            FermatFactors(
                new BigInteger(N)));
    }
}
```

**Output:**

```
10223, 10303

```

**性能分析:**

*   ***时间复杂度:** O(sqrt(N))*
*   ***空间复杂度:** O(1)*
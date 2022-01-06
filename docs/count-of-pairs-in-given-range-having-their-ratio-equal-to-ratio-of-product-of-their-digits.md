# 给定范围内配对数，其比值等于其位数乘积的比值

> 原文:[https://www . geeksforgeeks . org/给定范围内的配对计数，其比率等于其位数的乘积比率/](https://www.geeksforgeeks.org/count-of-pairs-in-given-range-having-their-ratio-equal-to-ratio-of-product-of-their-digits/)

给定两个整数 **L** 和 **R** ，任务是在**【L，R】**范围内找到无序整数对 **(A，B)** 的个数，使得 **A** 和 **B** 的比值与 A 的位数的**乘积和 B** 的位数的**乘积的比值相同。**

**示例:**

> **输入:** L = 10，R = 50
> **输出:** 2
> **说明:**符合给定条件的[10，50]范围内的对为(15，24)为 15:24 = 5:8≦(1 * 5):(2 * 4)= 5:8 和(18，45)为 18:45 = 2:5≦(1 * 8):(4 * 5)=
> 
> **输入:** L = 1，R = 100
> T3】输出: 43

**方法:**给定的问题可以使用下面讨论的步骤来解决:

*   创建一个[函数](https://www.geeksforgeeks.org/functions-in-c/)来计算一个数字的数字的[乘积。](https://www.geeksforgeeks.org/program-to-calculate-product-of-digits-of-a-number/)
*   使用 **a** 和 **b** 对范围**【L，R】**内的所有无序整数对进行迭代，对于每一对 **(a，b)*****a:b*****相当于 a 的位数的 ***乘积:b 的位数的乘积*** 当且仅当***a * b 的位数的乘积*****
*   **利用上述观察，保持变量**中 **(a，b)** 的有效对的计数，使得***a * b 的位数乘积***=***b * a 的位数乘积*** 。****
*   **完成以上步骤后，打印 **cntPair** 的值作为结果。**

**下面是上述方法的实现:**

## **C++**

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the product of
// digits of the given number
int getProduct(int n)
{
    int product = 1;
    while (n != 0) {
        product = product * (n % 10);
        n = n / 10;
    }
    return product;
}

// Function to find the count of pairs
// (a, b) such that a:b = (product of
// digits of a):(product of digits of b)
int countPairs(int L, int R)
{
    // Stores the count of the valid pairs
    int cntPair = 0;

    // Loop to iterate over all unordered
    // pairs (a, b)
    for (int a = L; a <= R; a++) {
        for (int b = a + 1; b <= R; b++) {

            // Stores the product of
            // digits of a
            int x = getProduct(a);

            // Stores the product of
            // digits of b
            int y = getProduct(b);

            // If x!=0 and y!=0 and a:b
            // is equivalent to x:y
            if (x && y && (a * y) == (b * x)) {

                // Increment valid pair count
                cntPair++;
            }
        }
    }

    // Return Answer
    return cntPair;
}

// Driver code
int main()
{
    int L = 1;
    int R = 100;

    // Function Call
    cout << countPairs(1, 100);
    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java program for the above approach
class GFG{

// Function to find the product of
// digits of the given number
public static int getProduct(int n)
{
    int product = 1;
    while (n != 0) {
        product = product * (n % 10);
        n = n / 10;
    }
    return product;
}

// Function to find the count of pairs
// (a, b) such that a:b = (product of
// digits of a):(product of digits of b)
public static int countPairs(int L, int R)
{
    // Stores the count of the valid pairs
    int cntPair = 0;

    // Loop to iterate over all unordered
    // pairs (a, b)
    for (int a = L; a <= R; a++) {
        for (int b = a + 1; b <= R; b++) {

            // Stores the product of
            // digits of a
            int x = getProduct(a);

            // Stores the product of
            // digits of b
            int y = getProduct(b);

            // If x!=0 and y!=0 and a:b
            // is equivalent to x:y
            if (x !=0  && y != 0 && (a * y) == (b * x)) {

                // Increment valid pair count
                cntPair++;
            }
        }
    }

    // Return Answer
    return cntPair;
}

// Driver code
public static void  main(String args[])
{
    int L = 1;
    int R = 100;

    // Function Call
    System.out.println(countPairs(L, R));
}

}

// This code is contributed by _saurabh_jaiswal.
```

## **蟒蛇 3**

```
# Python 3 program for the above approach

# Function to find the product of
# digits of the given number
def getProduct(n):
    product = 1
    while (n != 0):
        product = product * (n % 10)
        n = n // 10
    return product

# Function to find the count of pairs
# (a, b) such that a:b = (product of
# digits of a):(product of digits of b)
def countPairs(L, R):
    # Stores the count of the valid pairs
    cntPair = 0

    # Loop to iterate over all unordered
    # pairs (a, b)
    for a in range(L,R+1,1):
        for b in range(a + 1,R+1,1):
            # Stores the product of
            # digits of a
            x = getProduct(a)

            # Stores the product of
            # digits of b
            y = getProduct(b)

            # If x!=0 and y!=0 and a:b
            # is equivalent to x:y
            if (x and y and (a * y) == (b * x)):
                # Increment valid pair count
                cntPair += 1

    # Return Answer
    return cntPair

# Driver code
if __name__ == '__main__':
    L = 1
    R = 100

    # Function Call
    print(countPairs(1, 100))

    # This code is contributed by SURENDRA_GANGWAR.
```

## **C#**

```
// C# program for the above approach
using System;

public class GFG{

    // Function to find the product of
    // digits of the given number
    public static int getProduct(int n)
    {
        int product = 1;
        while (n != 0) {
            product = product * (n % 10);
            n = n / 10;
        }
        return product;
    }

    // Function to find the count of pairs
    // (a, b) such that a:b = (product of
    // digits of a):(product of digits of b)
    public static int countPairs(int L, int R)
    {
        // Stores the count of the valid pairs
        int cntPair = 0;

        // Loop to iterate over all unordered
        // pairs (a, b)
        for (int a = L; a <= R; a++) {
            for (int b = a + 1; b <= R; b++) {

                // Stores the product of
                // digits of a
                int x = getProduct(a);

                // Stores the product of
                // digits of b
                int y = getProduct(b);

                // If x!=0 and y!=0 and a:b
                // is equivalent to x:y
                if (x !=0  && y != 0 && (a * y) == (b * x)) {

                    // Increment valid pair count
                    cntPair++;
                }
            }
        }

        // Return Answer
        return cntPair;
    }

    // Driver code
    public static void Main(string []args)
    {
        int L = 1;
        int R = 100;

        // Function Call
        Console.WriteLine(countPairs(L, R));
    }

}

// This code is contributed by AnkThon
```

## **java 描述语言**

```
<script>
        // JavaScript Program to implement
        // the above approach

        // Function to find the product of
        // digits of the given number
        function getProduct(n) {
            let product = 1;
            while (n != 0) {
                product = product * (n % 10);
                n = Math.floor(n / 10);
            }
            return product;
        }

        // Function to find the count of pairs
        // (a, b) such that a:b = (product of
        // digits of a):(product of digits of b)
        function countPairs(L, R) {
            // Stores the count of the valid pairs
            let cntPair = 0;

            // Loop to iterate over all unordered
            // pairs (a, b)
            for (let a = L; a <= R; a++) {
                for (let b = a + 1; b <= R; b++) {

                    // Stores the product of
                    // digits of a
                    let x = getProduct(a);

                    // Stores the product of
                    // digits of b
                    let y = getProduct(b);

                    // If x!=0 and y!=0 and a:b
                    // is equivalent to x:y
                    if (x && y && (a * y) == (b * x)) {

                        // Increment valid pair count
                        cntPair++;
                    }
                }
            }

            // Return Answer
            return cntPair;
        }

        // Driver code

        let L = 1;
        let R = 100;

        // Function Call
        document.write(countPairs(1, 100));

// This code is contributed by Potta Lokesh

    </script>
```

****Output:** 

```
43
```** 

*****时间复杂度:** O(N <sup>2</sup> *log N)其中 **N** 代表给定范围内的整数个数，即 R–l .*
***辅助空间:** O(1)***
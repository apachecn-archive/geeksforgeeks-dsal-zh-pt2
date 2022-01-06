# 在一个范围内寻找一个不可传递的同素三元组

> 原文:[https://www . geesforgeks . org/finding-不可传递-互素-三元组-范围/](https://www.geeksforgeeks.org/finding-non-transitive-coprime-triplet-range/)

给定 L 和 R，找到一个可能的非传递三元组(a，b，c)，使得对(a，b)是同素的，对(b，c)是同素的，但(a，c)不是同素的。
Eg: (2，5，6)是不可传递的三元组，因为对(2，5)是同素的，对(5，6)是同素的，但对(2，6)不是同素的。

**示例:**

> 输入:L = 2，R = 10
> 输出:a = 4，b = 7，c = 8 就是这样一个三元组
> **解释** (4，7，8)是一个可能的三元组(而在这个范围内存在其他这样的三元组)，这里，对(4，7)是同素的，对(7，8)是同素的但对(4，8)不是同素的
> 输入:L = 21，R = 47
> 输出:a = 23， b = 25，c = 46 是一个这样的三元组
> **解释** (23，25，46)是一个可能的三元组(虽然在这个范围内存在其他这样的三元组)，这里，对(23，25)是同素的，对(25，46)是同素的，但是对(23，46)不是同素的

**方法 1(蛮力):**

我们在 L 和 R 之间生成所有可能的三元组，并检查该属性是否成立，即对(a，b)是同素的，对(b，c)是同素的，但对(a，c)不是。

## C++

```
// C++ program to find possible non transitive triplets btw L and R
#include <bits/stdc++.h>
using namespace std;

// Function to return gcd of a and b
int gcd(int a, int b)
{
    if (a == 0)
        return b;
    return gcd(b % a, a);
}

// function to check for gcd
bool coprime(int a, int b)
{
    // a and b are coprime if their gcd is 1.
    return (gcd(a, b) == 1);
}

/* Checks if any possible triplet (a, b, c) satisfying the condition
   that (a, b) is coprime, (b, c) is coprime but (a, c) isnt */
void possibleTripletInRange(int L, int R)
{

    bool flag = false;
    int possibleA, possibleB, possibleC;

    // Generate and check for all possible triplets
    // between L and R
    for (int a = L; a <= R; a++) {
        for (int b = a + 1; b <= R; b++) {
            for (int c = b + 1; c <= R; c++) {

                // if we find any such triplets set flag to true
                if (coprime(a, b) && coprime(b, c) && !coprime(a, c)) {
                    flag = true;
                    possibleA = a;
                    possibleB = b;
                    possibleC = c;
                    break;
                }
            }
        }
    }

    // flag = True indicates that a pair exists
    // between L and R
    if (flag == true) {
        cout << "(" << possibleA << ", " << possibleB
             << ", " << possibleC << ")"
             << " is one such possible triplet between "
             << L << " and " << R << "\n";
    }
    else {
        cout << "No Such Triplet exists between "
             << L << " and " << R << "\n";
    }
}

// Driver code
int main()
{
    int L, R;

    // finding possible Triplet between 2 and 10
    L = 2;
    R = 10;
    possibleTripletInRange(L, R);

    // finding possible Triplet between 23 and 46
    L = 23;
    R = 46;
    possibleTripletInRange(L, R);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find possible non
// transitive triplets btw L and R
class GFG {

    // Function to return gcd of a and b
    static int gcd(int a, int b)
    {
        if (a == 0)
            return b;

        return gcd(b % a, a);
    }

    // function to check for gcd
    static boolean coprime(int a, int b)
    {

        // a and b are coprime if their
        // gcd is 1.
        return (gcd(a, b) == 1);
    }

    // Checks if any possible triplet
    // (a, b, c) satifying the condition
    // that (a, b) is coprime, (b, c) is
    // coprime but (a, c) isnt */
    static void possibleTripletInRange(int L, int R)
    {

        boolean flag = false;
        int possibleA = 0, possibleB = 0,
                           possibleC = 0;

        // Generate and check for all possible
        // triplets between L and R
        for (int a = L; a <= R; a++) {
            for (int b = a + 1; b <= R; b++) {
                for (int c = b + 1; c <= R; c++)
                {

                    // if we find any such triplets
                    // set flag to true
                    if (coprime(a, b) && coprime(b, c)
                                    && !coprime(a, c))
                    {
                        flag = true;
                        possibleA = a;
                        possibleB = b;
                        possibleC = c;
                        break;
                    }
                }
            }
        }

        // flag = True indicates that a pair exists
        // between L and R
        if (flag == true) {
            System.out.println("(" + possibleA + ", "
                  + possibleB + ", " + possibleC + ")"
                    + " is one such possible triplet "
                      + "between " + L + " and " + R);
        }
        else {
            System.out.println("No Such Triplet exists"
                      + "between " + L + " and " + R);
        }
    }

    // Driver code
    public static void main(String[] args)
    {

        int L, R;

        // finding possible Triplet between
        // 2 and 10
        L = 2;
        R = 10;
        possibleTripletInRange(L, R);

        // finding possible Triplet between
        // 23 and 46
        L = 23;
        R = 46;
        possibleTripletInRange(L, R);
    }
}

// This code is contributed by
// Smitha DInesh Semwal
```

## 蟒蛇 3

```
# Python3 program to find possible non
# transitive triplets btw L and R

# Function to return gcd of a and b
def gcd(a, b):

    if (a == 0):
        return b;
    return gcd(b % a, a);

# function to check for gcd
def coprime(a, b):

    # a and b are coprime if
    # their gcd is 1.
    return (gcd(a, b) == 1);

# Checks if any possible triplet
# (a, b, c) satifying the condition
# that (a, b) is coprime, (b, c)
# is coprime but (a, c) isnt
def possibleTripletInRange(L, R):

    flag = False;
    possibleA = 0;
    possibleB = 0;
    possibleC = 0;

    # Generate and check for all
    # possible triplets between L and R
    for a in range(L, R + 1):
        for b in range(a + 1, R + 1):
            for c in range(b + 1, R + 1):

                # if we find any such triplets
                # set flag to true
                if (coprime(a, b) and coprime(b, c) and    
                                      coprime(a, c) == False):
                    flag = True;
                    possibleA = a;
                    possibleB = b;
                    possibleC = c;
                    break;

    # flag = True indicates that a
    # pair exists between L and R
    if (flag == True):
        print("(", possibleA, ",", possibleB,
              ",", possibleC, ") is one such",
              "possible triplet between", L, "and", R);
    else:
        print("No Such Triplet exists between",
                                  L, "and", R);

# Driver Code

# finding possible Triplet
# between 2 and 10
L = 2;
R = 10;
possibleTripletInRange(L, R);

# finding possible Triplet
# between 23 and 46
L = 23;
R = 46;
possibleTripletInRange(L, R);

# This code is contributed by mits
```

## C#

```
// C# program to find possible
// non transitive triplets
// btw L and R
using System;
class GFG
{
    // Function to return
    // gcd of a and b
    static int gcd(int a,
                   int b)
    {
        if (a == 0)
            return b;

        return gcd(b % a, a);
    }

    // function to
    // check for gcd
    static bool coprime(int a,
                        int b)
    {

        // a and b are coprime
        // if their gcd is 1.
        return (gcd(a, b) == 1);
    }

    // Checks if any possible
    // triplet (a, b, c) satifying
    // the condition that (a, b)
    // is coprime, (b, c) is
    // coprime but (a, c) isnt */
    static void possibleTripletInRange(int L,
                                       int R)
    {

        bool flag = false;
        int possibleA = 0,
            possibleB = 0,
            possibleC = 0;

        // Generate and check for
        // all possible triplets
        // between L and R
        for (int a = L; a <= R; a++)
        {
            for (int b = a + 1;
                     b <= R; b++)
            {
                for (int c = b + 1;
                         c <= R; c++)
                {

                    // if we find any
                    // such triplets
                    // set flag to true
                    if (coprime(a, b) &&
                        coprime(b, c) &&
                       !coprime(a, c))
                    {
                        flag = true;
                        possibleA = a;
                        possibleB = b;
                        possibleC = c;
                        break;
                    }
                }
            }
        }

        // flag = True indicates
        // that a pair exists
        // between L and R
        if (flag == true)
        {
            Console.WriteLine("(" + possibleA + ", " +
                                    possibleB + ", " +
                                    possibleC + ")" +
                    " is one such possible triplet " +
                        "between " + L + " and " + R);
        }
        else
        {
            Console.WriteLine("No Such Triplet exists" +
                          "between " + L + " and " + R);
        }
    }

    // Driver code
    public static void Main()
    {
        int L, R;

        // finding possible
        // Triplet between
        // 2 and 10
        L = 2;
        R = 10;
        possibleTripletInRange(L, R);

        // finding possible
        // Triplet between
        // 23 and 46
        L = 23;
        R = 46;
        possibleTripletInRange(L, R);
    }
}

// This code is contributed
// by anuj_67.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find possible non
// transitive triplets btw L and R

// Function to return gcd of a and b
function gcd($a, $b)
{
    if ($a == 0)
        return $b;
    return gcd($b % $a, $a);
}

// function to check for gcd
function coprime($a, $b)
{
    // a and b are coprime if
    // their gcd is 1.
    return (gcd($a, $b) == 1);
}

/* Checks if any possible triplet
   (a, b, c) satifying the condition
   that (a, b) is coprime, (b, c)
   is coprime but (a, c) isnt */
function possibleTripletInRange($L, $R)
{
    $flag = false;
    $possibleA;
    $possibleB;
    $possibleC;

    // Generate and check for all
    // possible triplets between L and R
    for ($a = $L; $a <= $R; $a++)
    {
        for ($b = $a + 1; $b <= $R; $b++)
        {
            for ( $c = $b + 1; $c <= $R; $c++)
            {

                // if we find any such triplets
                // set flag to true
                if (coprime($a, $b) &&
                    coprime($b, $c) &&
                   !coprime($a, $c))
                {
                    $flag = true;
                    $possibleA = $a;
                    $possibleB = $b;
                    $possibleC = $c;
                    break;
                }
            }
        }
    }

    // flag = True indicates that a
    // pair exists between L and R
    if ($flag == true)
    {
        echo "(" ,$possibleA ,
             ", " , $possibleB,
             ", " , $possibleC , ")",
             " is one such possible triplet between ",
               $L , " and " , $R , "\n";
    }
    else
    {
        echo "No Such Triplet exists between ",
                      $L , " and " , $R , "\n";
    }
}

// Driver Code
$L;
$R;

// finding possible Triplet
// between 2 and 10
$L = 2;
$R = 10;
possibleTripletInRange($L, $R);

// finding possible Triplet
// between 23 and 46
$L = 23;
$R = 46;
possibleTripletInRange($L, $R);

// This code is contributed by jit_t
?>
```

## java 描述语言

```
<script>

    // Javascript program to find possible
    // non transitive triplets
    // btw L and R

    // Function to return
    // gcd of a and b
    function gcd(a, b)
    {
        if (a == 0)
            return b;

        return gcd(b % a, a);
    }

    // function to
    // check for gcd
    function coprime(a, b)
    {

        // a and b are coprime
        // if their gcd is 1.
        return (gcd(a, b) == 1);
    }

    // Checks if any possible
    // triplet (a, b, c) satifying
    // the condition that (a, b)
    // is coprime, (b, c) is
    // coprime but (a, c) isnt */
    function possibleTripletInRange(L, R)
    {

        let flag = false;
        let possibleA = 0,
            possibleB = 0,
            possibleC = 0;

        // Generate and check for
        // all possible triplets
        // between L and R
        for (let a = L; a <= R; a++)
        {
            for (let b = a + 1;
                     b <= R; b++)
            {
                for (let c = b + 1;
                         c <= R; c++)
                {

                    // if we find any
                    // such triplets
                    // set flag to true
                    if (coprime(a, b) &&
                        coprime(b, c) &&
                       !coprime(a, c))
                    {
                        flag = true;
                        possibleA = a;
                        possibleB = b;
                        possibleC = c;
                        break;
                    }
                }
            }
        }

        // flag = True indicates
        // that a pair exists
        // between L and R
        if (flag == true)
        {
            document.write("(" + possibleA + ", " +
                              possibleB + ", " +
                         possibleC + ")" +
             " is one such possible triplet " +
              "between " + L + " and " + R + "</br>");
        }
        else
        {
            document.write("No Such Triplet exists" +
             "between " + L + " and " + R + "</br>");
        }
    }

    let L, R;

    // finding possible
    // Triplet between
    // 2 and 10
    L = 2;
    R = 10;
    possibleTripletInRange(L, R);

    // finding possible
    // Triplet between
    // 23 and 46
    L = 23;
    R = 46;
    possibleTripletInRange(L, R);

</script>
```

**输出:**

```
(8, 9, 10) is one such possible triplet between 2 and 10
(44, 45, 46) is one such possible triplet between 23 and 46
```

强力解的时间复杂度为 O(n <sup>3</sup> log(A))，其中 A 是三元组的最小数。
**注**:复杂度的对数因子是计算一对数字的 GCD。

**方法 2(高效)**:

因为我们只需要一个这样的可能对，我们可以用它来进一步分解我们的复杂性。
我们只需要识别一些案例，并寻找解决这些案例的方法来解决这个问题。
**例 1:L 和 r 之间的数字少于 3**
例 2:L 和 r 之间的数字多于 3
例 3:这个例子很简单，我们不能形成任何三元组，所以答案是这个例子永远是‘不可能的’
**例 2:L 和 r 之间的数字多于 3 个**
现在，
这是众所周知的连续数字总是同素的证明。我们甚至可以轻松证明这一点。

```
Proof:
Given that N and N + 1 are two consecutive integers. 
Now suppose gcd(n, n + 1) = X,
? X divides n and X also divides (n + 1). 
Which implies that X divides ((n + 1) - n) or X divides 1.
But, There is no number which divides 1 except 1.
? X = 1, or we can also say that gcd(n, n + 1) = 1 

Thus, n and n + 1 are coprime.
```

因此，如果我们取形式为 2k，2k + 1，2k + 2 的三个连续数，我们总是会得到一个可能的三元组，因为如上所述，作为连续数对的对(2k，2k + 1)和(2k + 1，2k + 2)是同素的，而对(2k，2k+2)的 gcd 是 2(因为它们是偶数)。
**情况 3:当 L 和 R 之间正好有 3 个数字时**
这是情况 3 的扩展，现在这个情况可以有 2 个情况，
**情况 3.1 当这三个数字是 2k，2k + 1，2k + 2**
的形式时，我们已经在情况 2 中看到了这个情况。所以这是唯一的三元组，也是 L 和 r 之间的有效三元组
**情况 3.2 当这三个数的形式为 2k–1，2k，2k + 1**
我们已经看到(2k–1，2k)和(2k，2k + 1)是一对连续的数是同素对，所以我们需要检查这一对(2k–1，2k + 1)是不是同素的
可以证明这一对(2k–1，2k + 1

```
Proof:
Given that 2k - 1 and 2k + 1 are two numbers 
Now suppose gcd((2k - 1), (2k + 1)) = X,
? X divides (2k - 1) and X also divides (2k + 1). 
Which implies that X divides ((2k + 1) - (2k - 1)) or X divides 2.
2 being a prime is only divisible by 1 and 2 itself. 
But, 2k - 1 and 2k + 1 are odd numbers so X can never be equal to 2.
? X = 1, or we can also say that gcd((2k -1), (2k + 1)) = 1 

Thus, 2k - 1 and 2k + 1 are coprime.
```

因此，在这种情况下，我们将无法找到任何可能的有效三元组。
以下是上述方法的实现:

## C++

```
/* C++ program to find a non transitive co-prime
   triplets between L and R */
#include <bits/stdc++.h>
using namespace std;

/* Checks if any possible triplet (a, b, c) satisfying the condition
   that (a, b) is coprime, (b, c) is coprime but (a, c) isnt */

void possibleTripletInRange(int L, int R)
{

    bool flag = false;
    int possibleA, possibleB, possibleC;

    int numbersInRange = (R - L + 1);

    /* Case 1 : Less than 3 numbers between L and R */
    if (numbersInRange < 3) {
        flag = false;
    }

    /* Case 2: More than 3 numbers between L and R */
    else if (numbersInRange > 3) {
        flag = true;

        // triplets should always be of form (2k, 2k + 1, 2k + 2)
        if (L % 2) {
            L++;
        }

        possibleA = L;
        possibleB = L + 1;
        possibleC = L + 2;
    }

    else {
        /* Case 3.1: Exactly 3 numbers in range of form
                     (2k, 2k + 1, 2k + 2) */
        if (!(L % 2)) {
            flag = true;
            possibleA = L;
            possibleB = L + 1;
            possibleC = L + 2;
        }
        else {
            /* Case 3.2: Exactly 3 numbers in range of form
                         (2k - 1, 2k, 2k + 1) */
            flag = false;
        }
    }

    // flag = True indicates that a pair exists between L and R
    if (flag == true) {
        cout << "(" << possibleA << ", " << possibleB
             << ", " << possibleC << ")"
             << " is one such possible triplet between "
             << L << " and " << R << "\n";
    }
    else {
        cout << "No Such Triplet exists between "
             << L << " and " << R << "\n";
    }
}

// Driver code
int main()
{
    int L, R;

    // finding possible Triplet between 2 and 10
    L = 2;
    R = 10;
    possibleTripletInRange(L, R);

    // finding possible Triplet between 23 and 46
    L = 23;
    R = 46;
    possibleTripletInRange(L, R);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find a
// non transitive co-prime
// triplets between L and R
import java.io.*;

class GFG
{

// Checks if any possible triplet
// (a, b, c) satifying the condition
// that (a, b) is coprime, (b, c)
// is coprime but (a, c) isnt
static void possibleTripletInRange(int L,
                                   int R)
{
    boolean flag = false;
    int possibleA = 0,
        possibleB = 0,
        possibleC = 0;

    int numbersInRange = (R - L + 1);

    // Case 1 : Less than 3
    // numbers between L and R
    if (numbersInRange < 3)
    {
        flag = false;
    }

    // Case 2: More than 3
    // numbers between L and R
    else if (numbersInRange > 3)
    {
        flag = true;

        // triplets should always
        // be of form (2k, 2k + 1,
        // 2k + 2)
        if (L % 2 > 0)
        {
            L++;
        }

        possibleA = L;
        possibleB = L + 1;
        possibleC = L + 2;
    }

    else
    {
        /* Case 3.1: Exactly 3 numbers
                      in range of form
                     (2k, 2k + 1, 2k + 2) */
        if (!(L % 2 > 0))
        {
            flag = true;
            possibleA = L;
            possibleB = L + 1;
            possibleC = L + 2;
        }
        else
        {
            /* Case 3.2: Exactly 3 numbers
                         in range of form
                         (2k - 1, 2k, 2k + 1) */
            flag = false;
        }
    }

    // flag = True indicates
    // that a pair exists
    // between L and R
    if (flag == true)
    {
        System.out.println("(" + possibleA +
                          ", " + possibleB +
                          ", " + possibleC +
             ")" + " is one such possible" +
                       " triplet between " +
                          L + " and " + R );
    }
    else {
        System.out.println("No Such Triplet" +
                          " exists between " +
                             L + " and " + R);
    }
}

// Driver code
public static void main (String[] args)
{
int L, R;

// finding possible Triplet
// between 2 and 10
L = 2;
R = 10;
possibleTripletInRange(L, R);

// finding possible Triplet
// between 23 and 46
L = 23;
R = 46;
possibleTripletInRange(L, R);
}
}

// This code is contributed
// by anuj_67.
```

## 蟒蛇 3

```
# Python3 program to find a non transitive
# co-prime triplets between L and R

# Checks if any possible triplet (a, b, c)
# satifying the condition that (a, b) is
# coprime, (b, c) is coprime but (a, c) isnt
def possibleTripletInRange(L, R):

    flag = False;
    possibleA = 0;
    possibleB = 0;
    possibleC = 0;

    numbersInRange = (R - L + 1);

    # Case 1 : Less than 3 numbers
    # between L and R
    if (numbersInRange < 3):
        flag = False;

    # Case 2: More than 3 numbers
    # between L and R
    elif (numbersInRange > 3):
        flag = True;

        # triplets should always be of
        # form (2k, 2k + 1, 2k + 2)
        if ((L % 2) > 0):
            L += 1;

        possibleA = L;
        possibleB = L + 1;
        possibleC = L + 2;

    else:

        # Case 3.1: Exactly 3 numbers in range
        #            of form (2k, 2k + 1, 2k + 2)
        if ((L % 2) == 0):
            flag = True;
            possibleA = L;
            possibleB = L + 1;
            possibleC = L + 2;
        else:

            # Case 3.2: Exactly 3 numbers in range
            #            of form (2k - 1, 2k, 2k + 1)
            flag = False;

    # flag = True indicates that a pair
    # exists between L and R
    if (flag == True):
        print("(", possibleA, ",", possibleB,
              ",", possibleC, ") is one such",
              "possible triplet between", L, "and", R);
    else:
        print("No Such Triplet exists between",
                                  L, "and", R);

# Driver code

# finding possible Triplet
# between 2 and 10
L = 2;
R = 10;
possibleTripletInRange(L, R);

# finding possible Triplet
# between 23 and 46
L = 23;
R = 46;
possibleTripletInRange(L, R);

# This code is contributed by mits
```

## C#

```
// C#  program to find a
// non transitive co-prime
// triplets between L and R
using System;

public class GFG{

// Checks if any possible triplet
// (a, b, c) satifying the condition
// that (a, b) is coprime, (b, c)
// is coprime but (a, c) isnt
static void possibleTripletInRange(int L,
                                int R)
{
    bool flag = false;
    int possibleA = 0,
        possibleB = 0,
        possibleC = 0;

    int numbersInRange = (R - L + 1);

    // Case 1 : Less than 3
    // numbers between L and R
    if (numbersInRange < 3)
    {
        flag = false;
    }

    // Case 2: More than 3
    // numbers between L and R
    else if (numbersInRange > 3)
    {
        flag = true;

        // triplets should always
        // be of form (2k, 2k + 1,
        // 2k + 2)
        if (L % 2 > 0)
        {
            L++;
        }

        possibleA = L;
        possibleB = L + 1;
        possibleC = L + 2;
    }

    else
    {
        /* Case 3.1: Exactly 3 numbers
                    in range of form
                    (2k, 2k + 1, 2k + 2) */
        if (!(L % 2 > 0))
        {
            flag = true;
            possibleA = L;
            possibleB = L + 1;
            possibleC = L + 2;
        }
        else
        {
            /* Case 3.2: Exactly 3 numbers
                        in range of form
                        (2k - 1, 2k, 2k + 1) */
            flag = false;
        }
    }

    // flag = True indicates
    // that a pair exists
    // between L and R
    if (flag == true)
    {
            Console.WriteLine("(" + possibleA +
                        ", " + possibleB +
                        ", " + possibleC +
            ")" + " is one such possible" +
                    " triplet between " +
                        L + " and " + R );
    }
    else {
        Console.WriteLine("No Such Triplet" +
                        " exists between " +
                            L + " and " + R);
    }
}

// Driver code

static public void Main (){

    int L, R;
    // finding possible Triplet
    // between 2 and 10
    L = 2;
    R = 10;
    possibleTripletInRange(L, R);
    // finding possible Triplet
    // between 23 and 46
    L = 23;
    R = 46;
    possibleTripletInRange(L, R);
    }
}
// This code is contributed by ajit
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find possible
// non transitive triplets
// btw L and R
function gcd($a, $b)
{
    if ($a == 0)
        return $b;
    return gcd($b % $a, $a);
}

// function to check for gcd
function coprime($a, $b)
{
    // a and b are coprime
    // if their gcd is 1.
    return (gcd($a, $b) == 1);
}

/* Checks if any possible triplet
(a, b, c) satifying the condition
that (a, b) is coprime, (b, c) is
coprime but (a, c) isnt */
function possibleTripletInRange($L, $R)
{

    $flag = false;
    $possibleA;
    $possibleB;
    $possibleC;

    // Generate and check for
    // all possible triplets
    // between L and R
    for ($a = $L; $a <= $R; $a++)
    {
        for ($b = $a + 1; $b <= $R; $b++)
        {
            for ($c = $b + 1; $c <= $R; $c++)
            {

                // if we find any such
                // triplets set flag to true
                if (coprime($a, $b) &&
                    coprime($b, $c) &&
                    !coprime($a, $c))
                {
                    $flag = true;
                    $possibleA = $a;
                    $possibleB = $b;
                    $possibleC = $c;
                    break;
                }
            }
        }
    }

    // flag = True indicates
    // that a pair exists
    // between L and R
    if ($flag == true)
    {
        echo "(" , $possibleA ,
            ", " , $possibleB ,
            ", " , $possibleC ,
            ")" , " is one such possible ",
                  "triplet between " , $L ,
                       " and " , $R , "\n";
    }
    else
    {
        echo "No Such Triplet exists between ",
                      $L , " and " , $R , "\n";
    }
}

// Driver code

// finding possible Triplet
// between 2 and 10
$L = 2;
$R = 10;
possibleTripletInRange($L, $R);

// finding possible Triplet
// between 23 and 46
$L = 23;
$R = 46;
possibleTripletInRange($L, $R);

// This code is contributed
// by Akanksha Rai(Abby_akku)
```

## java 描述语言

```
<script>
    /* Javascript program to find a non transitive co-prime
   triplets between L and R */

   /* Checks if any possible triplet (a, b, c) satisfying the condition
   that (a, b) is coprime, (b, c) is coprime but (a, c) isnt */

  function possibleTripletInRange(L, R)
  {

    let flag = false;
    let possibleA, possibleB, possibleC;

    let numbersInRange = (R - L + 1);

    /* Case 1 : Less than 3 numbers between L and R */
    if (numbersInRange < 3) {
      flag = false;
    }

    /* Case 2: More than 3 numbers between L and R */
    else if (numbersInRange > 3) {
      flag = true;

      // triplets should always be of form (2k, 2k + 1, 2k + 2)
      if (L % 2) {
        L++;
      }

      possibleA = L;
      possibleB = L + 1;
      possibleC = L + 2;
    }

    else {
      /* Case 3.1: Exactly 3 numbers in range of form
                         (2k, 2k + 1, 2k + 2) */
      if (!(L % 2)) {
        flag = true;
        possibleA = L;
        possibleB = L + 1;
        possibleC = L + 2;
      }
      else {
        /* Case 3.2: Exactly 3 numbers in range of form
                             (2k - 1, 2k, 2k + 1) */
        flag = false;
      }
    }

    // flag = True indicates that a pair exists between L and R
    if (flag == true) {
      document.write("(" + possibleA + ", " + possibleB
      + ", " + possibleC + ")"
      + " is one such possible triplet between "
      + L + " and " + R + "</br>");
    }
    else {
      document.write("No Such Triplet exists between "
      + L + " and " + R + "</br>");
    }
  }

  let L, R;

  // finding possible Triplet between 2 and 10
  L = 2;
  R = 10;
  possibleTripletInRange(L, R);

  // finding possible Triplet between 23 and 46
  L = 23;
  R = 46;
  possibleTripletInRange(L, R);

</script>
```

**输出:**

```
(2, 3, 4) is one such possible triplet between 2 and 10
(24, 25, 26) is one such possible triplet between 24 and 46
```

该方法的时间复杂度为 O(1)。
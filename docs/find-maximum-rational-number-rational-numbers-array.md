# 数组中的最大有理数(或分数)

> 原文:[https://www . geeksforgeeks . org/find-max-有理数-有理数-数组/](https://www.geeksforgeeks.org/find-maximum-rational-number-rational-numbers-array/)

给定有理数，任务是找到最大有理数。

**示例:**

```
Input : ra_num = {{1, 2},
              {2, 3},
              {3, 4},
              {4, 5}};
Output : 4 5

Input : ra_num = {{10, 12},
              {12, 33},
              {33, 14},
              {14, 15}};
Output : 33 14
```

一个简单的解决方案是找到浮点值并比较浮点值。浮点计算可能会导致精度错误。我们可以使用下面的方法来避免它们。
说数字是 1/2，2/3，3/4，4/5
首先取(2，3，4，5)的 LCM，它是所有有理数的分母。所以这个的 LCM 是 60，然后除以所有分母，再乘以所有记数器，所以记数器的值是(30，40，45，48)
然后找出这些有理数之间的最大值。最后一个分子是 max，然后打印最后一个有理数，是 4/5。

## C++

```
// CPP program to find the maximum rational
// number in an array.
#include <bits/stdc++.h>
using namespace std;

struct Rational {

    // numerator and Denominator
    int nume, deno;
};

// here we find the Denominator LCM
int lcmOfDenominator(vector<Rational> ra_num)
{
    // get the first Denominator as lcm
    int lcm = ra_num[0].deno;
    int i;

    // find the lcm of all relational
    // number Denominator
    for (i = 1; i < ra_num.size(); i++)
        lcm = (lcm * (ra_num[i].deno)) /
                 __gcd(lcm, ra_num[i].deno);

    // return the lcm
    return lcm;
}

int maxRational(vector<Rational> ra_num)
{
    // take a temp array for find
    // maximum numerator after multiple
    int temp[ra_num.size()] = { 0 };

    // get here the lcm of all rational
    //number denominator
    int lcm = lcmOfDenominator(ra_num);

    // take maximum for get maximum index
    int maximum = 0;
    int maximumind = 0;

    // find the index which contain maximum value
    for (int i = 0; i < ra_num.size(); i++) {

        // divide lcm with denominator
        // and multiple with numerator
        temp[i] = (ra_num[i].nume) *
                  (lcm / ra_num[i].deno);

        // get the maximum numerator
        if (maximum < temp[i]) {
            maximum = temp[i];
            maximumind = i;
        }
    }

    // return index which contain
    // maximum rational number
    return maximumind;
}

int main()
{
    // given rational number
    vector<Rational> ra_num = { { 1, 2 },
                                { 2, 3 },
                                { 3, 4 },
                                { 4, 5 } };

    // get the index which contain maximum value
    int index_max = maxRational(ra_num);

    // print numerator and denominator
    cout << ra_num[index_max].nume << " "
         << ra_num[index_max].deno << "\n";
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the maximum rational
// number in an array.
import java.util.*;

class GFG
{

static class Rational
{

    // numerator and Denominator
    int nume, deno;

    public Rational(int nume, int deno)
    {
        this.nume = nume;
        this.deno = deno;
    }

};

// here we find the Denominator LCM
static int lcmOfDenominator(Vector<Rational> ra_num)
{
    // get the first Denominator as lcm
    int lcm = ra_num.get(0).deno;
    int i;

    // find the lcm of all relational
    // number Denominator
    for (i = 1; i < ra_num.size(); i++)
        lcm = (lcm * (ra_num.get(i).deno)) /
                __gcd(lcm, ra_num.get(i).deno);

    // return the lcm
    return lcm;
}

static int maxRational(Vector<Rational> ra_num)
{
    // take a temp array for find
    // maximum numerator after multiple
    int []temp = new int[ra_num.size()];

    // get here the lcm of all rational
    //number denominator
    int lcm = lcmOfDenominator(ra_num);

    // take maximum for get maximum index
    int maximum = 0;
    int maximumind = 0;

    // find the index which contain maximum value
    for (int i = 0; i < ra_num.size(); i++)
    {

        // divide lcm with denominator
        // and multiple with numerator
        temp[i] = (ra_num.get(i).nume) *
                  (lcm / ra_num.get(i).deno);

        // get the maximum numerator
        if (maximum < temp[i])
        {
            maximum = temp[i];
            maximumind = i;
        }
    }

    // return index which contain
    // maximum rational number
    return maximumind;
}

static int __gcd(int a, int b)
{
    if (b == 0)
        return a;
    return __gcd(b, a % b);
}

// Driver Code
public static void main(String[] args)
{
    // given rational number
    Vector<Rational> ra_num = new Vector<Rational>();
        ra_num.add(new Rational( 1, 2 ));
    ra_num.add(new Rational( 2, 3 ));                        
    ra_num.add(new Rational( 3, 4 ));                        
    ra_num.add(new Rational( 4, 5 ));                        

    // get the index which contain maximum value
    int index_max = maxRational(ra_num);

    // print numerator and denominator
    System.out.println(ra_num.get(index_max).nume +
                 " " + ra_num.get(index_max).deno);
    }
}

// This code is contributed by Princi Singh
```

## 蟒蛇 3

```
# Python3 program to find the maximum rational
# number in an array.
class Rational:

    def __init__(self, nume, deno):

        # Numerator and Denominator
        self.nume = nume
        self.deno = deno

def computeGCD(x, y):

    while(y):
        x, y = y, x % y

    return x

# Here we find the Denominator LCM
def lcmOfDenominator(ra_num):

    # Get the first Denominator as lcm
    lcm = ra_num[0].deno

    # Find the lcm of all relational
    # number Denominator
    for i in range(1, len(ra_num)):
        lcm = ((lcm * (ra_num[i].deno)) //
       computeGCD(lcm, ra_num[i].deno))

    # return the lcm
    return lcm

def maxRational(ra_num):

    # Take a temp array for find
    # maximum numerator after multiple
    temp = [0 for i in range(len(ra_num))]

    # Get here the lcm of all rational
    # number denominator
    lcm = lcmOfDenominator(ra_num)

    # Take maximum for get maximum index
    maximum = 0
    maximumind = 0

    # Find the index which contain
    # maximum value
    for i in range(len(ra_num)):

        # Divide lcm with denominator
        # and multiple with numerator
        temp[i] = ((ra_num[i].nume) *
            (lcm // ra_num[i].deno))

        # Get the maximum numerator
        if (maximum < temp[i]):
            maximum = temp[i]
            maximumind = i

    # Return index which contain
    # maximum rational number
    return maximumind

# Driver code
if __name__=="__main__":

    # Given rational number
    ra_num = []
    ra_num.append(Rational(1, 2))
    ra_num.append(Rational(2, 3))
    ra_num.append(Rational(3, 4))
    ra_num.append(Rational(4, 5))

    # Get the index which contain maximum value
    index_max = maxRational(ra_num)

    # Print numerator and denominator
    print(str(ra_num[index_max].nume) + " " +
          str(ra_num[index_max].deno))

# This code is contributed by rutvik_56
```

## C#

```
// C# program to find the maximum rational
// number in an array.
using System;
using System.Collections.Generic;

class GFG
{

public class Rational
{

    // numerator and Denominator
    public int nume, deno;

    public Rational(int nume, int deno)
    {
        this.nume = nume;
        this.deno = deno;
    }

};

// here we find the Denominator LCM
static int lcmOfDenominator(List<Rational> ra_num)
{
    // get the first Denominator as lcm
    int lcm = ra_num[0].deno;
    int i;

    // find the lcm of all relational
    // number Denominator
    for (i = 1; i < ra_num.Count; i++)
        lcm = (lcm * (ra_num[i].deno)) /
                __gcd(lcm, ra_num[i].deno);

    // return the lcm
    return lcm;
}

static int maxRational(List<Rational> ra_num)
{
    // take a temp array for find
    // maximum numerator after multiple
    int []temp = new int[ra_num.Count];

    // get here the lcm of all rational
    //number denominator
    int lcm = lcmOfDenominator(ra_num);

    // take maximum for get maximum index
    int maximum = 0;
    int maximumind = 0;

    // find the index which contain maximum value
    for (int i = 0; i < ra_num.Count; i++)
    {

        // divide lcm with denominator
        // and multiple with numerator
        temp[i] = (ra_num[i].nume) *
                  (lcm / ra_num[i].deno);

        // get the maximum numerator
        if (maximum < temp[i])
        {
            maximum = temp[i];
            maximumind = i;
        }
    }

    // return index which contain
    // maximum rational number
    return maximumind;
}

static int __gcd(int a, int b)
{
    if (b == 0)
        return a;
    return __gcd(b, a % b);
}

// Driver Code
public static void Main(String[] args)
{
    // given rational number
    List<Rational> ra_num = new List<Rational>();
                   ra_num.Add(new Rational( 1, 2 ));
                   ra_num.Add(new Rational( 2, 3 ));                        
                   ra_num.Add(new Rational( 3, 4 ));                        
                   ra_num.Add(new Rational( 4, 5 ));                        

    // get the index which contain maximum value
    int index_max = maxRational(ra_num);

    // print numerator and denominator
    Console.WriteLine(ra_num[index_max].nume +
                " " + ra_num[index_max].deno);
    }
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>
      // JavaScript program to find the maximum rational
      // number in an array.

      class Rational {
        constructor(nume, deno) {
          this.nume = nume;
          this.deno = deno;
        }
      }

      // here we find the Denominator LCM
      function lcmOfDenominator(ra_num) {
        // get the first Denominator as lcm
        var lcm = ra_num[0].deno;
        var i;

        // find the lcm of all relational
        // number Denominator
        for (i = 1; i < ra_num.length; i++)
          lcm = (lcm * ra_num[i].deno) / __gcd(lcm, ra_num[i].deno);

        // return the lcm
        return lcm;
      }

      function maxRational(ra_num) {
        // take a temp array for find
        // maximum numerator after multiple
        var temp = new Array(ra_num.Count);

        // get here the lcm of all rational
        //number denominator
        var lcm = lcmOfDenominator(ra_num);

        // take maximum for get maximum index
        var maximum = 0;
        var maximumind = 0;

        // find the index which contain maximum value
        for (var i = 0; i < ra_num.length; i++) {
          // divide lcm with denominator
          // and multiple with numerator
          temp[i] = ra_num[i].nume * (lcm / ra_num[i].deno);

          // get the maximum numerator
          if (maximum < temp[i]) {
            maximum = temp[i];
            maximumind = i;
          }
        }

        // return index which contain
        // maximum rational number
        return maximumind;
      }

      function __gcd(a, b) {
        if (b === 0) return a;
        return __gcd(b, a % b);
      }

      // Driver Code
      // given rational number
      var ra_num = [];
      ra_num.push(new Rational(1, 2));
      ra_num.push(new Rational(2, 3));
      ra_num.push(new Rational(3, 4));
      ra_num.push(new Rational(4, 5));

      // get the index which contain maximum value
      var index_max = maxRational(ra_num);

      // print numerator and denominator
      document.write(ra_num[index_max].nume + " " + ra_num[index_max].deno);
    </script>
```

**输出:**

```
4 5
```
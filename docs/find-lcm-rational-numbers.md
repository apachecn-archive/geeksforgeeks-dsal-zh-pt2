# 求有理数的 LCM

> 原文:[https://www.geeksforgeeks.org/find-lcm-rational-numbers/](https://www.geeksforgeeks.org/find-lcm-rational-numbers/)

给定一组有理数，任务是找到这些数的 LCM。
示例:

```
Input : vect[] = {2/7, 3/14, 5/3}
Output : 30/1

Input : vect[] = {3/14, 5/3}
Output : 15/1

Input : vect[] = {3/4, 3/2}
Output : 3/2
```

首先求有理数所有分子的 lcm，然后求有理数所有分母的 gcd，然后除以所有分子的 lcm/所有分母的 gcd，这就是有理数的 LCM。
公式:-

```
      LCM of all the numerator of Rational number's
lcm = -----------------------------------------------
      GCD of all the denominator of Rational number's
```

## C++

```
// CPP program to find LCM of given array
#include <bits/stdc++.h>
using namespace std;

// get lcm of two numbers
int LCM(int a, int b)
{
    return (a * b) / (__gcd(a, b));
}

// Finds LCM of numerators
int lcmOfNumerator(vector<pair<int, int> > vect)
{
    // calculate the lcm of all numerators
    int lcm = vect[0].first;
    for (int i = 1; i < vect.size(); i++)
        lcm = LCM(vect[i].first, lcm);

    // return all numerator lcm
    return lcm;
}

// Get GCD of all the denominators
int gcdOfDemoninators(vector<pair<int, int> > vect)
{
    // calculate the gcd of all the denominators
    int gcd = vect[0].second;
    for (int i = 1; i < vect.size(); i++)
        gcd = __gcd(vect[i].second, gcd);

    // return all denominator gcd
    return gcd;
}

// find lcm of all the rational number
void lcmOfRationals(vector<pair<int, int> > vect)
{
    // return the LCM of all numerator/ GCD of all
    // denominator
    cout << lcmOfNumerator(vect) << "/"
        << gcdOfDemoninators(vect);
}

// Driver code
int main()
{
    vector<pair<int, int> > vect;

    // give rational number 2/7, 3/14, 5/3
    // make pair as a numerator and denominator
    vect.push_back(make_pair(2, 7));
    vect.push_back(make_pair(3, 14));
    vect.push_back(make_pair(5, 3));
    lcmOfRationals(vect);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// JAVA program to find LCM of given array
import java.util.*;

class GFG
{

static class pair
{
    int first, second;
    public pair(int first, int second)
    {
        this.first = first;
        this.second = second;
    }
}

// get lcm of two numbers
static int LCM(int a, int b)
{
    return (a * b) / (__gcd(a, b));
}
static int __gcd(int a, int b)
{
    return b == 0? a:__gcd(b, a % b);    
}

// Finds LCM of numerators
static int lcmOfNumerator(Vector<pair> vect)
{
    // calculate the lcm of all numerators
    int lcm = vect.get(0).first;
    for (int i = 1; i < vect.size(); i++)
        lcm = LCM(vect.get(i).first, lcm);

    // return all numerator lcm
    return lcm;
}

// Get GCD of all the denominators
static int gcdOfDemoninators(Vector<pair> vect)
{
    // calculate the gcd of all the denominators
    int gcd = vect.get(0).second;
    for (int i = 1; i < vect.size(); i++)
        gcd = __gcd(vect.get(i).second, gcd);

    // return all denominator gcd
    return gcd;
}

// find lcm of all the rational number
static void lcmOfRationals(Vector<pair> vect)
{
    // return the LCM of all numerator/ GCD of all
    // denominator
    System.out.print(lcmOfNumerator(vect)+ "/"
        + gcdOfDemoninators(vect));
}

// Driver code
public static void main(String[] args)
{
    Vector<pair> vect = new Vector<pair>();

    // give rational number 2/7, 3/14, 5/3
    // make pair as a numerator and denominator
    vect.add(new pair(2, 7));
    vect.add(new pair(3, 14));
    vect.add(new pair(5, 3));
    lcmOfRationals(vect);
}
}

// This code is contributed by Rajput-Ji
```

## 计算机编程语言

```
# Python program to find LCM of given array
import math

# get lcm of two numbers
def LCM(a, b):

    return (a * b) // (math.gcd(a, b))

# Finds LCM of numerators
def lcmOfNumerator(vect):

    # calculate the lcm of all numerators
    lcm = vect[0][0]
    for i in range(1, len(vect)):
        lcm = LCM(vect[i][0], lcm)

    # return all numerator lcm
    return lcm

# Get GCD of all the denominators
def gcdOfDemoninators(vect):

    # calculate the gcd of all the denominators
    gcd = vect[0][1]
    for i in range(1, len(vect)):
        gcd = math.gcd(vect[i][1], gcd)

    # return all denominator gcd
    return gcd

# find lcm of all the rational number
def lcmOfRationals(vect):

    # return the LCM of all numerator/ GCD of all
    # denominator
    print(lcmOfNumerator(vect), "/",
            gcdOfDemoninators(vect), sep = "")

# Driver code

vect = []

# give rational number 2/7, 3/14, 5/3
# make pair as a numerator and denominator
vect.append((2, 7))
vect.append((3, 14))
vect.append((5, 3))
lcmOfRationals(vect)

# This code is contributed by SHUBHAMSINGH10
```

## C#

```
// C# program to find LCM of given array
using System;
using System.Collections.Generic;

class GFG
{

class pair
{
    public int first, second;
    public pair(int first, int second)
    {
        this.first = first;
        this.second = second;
    }
}

// get lcm of two numbers
static int LCM(int a, int b)
{
    return (a * b) / (__gcd(a, b));
}
static int __gcd(int a, int b)
{
    return b == 0? a:__gcd(b, a % b);    
}

// Finds LCM of numerators
static int lcmOfNumerator(List<pair> vect)
{
    // calculate the lcm of all numerators
    int lcm = vect[0].first;
    for (int i = 1; i < vect.Count; i++)
        lcm = LCM(vect[i].first, lcm);

    // return all numerator lcm
    return lcm;
}

// Get GCD of all the denominators
static int gcdOfDemoninators(List<pair> vect)
{
    // calculate the gcd of all the denominators
    int gcd = vect[0].second;
    for (int i = 1; i < vect.Count; i++)
        gcd = __gcd(vect[i].second, gcd);

    // return all denominator gcd
    return gcd;
}

// find lcm of all the rational number
static void lcmOfRationals(List<pair> vect)
{
    // return the LCM of all numerator/ GCD of all
    // denominator
    Console.Write(lcmOfNumerator(vect)+ "/"
        + gcdOfDemoninators(vect));
}

// Driver code
public static void Main(String[] args)
{
    List<pair> vect = new List<pair>();

    // give rational number 2/7, 3/14, 5/3
    // make pair as a numerator and denominator
    vect.Add(new pair(2, 7));
    vect.Add(new pair(3, 14));
    vect.Add(new pair(5, 3));
    lcmOfRationals(vect);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// JAVASCRIPT program to find LCM of given array
class pair
{
    constructor(first, second)
    {
        this.first = first;
        this.second = second;
    }
}

// get lcm of two numbers
function LCM(a, b) {
    return Math.floor((a * b) / (__gcd(a, b)));
}

function __gcd(a, b) {
    return b == 0 ? a : __gcd(b, a % b);
}

// Finds LCM of numerators
function lcmOfNumerator(vect)
{

    // calculate the lcm of all numerators
    let lcm = vect[0].first;
    for (let i = 1; i < vect.length; i++)
        lcm = LCM(vect[i].first, lcm);

    // return all numerator lcm
    return lcm;
}

// Get GCD of all the denominators
function gcdOfDemoninators(vect)
{

    // calculate the gcd of all the denominators
    let gcd = vect[0].second;
    for (let i = 1; i < vect.length; i++)
        gcd = __gcd(vect[i].second, gcd);

    // return all denominator gcd
    return gcd;
}

// find lcm of all the rational number
function lcmOfRationals(vect) {
    // return the LCM of all numerator/ GCD of all
    // denominator
    document.write(lcmOfNumerator(vect) + "/"
        + gcdOfDemoninators(vect));
}

// Driver code

let vect = [];

// give rational number 2/7, 3/14, 5/3
// make pair as a numerator and denominator
vect.push(new pair(2, 7));
vect.push(new pair(3, 14));
vect.push(new pair(5, 3));
lcmOfRationals(vect);

// This code is contributed by _SAURABH_JAISWAL
</script>
```

**输出:**

```
30/1
```
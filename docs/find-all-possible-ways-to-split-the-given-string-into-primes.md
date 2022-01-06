# 找到所有可能的方法将给定的字符串拆分成素数

> 原文:[https://www . geeksforgeeks . org/find-所有可能的方法将给定的字符串拆分成素数/](https://www.geeksforgeeks.org/find-all-possible-ways-to-split-the-given-string-into-primes/)

给定代表数字的字符串**字符串**。任务是找到所有可能的方法来分割给定的字符串，使得每个片段都是 1 到 10 <sup>6</sup> 范围内的素数。
**例:**

> **输入:** str = "3175"
> **输出:**
> 【317，5】
> 【31，7，5】
> 【3，17，5】
> **解释:**
> 可以有 8 种可能的拆分方式:
> 【3175】
> 【317，5】–所有素数
> 【31，75】
> 【31，5】 5]
> **输入:** str = "11373"
> **输出:**
> 【113，73】
> 【113，7，3】
> 【11，373】
> 【11，37，3】
> 【11，3，73】
> 【11，3，7，3】

**进场:**

*   这个想法是通过计算从 0 到 2 的二进制数<sup>(N–1)</sup>–1 来生成大小为 N 的字符串的所有可能的拆分。其中每 1 表示字符串应该在该点拆分。
    **例如:**

```
 S = "3175"
 0 0 0   3175
 0 0 1   317, 5
 0 1 0   31, 75
 0 1 1   31, 7, 5
 1 0 0   3, 175
 1 0 1   3, 17, 5
 1 1 0   3, 1, 75
 1 1 1   3, 1, 7, 5
```

*   为了有效地检查素数，我们将使用厄拉多塞的[筛在布尔数组中预处理素数。](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)

下面是上述方法的实现。

## C++

```
// C++ program to Find all the
// ways to split the given string
// into Primes.
#include<bits/stdc++.h>
using namespace std;

bool primes[1000000];
const int maxn = 1000000;

// Sieve of Eratosthenes
void sieve()
{
    memset(primes,true,sizeof(primes));
    primes[0] = primes[1] = 0;

    for(int i = 2; i * i <= maxn; i++)
    {
        if(primes[i])
        {
            for(int j = i * i ;
                   j <= maxn ; j += i)
            primes[j] = false;
        }
    }
}

// Function Convert integer
// to binary string
string toBinary(int n)
{
    string r = "";
    while(n != 0)
    {
        r = (n % 2 == 0 ?"0":"1") + r;
        n /= 2;
    }
    return (r == "")?"0":r;
}

// Function print all the all the
// ways to split the given string
// into Primes.
void PrimeSplit(string str)
{
    string temp;
    int cnt=0;

    // To store all possible strings
    vector<string> ans;
    int bt = 1<<(str.size()-1);
    int n = str.size();

    // Exponetnital complexity n*(2^(n-1))
    // for bit
    for(int i = 0 ; i < bt ; i++)
    {
        temp = toBinary(i) + "0";
        int j = 0, x = n - temp.size(), y;
        while(j < x)
        {
            temp = "0" + temp;
            j++;
        }
        j = 0;
        x = 0;
        y = -1;

        string sp = "", tp = "";
        bool flag = 0;

        while(j < n)
        {
            sp += str[j];
            if(temp[j] == '1')
            {
                tp += sp + ',';
                y = stoi(sp);

                // Pruning step
                if(!primes[y])
                {
                    flag = 1;
                    break;
                }
                sp = "";
            }
            j++;
        }
        tp += sp;
        if(sp != "")
        {
            y = stoi(sp);
            if(!primes[y])
            flag = 1;
        }
        if(!flag)
        ans.push_back(tp);
    }
    if(ans.size() == 0)
    {
        cout << -1 << endl;
    }
    for(auto i:ans)
    {
        cout << i << endl;
    }
}

// Driver code
int main()
{
    string str = "11373";
    sieve();

    PrimeSplit(str);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to Find all the 
// ways to split the given string
// into Primes.
import java.util.*;
import java.lang.*;

class GFG{

static boolean[] primes = new boolean[1000001];
static int maxn = 1000000;

// Sieve of Eratosthenes
static void sieve()
{
    Arrays.fill(primes, true);
    primes[0] = false;
    primes[1] = false;

    for(int i = 2; i * i <= maxn; i++)
    {
        if (primes[i])
        {
            for(int j = i * i;
                    j <= maxn; j += i)
                primes[j] = false;
        }
    }
}

// Function Convert integer
// to binary string
static String toBinary(int n)
{
    String r = "";

    while(n != 0)
    {
        r = (n % 2 == 0 ? "0" : "1") + r;
        n /= 2;
    }
    return (r == "") ? "0" : r;
}

// Function print all the all the
// ways to split the given string
// into Primes.
static void PrimeSplit(String str)
{
    String temp;
    int cnt = 0;

    // To store all possible strings
    ArrayList<String> ans = new ArrayList<>();
    int bt = 1 << (str.length() - 1);
    int n = str.length();

    // Exponetnital complexity n*(2^(n-1))
    // for bit
    for(int i = 0; i < bt; i++)
    {
        temp = toBinary(i) + "0";
        int j = 0, x = n - temp.length(), y;

        while(j < x)
        {
            temp = "0" + temp;
            j++;
        }
        j = 0;
        x = 0;
        y = -1;

        String sp = "", tp = "";
        boolean flag = false;

        while(j < n)
        {
            sp += str.charAt(j);

            if (temp.charAt(j) == '1')
            {
                tp += sp + ',';
                y = Integer.parseInt(sp);

                // Pruning step
                if (!primes[y])
                {
                    flag = true;
                    break;
                }
                sp = "";
            }
            j++;
        }
        tp += sp;

        if (sp != "")
        {
            y = Integer.parseInt(sp);

            if (!primes[y])
                flag = true;
        }
        if (!flag)
        ans.add(tp);
    }

    if (ans.size() == 0)
    {
        System.out.println(-1);
    }

    for(String i : ans)
    {
        System.out.println(i);
    }
}

// Driver Code
public static void main (String[] args)
{
    String str = "11373";
    sieve();

    PrimeSplit(str);
}
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python 3 program to Find all the
# ways to split the given string
# into Primes.
primes = [True] * 1000001
maxn = 1000000

# Sieve of Eratosthenes
def sieve():

    primes[0] = primes[1] = 0   
    i = 2

    while i * i <= maxn:
        if(primes[i]):
            for j in range(i * i,
                           maxn + 1, i):
                primes[j] = False
        i += 1

# Function Convert integer
# to binary string
def toBinary(n):

    r = ""
    while(n != 0):
        if(n % 2 == 0 ):
          r = "0" + r
        else:
          r = "1" + r
        n //= 2

    if (r == ""):
      return "0"
    return r

# Function print all the all the
# ways to split the given string
# into Primes.
def PrimeSplit(st):

    cnt = 0

    # To store all
    # possible strings
    ans = []
    bt = 1 << (len(st) - 1)
    n = len(st)

    # Exponetnital complexity
    # n*(2^(n-1)) for bit
    for i in range(bt):   
        temp = toBinary(i) + "0"
        j = 0
        x = n - len(temp)
        while(j < x):
            temp = "0" + temp
            j += 1

        j = 0
        x = 0
        y = -1

        sp = ""
        tp = ""
        flag = 0

        while(j < n):
            sp += st[j]
            if(temp[j] == '1'):           
                tp += sp + ','
                y = int(sp)

                # Pruning step
                if(not primes[y]):
                    flag = 1
                    break
                sp = ""
            j += 1

        tp += sp

        if(sp != ""):
            y = int(sp)
            if(not primes[y]):
               flag = 1

        if(not flag):
           ans.append(tp)

    if(len(ans) == 0):
        print (-1)

    for i in ans:
        print (i)

# Driver code
if __name__ == "__main__":

    st = "11373"
    sieve()   
    PrimeSplit(st)

# This code is contributed by Chitranayal
```

## C#

```
// C# program to Find all the 
// ways to split the given string
// into Primes.
using System;
using System.Collections.Generic;
class GFG{

static bool[] primes =
       new bool[1000001];
static int maxn = 1000000;

// Sieve of Eratosthenes
static void sieve()
{
  for(int i = 0;
          i < primes.Length; i++)
  {
    primes[i] = true;
  }
  primes[0] = false;
  primes[1] = false;

  for(int i = 2; i * i <= maxn; i++)
  {
    if (primes[i])
    {
      for(int j = i * i;
              j <= maxn; j += i)
        primes[j] = false;
    }
  }
}

// Function Convert integer
// to binary string
static String toBinary(int n)
{
  String r = "";

  while(n != 0)
  {
    r = (n % 2 == 0 ?
         "0" : "1") + r;
    n /= 2;
  }
  return (r == "") ? "0" : r;
}

// Function print all the all the
// ways to split the given string
// into Primes.
static void PrimeSplit(String str)
{
  String temp;

  // To store all possible strings
  List<String> ans = new List<String>();
  int bt = 1 << (str.Length - 1);
  int n = str.Length;

  // Exponetnital complexity
  // n*(2^(n-1)) for bit
  for(int i = 0; i < bt; i++)
  {
    temp = toBinary(i) + "0";
    int j = 0, x = n - temp.Length, y;

    while(j < x)
    {
      temp = "0" + temp;
      j++;
    }
    j = 0;
    x = 0;
    y = -1;

    String sp = "", tp = "";
    bool flag = false;

    while(j < n)
    {
      sp += str[j];

      if (temp[j] == '1')
      {
        tp += sp + ',';
        y = Int32.Parse(sp);

        // Pruning step
        if (!primes[y])
        {
          flag = true;
          break;
        }
        sp = "";
      }
      j++;
    }
    tp += sp;

    if (sp != "")
    {
      y = Int32.Parse(sp);

      if (!primes[y])
        flag = true;
    }

    if (!flag)
      ans.Add(tp);
  }

  if (ans.Count == 0)
  {
    Console.WriteLine(-1);
  }

  foreach(String i in ans)
  {
    Console.WriteLine(i);
  }
}

// Driver Code
public static void Main(String[] args)
{
  String str = "11373";
  sieve();
  PrimeSplit(str);
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>
// Javascript program to Find all the
// ways to split the given string
// into Primes.

let primes = new Array(1000000);
const maxn = 1000000;

// Sieve of Eratosthenes
function sieve()
{
    primes.fill(true)
    primes[0] = primes[1] = 0;

    for(let i = 2; i * i <= maxn; i++)
    {
        if(primes[i])
        {
            for(let j = i * i ;
                j <= maxn ; j += i)
            primes[j] = false;
        }
    }
}

// Function Convert integer
// to binary string
function toBinary(n)
{
    let r = "";
    while(n != 0)
    {
        r = (n % 2 == 0 ?"0":"1") + r;
        n = Math.floor(n / 2);
    }
    return (r == "")?"0":r;
}

// Function print all the all the
// ways to split the given string
// into Primes.
function PrimeSplit(str)
{
    let temp;
    let cnt=0;

    // To store all possible strings
    let ans = new Array();
    let bt = 1 << (str.length-1);
    let n = str.length;

    // Exponetnital complexity n*(2^(n-1))
    // for bit
    for(let i = 0 ; i < bt ; i++)
    {
        temp = toBinary(i) + "0";
        let j = 0, x = n - temp.length, y;
        while(j < x)
        {
            temp = "0" + temp;
            j++;
        }
        j = 0;
        x = 0;
        y = -1;

        let sp = "", tp = "";
        let flag = 0;

        while(j < n)
        {
            sp += str[j];
            if(temp[j] == '1')
            {
                tp += sp + ',';
                y = parseInt(sp);

                // Pruning step
                if(!primes[y])
                {
                    flag = 1;
                    break;
                }
                sp = "";
            }
            j++;
        }
        tp += sp;
        if(sp != "")
        {
            y = parseInt(sp);
            if(!primes[y])
            flag = 1;
        }
        if(!flag)
        ans.push(tp);
    }
    if(ans.length == 0)
    {
        document.write(-1 + "<br>");
    }
    for(let i of ans)
    {
        document.write(i + "<br>");
    }
}

// Driver code

let str = "11373";
sieve();

PrimeSplit(str);

// This code is contributed by _saurabh_jaiswal
</script>
```

**Output:** 

```
113,73
113,7,3
11,373
11,37,3
11,3,73
11,3,7,3
```
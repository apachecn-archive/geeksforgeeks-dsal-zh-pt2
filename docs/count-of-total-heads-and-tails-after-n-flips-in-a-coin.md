# 硬币中 N 次翻转后正面和反面总数的计数

> 原文:[https://www . geesforgeks . org/硬币翻转后正面和反面总数/](https://www.geeksforgeeks.org/count-of-total-heads-and-tails-after-n-flips-in-a-coin/)

给定**字符 C** 和一个**整数 N** 表示 C 位置的 N 个硬币，其中 C 可以是**头**或**尾**。我们可以将硬币翻转 N 次，其中第一轮玩家将翻转所有数量小于或等于 I 的硬币的正面，任务是在翻转 N 次可能的情况下确定头尾总数。

**示例:**

> **输入:** C = 'H '，N = 5
> **输出:**头= 2，尾= 3
> **说明:**
> H 表示最初所有硬币面向头方向，N 表示硬币总数。
> 所以最初对于 i = 0， 我们有:H H H H H
> 第一回合后即 i = 1: T H H H H
> 第二回合后即 i = 2: H T H H H
> 第三回合后即 i = 3: T H T H H
> 第四回合后即 i = 4: H T H T H
> 第五回合后即 i = 5: T H T H T
> 因此头尾总数为 2。
> 
> **输入:** C = 'T '，N = 7
> **输出:**头= 4，尾= 3
> **解释:**
> 在所有可能的空翻之后，头尾计数为 4 和 3。

**方法:**
要解决上面提到的问题，我们必须遵循下面给出的步骤:

*   在上面的问题中，如果我们观察，那么有一个模式，如果最初，所有的硬币都面向**头**方向，那么 N 轮后的头总数将是(n / 2)的底值，尾部将是(n / 2)的单元值。
*   否则，如果所有硬币都朝向**尾部**方向，那么 N 轮后尾部的总数将是地板值(n / 2)，头部将是天花板值(n / 2)。

下面是实现:

## C++

```
// C++ program to count total heads
// and tails after N flips in a coin
#include<bits/stdc++.h>
using namespace std;

// Function to find count of head and tail
pair<int, int> count_ht(char s, int N)
{

    // Check if initially all the
    // coins are facing towards head
    pair<int, int>p;
    if(s == 'H')
    {
        p.first = floor(N / 2.0);
        p.second = ceil(N / 2.0);
    }

    // Check if initially all the coins
    // are facing towards tail
    else if(s == 'T')
    {
        p.first = ceil(N / 2.0);
        p.second = floor(N / 2.0);
    }

    return p;
}

// Driver code
int main()
{
    char C = 'H';
    int N = 5;

    pair<int, int> p = count_ht(C, N);

    cout << "Head = " << (p.first) << "\n";
    cout << "Tail = " << (p.second) << "\n";
}

// This code is contributed by virusbuddah_
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count
// total heads and tails
// after N flips in a coin
import javafx.util.Pair;
public class Main
{
// Function to find count of head and tail 
public static Pair <Integer,
                    Integer> count_ht(char s,
                                      int N)
{              
  // Check if initially all the 
  // coins are facing towards head 
  Pair <Integer,
        Integer> p = new Pair <Integer,
                               Integer> (0, 0);
  if(s == 'H')
  {
     p = new Pair <Integer,
                   Integer> ((int)Math.floor(N / 2.0),
                             (int)Math.ceil(N / 2.0));
  }

  // Check if initially all the coins 
  // are facing towards tail 
  else if(s == 'T')
  {
     p = new Pair <Integer,
                   Integer> ((int)Math.ceil(N / 2.0),
                             (int)Math.floor(N / 2.0));
  }
  return p;
}

public static void main(String[] args)
{
  char C = 'H';
  int N = 5;
  Pair <Integer,
        Integer> p = count_ht(C, N);
  System.out.println("Head = " + p.getKey());
  System.out.println("Tail = " + p.getValue());
}
}

// This code is contributed by divyeshrabadiya07
```

## 蟒蛇 3

```
# Python3 program to Count total heads
# and tails after N flips in a coin

# Function to find count of head and tail
import math
def count_ht( s, N ):

    # Check if initially all the
    # coins are facing towards head
    if s == "H":
        h = math.floor( N / 2 )
        t = math.ceil( N / 2 )

    # Check if initially all the coins
    # are facing towards tail
    elif s == "T":
        h = math.ceil( N / 2 )
        t = math.floor( N / 2 )

    return [h, t]

# Driver Code
if __name__ == "__main__":
    C = "H"
    N = 5
    l = count_ht(C, n)
    print("Head = ", l[0])
    print("Tail = ", l[1])
```

## C#

```
// C# program to count total heads
// and tails after N flips in a coin
using System;

class GFG{

// Function to find count of head and tail 
public static Tuple<int, int> count_ht(char s,
                                       int N)
{ 

    // Check if initially all the 
    // coins are facing towards head 
    Tuple<int, int> p = Tuple.Create(0, 0);

    if (s == 'H')
    {
        p = Tuple.Create((int)Math.Floor(N / 2.0),
                         (int)Math.Ceiling(N / 2.0));
    }

    // Check if initially all the coins 
    // are facing towards tail 
    else if (s == 'T')
    {
        p = Tuple.Create((int)Math.Ceiling(N / 2.0),
                         (int)Math.Floor(N / 2.0));
    }
    return p;
}

// Driver Code
static void Main()
{
    char C = 'H';
    int N = 5;
    Tuple<int, int> p = count_ht(C, N);

    Console.WriteLine("Head = " + p.Item1);
    Console.WriteLine("Tail = " + p.Item2);
}
}

// This code is contributed by divyesh072019
```

## java 描述语言

```
<script>

// JavaScript program to count total heads
// and tails after N flips in a coin

// Function to find count of head and tail
function count_ht(s, N)
{

    // Check if initially all the
    // coins are facing towards head
    var p = [0,0];
    if(s == 'H')
    {
        p[0] = Math.floor(N / 2.0);
        p[1] = Math.ceil(N / 2.0);
    }

    // Check if initially all the coins
    // are facing towards tail
    else if(s == 'T')
    {
        p[0] = Math.ceil(N / 2.0);
        p[1] = Math.floor(N / 2.0);
    }

    return p;
}

// Driver code
var C = 'H';
var N = 5;

var p = count_ht(C, N);

document.write( "Head = " + (p[0]) + "<br>");
document.write( "Tail = " + (p[1]) + "<br>");

</script>
```

**Output:** 

```
Head =  2
Tail =  3
```

***时间复杂度:** O(1)*
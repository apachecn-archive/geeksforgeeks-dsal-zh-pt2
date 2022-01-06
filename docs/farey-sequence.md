# Farey 序列

> 原文:[https://www.geeksforgeeks.org/farey-sequence/](https://www.geeksforgeeks.org/farey-sequence/)

Farey 序列是为 n 阶生成的序列。该序列将[0/0 到 1/1]范围内的所有有理数按递增顺序排序，使得分母小于或等于 n，并且所有数都是简化形式，即 4/4 不能存在，因为它可以简化为 1/1。
**例:**

```
F1 = 0/1, 1/1
F2 = 0/1, 1/2, 1/1
F3 = 0/1, 1/3, 1/2, 2/3, 1/1
.
.
F7 = 0/1, 1/7, 1/6, 1/5, 1/4, 2/7, 1/3, 2/5,
     3/7, 1/2, 4/7, 3/5, 2/3, 5/7, 3/4, 4/5,
     5/6, 6/7, 1/1
```

Farey 序列用于无理数的有理逼近，福特圆和黎曼假设中的
(详见[本](https://en.wikipedia.org/wiki/Farey_sequence#Applications))
**如何生成给定顺序的 Farey 序列？**
思路很简单，我们考虑从 1/1 到 n/n 的每一个可能的有理数，并且对于每一个生成的有理数，我们检查它是否是约化形式。如果是，那么我们将其添加到 Farey 序列中。如果分子和分母的 [GCD](https://www.geeksforgeeks.org/basic-and-extended-euclidean-algorithms/) 为 1，则有理数为简化形式。
以下是基于上述思路的实现。

## C++

```
// C++ program to print Farey Sequence of given order
#include <bits/stdc++.h>
using namespace std;

// class for x/y (a term in farey sequence
class Term {
public:
    int x, y;

    // Constructor to initialize x and y in x/y
    Term(int x, int y)
        : x(x), y(y)
    {
    }
};

// Comparison function for sorting
bool cmp(Term a, Term b)
{
    // Comparing two ratio
    return a.x * b.y < b.x * a.y;
}

// GCD of a and b
int gcd(int a, int b)
{
    if (b == 0)
        return a;
    return gcd(b, a % b);
}

// Function to print Farey sequence of order n
void farey(int n)
{
    // Create a vector to store terms of output
    vector<Term> v;

    // One by one find and store all terms except 0/1 and n/n
    // which are known
    for (int i = 1; i <= n; ++i) {
        for (int j = i + 1; j <= n; ++j)

            // Checking whether i and j are in lowest term
            if (gcd(i, j) == 1)
                v.push_back(Term(i, j));
    }

    // Sorting the term of sequence
    sort(v.begin(), v.end(), cmp);

    // Explicitly printing first term
    cout << "0/1 ";

    // Printing other terms
    for (int i = 0; i < v.size(); ++i)
        cout << v[i].x << "/" << v[i].y << " ";

    // explicitly printing last term
    cout << "1/1";
}

// Driver program
int main()
{
    int n = 7;
    cout << "Farey Sequence of order " << n << " is\n";
    farey(n);
    return 0;
}
```

## 蟒蛇 3

```
# Python3 program to print
# Farey Sequence of given order

# class for x/y (a term in farey sequence
class Term:

    # Constructor to initialize
    # x and y in x/y
    def __init__(self, x, y):
        self.x = x
        self.y = y

# GCD of a and b
def gcd(a, b):
    if b == 0:
        return a
    return gcd(b, a % b)

# Function to print
# Farey sequence of order n
def farey(n):

    # Create a vector to
    # store terms of output
    v = []

    # One by one find and store
    # all terms except 0/1 and n/n
    # which are known
    for i in range(1, n + 1):
        for j in range(i + 1, n + 1):

            # Checking whether i and j
            # are in lowest term
            if gcd(i, j) == 1:
                v.append(Term(i, j))

    # Sorting the term of sequence
    for i in range(len(v)):
        for j in range(i + 1, len(v)):
            if (v[i].x * v[j].y > v[j].x * v[i].y):
                v[i], v[j] = v[j], v[i]

    # Explicitly printing first term
    print("0/1", end = " ")

    # Printing other terms
    for i in range(len(v)):
        print("%d/%d" % (v[i].x,
                        v[i].y), end = " ")

    # explicitly printing last term
    print("1/1")

# Driver Code
if __name__ == "__main__":
    n = 7
    print("Farey sequence of order %d is" % n)
    farey(n)

# This code is contributed by
# sanjeev2552
```

## java 描述语言

```
<script>
// Javascript program to print
// Farey Sequence of given order

// class for x/y (a term in farey sequence
class Term
{
    // Constructor to initialize
    // x and y in x/y
    constructor(x, y)
    {
        this.x = x;
        this.y = y;
    }
}

// GCD of a and b
function gcd(a, b)
{
    if(b == 0)
        return a
    return gcd(b, a % b)   
}

// Function to print
// Farey sequence of order n
function farey(n)
{
    // Create a vector to
    // store terms of output
    let v = []

    // One by one find and store
    // all terms except 0/1 and n/n
    // which are known
    for(let i=1;i<n + 1;i++)
    {
        for(j=i+1;j<n + 1;j++)
         {
            // Checking whether i and j
            // are in lowest term
            if (gcd(i, j) == 1)
                v.push(new Term(i, j))
         }
    }
    // Sorting the term of sequence
    for(let i=0;i<(v).length;i++)
    {
        for(let j=i + 1; j<(v).length; j++)
        {
            if (v[i].x * v[j].y > v[j].x * v[i].y)
            {
                let temp = v[j];
                v[j] = v[i];
                v[i] = temp;

            }
        }
     }
    // Explicitly printing first term
    document.write("0/1 ")

    // Printing other terms
    for(let i=0;i<(v).length;i++)
        document.write(v[i].x+"/"+v[i].y+" ")

    // explicitly printing last term
    document.write("1/1")
}

// Driver Code
let n = 7;
document.write("Farey sequence of order "+n+ " is<br>" );
farey(n)

// This code is contributed by patel2127
</script>
```

**输出:**

```
Farey Sequence of order 7 is
0/1 1/7 1/6 1/5 1/4 2/7 1/3 2/5 3/7 1/2 4/7 
3/5 2/3 5/7 3/4 4/5 5/6 6/7 1/1
```

上述方法的时间复杂度为 O(n <sup>2</sup> Log n)，其中 O(log n)是[欧几里德算法对 GCD](https://www.geeksforgeeks.org/basic-and-extended-euclidean-algorithms/) 所用时间的上限。
Farey Sequence 有以下属性【详情见[wiki](https://en.wikipedia.org/wiki/Farey_sequence#Next_term)
一个项 x/y 可以用前面两个项递归求值。下面是由 x <sub>n+1</sub> /y <sub>n+1</sub> 和 x <sub>n</sub> /y <sub>n</sub> 计算 x<sub>n+2</sub>/y 的公式。

```
x[n+2] = floor((y[n]+n) / y[n+1])x[n+1]– x[n]      
y[n+2] = floor((y[n]+n) / y[n+1])y[n+1]– y[n]    
```

我们可以利用以上属性进行优化。

## C++

```
// Efficient C++ program to print Farey Sequence of order n
#include <bits/stdc++.h>
using namespace std;

// Optimized function to print Farey sequence of order n
void farey(int n)
{
    // We know first two terms are 0/1 and 1/n
    double x1 = 0, y1 = 1, x2 = 1, y2 = n;

    printf("%.0f/%.0f %.0f/%.0f", x1, y1, x2, y2);

    double x, y = 0; // For next terms to be evaluated
    while (y != 1.0) {
        // Using recurrence relation to find the next term
        x = floor((y1 + n) / y2) * x2 - x1;
        y = floor((y1 + n) / y2) * y2 - y1;

        // Print next term
        printf(" %.0f/%.0f", x, y);

        // Update x1, y1, x2 and y2 for next iteration
        x1 = x2, x2 = x, y1 = y2, y2 = y;
    }
}

// Driver program
int main()
{
    int n = 7;
    cout << "Farey Sequence of order " << n << " is\n";
    farey(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Efficient Java program to print
// Farey Sequence of order n
class GFG
{

// Optimized function to print
// Farey sequence of order n
static void farey(int n)
{
    // We know first two terms are 0/1 and 1/n
    double x1 = 0, y1 = 1, x2 = 1, y2 = n;

    System.out.printf("%.0f/%.0f %.0f/%.0f", x1, y1, x2, y2);

    double x, y = 0; // For next terms to be evaluated
    while (y != 1.0)
    {
        // Using recurrence relation to find the next term
        x = Math.floor((y1 + n) / y2) * x2 - x1;
        y = Math.floor((y1 + n) / y2) * y2 - y1;

        // Print next term
        System.out.printf(" %.0f/%.0f", x, y);

        // Update x1, y1, x2 and y2 for next iteration
        x1 = x2;
        x2 = x;
        y1 = y2;
        y2 = y;
    }
}

// Driver program
public static void main(String[] args)
{
    int n = 7;
    System.out.print("Farey Sequence of order " + n + " is\n");
    farey(n);
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Efficient Python3 program to print
# Farey Sequence of order n
import math

# Optimized function to print Farey
# sequence of order n
def farey(n):

    # We know first two terms are
    # 0/1 and 1/n
    x1 = 0;
    y1 = 1;
    x2 = 1;
    y2 = n;

    print(x1, end = "")
    print("/", end = "")
    print(y1, x2, end = "")
    print("/", end = "")
    print(y2, end = " ");

    # For next terms to be evaluated
    x = 0;
    y = 0;
    while (y != 1.0):

        # Using recurrence relation to
        # find the next term
        x = math.floor((y1 + n) / y2) * x2 - x1;
        y = math.floor((y1 + n) / y2) * y2 - y1;

        # Print next term
        print(x, end = "")
        print("/", end = "")
        print(y, end = " ");

        # Update x1, y1, x2 and y2 for
        # next iteration
        x1 = x2;
        x2 = x;
        y1 = y2;
        y2 = y;

# Driver Code
n = 7;
print("Farey Sequence of order", n, "is");
farey(n);

# This code is contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// Efficient php program to print
// Farey Sequence of order n

// Optimized function to print
// Farey sequence of order n
function farey($n)
{

    // We know first two
    // terms are 0/1 and 1/n
    $x1 = 0;
    $y1 = 1;
    $x2 = 1;
    $y2 = $n;

        echo $x1, "/", $y1,
             " ", $x2, "/",
             $y2, " ";

    // For next terms
    // to be evaluated
    $x;
    $y = 0;
    while ($y != 1.0)
    {

        // Using recurrence relation to
        // find the next term
        $x = floor(($y1 + $n) / $y2) * $x2 - $x1;
        $y = floor(($y1 + $n) / $y2) * $y2 - $y1;

        // Print next term
        echo $x, "/", $y, " ";

        // Update x1, y1, x2 and
        // y2 for next iteration
        $x1 = $x2;
        $x2 = $x;
        $y1 = $y2;
        $y2 = $y;
    }
}

    // Driver Code
    $n = 7;
    echo "Farey Sequence of order ", $n, " is\n";
    farey($n);

// This code is contributed by ajit
?>
```

## C#

```
// Efficient C# program to print
// Farey Sequence of order n
using System;

public class GFG
{

// Optimized function to print
// Farey sequence of order n
static void farey(int n)
{
    // We know first two terms are 0/1 and 1/n
    double x1 = 0, y1 = 1, x2 = 1, y2 = n;

    Console.Write("{0:F0}/{1:F0} {2:F0}/{3:F0}", x1, y1, x2, y2);

    double x, y = 0; // For next terms to be evaluated
    while (y != 1.0)
    {
        // Using recurrence relation to find the next term
        x = Math.Floor((y1 + n) / y2) * x2 - x1;
        y = Math.Floor((y1 + n) / y2) * y2 - y1;

        // Print next term
        Console.Write(" {0:F0}/{1:F0}", x, y);

        // Update x1, y1, x2 and y2 for next iteration
        x1 = x2;
        x2 = x;
        y1 = y2;
        y2 = y;
    }
}

// Driver program
public static void Main(String[] args)
{
    int n = 7;
    Console.Write("Farey Sequence of order " + n + " is\n");
    farey(n);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// Efficient javascript program to print
// Farey Sequence of order n   
// Optimized function to print
    // Farey sequence of order n
    function farey(n)
    {

        // We know first two terms are 0/1 and 1/n
        var x1 = 0, y1 = 1, x2 = 1, y2 = n;

        document.write(x1+"/"+y1+" "+x2+"/"+y2+" ");

        var x, y = 0; // For next terms to be evaluated
        while (y != 1.0)
        {

            // Using recurrence relation to find the next term
            x = Math.floor((y1 + n) / y2) * x2 - x1;
            y = Math.floor((y1 + n) / y2) * y2 - y1;

            // Print next term
            document.write(x+"/"+ y+" ");

            // Update x1, y1, x2 and y2 for next iteration
            x1 = x2;
            x2 = x;
            y1 = y2;
            y2 = y;
        }
    }

    // Driver program   
        var n = 7;
        document.write("Farey Sequence of order " + n + " is<br/>");
        farey(n);

// This code is contributed by gauravrajput1
</script>
```

**输出:**

```
Farey Sequence of order 7 is
0/1 1/7 1/6 1/5 1/4 2/7 1/3 2/5 3/7 1/2 4/7 
3/5 2/3 5/7 3/4 4/5 5/6 6/7 1/1
```

该解的时间复杂度为 O(n)
**参考文献:**
[【https://en.wikipedia.org/wiki/Farey_sequence】](https://en.wikipedia.org/wiki/Farey_sequence)
本文由乌特卡什·特里维迪供稿。如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。
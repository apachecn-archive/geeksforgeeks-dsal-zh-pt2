# 从 N 个容器中最大化一种类型的概率

> 原文:[https://www . geesforgeks . org/maximization-probability-one-type-n-containers/](https://www.geeksforgeeks.org/maximizing-probability-one-type-n-containers/)

给定由数字 A 的 N 个副本和数字 b 的 N 个副本组成的 N 个容器。我们需要将数字排列在 N 个容器中，使得随机选择一个容器并绘制一个数字 A 的副本的概率最大。

**示例:**

```
Input : N = 1
Output : 0.5,

Input : N = 2
Output : 0.667
```

我们需要在 N 个容器中寻找编号 A 的 N 个副本和编号 B 的 N 个副本的最佳排列。

```
Pi = (Favorable Outcomes) / (Total Outcomes)

where Pi denotes the probability of an event i.
```

因此，为了最大化这一点，我们要么最小化分母(即总结果)，要么最大化分子(即总有利结果)，同时保持另一个不变。

考虑一种可能的安排，在第一(N-1)个容器中，我们只放入编号 A 的副本，这样第一(N-1)个容器包含编号 A 的(N-1)个副本，而不包含编号 B 的副本。然后将编号 A 的遗漏副本和编号 B 的 N 个副本放入最后一个容器中。

> 概率(来自第一(N-1)个容器的 a 副本)= **P <sub>n-1 个容器</sub> = 1**
> 概率(来自第 n 个<sup>第</sup>个容器的 a 副本)=**p<sub>n</sub>=<sup>1</sup>ⅰ<sub>(n+1)</sub>**t15】p<sub>max</sub>= p<sub>n-1 个容器</sub>*(n–1)

## C++

```
// CPP program to find maximum probability of
// getting a copy 'A' from N
#include <bits/stdc++.h>
using namespace std;

// Returns the Maximum probability for Drawing
// 1 copy of number A from N containers with N
// copies each of numbers A and B
double calculateProbability(int N)
{
    // Pmax = N/(N+1)
    double probability = (double)N / (N + 1);
    return probability;
}

int main()
{
    int N;
    double probabilityMax;

    // 1\. N = 1
    N = 1;
    probabilityMax = calculateProbability(N);
    cout << "Maximum Probability for N = "
         << N << " is, " << setprecision(4)
        << fixed << probabilityMax << endl;

    // 2\. N = 2
    N = 2;
    probabilityMax = calculateProbability(N);
    cout << "Maximum Probability for N = "
         << N << " is, " << setprecision(4)
         << fixed << probabilityMax << endl;

    // 3\. N = 10
    N = 10;
    probabilityMax = calculateProbability(N);
    cout << "Maximum Probability for N = "
         << N << " is, " << setprecision(4)
         << fixed << probabilityMax << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find maximum probability of
// getting a copy 'A' from N
class GFG {

    // Returns the Maximum probability for Drawing
    // 1 copy of number A from N containers with N
    // copies each of numbers A and B
    static double calculateProbability(int N)
    {

        // Pmax = N/(N+1)
        double probability = (double)N / (N + 1);

        return probability;
    }

    // Driver code
    public static void main(String[] args)
    {

        int N;
        double probabilityMax;

        // 1\. N = 1
        N = 1;
        probabilityMax = calculateProbability(N);

        System.out.println("Maximum Probability for"
                  + " N = " + N + " is, " + Math.round(
                  probabilityMax * 10000.0) / 10000.0);

        // 2\. N = 2
        N = 2;
        probabilityMax = calculateProbability(N);
        System.out.println("Maximum Probability for N = "
                          + N + " is, " + Math.round(
                     probabilityMax * 10000.0) / 10000.0);

        // 3\. N = 10
        N = 10;
        probabilityMax = calculateProbability(N);
        System.out.println("Maximum Probability for N = "
                            + N + " is, " + Math.round(
                     probabilityMax * 10000.0) / 10000.0);
    }
}

// This code is contributed by Anant Agarwal.
```

## 蟒蛇 3

```
# Python3 program to find maximum
# probability of getting a copy 'A' from N

# Returns the Maximum probability for
# Drawing 1 copy of number A from N
# containers with N copies each of
# numbers A and B
def calculateProbability(N):

    # Pmax = N / (N+1)
    probability = N / (N + 1)
    return probability

# Driver code

# 1\. N = 1
N = 1
probabilityMax = calculateProbability(N)
print("Maximum Probability for N = ",
       N , "is, %.4f" %probabilityMax)

# 2\. N = 2
N = 2
probabilityMax = calculateProbability(N);
print("Maximum Probability for N =",
       N, "is, %.4f" %probabilityMax)

# 3\. N = 10
N = 10
probabilityMax = calculateProbability(N);
print("Maximum Probability for N =",
       N,"is, %.4f" %probabilityMax)

# This code is contributed by Anant Agarwal.
```

## C#

```
// C# program to find maximum probability of
// getting a copy 'A' from N
using System;

class GFG {

    // Returns the Maximum probability for Drawing
    // 1 copy of number A from N containers with N
    // copies each of numbers A and B
    static double calculateProbability(int N)
    {

        // Pmax = N/(N+1)
        double probability = (double)N / (N + 1);
        return probability;
    }

    //Driver code
    public static void Main ()
    {
        int N;
        double probabilityMax;

        // 1\. N = 1
        N = 1;
        probabilityMax = calculateProbability(N);
        Console.WriteLine("Maximum Probability for N = "
             + N + " is, " +
        Math.Round(probabilityMax * 10000.0) / 10000.0);

        // 2\. N = 2
        N = 2;
        probabilityMax = calculateProbability(N);
        Console.WriteLine("Maximum Probability for N = "
             + N + " is, " +
        Math.Round(probabilityMax * 10000.0) / 10000.0);

        // 3\. N = 10
        N = 10;
        probabilityMax = calculateProbability(N);
        Console.WriteLine("Maximum Probability for N = "
             + N + " is, " +
        Math.Round(probabilityMax * 10000.0) / 10000.0);

    }
}

// This code is contributed by Anant Agarwal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find maximum
// probability of getting a
// copy 'A' from N

// Returns the Maximum probability
// for Drawing 1 copy of number A
// from N containers with N
// copies each of numbers A and B
function calculateProbability($N)
{
    // Pmax = N/(N+1)
    $probability = $N / ($N + 1);
    return $probability;
}

// 1\. N = 1
$N = 1;
$probabilityMax = calculateProbability($N);
echo ("Maximum Probability for N = ".
                        $N . " is, ".
    round($probabilityMax, 4). "\n");

// 2\. N = 2
$N = 2;
$probabilityMax = calculateProbability($N);
echo ("Maximum Probability for N = " .
                         $N. " is, " .
    round($probabilityMax, 4) . "\n");

// 3\. N = 10
$N = 10;
$probabilityMax = calculateProbability($N);
echo ("Maximum Probability for N = " .
                        $N . " is, " .
    round($probabilityMax, 4) . "\n");

// This code is contributed by
// Manish Shaw(manishshaw1)
?>
```

## java 描述语言

```
<script>

// JavaScript program to find maximum probability of
// getting a copy 'A' from N

// Returns the Maximum probability for Drawing
// 1 copy of number A from N containers with N
// copies each of numbers A and B
function calculateProbability(N)
{

    // Pmax = N/(N+1)
    let probability = N / (N + 1);

    return probability;
}

// Driver Code
let N;
let probabilityMax;

// 1\. N = 1
N = 1;
probabilityMax = calculateProbability(N);

document.write("Maximum Probability for" +
               " N = " + N + " is, " + Math.round(
               probabilityMax * 10000.0) / 10000.0 + "<br/>");

// 2\. N = 2
N = 2;
probabilityMax = calculateProbability(N);
document.write("Maximum Probability for N = " + N +
               " is, " + Math.round(
               probabilityMax * 10000.0) / 10000.0 + "<br/>");

// 3\. N = 10
N = 10;
probabilityMax = calculateProbability(N);
document.write("Maximum Probability for N = " +
               N + " is, " + Math.round(
               probabilityMax * 10000.0) / 10000.0 + "<br/>");

// This code is contributed by avijitmondal1998

</script>
```

**Output:** 

```
Maximum Probability for N = 1 is, 0.5000
Maximum Probability for N = 2 is, 0.6667
Maximum Probability for N = 10 is, 0.9091
```

上述程序的时间复杂度为 0(1)。
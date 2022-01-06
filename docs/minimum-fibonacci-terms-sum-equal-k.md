# 总和等于 K 的最小斐波那契项

> 原文:[https://www . geesforgeks . org/minimum-Fibonacci-terms-sum-equal-k/](https://www.geeksforgeeks.org/minimum-fibonacci-terms-sum-equal-k/)

给定一个数 k，求其和等于 k 的斐波那契项所需的最小个数，我们可以多次选择一个[斐波那契数](https://www.geeksforgeeks.org/program-for-nth-fibonacci-number/)。

**示例:**

```
Input : k = 4
Output : 2
Fibonacci term added twice that is
2 + 2 = 4\. 
Other combinations are 
1 + 1 + 2\. 
1 + 1 + 1 + 1
Among all cases first case has the 
minimum number of terms = 2.

Input : k = 17
Output : 3
```

[Recommended : Please try your approach first on IDE and then look at the solution](https://ide.geeksforgeeks.org/)

我们可以用斐波那契数得到任何和，因为 1 是斐波那契数。例如，要得到 n，我们可以 n 次加 1。这里我们需要最小化贡献总和的斐波那契数的计数。所以这个问题基本上就是[硬币兑换问题](https://www.geeksforgeeks.org/dynamic-programming-set-7-coin-change/)硬币有斐波那契值。通过举一些例子，我们可以注意到斐波那契硬币价值[贪婪方法](https://www.geeksforgeeks.org/greedy-algorithms/)的工作原理。
首先我们计算斐波那契项，直到小于或等于 k。然后从最后一项开始，继续从 k 中减去该项，直到 k >(第 n 项)。与此同时，不断增加术语的数量。

当 k < (nth Fibonacci term) move to next Fibonacci term which is less than or Equal to k. at last, print the value of count.
时，逐步算法为:

```
  1\. Find all Fibonacci Terms less than or equal to K.
  2\. Initialize count = 0.
  3\. j = Index of last calculated Fibonacci Term.
  4\. while K > 0 do:

      // Greedy step
      count += K / (fibo[j])     // Note that division 
                                 // is repeated subtraction.
      K = K % (fibo[j])
      j--;
  5\. Print count.
```

下面是上述方法的实现。

## C++

```
// C++ code to find minimum number of fibonacci
// terms that sum to K.
#include <bits/stdc++.h>
using namespace std;

// Function to calculate Fibonacci Terms
void calcFiboTerms(vector<int>& fiboTerms, int K)
{
    int i = 3, nextTerm;
    fiboTerms.push_back(0);
    fiboTerms.push_back(1);
    fiboTerms.push_back(1);

    // Calculate all Fibonacci terms
    // which are less than or equal to K.
    while (1) {
        nextTerm = fiboTerms[i - 1] + fiboTerms[i - 2];

        // If next term is greater than K
        // do not push it in vector and return.
        if (nextTerm > K)
            return;

        fiboTerms.push_back(nextTerm);
        i++;
    }
}

// Function to find the minimum number of
// Fibonacci terms having sum equal to K.
int findMinTerms(int K)
{

    // Vector to store Fibonacci terms.
    vector<int> fiboTerms;

    calcFiboTerms(fiboTerms, K);

    int count = 0, j = fiboTerms.size() - 1;

    // Subtract Fibonacci terms from sum K
    // until sum > 0.
    while (K > 0) {

        // Divide sum K by j-th Fibonacci term to find
        // how many terms it contribute in sum.
        count += (K / fiboTerms[j]);
        K %= (fiboTerms[j]);

        j--;
    }

    return count;
}

// driver code
int main()
{
    int K = 17;

    cout << findMinTerms(K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to find the minimum number of Fibonacci terms
// that sum to k.
import java.util.*;

class GFG
{
    // Function to calculate Fibonacci Terms
    public static void calcFiboTerms(ArrayList<Integer> fiboterms,
                                                            int k)
    {
        int i = 3, nextTerm = 0;

        fiboterms.add(0);
        fiboterms.add(1);
        fiboterms.add(1);

        // Calculate all Fibonacci terms
        // which are less than or equal to k.
        while(true)
        {
            nextTerm = fiboterms.get(i - 1) + fiboterms.get(i - 2);

            // If next term is greater than k
            // do not add in arraylist and return.
            if(nextTerm>k)
            return;

            fiboterms.add(nextTerm);
            i++;
        }
    }

    // Function to find the minimum number of
    // Fibonacci terms having sum equal to k.
    public static int fibMinTerms(int k)
    {
        // ArrayList to store Fibonacci terms.
        ArrayList<Integer> fiboterms = new ArrayList<Integer>();
        calcFiboTerms(fiboterms,k);

        int count = 0, j = fiboterms.size() - 1;

        // Subtract Fibonacci terms from sum k
        // until sum > 0.
        while(k > 0)
        {
            // Divide sum k by j-th Fibonacci term to find
            // how many terms it contribute in sum.
            count += (k / fiboterms.get(j));
            k %= (fiboterms.get(j));

            j--;
        }
        return count;
    }

    // driver code
    public static void main (String[] args) {

        int k = 17;

        System.out.println(fibMinTerms(k));
    }
}

/* This code is contributed by Akash Singh*/
```

## 蟒蛇 3

```
# Python3 code to find minimum number
# of Fibonacci terms that sum to K.

# Function to calculate Fibonacci Terms
def calcFiboTerms(fiboTerms, K):

    i = 3
    fiboTerms.append(0)
    fiboTerms.append(1)
    fiboTerms.append(1)

    # Calculate all Fibonacci terms
    # which are less than or equal to K.
    while True:
        nextTerm = (fiboTerms[i - 1] +
                    fiboTerms[i - 2])

        # If next term is greater than K
        # do not push it in vector and return.
        if nextTerm > K:
            return

        fiboTerms.append(nextTerm)
        i += 1

# Function to find the minimum number of
# Fibonacci terms having sum equal to K.
def findMinTerms(K):

    # Vector to store Fibonacci terms.
    fiboTerms = []
    calcFiboTerms(fiboTerms, K)

    count, j = 0, len(fiboTerms) - 1

    # Subtract Fibonacci terms from
    # sum K until sum > 0.
    while K > 0:

        # Divide sum K by j-th Fibonacci
        # term to find how many terms it
        # contribute in sum.
        count += K // fiboTerms[j]
        K %= fiboTerms[j]

        j -= 1

    return count

# Driver code
if __name__ == "__main__":

    K = 17
    print(findMinTerms(K))

# This code is contributed
# by Rituraj Jain
```

## C#

```
// C# code to find the minimum number
// of Fibonacci terms that sum to k.
using System;
using System.Collections.Generic;

class GFG
{
// Function to calculate Fibonacci Terms
public static void calcFiboTerms(List<int> fiboterms,
                                      int k)
{
    int i = 3, nextTerm = 0;

    fiboterms.Add(0);
    fiboterms.Add(1);
    fiboterms.Add(1);

    // Calculate all Fibonacci terms
    // which are less than or equal to k.
    while(true)
    {
        nextTerm = fiboterms[i - 1] +
                   fiboterms[i - 2];

        // If next term is greater than k
        // do not add in arraylist and return.
        if(nextTerm > k)
            return;

        fiboterms.Add(nextTerm);
        i++;
    }
}

// Function to find the minimum number of
// Fibonacci terms having sum equal to k.
public static int fibMinTerms(int k)
{
    // List to store Fibonacci terms.
    List<int> fiboterms = new List<int>();
    calcFiboTerms(fiboterms, k);

    int count = 0, j = fiboterms.Count - 1;

    // Subtract Fibonacci terms from sum k
    // until sum > 0.
    while(k > 0)
    {
        // Divide sum k by j-th Fibonacci term to find
        // how many terms it contribute in sum.
        count += (k / fiboterms[j]);
        k %= (fiboterms[j]);

        j--;
    }
    return count;
}

// Driver Code
public static void Main (String[] args)
{
    int k = 17;

    Console.WriteLine(fibMinTerms(k));
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// Javascript code to find minimum
// number of fibonacci terms that
// sum to K.

// Function to calculate Fibonacci Terms
function calcFiboTerms(fiboTerms, K)
{
    var i = 3, nextTerm;
    fiboTerms.push(0);
    fiboTerms.push(1);
    fiboTerms.push(1);

    // Calculate all Fibonacci terms
    // which are less than or equal to K.
    while (1)
    {
        nextTerm = fiboTerms[i - 1] +
                   fiboTerms[i - 2];

        // If next term is greater than K
        // do not push it in vector and return.
        if (nextTerm > K)
            return;

        fiboTerms.push(nextTerm);
        i++;
    }
}

// Function to find the minimum number of
// Fibonacci terms having sum equal to K.
function findMinTerms(K)
{

    // Vector to store Fibonacci terms.
    var fiboTerms = [];

    calcFiboTerms(fiboTerms, K);

    var count = 0;
    var j = fiboTerms.length - 1;

    // Subtract Fibonacci terms from sum K
    // until sum > 0.
    while (K > 0)
    {

        // Divide sum K by j-th Fibonacci
        // term to find how many terms it
        // contribute in sum.
        count += parseInt(K / fiboTerms[j]);
        K %= (fiboTerms[j]);

        j--;
    }
    return count;
}

// Driver code
var K = 17;

document.write(findMinTerms(K));  

// This code is contributed by SoumikMondal

</script>
```

**Output:** 

```
3
```
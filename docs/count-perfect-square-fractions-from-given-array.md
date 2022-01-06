# 计算给定数组的完美平方分数

> 原文:[https://www . geeksforgeeks . org/count-perfect-square-fractions-from-给定-array/](https://www.geeksforgeeks.org/count-perfect-square-fractions-from-given-array/)

给定两个长度为 **N** 的[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr 1【】**和**arr 2【】**，分别包含 **N** 分数的分子和分母，任务是计算数组中分数的数量，该数组是分数的[完美平方。](https://www.geeksforgeeks.org/perfect-square-factors-of-a-number/)

**示例:**

> **输入:** arr1[] = {3，25，49，9}，arr2[] = {27，64，7，3}
> **输出:** 2
> **解释:**
> (arr 1[0]/arr 2[0])=(3/27)=(1/9)=(1/3)<sup>2</sup>
> (arr 1[1]/arr 2[1])=(25/64)=(5)因此，所需的输出为 2。
> 
> **输入:** arr1[] = {1，11，3，9}，arr2[] = {9，11，5，1 }
> T3】输出: 3

**方法:**按照以下步骤解决问题:

*   初始化一个变量 **cntPerfNum** 来存储完美平方分数的计数。
*   [遍历两个数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)并针对每个数组元素，检查**(arr 1[I]/**[**GCD(arr 1[I]、arr2[i])**](https://www.geeksforgeeks.org/c-program-find-gcd-hcf-two-numbers/) **)** 和**(arr 2[I]/**[**GCD(arr 1[I]、arr2[i])**](https://www.geeksforgeeks.org/c-program-find-gcd-hcf-two-numbers/) **)** 的值是否为[完美正方形](https://www.geeksforgeeks.org/check-if-given-number-is-perfect-square-in-cpp/)[如果发现为真，则将**cntpernum**的值增加 **1** 。](https://www.geeksforgeeks.org/c-program-find-gcd-hcf-two-numbers/)
*   最后，打印**cntpernum**的值。

下面是上述方法的实现:

## C++

```
// C++ implementation of the
// above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the GCD
// of two numbers
int GCD(int a,int b)
{
    // If b is 0
    if (b ==0 ) {
      return a;
    }
    return GCD(b,a%b);
}

// Function to check if N
// is perfect square
bool isPerfectSq(int N)
{
   // Stores square root
   // of N
   int x = sqrt(N);

   // Check if N is a
   // perfect square
   if (x * x == N) {
       return 1;
   }

   return 0;
}

// Function to count perfect square fractions
int cntPerSquNum(int arr1[], int arr2[],
                                  int N)
{
    // Stores count of perfect square
    // fractions in both arrays
    int cntPerfNum = 0;

    // Traverse both the arrays
    for (int i = 0; i < N; i++) {

        // Stores gcd of (arr1[i], arr2[i])
        int gcd = GCD(arr1[i], arr2[i]);

        // If numerator and denomerator of a
        // reduced fraction is a perfect square
        if (isPerfectSq(arr1[i]/ gcd) &&
           isPerfectSq(arr2[i]/ gcd)) {

            // Update cntPerfNum
            cntPerfNum++;      
        }

    }

    return cntPerfNum;
}

//Driver Code
int main() {

    int arr1[]={ 3, 25, 49, 9 };
    int arr2[]={ 27, 64, 7, 3 };

    int N = sizeof(arr1) / sizeof(arr1[0]);

    cout<<cntPerSquNum(arr1, arr2, N);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the
// above approach
import java.lang.Math;

class GFG{

// Function to find the GCD
// of two numbers
public static int GCD(int a, int b)
{

    // If b is 0
    if (b == 0)
    {
      return a;
    }
    return GCD(b, a % b);
}

// Function to check if N
// is perfect square
public static boolean isPerfectSq(int N)
{

    // Stores square root
    // of N 
    int x = (int)Math.sqrt(N);

    // Check if N is a 
    // perfect square
    if (x * x == N)
    {
        return true;
    }

    return false;
}

// Function to count perfect square fractions
public static int cntPerSquNum(int arr1[],
                               int arr2[], 
                               int N)
{

    // Stores count of perfect square
    // fractions in both arrays
    int cntPerfNum = 0;

    // Traverse both the arrays
    for(int i = 0; i < N; i++)
    {

        // Stores gcd of (arr1[i], arr2[i])
        int gcd = GCD(arr1[i], arr2[i]);

        // If numerator and denomerator of a
        // reduced fraction is a perfect square
        if (isPerfectSq(arr1[i] / gcd) &&
            isPerfectSq(arr2[i] / gcd))
        {

            // Update cntPerfNum
            cntPerfNum++;       
        }
    }

    return cntPerfNum;
}

// Driver code
public static void main(String[] args)
{
    int arr1[] = { 3, 25, 49, 9 };
    int arr2[] = { 27, 64, 7, 3 };

    int N = arr1.length;

    System.out.println(cntPerSquNum(arr1, arr2, N));
}
}

// This code is contributed by divyeshrabadiya07
```

## 蟒蛇 3

```
# Python3 implementation of the
# above approach

# Function to find the GCD
# of two numbers
def GCD(a, b):

    # If b is 0
    if (b == 0):
        return a

    return GCD(b, a % b)

# Function to check if N
# is perfect square
def isPerfectSq(N):

    # Stores square root
    # of N
    x = (int)(pow(N, 1 / 2))

    # Check if N is a
    # perfect square
    if (x * x == N):
        return True

    return False

# Function to count perfect square
# fractions
def cntPerSquNum(arr1, arr2, N):

    # Stores count of perfect square
    # fractions in both arrays
    cntPerfNum = 0

    # Traverse both the arrays
    for i in range(N):

        # Stores gcd of (arr1[i], arr2[i])
        gcd = GCD(arr1[i], arr2[i])

        # If numerator and denomerator of a
        # reduced fraction is a perfect square
        if (isPerfectSq(arr1[i] / gcd) and
            isPerfectSq(arr2[i] / gcd)):

            # Update cntPerfNum
            cntPerfNum += 1

    return cntPerfNum

# Driver code
if __name__ == '__main__':

    arr1 = [ 3, 25, 49, 9 ]
    arr2 = [ 27, 64, 7, 3 ]

    N = len(arr1)

    print(cntPerSquNum(arr1, arr2, N))

# This code is contributed by Princi Singh
```

## C#

```
// C# implementation of the
// above approach
using System;
class GFG{

// Function to find the GCD
// of two numbers
public static int GCD(int a,
                      int b)
{    
  // If b is 0
  if (b == 0)
  {
    return a;
  }
  return GCD(b, a % b);
}

// Function to check if N
// is perfect square
public static bool isPerfectSq(int N)
{
  // Stores square root
  // of N 
  int x = (int)Math.Sqrt(N);

  // Check if N is a 
  // perfect square
  if (x * x == N)
  {
    return true;
  }

  return false;
}

// Function to count perfect
// square fractions
public static int cntPerSquNum(int []arr1,
                               int []arr2, 
                               int N)
{    
  // Stores count of perfect square
  // fractions in both arrays
  int cntPerfNum = 0;

  // Traverse both the arrays
  for(int i = 0; i < N; i++)
  {
    // Stores gcd of (arr1[i], arr2[i])
    int gcd = GCD(arr1[i], arr2[i]);

    // If numerator and denomerator
    // of a reduced fraction is a
    // perfect square
    if (isPerfectSq(arr1[i] / gcd) &&
        isPerfectSq(arr2[i] / gcd))
    {
      // Update cntPerfNum
      cntPerfNum++;       
    }
  }

  return cntPerfNum;
}

// Driver code
public static void Main(String[] args)
{
  int []arr1 = {3, 25, 49, 9};
  int []arr2 = {27, 64, 7, 3};
  int N = arr1.Length;
  Console.WriteLine(cntPerSquNum(arr1,
                                 arr2, N));
}
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>

// Function to find the GCD
// of two numbers
function GCD(a,b)
{
    // If b is 0
    if (b ==0 ) {
      return a;
    }
    return GCD(b,a%b);
}

// Function to check if N
// is perfect square
function isPerfectSq( N)
{
   // Stores square root
   // of N
  var x = Math.sqrt(N);

   // Check if N is a
   // perfect square
   if (x * x == N) {
       return 1;
   }

   return 0;
}

// Function to count perfect square fractions
function cntPerSquNum(arr1,arr2,N)
{

    // Stores count of perfect square
    // fractions in both arrays
    var cntPerfNum = 0;

    // Traverse both the arrays
    for (var i = 0; i < N; i++) {

        // Stores gcd of (arr1[i], arr2[i])
        var gcd = GCD(arr1[i], arr2[i]);

        // If numerator and denomerator of a
        // reduced fraction is a perfect square
        if (isPerfectSq(arr1[i]/ gcd) &&
           isPerfectSq(arr2[i]/ gcd)) {

            // Update cntPerfNum
            cntPerfNum++;      
        }

    }   
    return cntPerfNum;
}

var arr1 = [ 3, 25, 49, 9 ];
    var arr2 = [ 27, 64, 7, 3 ]; 
    var N = 4;
    document.write(cntPerSquNum(arr1, arr2, N));

// This code is contributed by akshitsaxenaa09.
</script>
```

**Output:** 

```
2
```

***时间复杂度:** O(N * log(M))，其中 M 是两个数组的最大元素。*
***辅助空间:** O(1)*
# 统计元素顺序递增且乘积小于等于整数 X 的无序三元组数量

> 原文:[https://www . geeksforgeeks . org/count-带有递增顺序元素的无序三元组的数量和小于或等于整数的乘积-x/](https://www.geeksforgeeks.org/count-the-number-of-unordered-triplets-with-elements-in-increasing-order-and-product-less-than-or-equal-to-integer-x/)

给定一个**数组 A[]和一个整数 X** 。求无序三元组(I，j，k)的个数，使得 A[i] < A[j] < A[k]和 A[i] * A[j] * A[k] < = X

**示例:**

> **输入:**A =【3，2，5，7】，X = 42
> **输出:** 2
> **说明:**
> 三胞胎是:
> 
> *   (1, 0, 2) => 2 < 3 < 5, 2 * 3 * 5 < = 42
> *   (1, 0, 3) => 2 < 3 < 7, 2 * 3 * 7 < = 42
> 
> **输入:** A = [3，1，2，56，21，8]，X = 49
> T3】输出: 5

**天真方法:**
解决上述问题的天真方法是遍历所有的三元组。对于每个三元组，以升序排列它们(因为我们必须计算无序的三元组，因此允许重新排列它们)，并检查给定的条件。但是这个方法需要 O(N <sup>3</sup> 时间。

下面是上述方法的实现:

## C++

```
// C++ implementation to Count the number of
// unordered triplets such that the numbers are
// in increasing order and the product of them is
// less than or equal to integer X
#include <bits/stdc++.h>
using namespace std;

// Function to count the number of triplets
int countTriplets(int a[], int n, int x)
{
    int answer = 0;

    // Iterate through all the triplets
    for (int i = 0; i < n; i++) {
        for (int j = i + 1; j < n; j++) {
            for (int k = j + 1; k < n; k++) {
                vector<int> temp;
                temp.push_back(a[i]);
                temp.push_back(a[j]);
                temp.push_back(a[k]);

                // Rearrange the numbers in ascending order
                sort(temp.begin(), temp.end());

                // Check if the necessary conditions satisfy
                if (temp[0] < temp[1] && temp[1] < temp[2]
                    && temp[0] * temp[1] * temp[2] <= x)

                    // Increment count
                    answer++;
            }
        }
    }

    // Return the answer
    return answer;
}

// Driver code
int main()
{

    int A[] = { 3, 2, 5, 7 };

    int N = sizeof(A) / sizeof(A[0]);

    int X = 42;

    cout << countTriplets(A, N, X);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to count the number of
// unordered triplets such that the numbers are
// in increasing order and the product of them
// is less than or equal to integer X
import java.util.*;

class GFG{

// Function to count the number of triplets
static int countTriplets(int a[], int n, int x)
{
    int answer = 0;

    // Iterate through all the triplets
    for(int i = 0; i < n; i++)
    {
       for(int j = i + 1; j < n; j++)
       {
          for(int k = j + 1; k < n; k++)
          {
              Vector<Integer> temp = new Vector<>();
              temp.add(a[i]);
              temp.add(a[j]);
              temp.add(a[k]);

              // Rearrange the numbers in
              // ascending order
              Collections.sort(temp);

              // Check if the necessary conditions
              // satisfy
              if (temp.get(0) < temp.get(1) &&
                  temp.get(1) < temp.get(2) &&
                  temp.get(0) * temp.get(1) *
                  temp.get(2) <= x)

                  // Increment count
                  answer++;
          }
       }
    }

    // Return the answer
    return answer;
}

// Driver code
public static void main(String[] args)
{
    int A[] = { 3, 2, 5, 7 };
    int N = A.length;
    int X = 42;

    System.out.println(countTriplets(A, N, X));
}
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python3 implementation to count the number of
# unordered triplets such that the numbers are
# in increasing order and the product of them is
# less than or equal to integer X

# Function to count the number of triplets
def countTriplets(a, n, x):

    answer = 0

    # Iterate through all the triplets
    for i in range(n):
        for j in range(i + 1, n):
            for k in range(j + 1, n):
                temp = []
                temp.append(a[i])
                temp.append(a[j])
                temp.append(a[k])

                # Rearrange the numbers in
                # ascending order
                temp.sort()

                # Check if the necessary
                # conditions satisfy
                if (temp[0] < temp[1] and
                    temp[1] < temp[2] and
                    temp[0] * temp[1] * temp[2] <= x):

                    # Increment count
                    answer += 1

    # Return the answer               
    return answer

# Driver code
A = [ 3, 2, 5, 7 ]
N = len(A)
X = 42

print(countTriplets(A, N, X))

# This code is contributed by shubhamsingh10
```

## C#

```
// C# implementation to count the number of
// unordered triplets such that the numbers are
// in increasing order and the product of them
// is less than or equal to integer X
using System;

class GFG{

// Function to count the number of triplets
static int countTriplets(int []a, int n, int x)
{
    int answer = 0;

    // Iterate through all the triplets
    for(int i = 0; i < n; i++)
    {
        for(int j = i + 1; j < n; j++)
        {
            for(int k = j + 1; k < n; k++)
            {
                int []temp = { a[i], a[j], a[k] };

                // Rearrange the numbers in
                // ascending order
                Array.Sort(temp);

                // Check if the necessary conditions
                // satisfy
                if (temp[0] < temp[1] &&
                    temp[1] < temp[2] &&
                    temp[0] * temp[1] *
                    temp[2] <= x)

                    // Increment count
                    answer++;
            }
        }
    }

    // Return the answer
    return answer;
}

// Driver code
public static void Main()
{
    int []A = { 3, 2, 5, 7 };
    int N = A.Length;
    int X = 42;

    Console.WriteLine(countTriplets(A, N, X));
}
}

// This code is contributed by Stream_Cipher    
```

## java 描述语言

```
<script>

// JavaScript implementation to Count the number of
// unordered triplets such that the numbers are
// in increasing order and the product of them is
// less than or equal to integer X

// Function to count the number of triplets
function countTriplets(a, n, x)
{
    var answer = 0;

    // Iterate through all the triplets
    for (var i = 0; i < n; i++) {
        for (var j = i + 1; j < n; j++) {
            for (var k = j + 1; k < n; k++) {
                var temp = [];
                temp.push(a[i]);
                temp.push(a[j]);
                temp.push(a[k]);

                // Rearrange the numbers in ascending order
                temp.sort((a,b)=>a-b)

                // Check if the necessary conditions satisfy
                if (temp[0] < temp[1] && temp[1] < temp[2]
                    && temp[0] * temp[1] * temp[2] <= x)

                    // Increment count
                    answer++;
            }
        }
    }

    // Return the answer
    return answer;
}

// Driver code
var A = [3, 2, 5, 7];
var N = A.length;
var X = 42;
document.write( countTriplets(A, N, X));

</script>
```

**Output:** 

```
2
```

**时间复杂度:**O(N)
T3】辅助空间: O(1)

**有效方法:**
为了优化上面给出的方法，我们可以使用数组的排序形式，因为它不会改变答案，因为三元组是无序的。遍历排序数组中的所有元素对。对于一对(p，q)，问题现在简化为找到排序数组中的元素数 r，使得 r < = X/(p*q)。为了高效地执行此操作，我们将使用**二分搜索法**方法并找到数组中最大元素的位置，即< = X/(p*q)。q 的索引到位置之间的所有元素将被添加到答案中。

下面是上述方法的实现:

## C++

```
// C++ implementation to Count the number of
// unordered triplets such that the numbers are
// in increasing order and the product of them is
// less than or equal to integer X
#include <bits/stdc++.h>
using namespace std;

// Function to count the triplets
int countTriplets(int a[], int n, int x)
{
    int answer = 0;

    // Sort the array
    sort(a, a + n);

    // Iterate through all the triplets
    for (int i = 0; i < n; i++) {
        for (int j = i + 1; j < n; j++) {

            // Apply Binary Search method
            long long limit = (long long)x / a[i];

            limit = limit / a[j];

            int pos = upper_bound(a, a + n, limit) - a;

            // Check if the position is greater than j
            if (pos > j)
                answer = answer + (pos - j - 1);
        }
    }

    // Return the answer
    return answer;
}

// Driver code
int main()
{

    int A[] = { 3, 2, 5, 7 };

    int N = sizeof(A) / sizeof(A[0]);

    int X = 42;

    cout << countTriplets(A, N, X);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to count the number
// of unordered triplets such that the
// numbers are in increasing order and
// the product of them is less than or
// equal to integer X
import java.io.*;
import java.util.Arrays;

class GFG{

// Function to count the triplets
static int countTriplets(int a[], int n, int x)
{
    int answer = 0;

    // Sort the array
    Arrays.sort(a);

    // Iterate through all the triplets
    for(int i = 0; i < n; i++)
    {
        for(int j = i + 1; j < n; j++)
        {

            // Apply Binary Search method
            int limit = x / a[i];

            limit = limit / a[j];

            int pos = Arrays.binarySearch(a, limit) + 1;

            // Check if the position is greater than j
            if (pos > j)
                answer = answer + (pos - j - 1);
        }
    }

    // Return the answer
    return answer;
}

// Driver Code
public static void main (String[] args)
{
    int A[] = { 3, 2, 5, 7 };
    int N = A.length;
    int X = 42;

    System.out.print(countTriplets(A, N, X));
}
}

// This code is contributed by math_lover
```

## 蟒蛇 3

```
# Python3 implementation to Count the number of
# unordered triplets such that the numbers are
# in increasing order and the product of them is
# less than or equal to integer X
import bisect

# Function to count the triplets
def countTriplets(a, n, x):

    answer = 0

    # Sort the array
    a.sort()

    # Iterate through all the triplets
    for i in range(n):
        for j in range(i + 1, n):

            # Apply Binary Search method
            limit = x / a[i]

            limit = limit / a[j]

            pos = bisect.bisect_right(a, limit)

            # Check if the position is greater than j
            if (pos > j):
                answer = answer + (pos - j - 1)

    # Return the answer
    return answer

# Driver code
A = [3, 2, 5, 7]

N = len(A)

X = 42

print(countTriplets(A, N, X))

# This code is contributed by shubhamsingh10
```

## C#

```
// C# implementation to Count the number
// of unordered triplets such that the
// numbers are in increasing order and
// the product of them is less than or
// equal to integer X
using System;

class GFG{

// Function to count the triplets
static int countTriplets(int []a, int n, int x)
{
    int answer = 0;

    // Sort the array
    Array.Sort(a);

    // Iterate through all the triplets
    for(int i = 0; i < n; i++)
    {
        for(int j = i + 1; j < n; j++)
        {

            // Apply Binary Search method
            int limit = x / a[i];

            limit = limit / a[j];

            int pos = Array.BinarySearch(a, limit) + 1;

            // Check if the position is greater than j
            if (pos > j)
                answer = answer + (pos - j - 1);
        }
    }

    // Return the answer
    return answer;
}

// Driver Code
public static void Main (String[] args)
{
    int []A = { 3, 2, 5, 7 };
    int N = A.Length;
    int X = 42;

    Console.Write(countTriplets(A, N, X));
}
}

// This code is contributed by math_lover
```

## java 描述语言

```
<script>

// Javascript implementation to Count the number of
// unordered triplets such that the numbers are
// in increasing order and the product of them is
// less than or equal to integer X

// Function to count the triplets
function countTriplets(a, n, x)
{
    var answer = 0;

    // Sort the array
    a.sort((a, b) => a - b)

    // Iterate through all the triplets
    for(var i = 0; i < n; i++)
    {
        for(var j = i + 1; j < n; j++)
        {

            // Apply Binary Search method
            var limit = parseInt(x / a[i]);

            limit = parseInt(limit / a[j]);

            var pos = 0;

            for(var k = a.length - 1; k >= 0; k--)
            {
                if(a[k] == limit)
                {
                    pos = k;
                    break;
                }
            }
            pos += 1

            // Check if the position is greater than j
            if (pos > j)
                answer = answer + (pos - j - 1);
        }
    }

    // Return the answer
    return answer;
}

// Driver code
var A = [ 3, 2, 5, 7 ];
var N = A.length;
var X = 42;

document.write(countTriplets(A, N, X));

// This code is contributed by itsok

</script>
```

**Output:** 

```
2
```

**时间复杂度:**O(N<sup>2</sup>* log(N)
T5】辅助空间: O(1)
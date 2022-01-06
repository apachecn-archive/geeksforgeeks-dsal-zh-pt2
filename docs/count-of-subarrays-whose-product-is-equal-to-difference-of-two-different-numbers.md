# 乘积等于两个不同数之差的子阵的计数

> 原文:[https://www . geesforgeks . org/子阵列计数-其乘积等于两个不同数字的差值/](https://www.geeksforgeeks.org/count-of-subarrays-whose-product-is-equal-to-difference-of-two-different-numbers/)

给定一个**非负数组 a** ，任务是找出子阵的个数，子阵的元素乘积可以表示为两个不同数的差。
**例:**

> **输入:** arr = {2，5，6}
> **输出:** 2
> **说明:**
> 子阵列{5}的元素积可以表示为 3<sup>2</sup>–2<sup>2</sup>等于 5
> 子阵列{2，5，6}的元素积可以表示为 8<sup>2</sup>–2<sup>2</sup>等于 60
> **输入:** arr = {1，2，3}
> **输出:** 2

**天真方法:**
上述问题的天真解决方案是从给定阵列计算所有可能的子阵列。然后我们要计算每个子阵列的乘积。但是这种方法效率不高，而且耗时。
**有效方法:**
对上述问题的有效方法的一个常见观察是，一个可被 2 整除但不能被 4 整除的数被 4 整除时会得到余数 2。因此，所有的数都可以表示为两个不同数的乘积，除了当用 4 取模时给出余数 2 的数。现在为了解决这个问题，我们取一对向量，存储元素以及下一个可被 2 整除的元素的位置。之后，遍历数组并寻找下面给出的必要条件:

*   如果遇到一个奇数，那么这个数形成所有的子阵列，除非出现一个可被 2 整除的数。现在，当另一个可被 2 整除的数出现时，这个数也可以形成子阵。这两者都存储在成对类型向量中。
*   如果遇到一个能被 4 整除的数，那么这个数可以构成所有的子阵。
*   如果出现一个只能被 2 整除的数，那么这个数不能形成子阵列，除非出现另一个是 2 的倍数的数。

以下是上述方法的实现:

## C++

```
// C++ program to Find count of
// Subarrays whose product can be
// represented as the difference between
// two different numbers

#include <bits/stdc++.h>
using namespace std;

// Function to print number of subarrays
void numberOfSubarrays(int arr[], int n)
{

    vector<pair<int, int> > next(n);
    vector<pair<int, int> > next_to_next(n);

    int f = -1;
    int s = -1;

    for (int i = n - 1; i >= 0; i--) {
        next[i].first = arr[i];

        next_to_next[i].first = arr[i];

        // check if number is divisible by 2
        if (arr[i] % 2 == 0) {
            s = f;
            f = i;
        }

        // Store the position
        // of the next element
        next[i].second = f;

        // Store the position of
        // next to next element
        // which is multiple of 2
        next_to_next[i].second = s;
    }

    int total = 0;

    for (int i = 0; i < n; i++) {
        int calculate;

        // Check if the element is divisible
        // is divisible by 4
        if (next[i].first % 4 == 0) {
            calculate = n - i;

            total += calculate;
        }

        // Check if current element
        // is an odd number
        else if (next[i].first & 1 == 1) {

            if (next[i].second == -1) {
                calculate = n - i;

                total += calculate;
            }

            else {

                // check if after the current element
                // only 1 element exist which is a
                // multiple of only 2 but not 4
                if (next_to_next[i].second == -1
                 && next[next[i].second].first % 4 != 0)

                {
                    calculate = next[i].second - i;
                    total += calculate;
                }

                // Check if after the current element an element exist
                // which is multiple of only 2 and not 4 and after that
                // an element also exist which is multiple of 2
                else if (next_to_next[i].second != -1
                         && next[next[i].second].first % 4 != 0) {
                    calculate = n - i;
                    total += calculate;
                    total -= next_to_next[i].second - next[i].second;
                }

                // All subarrays can be formed by current element
                else {
                    calculate = n - i;
                    total = total + calculate;
                }
            }
        }

        // Condition for an even number
        else {

            // Check if next element does not
            // exist which is multiple of 2
            if (next_to_next[i].second == -1)
                total = total;

            // Check if next element exist
            // which is multiple of 2
            else {
                calculate = n - i;
                total += calculate;
                total = total - next_to_next[i].second + i;
            }
        }
    }

    // Print the output
    cout << total << "\n";
}

// Driver Code
int main()
{
    // array initialisation
    int arr[] = { 2, 5, 6 };

    int size = sizeof(arr) / sizeof(arr[0]);

    numberOfSubarrays(arr, size);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find count of
// subarrays whose product can be
// represented as the difference
// between two different numbers
import java.io.*;
import java.util.*;

class GFG{

// Function to print number of subarrays
static void numberOfSubarrays(int arr[], int n)
{
    int[][] next = new int[n][2];
    int[][] next_to_next = new int[n][2];

    int f = -1;
    int s = -1;

    for(int i = n - 1; i >= 0; i--)
    {
        next[i][0] = arr[i];

        next_to_next[i][0] = arr[i];

        // Check if number is divisible by 2
        if (arr[i] % 2 == 0)
        {
            s = f;
            f = i;
        }

        // Store the position
        // of the next element
        next[i][1] = f;

        // Store the position of
        // next to next element
        // which is multiple of 2
        next_to_next[i][1] = s;
    }

    int total = 0;

    for(int i = 0; i < n; i++)
    {
        int calculate;

        // Check if the element is divisible
        // is divisible by 4
        if (next[i][0] % 4 == 0)
        {
            calculate = n - i;
            total += calculate;
        }

        // Check if current element
        // is an odd number
        else if ((next[i][0] & 1) == 1)
        {
            if (next[i][1] == -1)
            {
                calculate = n - i;
                total += calculate;
            }

            else
            {

                // Check if after the current element
                // only 1 element exist which is a
                // multiple of only 2 but not 4
                if (next_to_next[i][1] == -1 &&
                    next[next[i][1]][0] % 4 != 0)
                {
                    calculate = next[i][1] - i;
                    total += calculate;
                }

                // Check if after the current element
                // an element exist which is multiple
                // of only 2 and not 4 and after that
                // an element also exist which is
                // multiple of 2
                else if (next_to_next[i][1] != -1 &&
                         next[next[i][1]][0] % 4 != 0)
                {
                    calculate = n - i;
                    total += calculate;
                    total -= next_to_next[i][1] -
                                     next[i][1];
                }

                // All subarrays can be formed
                // by current element
                else
                {
                    calculate = n - i;
                    total = total + calculate;
                }
            }
        }

        // Condition for an even number
        else
        {

            // Check if next element does not
            // exist which is multiple of 2
            if (next_to_next[i][1] == -1)
                total = total;

            // Check if next element exist
            // which is multiple of 2
            else
            {
                calculate = n - i;
                total += calculate;
                total = total - next_to_next[i][1] + i;
            }
        }
    }

    // Print the output
    System.out.println(total);
}

// Driver Code
public static void main(String args[])
{

    // Array initialisation
    int arr[] = { 2, 5, 6 };

    int size = arr.length;

    numberOfSubarrays(arr, size);
}
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python program to find count of
# subarrays whose product can be
# represented as the difference
# between two different numbers

# Function to print number of subarrays
def numberOfSubarrays(arr, n):

    Next = [[0 for i in range(2)] for j in range(n)]
    next_to_next = [[0 for i in range(2)] for j in range(n)]

    f = -1
    s = -1

    for i in range(n - 1, -1, -1) :

        Next[i][0] = arr[i]

        next_to_next[i][0] = arr[i]

        # Check if number is divisible by 2
        if (arr[i] % 2 == 0) :

            s = f
            f = i

        # Store the position
        # of the next element
        Next[i][1] = f

        # Store the position of
        # next to next element
        # which is multiple of 2
        next_to_next[i][1] = s

    total = 0

    for i in range(n) :

        calculate = 0

        # Check if the element is divisible
        # is divisible by 4
        if (Next[i][0] % 4 == 0) :

            calculate = n - i
            total += calculate

        # Check if current element
        # is an odd number
        elif ((Next[i][0] & 1) == 1) :

            if (Next[i][1] == -1) :

                calculate = n - i
                total += calculate

            else :

                # Check if after the current element
                # only 1 element exist which is a
                # multiple of only 2 but not 4
                if (next_to_next[i][1] == -1 and Next[Next[i][1]][0] % 4 != 0) :

                    calculate = Next[i][1] - i
                    total += calculate

                # Check if after the current element
                # an element exist which is multiple
                # of only 2 and not 4 and after that
                # an element also exist which is
                # multiple of 2
                elif (next_to_next[i][1] != -1 and Next[Next[i][1]][0] % 4 != 0) :

                    calculate = n - i
                    total += calculate
                    total -= next_to_next[i][1] - Next[i][1]

                # All subarrays can be formed
                # by current element
                else :

                    calculate = n - i
                    total = total + calculate

        # Condition for an even number
        else :

            # Check if next element does not
            # exist which is multiple of 2
            if (next_to_next[i][1] == -1) :
                total = total

            # Check if next element exist
            # which is multiple of 2
            else :

                calculate = n - i
                total += calculate
                total = total - next_to_next[i][1] + i

    # Print the output
    print(total)

# Array initialisation
arr = [ 2, 5, 6 ]

size = len(arr)

numberOfSubarrays(arr, size)

# This code is contributed by divyesh072019
```

## C#

```
// C# program to find count of 
// subarrays whose product can be 
// represented as the difference 
// between two different numbers 
using System;
class GFG{

// Function to print number
// of subarrays 
static void numberOfSubarrays(int[] arr,
                              int n) 
{ 
  int[,] next = new int[n, 2]; 
  int[,] next_to_next = new int[n, 2];
  int f = -1; 
  int s = -1; 

  for(int i = n - 1; i >= 0; i--)
  { 
    next[i, 0] = arr[i]; 
    next_to_next[i, 0] = arr[i]; 

    // Check if number is
    // divisible by 2 
    if (arr[i] % 2 == 0)
    { 
      s = f; 
      f = i; 
    } 

    // Store the position 
    // of the next element 
    next[i, 1] = f; 

    // Store the position of 
    // next to next element 
    // which is multiple of 2 
    next_to_next[i, 1] = s; 
  } 

  int total = 0; 

  for(int i = 0; i < n; i++)
  { 
    int calculate; 

    // Check if the element is
    // divisible is divisible by 4 
    if (next[i, 0] % 4 == 0) 
    { 
      calculate = n - i; 
      total += calculate; 
    } 

    // Check if current element 
    // is an odd number 
    else if ((next[i, 0] & 1) == 1)
    { 
      if (next[i, 1] == -1) 
      { 
        calculate = n - i; 
        total += calculate; 
      } 
      else
      {
        // Check if after the current element 
        // only 1 element exist which is a 
        // multiple of only 2 but not 4 
        if (next_to_next[i, 1] == -1 && 
            next[next[i, 1], 0] % 4 != 0) 
        { 
          calculate = next[i, 1] - i; 
          total += calculate; 
        } 

        // Check if after the current element
        // an element exist which is multiple
        // of only 2 and not 4 and after that 
        // an element also exist which is 
        // multiple of 2 
        else if (next_to_next[i, 1] != -1 &&
                 next[next[i, 1], 0] % 4 != 0)
        { 
          calculate = n - i; 
          total += calculate; 
          total -= next_to_next[i, 1] - 
            next[i, 1]; 
        } 

        // All subarrays can be formed
        // by current element 
        else
        { 
          calculate = n - i; 
          total = total + calculate; 
        } 
      } 
    } 

    // Condition for an even number 
    else
    { 
      // Check if next element does not 
      // exist which is multiple of 2 
      if (next_to_next[i, 1] == -1)
      {
        //total = total;
      }

      // Check if next element exist 
      // which is multiple of 2 
      else
      { 
        calculate = n - i; 
        total += calculate; 
        total = total -
                next_to_next[i, 1] + i; 
      } 
    } 
  } 

  // Print the output 
  Console.WriteLine(total); 
} 

static void Main()
{

  // Array initialisation 
  int[] arr = {2, 5, 6}; 

  int size = arr.Length; 

  numberOfSubarrays(arr, size); 
}
}

// This code is contributed by divyeshrabadiya07
```

## java 描述语言

```
<script>

    // Javascript program to find count of
    // subarrays whose product can be
    // represented as the difference
    // between two different numbers

    // Function to print number of subarrays
    function numberOfSubarrays(arr, n)
    {
        let next = new Array(n);
        let next_to_next = new Array(n);

        let f = -1;
        let s = -1;

        for(let i = 0; i < n; i++)
        {
            next[i] = new Array(2);
            next_to_next[i] = new Array(2);
        }

        for(let i = n - 1; i >= 0; i--)
        {
            next[i][0] = arr[i];

            next_to_next[i][0] = arr[i];

            // Check if number is divisible by 2
            if (arr[i] % 2 == 0)
            {
                s = f;
                f = i;
            }

            // Store the position
            // of the next element
            next[i][1] = f;

            // Store the position of
            // next to next element
            // which is multiple of 2
            next_to_next[i][1] = s;
        }

        let total = 0;

        for(let i = 0; i < n; i++)
        {
            let calculate;

            // Check if the element is divisible
            // is divisible by 4
            if (next[i][0] % 4 == 0)
            {
                calculate = n - i;
                total += calculate;
            }

            // Check if current element
            // is an odd number
            else if ((next[i][0] & 1) == 1)
            {
                if (next[i][1] == -1)
                {
                    calculate = n - i;
                    total += calculate;
                }

                else
                {

                    // Check if after the current element
                    // only 1 element exist which is a
                    // multiple of only 2 but not 4
                    if (next_to_next[i][1] == -1 &&
                        next[next[i][1]][0] % 4 != 0)
                    {
                        calculate = next[i][1] - i;
                        total += calculate;
                    }

                    // Check if after the current element
                    // an element exist which is multiple
                    // of only 2 and not 4 and after that
                    // an element also exist which is
                    // multiple of 2
                    else if (next_to_next[i][1] != -1 &&
                             next[next[i][1]][0] % 4 != 0)
                    {
                        calculate = n - i;
                        total += calculate;
                        total -= next_to_next[i][1] -
                                         next[i][1];
                    }

                    // All subarrays can be formed
                    // by current element
                    else
                    {
                        calculate = n - i;
                        total = total + calculate;
                    }
                }
            }

            // Condition for an even number
            else
            {

                // Check if next element does not
                // exist which is multiple of 2
                if (next_to_next[i][1] == -1)
                    total = total;

                // Check if next element exist
                // which is multiple of 2
                else
                {
                    calculate = n - i;
                    total += calculate;
                    total = total - next_to_next[i][1] + i;
                }
            }
        }

        // Print the output
        document.write(total);
    }

    // Array initialisation
    let arr = [ 2, 5, 6 ];

    let size = arr.length;

    numberOfSubarrays(arr, size);

</script>
```

**Output:** 

```
2
```

**时间复杂度:** O(N)
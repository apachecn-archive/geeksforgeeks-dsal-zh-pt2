# 乘积为两个整数平方之差的子序列的计数

> 原文:[https://www . geesforgeks . org/子序列计数-其乘积是两个整数的平方之差/](https://www.geeksforgeeks.org/count-of-subsequences-whose-product-is-a-difference-of-square-of-two-integers/)

给定一个既包含正元素又包含负元素的包含 **N** 元素的数组 **arr[]** ，任务是找出其乘积可以表示为两个整数的平方之差的连续子序列的总数。

**示例:**

> **输入:** arr[] = {1，0，2，4，5}
> **输出:** 14
> **说明:**
> 有 14 个子序列，它们的乘积可以表示为两个整数的平方之差。
> 它们是:{1}、{0}、{4}、{5}、{1，0}、{1，0，2}、{1，0，2，4}、{1，0，2，4，5}、{0，2，4}、{0，2，4，5}、{2，4}、{2，4，5}、{4，5}
> 所有子序列的乘积可以表示为两个正方形的差。例如:
> 1->1^2–0^2
> 0->1^2–1^2
> 4->2^2–0^2
> 5->3^2–2^2
> 8->3 2–1 2……等等。
> 
> **输入:** arr[] = {-2，-7，8，9}
> **输出:** 8
> **说明:**
> 有 8 个子序列，它们的乘积可以表示为两个整数的平方之差。
> 它们是:{-7}、{8}、{9}、{-2，-7，8}、{-2，-7，8，9}、{-7，8}、{-7，8，9}、{8，9}
> 所有子序列的乘积可以表示为两个平方的差。例如:
> -7->3^2-4^2
> 8->3^2-1^2
> 9->3^2-0^2
> 112->11^2-3^2……等等。

**天真方法:**这个问题的天真方法是[生成所有连续的子序列](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)并计算其乘积，然后简单地[检查该数是否可以表示为两个正方形的差。](https://www.geeksforgeeks.org/check-whether-a-number-can-be-represented-as-difference-of-two-squares/)

下面是上述方法的实现:

## C++

```
// C++ implementation to count the
// number of contiguous subsequences
// whose product can be expressed as
// the square of difference of two integers

#include <bits/stdc++.h>
using namespace std;

// Function to count the number
// of contiguous subsequences
// whose product can be expressed
// as square of difference of two integers
int CntcontSubs(int a[], int n)
{
    int c = 0, d = 0, i, sum = 1, j;

    // Iterating through the array
    for (i = 0; i < n; i++) {

        // Check if that number can be
        // expressed as the square of
        // difference of two numbers
        if (a[i] % 2 != 0 || a[i] % 4 == 0)
            d++;

        // Variable to compute the product
        sum = a[i];

        // Finding the remaining subsequences
        for (j = i + 1; j < n; j++) {
            sum = sum * a[j];

            // Check if that number can be
            // expressed as the square of
            // difference of two numbers
            if (sum % 2 != 0 || sum % 4 == 0)
                c++;
        }
        sum = 1;
    }

    // Return the number of subsequences
    return c + d;
}

// Driver code
int main()
{
    int arr[] = { 5, 4, 2, 9, 8 };
    int n = sizeof(arr) / sizeof(arr[0]);

    cout << CntcontSubs(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to count the
// number of contiguous subsequences
// whose product can be expressed as
// the square of difference of two integers

class GFG{

// Function to count the number
// of contiguous subsequences
// whose product can be expressed
// as square of difference of two integers
static int CntcontSubs(int a[], int n)
{
    int c = 0, d = 0, i, sum = 1, j;

    // Iterating through the array
    for (i = 0; i < n; i++) {

        // Check if that number can be
        // expressed as the square of
        // difference of two numbers
        if (a[i] % 2 != 0 || a[i] % 4 == 0)
            d++;

        // Variable to compute the product
        sum = a[i];

        // Finding the remaining subsequences
        for (j = i + 1; j < n; j++) {
            sum = sum * a[j];

            // Check if that number can be
            // expressed as the square of
            // difference of two numbers
            if (sum % 2 != 0 || sum % 4 == 0)
                c++;
        }
        sum = 1;
    }

    // Return the number of subsequences
    return c + d;
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 5, 4, 2, 9, 8 };
    int n = arr.length;

    System.out.print(CntcontSubs(arr, n));

}
}

// This code contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 implementation to count the
# number of contiguous subsequences
# whose product can be expressed as
# the square of difference of two integers

# Function to count the number
# of contiguous subsequences
# whose product can be expressed
# as square of difference of two integers
def CntcontSubs(a, n):
    c = 0
    d = 0
    sum = 1

    # Iterating through the array
    for i in range(n):

        # Check if that number can be
        # expressed as the square of
        # difference of two numbers
        if (a[i] % 2 != 0 or a[i] % 4 == 0):
            d += 1

        # Variable to compute the product
        sum = a[i]

        # Finding the remaining subsequences
        for j in range(i + 1, n):
            sum = sum * a[j]

            # Check if that number can be
            # expressed as the square of
            # difference of two numbers
            if (sum % 2 != 0 or sum % 4 == 0):
                c += 1
        sum = 1

    # Return the number of subsequences
    return c + d

# Driver code
if __name__ == '__main__':
    arr=[5, 4, 2, 9, 8]
    n = len(arr)

    print(CntcontSubs(arr, n))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# implementation to count the
// number of contiguous subsequences
// whose product can be expressed as
// the square of difference of two integers
using System;

class GFG{

// Function to count the number
// of contiguous subsequences
// whose product can be expressed
// as square of difference of two integers
static int CntcontSubs(int []a, int n)
{
    int c = 0, d = 0, i, sum = 1, j;

    // Iterating through the array
    for(i = 0; i < n; i++)
    {

       // Check if that number can be
       // expressed as the square of
       // difference of two numbers
       if (a[i] % 2 != 0 || a[i] % 4 == 0)
           d++;

       // Variable to compute the product
       sum = a[i];

       // Finding the remaining subsequences
       for(j = i + 1; j < n; j++)
       {
          sum = sum * a[j];

          // Check if that number can be
          // expressed as the square of
          // difference of two numbers
          if (sum % 2 != 0 || sum % 4 == 0)
              c++;
       }
       sum = 1;
    }

    // Return the number of subsequences
    return c + d;
}

// Driver code
static void Main()
{
    int []arr = { 5, 4, 2, 9, 8 };
    int n = arr.Length;

    Console.Write(CntcontSubs(arr, n));
}
}

// This code is contributed by grand_master
```

## java 描述语言

```
<script>

// Javascript implementation to count the
// number of contiguous subsequences
// whose product can be expressed as
// the square of difference of two integers

// Function to count the number
// of contiguous subsequences
// whose product can be expressed
// as square of difference of two integers
function CntcontSubs(a, n)
{
    let c = 0, d = 0, i, sum = 1, j;

    // Iterating through the array
    for (i = 0; i < n; i++) {

        // Check if that number can be
        // expressed as the square of
        // difference of two numbers
        if (a[i] % 2 != 0 || a[i] % 4 == 0)
            d++;

        // Variable to compute the product
        sum = a[i];

        // Finding the remaining subsequences
        for (j = i + 1; j < n; j++) {
            sum = sum * a[j];

            // Check if that number can be
            // expressed as the square of
            // difference of two numbers
            if (sum % 2 != 0 || sum % 4 == 0)
                c++;
        }
        sum = 1;
    }

    // Return the number of subsequences
    return c + d;
}

// Driver code
let arr = [ 5, 4, 2, 9, 8 ];
let n = arr.length;

document.write(CntcontSubs(arr, n));

</script>
```

**Output:** 

```
13
```

**时间复杂度:** *O(N <sup>2</sup> )* 其中 N 是数组的长度。

**辅助空间:** O(1)

**有效方法:**这个想法的背后是这样一个恒等式:[如果一个数除以 4 得到的余数是 2，那么这个数就不能表示为两个平方的差。](https://www.geeksforgeeks.org/check-whether-a-number-can-be-represented-as-difference-of-two-squares/)因此，想法是找到所有产生 2 的乘积的子序列，并从该数组的所有可能子序列中减去这些子序列。连续子序列的总数可以通过公式获得: **(N * (N + 1)) / 2**

*   如果数组包含元素 0，那么包含这个元素的所有子序列的乘积变成 0。因此，所有这些子序列都可以表示为两个平方的差。
*   如果任何元素在数除以 4 时给出余数 2，[则必须避免直到最近的 2 或 0 的所有子序列](https://www.geeksforgeeks.org/find-closest-number-array/)，因为当遇到 2 时余数变成 4，当遇到 0 时余数变成 0。

**示例:**

*   让 arr[] = {6，5，13，10，4，8，14，17}。
*   当元素除以 4 时，我们计算余数。因此，{2，1，1，2，0，0，2，1}是给定数组的余数。
*   这里我们得到了指数 1，4，7 的余数 2。让我们观察第一个索引处的 2。
*   以下是余数数组{2}、{2，1}、{2，1，1}、{2，1，1，2}、{2，1，1，2}，{2，1，2，0 }……{ 2，1，1，2，0，0，2，1}的子序列。
*   子序列的乘积是{2，2，2，4，0 …0}.
*   所以我们得到从指数 1 到指数 3 的乘积为 2。因此，从索引 1 到其乘积为 2 的索引 3 的全部连续子序列是 2(即)[索引-3–索引-1]。
*   所以，很明显，我们找到元素 2 或 0 的最近索引，忽略所有子序列，直到这个索引。

下面是上述方法的实现:

## C++

```
// C++ implementation to count all the
// contiguous subsequences whose
// product is expressed as the square
// of the difference of two integers

#include <bits/stdc++.h>
using namespace std;

// Function to count all the
// contiguous subsequences whose
// product is expressed as the square
// of the difference of two integers
int CntcontSubs(int a[], int n)
{
    int prod = 1;

    // Creating vectors to store
    // the remainders and the
    // subsequences
    vector<pair<int, int> > vect;

    vect.push_back(make_pair(0, 2));

    vector<int> two, zero;

    // Iterating through the array
    for (int i = 0; i < n; i++) {

        // Finding the remainder when the
        // element is divided by 4
        a[i] = a[i] % 4;

        // Bringing all the elements in
        // the range [0, 3]
        if (a[i] < 0)
            a[i] = a[i] + 4;

        // If the remainder is 2, store
        // the index of the
        if (a[i] == 2)
            two.push_back(i + 1);

        // If the remainder is 2, store
        // the index of the
        if (a[i] == 0)
            zero.push_back(i + 1);

        if (a[i] == 0 || a[i] == 2)
            vect.push_back(make_pair(i + 1, a[i]));
    }
    vect.push_back(make_pair(n + 1, 2));

    // Finding the total number of subsequences
    int total = (n * (n + 1)) / 2;

    // If there are no numbers which
    // yield the remainder 2
    if (two.empty())
        return total;
    else {
        int sum = 0;

        int pos1 = -1, pos2 = -1, pos3 = -1;

        int sz = vect.size();

        // Iterating through the vector
        for (int i = 1; i + 1 < sz; i++) {

            // If the element is 2, find the nearest
            // 2 or 0 and find the number of
            // elements between them
            if (vect[i].second == 2) {
                sum += (vect[i].first
                        - vect[i - 1].first)
                           * (vect[i + 1].first
                              - vect[i].first)
                       - 1;
            }
        }

        // Returning the count
        return total - sum - two.size();
    }
}

// Driver code
int main()
{
    int a[] = { 5, 4, 2, 9, 8 };
    int n = sizeof(a) / sizeof(a[0]);

    cout << CntcontSubs(a, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to count all the
// contiguous subsequences whose
// product is expressed as the square
// of the difference of two integers
import java.util.*;
class GFG{
static class pair
{
      int first, second;
    public pair(int first, int second) 
    {
          this.first = first;
        this.second = second;
    }   
}

// Function to count all the
// contiguous subsequences whose
// product is expressed as the square
// of the difference of two integers
static int CntcontSubs(int a[], int n)
{
    int prod = 1;

    // Creating vectors to store
    // the remainders and the
    // subsequences
    Vector<pair> vect = new Vector<pair>();

    vect.add(new pair(0, 2));
    Vector<Integer> two = new  Vector<Integer>();
    Vector<Integer> zero = new  Vector<Integer>();

    // Iterating through the array
    for (int i = 0; i < n; i++)
    {
        // Finding the remainder when the
        // element is divided by 4
        a[i] = a[i] % 4;

        // Bringing all the elements in
        // the range [0, 3]
        if (a[i] < 0)
            a[i] = a[i] + 4;

        // If the remainder is 2, store
        // the index of the
        if (a[i] == 2)
            two.add(i + 1);

        // If the remainder is 2, store
        // the index of the
        if (a[i] == 0)
            zero.add(i + 1);

        if (a[i] == 0 || a[i] == 2)
            vect.add(new pair(i + 1, a[i]));
    }
    vect.add(new pair(n + 1, 2));

    // Finding the total number of subsequences
    int total = (n * (n + 1)) / 2;

    // If there are no numbers which
    // yield the remainder 2
    if (two.isEmpty())
        return total;
    else
    {
        int sum = 0;
        int pos1 = -1, pos2 = -1, pos3 = -1;
        int sz = vect.size();

        // Iterating through the vector
        for (int i = 1; i + 1 < sz; i++)
        {
            // If the element is 2, find the nearest
            // 2 or 0 and find the number of
            // elements between them
            if (vect.get(i).second == 2)
            {
                sum += (vect.get(i).first -
                        vect.get(i-1).first) *
                       (vect.get(i+1).first -
                        vect.get(i).first) - 1;
            }
        }

        // Returning the count
        return total - sum - two.size();
    }
}

// Driver code
public static void main(String[] args)
{
    int a[] = {5, 4, 2, 9, 8};
    int n = a.length;
    System.out.print(CntcontSubs(a, n));
}
}

// This code is contributed by shikhasingrajput
```

## 蟒蛇 3

```
# Python3 implementation to count all the
# contiguous subsequences whose product is
# expressed as the square of the difference
# of two integers

# Function to count all the
# contiguous subsequences whose
# product is expressed as the square
# of the difference of two integers
def CntcontSubs(a, n):

    prod = 1

    # Creating vectors to store
    # the remainders and the
    # subsequences
    vect = []

    vect.append((0, 2))

    two, zero = [], []

    # Iterating through the array
    for i in range(n):

        # Finding the remainder when the
        # element is divided by 4
        a[i] = a[i] % 4

        # Bringing all the elements in
        # the range [0, 3]
        if (a[i] < 0):
            a[i] = a[i] + 4

        # If the remainder is 2, store
        # the index of the
        if (a[i] == 2):
            two.append(i + 1)

        # If the remainder is 2, store
        # the index of the
        if (a[i] == 0):
            zero.append(i + 1)

        if (a[i] == 0 or a[i] == 2):
            vect.append((i + 1, a[i]))

    vect.append((n + 1, 2))

    # Finding the total number of subsequences
    total = (n * (n + 1)) // 2

    # If there are no numbers which
    # yield the remainder 2
    if (len(two) == 0):
        return total
    else:
        Sum = 0

        pos1, pos2, pos3 = -1, -1, -1

        sz = len(vect)

        # Iterating through the vector
        for i in range(1, sz - 1):

            # If the element is 2, find the
            # nearest 2 or 0 and find the
            # number of elements between them
            if (vect[i][1] == 2) :
                Sum += ((vect[i][0] - vect[i - 1][0]) *
                        (vect[i + 1][0] - vect[i][0]) - 1)

        # Returning the count
        return (total - Sum - len(two))

# Driver Code
a = [ 5, 4, 2, 9, 8 ]
n = len(a)

print(CntcontSubs(a, n))

# This code is contributed by divyeshrabadiya07
```

## C#

```
// C# implementation to count all the
// contiguous subsequences whose
// product is expressed as the square
// of the difference of two integers
using System;
using System.Collections.Generic;

class GFG{

class pair
{
    public int first, second;
    public pair(int first, int second)
    {
        this.first = first;
        this.second = second;
    }
}

// Function to count all the
// contiguous subsequences whose
// product is expressed as the square
// of the difference of two integers
static int CntcontSubs(int []a, int n)
{

    // Creating vectors to store
    // the remainders and the
    // subsequences
    List<pair> vect = new List<pair>();

    vect.Add(new pair(0, 2));
    List<int> two = new List<int>();
    List<int> zero = new List<int>();

    // Iterating through the array
    for(int i = 0; i < n; i++)
    {

        // Finding the remainder when the
        // element is divided by 4
        a[i] = a[i] % 4;

        // Bringing all the elements in
        // the range [0, 3]
        if (a[i] < 0)
            a[i] = a[i] + 4;

        // If the remainder is 2, store
        // the index of the
        if (a[i] == 2)
            two.Add(i + 1);

        // If the remainder is 2, store
        // the index of the
        if (a[i] == 0)
            zero.Add(i + 1);

        if (a[i] == 0 || a[i] == 2)
            vect.Add(new pair(i + 1, a[i]));
    }

    vect.Add(new pair(n + 1, 2));

    // Finding the total number of subsequences
    int total = (n * (n + 1)) / 2;

    // If there are no numbers which
    // yield the remainder 2
    if (two.Count == 0)
        return total;
    else
    {
        int sum = 0;
        int sz = vect.Count;

        // Iterating through the vector
        for(int i = 1; i + 1 < sz; i++)
        {

            // If the element is 2, find the nearest
            // 2 or 0 and find the number of
            // elements between them
            if (vect[i].second == 2)
            {
                sum += (vect[i].first -
                        vect[i - 1].first) *
                       (vect[i + 1].first -
                        vect[i].first) - 1;
            }
        }

        // Returning the count
        return total - sum - two.Count;
    }
}

// Driver code
public static void Main(String[] args)
{
    int []a = { 5, 4, 2, 9, 8 };
    int n = a.Length;

    Console.Write(CntcontSubs(a, n));
}
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>
// Javascript implementation to count all the
// contiguous subsequences whose
// product is expressed as the square
// of the difference of two integers

// Function to count all the
// contiguous subsequences whose
// product is expressed as the square
// of the difference of two integers
function CntcontSubs(a,n)
{
    let prod = 1;

    // Creating vectors to store
    // the remainders and the
    // subsequences
    let vect = [];

    vect.push([0, 2]);
    let two = [];
    let zero = [];

    // Iterating through the array
    for (let i = 0; i < n; i++)
    {
        // Finding the remainder when the
        // element is divided by 4
        a[i] = a[i] % 4;

        // Bringing all the elements in
        // the range [0, 3]
        if (a[i] < 0)
            a[i] = a[i] + 4;

        // If the remainder is 2, store
        // the index of the
        if (a[i] == 2)
            two.push(i + 1);

        // If the remainder is 2, store
        // the index of the
        if (a[i] == 0)
            zero.push(i + 1);

        if (a[i] == 0 || a[i] == 2)
            vect.push([i + 1, a[i]]);
    }
    vect.push([n + 1, 2]);

    // Finding the total number of subsequences
    let total = Math.floor((n * (n + 1)) / 2);

    // If there are no numbers which
    // yield the remainder 2
    if (two.length==0)
        return total;
    else
    {
        let sum = 0;
        let pos1 = -1, pos2 = -1, pos3 = -1;
        let sz = vect.length;

        // Iterating through the vector
        for (let i = 1; i + 1 < sz; i++)
        {
            // If the element is 2, find the nearest
            // 2 or 0 and find the number of
            // elements between them
            if (vect[i][1] == 2)
            {
                sum += (vect[i][0] -
                        vect[i-1][0]) *
                       (vect[i+1][0] -
                        vect[i][0]) - 1;
            }
        }

        // Returning the count
        return total - sum - two.length;
    }
}

// Driver code
let a = [5, 4, 2, 9, 8];
let n = a.length;
document.write(CntcontSubs(a, n));

// This code is contributed by patel2127
</script>
```

**Output:** 

```
13
```

**时间复杂度:** *O(N)* 其中 N 是数组的长度。

**辅助空间:** O(N)
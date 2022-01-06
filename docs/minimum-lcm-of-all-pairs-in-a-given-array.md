# 给定阵列中所有对的最小 LCM

> 原文:[https://www . geesforgeks . org/最小给定阵列中所有对的 LCM/](https://www.geeksforgeeks.org/minimum-lcm-of-all-pairs-in-a-given-array/)

给定一个大小为 **N** 的数组**arr【】**，任务是找出给定数组中所有唯一对的最小 [LCM(最小公倍数)](https://www.geeksforgeeks.org/lcm-and-hcf/)，其中 1<=**N**<= 10<sup>5</sup>，1<=**arr【I】**<= 10<sup>5</sup>。

**示例:**

> **输入:** arr[] = {2，4，3}
> **输出:** 4
> **解释**
> LCM (2，4) = 4
> LCM (2，3) = 6
> LCM (4，3) = 12
> 最小可能 LCM 为 4。
> 
> **输入:** arr [] ={1，5，2，2，6}
> **输出:** 2

**天真的方法**

1.  [生成所有可能的对](https://www.geeksforgeeks.org/print-all-possible-combinations-of-r-elements-in-a-given-array-of-size-n/)并计算每个唯一对的 LCM。
2.  从所有唯一对中找出最小 LCM。

下面是上述方法的实现:

## C++

```
// C++ program to find
// minimum possible lcm
// from any pair

#include <bits/stdc++.h>
using namespace std;

// function to compute
// GCD of two numbers
int gcd(int a, int b)
{
    if (b == 0)
        return a;
    return gcd(b, a % b);
}

// function that return
// minimum possible lcm
// from any pair
int minLCM(int arr[], int n)
{
    int ans = INT_MAX;
    for (int i = 0; i < n; i++) {

        // fix the ith element and
        // iterate over all the array
        // to find minimum LCM
        for (int j = i + 1; j < n; j++) {

            int g = gcd(arr[i], arr[j]);
            int lcm = arr[i] / g * arr[j];
            ans = min(ans, lcm);
        }
    }

    return ans;
}

// Driver code
int main()
{
    int arr[] = { 2, 4, 3, 6, 5 };
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << minLCM(arr, n) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find minimum
// possible lcm from any pair
import java.io.*;
import java.util.*;

class GFG {

// Function to compute
// GCD of two numbers
static int gcd(int a, int b)
{
    if (b == 0)
        return a;
    return gcd(b, a % b);
}

// Function that return minimum
// possible lcm from any pair
static int minLCM(int arr[], int n)
{
    int ans = Integer.MAX_VALUE;

    for(int i = 0; i < n; i++)
    {

       // Fix the ith element and
       // iterate over all the array
       // to find minimum LCM
       for(int j = i + 1; j < n; j++)
       {
          int g = gcd(arr[i], arr[j]);
          int lcm = arr[i] / g * arr[j];
          ans = Math.min(ans, lcm);
       }
    }
    return ans;
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 2, 4, 3, 6, 5 };
    int n = arr.length;

    System.out.println(minLCM(arr,n));
}
}

// This code is contributed by coder001
```

## 蟒蛇 3

```
# Python3 program to find minimum
# possible lcm from any pair
import sys

# Function to compute
# GCD of two numbers
def gcd(a, b):

    if (b == 0):
        return a;
    return gcd(b, a % b);

# Function that return minimum
# possible lcm from any pair
def minLCM(arr, n):

    ans = 1000000000;
    for i in range(n):

        # Fix the ith element and
        # iterate over all the
        # array to find minimum LCM
        for j in range(i + 1, n):

            g = gcd(arr[i], arr[j]);
            lcm = arr[i] / g * arr[j];
            ans = min(ans, lcm);

    return ans;

# Driver code
arr = [ 2, 4, 3, 6, 5 ];

print(minLCM(arr, 5))

# This code is contributed by grand_master
```

## C#

```
// C# program to find minimum
// possible lcm from any pair
using System;
class GFG{

// Function to compute
// GCD of two numbers
static int gcd(int a, int b)
{
    if (b == 0)
        return a;
    return gcd(b, a % b);
}

// Function that return minimum
// possible lcm from any pair
static int minLCM(int []arr, int n)
{
    int ans = Int32.MaxValue;

    for(int i = 0; i < n; i++)
    {

    // Fix the ith element and
    // iterate over all the array
    // to find minimum LCM
    for(int j = i + 1; j < n; j++)
    {
        int g = gcd(arr[i], arr[j]);
        int lcm = arr[i] / g * arr[j];
        ans = Math.Min(ans, lcm);
    }
    }
    return ans;
}

// Driver code
public static void Main()
{
    int []arr = { 2, 4, 3, 6, 5 };
    int n = arr.Length;

    Console.Write(minLCM(arr,n));
}
}

// This code is contributed by Akanksha_Rai
```

## java 描述语言

```
<script>

    // Javascript program to find
    // minimum possible lcm
    // from any pair

    // function to compute
    // GCD of two numbers
    function gcd(a, b)
    {
        if (b == 0)
            return a;
        return gcd(b, a % b);
    }

    // function that return
    // minimum possible lcm
    // from any pair
    function minLCM(arr, n)
    {
        let ans = Number.MAX_VALUE;
        for (let i = 0; i < n; i++) {

            // fix the ith element and
            // iterate over all the array
            // to find minimum LCM
            for (let j = i + 1; j < n; j++) {

                let g = gcd(arr[i], arr[j]);
                let lcm = arr[i] / g * arr[j];
                ans = Math.min(ans, lcm);
            }
        }

        return ans;
    }

    let arr = [ 2, 4, 3, 6, 5 ];
    let n = arr.length;
    document.write(minLCM(arr, n));

</script>
```

**Output:** 

```
4
```

**时间复杂度:** *O(N <sup>2</sup> )*

**有效方法:**该方法取决于公式:

> 两个数的乘积= **两个数的 LCM*****两个数的 GCD**

1.  LCM 的公式中，分母是两个数的 GCD，两个数的 GCD 永远不会大于数本身。
2.  因此，对于一个固定的 GCD，找到给定数组中该固定 GCD 的最小二倍。
3.  只存储每个 GCD 的最小两个倍数，因为选择阵列中存在的 GCD 的更大倍数，无论如何，它都不会给出最小答案。
4.  最后，用筛子找出最小的两个数，即所选 GCD 的倍数。

下面是上述方法的实现:

## C++

```
// C++ program to find the
// pair having minimum LCM

#include <bits/stdc++.h>
using namespace std;

// function that return
// pair having minimum LCM
int minLCM(int arr[], int n)
{
    int mx = 0;
    for (int i = 0; i < n; i++) {

        // find max element in the array as
        // the gcd of two elements from the
        // array can't greater than max element.
        mx = max(mx, arr[i]);
    }

    // created a 2D array to store minimum
    // two multiple of any particular i.
    vector<vector<int> > mul(mx + 1);

    for (int i = 0; i < n; i++) {
        if (mul[arr[i]].size() > 1) {
            // we already found two
            // smallest multiple
            continue;
        }
        mul[arr[i]].push_back(arr[i]);
    }

    // iterating over all gcd
    for (int i = 1; i <= mx; i++) {

        // iterating over its multiple
        for (int j = i + i; j <= mx; j += i) {

            if (mul[i].size() > 1) {

                // if we already found the
                // two smallest multiple of i
                break;
            }
            for (int k : mul[j]) {
                if (mul[i].size() > 1)
                    break;
                mul[i].push_back(k);
            }
        }
    }

    int ans = INT_MAX;
    for (int i = 1; i <= mx; i++) {

        if (mul[i].size() <= 1)
            continue;

        // choosing smallest two multiple
        int a = mul[i][0], b = mul[i][1];

        // calculating lcm
        int lcm = (a * b) / i;

        ans = min(ans, lcm);
    }

    // return final answer
    return ans;
}

// Driver code
int main()
{
    int arr[] = { 2, 4, 3, 6, 5 };
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << minLCM(arr, n) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the
// pair having minimum LCM
import java.util.Vector;
class GFG{

// Function that return
// pair having minimum LCM
static int minLCM(int arr[],
                  int n)
{
  int mx = 0;
  for (int i = 0; i < n; i++)
  {
    // Find max element in the
    // array as the gcd of two
    // elements from the array
    // can't greater than max element.
    mx = Math.max(mx, arr[i]);
  }

  // Created a 2D array to store minimum
  // two multiple of any particular i.
  Vector<Integer> []mul = new Vector[mx + 1];

  for (int i = 0; i < mul.length; i++)
    mul[i] = new Vector<Integer>();
  for (int i = 0; i < n; i++)
  {
    if (mul[arr[i]].size() > 1)
    {
      // We already found two
      // smallest multiple
      continue;
    }
    mul[arr[i]].add(arr[i]);
  }

  // Iterating over all gcd
  for (int i = 1; i <= mx; i++)
  {
    // Iterating over its multiple
    for (int j = i + i; j <= mx; j += i)
    {
      if (mul[i].size() > 1)
      {
        // If we already found the
        // two smallest multiple of i
        break;
      }     
      for (int k : mul[j])
      {
        if (mul[i].size() > 1)
          break;
        mul[i].add(k);
      }
    }
  }

  int ans = Integer.MAX_VALUE;
  for (int i = 1; i <= mx; i++)
  {
    if (mul[i].size() <= 1)
      continue;

    //  Choosing smallest
    // two multiple
    int a = mul[i].get(0),
        b = mul[i].get(1);

    // Calculating lcm
    int lcm = (a * b) / i;

    ans = Math.min(ans, lcm);
  }

  // Return final answer
  return ans;
}

// Driver code
public static void main(String[] args)
{
  int arr[] = {2, 4, 3, 6, 5};
  int n = arr.length;
  System.out.print(minLCM(arr, n) + "\n");
}
}

// This code is contributed by shikhasingrajput
```

## 蟒蛇 3

```
# Python3 program to find the
# pair having minimum LCM
import sys

# function that return
# pair having minimum LCM
def minLCM(arr, n) :
    mx = 0
    for i in range(n) :

        # find max element in the array as
        # the gcd of two elements from the
        # array can't greater than max element.
        mx = max(mx, arr[i])

    # created a 2D array to store minimum
    # two multiple of any particular i.
    mul = [[] for i in range(mx + 1)]

    for i in range(n) :
        if (len(mul[arr[i]]) > 1) :

            # we already found two
            # smallest multiple
            continue

        mul[arr[i]].append(arr[i])

    # iterating over all gcd
    for i in range(1, mx + 1) :

        # iterating over its multiple
        for j in range(i + i, mx + 1, i) :

            if (len(mul[i]) > 1) :

                # if we already found the
                # two smallest multiple of i
                break

            for k in mul[j] :
                if (len(mul[i]) > 1) :
                    break
                mul[i].append(k)

    ans = sys.maxsize
    for i in range(1, mx + 1) :
        if (len(mul[i]) <= 1) :
            continue

        # choosing smallest two multiple
        a, b = mul[i][0], mul[i][1]

        # calculating lcm
        lcm = (a * b) // i
        ans = min(ans, lcm)

    # return final answer
    return ans

# Driver code
arr = [ 2, 4, 3, 6, 5 ]
n = len(arr)
print(minLCM(arr, n))

# This code is contributed by divyesh072019
```

## C#

```
// C# program to find the
// pair having minimum LCM
using System;
using System.Collections.Generic;
class GFG{

// Function that return
// pair having minimum LCM
static int minLCM(int []arr,
                  int n)
{
  int mx = 0;

  for (int i = 0; i < n; i++)
  {
    // Find max element in the
    // array as the gcd of two
    // elements from the array
    // can't greater than max element.
    mx = Math.Max(mx, arr[i]);
  }

  // Created a 2D array to store minimum
  // two multiple of any particular i.
  List<int> []mul = new List<int>[mx + 1];

  for (int i = 0; i < mul.Length; i++)
    mul[i] = new List<int>();

  for (int i = 0; i < n; i++)
  {
    if (mul[arr[i]].Count > 1)
    {
      // We already found two
      // smallest multiple
      continue;
    }
    mul[arr[i]].Add(arr[i]);
  }

  // Iterating over all gcd
  for (int i = 1; i <= mx; i++)
  {
    // Iterating over its multiple
    for (int j = i + i; j <= mx; j += i)
    {
      if (mul[i].Count > 1)
      {
        // If we already found the
        // two smallest multiple of i
        break;
      }     
      foreach (int k in mul[j])
      {
        if (mul[i].Count > 1)
          break;
        mul[i].Add(k);
      }
    }
  }

  int ans = int.MaxValue;
  for (int i = 1; i <= mx; i++)
  {
    if (mul[i].Count <= 1)
      continue;

    //  Choosing smallest
    // two multiple
    int a = mul[i][0],
        b = mul[i][1];

    // Calculating lcm
    int lcm = (a * b) / i;

    ans = Math.Min(ans, lcm);
  }

  // Return readonly answer
  return ans;
}

// Driver code
public static void Main(String[] args)
{
  int []arr = {2, 4, 3, 6, 5};
  int n = arr.Length;
  Console.Write(minLCM(arr, n) + "\n");
}
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>

// Javascript program to find the
// pair having minimum LCM

// function that return
// pair having minimum LCM
function minLCM(arr, n)
{
    var mx = 0;
    for(var i = 0; i < n; i++)
    {

        // Find max element in the array as
        // the gcd of two elements from the
        // array can't greater than max element.
        mx = Math.max(mx, arr[i]);
    }

    // Created a 2D array to store minimum
    // two multiple of any particular i.
    var mul = Array.from(Array(mx + 1), () => Array());

    for(var i = 0; i < n; i++)
    {
        if (mul[arr[i]].length > 1)
        {

            // We already found two
            // smallest multiple
            continue;
        }
        mul[arr[i]].push(arr[i]);
    }

    // Iterating over all gcd
    for(var i = 1; i <= mx; i++)
    {

        // Iterating over its multiple
        for(var j = i + i; j <= mx; j += i)
        {
            if (mul[i].length > 1)
            {

                // If we already found the
                // two smallest multiple of i
                break;
            }
            mul[j].forEach(k => {

                if (mul[i].length <= 1)
                {
                    mul[i].push(k);
                }
            });
        }
    }

    var ans = 1000000000;
    for(var i = 1; i <= mx; i++)
    {
        if (mul[i].length <= 1)
            continue;

        // Choosing smallest two multiple
        var a = mul[i][0], b = mul[i][1];

        // Calculating lcm
        var lcm = (a * b) / i;

        ans = Math.min(ans, lcm);
    }

    // Return final answer
    return ans;
}

// Driver code
var arr = [ 2, 4, 3, 6, 5 ];
var n = arr.length;

document.write( minLCM(arr, n) + "<br>");

// This code is contributed by itsok

</script>
```

**Output:** 

```
4
```

**时间复杂度:***O((N+M)* log(M))*
T5】辅助空间: *O(M)* 其中 M 是数组中最大的元素。
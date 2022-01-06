# 计数乘积包含单个不同质因数的对

> 原文:[https://www . geeksforgeeks . org/count-pairs-其产品包含单个不同的质因数/](https://www.geeksforgeeks.org/count-pairs-whose-product-contains-single-distinct-prime-factor/)

给定一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** ，任务是计算给定数组中其乘积只包含一个不同的[质因数的对的数量。](https://www.geeksforgeeks.org/prime-factor/)

**示例:**

> **输入:** arr[] = {1，2，3，4}
> **输出:** 4
> **解释:**
> 在其乘积中具有单个不同质因数的对如下:
> arr[0] * arr[1] = (1 * 2) = 2。因此，唯一不同的质因数是 2。
> arr[0] * arr[2] = (1 * 3) = 3。因此，唯一不同的质因数是 3。
> arr[0]* arr[3]=(1 * 4)= 2<sup>2</sup>因此，单个不同的质因数为 2。
> arr[1]* arr[3]=(2 * 4)= 8 2<sup>3</sup>因此，单个不同的质因数为 2。
> 因此，要求输出为 4。
> 
> **输入:** arr[] = {2，4，6，8}
> **输出:** 3

**天真方法:**解决这个问题最简单的方法是[遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)和[生成数组](https://www.geeksforgeeks.org/find-all-pairs-possible-from-the-given-array/)的所有可能的对，并且对于每个对，检查元素的乘积是否只包含单个不同的[素因子](https://www.geeksforgeeks.org/print-all-prime-factors-and-their-powers/)。如果发现为真，则增加计数。最后，打印计数。

***时间复杂度:** O(N <sup>2</sup> * √X)，其中 X 是给定数组中一对的最大可能乘积。*
***辅助空间:** O(1)*

**高效方法:**优化上述方法的思路是使用[哈希](https://www.geeksforgeeks.org/hashing-data-structure/)。按照以下步骤解决问题:

*   初始化一个变量，比如说 **cntof1** 来存储数组元素的计数，数组元素的值是 **1** 。
*   创建[图](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)，比如 **mp** 来存储数组元素的计数，该数组元素只包含一个不同的[质因数](https://www.geeksforgeeks.org/print-all-prime-factors-and-their-powers/)。
*   遍历数组，对于每个数组元素，检查不同质因数的计数是否为 **1** 。如果发现为真，则[将当前元素插入 mp](https://www.geeksforgeeks.org/map-insert-in-c-stl/) 。
*   初始化一个变量，比如说 **res** 来存储元素乘积只包含一个不同质因数的对的计数。
*   [遍历地图](https://www.geeksforgeeks.org/traversing-a-map-or-unordered_map-in-cpp-stl/)并更新**RES+= cntof 1 *(X)+(X *(X-1))/2**。其中 X 存储数组元素的计数，该数组元素只包含一个不同的质因数 **i** 。
*   最后，打印 **res** 的值。

下面是上述方法的实现

## C++

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find a single
// distinct prime factor of N
int singlePrimeFactor(int N)
{

    // Stores distinct
    // prime factors of N
    unordered_set<int>
              disPrimeFact;

    // Calculate prime factor of N
    for (int i = 2; i * i <= N; ++i) {

        // Calculate distinct
        // prime factor
        while (N % i == 0) {

            // Insert i into
            // disPrimeFact
            disPrimeFact.insert(i);

            // Update N
            N /= i;
        }
    }

    // If N is not equal to 1
    if (N != 1)
    {

        // Insert N into
        // disPrimeFact
        disPrimeFact.insert(N);
    }

    // If N contains a single
    // distinct prime factor
    if (disPrimeFact.size() == 1) {

        // Return single distinct
        // prime factor of N
        return *disPrimeFact.begin();
    }   

    // If N contains more than one
    // distinct prime factor   
    return -1;
}

// Function to count pairs in the array
// whose product contains only
// single distinct prime factor
int cntsingleFactorPair(int arr[], int N)
{

   // Stores count of 1s
   // in the array
    int countOf1 = 0;

    // mp[i]: Stores count of array elements
    // whose distinct prime factor is only i
    unordered_map<int, int> mp;

    // Traverse the array arr[]
    for (int i = 0; i < N; i++) {

        // If current element is 1
        if(arr[i] == 1)
        {
            countOf1++;
            continue;
        }

        // Store distinct
        // prime factor of arr[i]
        int factorValue
          = singlePrimeFactor(arr[i]);

        // If arr[i] contains more
        // than one prime factor
        if (factorValue == -1) {
            continue;
        }

        // If arr[i] contains
        // a single prime factor
        else {
            mp[factorValue]++;
        }
    }

    // Stores the count of pairs whose
    // product of elements contains only
    // a single distinct prime factor
    int res = 0;

    // Traverse the map mp[]
    for (auto it : mp) { 

        // Stores count of array elements
        // whose prime factor is (it.first)
        int X = it.second;

        // Update res
        res += countOf1 * X +
              (X * (X - 1) ) / 2;
    }

    return res;
}

// Driver Code
int main()
{

    int arr[] = { 1, 2, 3, 4 };
    int N = sizeof(arr) / sizeof(arr[0]);
    cout << cntsingleFactorPair(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;
class GFG{

// Function to find a single
// distinct prime factor of N
static int singlePrimeFactor(int N)
{
  // Stores distinct
  // prime factors of N
  HashSet<Integer> disPrimeFact =
                   new HashSet<>();

  // Calculate prime factor of N
  for (int i = 2;
           i * i <= N; ++i)
  {
    // Calculate distinct
    // prime factor
    while (N % i == 0)
    {
      // Insert i into
      // disPrimeFact
      disPrimeFact.add(i);

      // Update N
      N /= i;
    }
  }

  // If N is not equal to 1
  if (N != 1)
  {
    // Insert N into
    // disPrimeFact
    disPrimeFact.add(N);
  }

  // If N contains a single
  // distinct prime factor
  if (disPrimeFact.size() == 1)
  {
    // Return single distinct
    // prime factor of N
    for(int i : disPrimeFact)
      return i;
  }

  // If N contains more than
  // one distinct prime factor   
  return -1;
}

// Function to count pairs in
// the array whose product
// contains only single distinct
// prime factor
static int cntsingleFactorPair(int arr[],
                               int N)
{  
  // Stores count of 1s
  // in the array
  int countOf1 = 0;

  // mp[i]: Stores count of array
  // elements whose distinct prime
  // factor is only i
  HashMap<Integer,
          Integer> mp = new HashMap<Integer,
                                    Integer>();

  // Traverse the array arr[]
  for (int i = 0; i < N; i++)
  {
    // If current element is 1
    if(arr[i] == 1)
    {
      countOf1++;
      continue;
    }

    // Store distinct
    // prime factor of arr[i]
    int factorValue =
        singlePrimeFactor(arr[i]);

    // If arr[i] contains more
    // than one prime factor
    if (factorValue == -1)
    {
      continue;
    }

    // If arr[i] contains
    // a single prime factor
    else
    {
      if(mp.containsKey(factorValue))
        mp.put(factorValue,
        mp.get(factorValue) + 1);
      else
        mp.put(factorValue, 1);
    }
  }

  // Stores the count of pairs whose
  // product of elements contains only
  // a single distinct prime factor
  int res = 0;

  // Traverse the map mp[]
  for (Map.Entry<Integer,
                 Integer> it :
       mp.entrySet())
  {
    // Stores count of array
    // elements whose prime
    // factor is (it.first)
    int X = it.getValue();

    // Update res
    res += countOf1 * X +
           (X * (X - 1) ) / 2;
  }

  return res;
}

// Driver Code
public static void main(String[] args)
{
  int arr[] = {1, 2, 3, 4};
  int N = arr.length;
  System.out.print(
         cntsingleFactorPair(arr, N));
}
}

// This code is contributed by gauravrajput1
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to find a single
# distinct prime factor of N
def singlePrimeFactor(N):

    # Stores distinct
    # prime factors of N
    disPrimeFact = {}

    # Calculate prime factor of N
    for i in range(2, N + 1):
        if i * i > N:
            break

        # Calculate distinct
        # prime factor
        while (N % i == 0):

            # Insert i into
            # disPrimeFact
            disPrimeFact[i] = 1

            # Update N
            N //= i

    # If N is not equal to 1
    if (N != 1):

        # Insert N into
        # disPrimeFact
        disPrimeFact[N] = 1

    # If N contains a single
    # distinct prime factor
    if (len(disPrimeFact) == 1):

        # Return single distinct
        # prime factor of N
        return list(disPrimeFact.keys())[0]

    # If N contains more than one
    # distinct prime factor
    return -1

# Function to count pairs in the array
# whose product contains only
# single distinct prime factor
def cntsingleFactorPair(arr, N):

    # Stores count of 1s
    # in the array
    countOf1 = 0

    # mp[i]: Stores count of array elements
    # whose distinct prime factor is only i
    mp = {}

    # Traverse the array arr[]
    for i in range(N):

        # If current element is 1
        if (arr[i] == 1):
            countOf1 += 1
            continue

        # Store distinct
        # prime factor of arr[i]
        factorValue = singlePrimeFactor(arr[i])

        # If arr[i] contains more
        # than one prime factor
        if (factorValue == -1):
            continue

        # If arr[i] contains
        # a single prime factor
        else:
            mp[factorValue] = mp.get(factorValue, 0) + 1

    # Stores the count of pairs whose
    # product of elements contains only
    # a single distinct prime factor
    res = 0

    # Traverse the map mp[]
    for it in mp:

        # Stores count of array elements
        # whose prime factor is (it.first)
        X = mp[it]

        # Update res
        res += countOf1 * X + (X * (X - 1) ) // 2

    return res

# Driver Code
if __name__ == '__main__':

    arr = [ 1, 2, 3, 4 ]
    N = len(arr)

    print(cntsingleFactorPair(arr, N))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program to implement
// the above approach
using System;
using System.Collections.Generic;
class GFG{

// Function to find a single
// distinct prime factor of N
static int singlePrimeFactor(int N)
{
  // Stores distinct
  // prime factors of N
  HashSet<int> disPrimeFact =
          new HashSet<int>();

  // Calculate prime factor of N
  for (int i = 2;
           i * i <= N; ++i)
  {
    // Calculate distinct
    // prime factor
    while (N % i == 0)
    {
      // Insert i into
      // disPrimeFact
      disPrimeFact.Add(i);

      // Update N
      N /= i;
    }
  }

  // If N is not equal to 1
  if(N != 1)
  {
    // Insert N into
    // disPrimeFact
    disPrimeFact.Add(N);
  }

  // If N contains a single
  // distinct prime factor
  if (disPrimeFact.Count == 1)
  {
    // Return single distinct
    // prime factor of N
    foreach(int i in disPrimeFact)
      return i;
  }

  // If N contains more than
  // one distinct prime factor   
  return -1;
}

// Function to count pairs in
// the array whose product
// contains only single distinct
// prime factor
static int cntsingleFactorPair(int []arr,
                               int N)
{  
  // Stores count of 1s
  // in the array
  int countOf1 = 0;

  // mp[i]: Stores count of array
  // elements whose distinct prime
  // factor is only i
  Dictionary<int,
             int> mp =
             new Dictionary<int,
                            int>();

  // Traverse the array arr[]
  for (int i = 0; i < N; i++)
  {
    // If current element is 1
    if(arr[i] == 1)
    {
      countOf1++;
      continue;
    }

    // Store distinct
    // prime factor of arr[i]
    int factorValue =
        singlePrimeFactor(arr[i]);

    // If arr[i] contains more
    // than one prime factor
    if (factorValue == -1)
    {
      continue;
    }

    // If arr[i] contains
    // a single prime factor
    else
    {
      if(mp.ContainsKey(factorValue))
        mp[factorValue] = mp[factorValue] + 1;
      else
        mp.Add(factorValue, 1);
    }
  }

  // Stores the count of pairs whose
  // product of elements contains only
  // a single distinct prime factor
  int res = 0;

  // Traverse the map mp[]
  foreach(KeyValuePair<int,
                       int> ele1 in mp)
  {
    // Stores count of array
    // elements whose prime
    // factor is (it.first)
    int X = ele1.Value;

    // Update res
    res += countOf1 * X +
           (X * (X - 1) ) / 2;
  }

  return res;
}

// Driver Code
public static void Main()
{
  int []arr = {1, 2, 3, 4};
  int N = arr.Length;
  Console.WriteLine(
         cntsingleFactorPair(arr, N));
}
}

// This code is contributed by bgangwar59
```

## java 描述语言

```
<script>

// JavaScript program to implement
// the above approach

// Function to find a single
// distinct prime factor of N
function singlePrimeFactor(N)
{

    // Stores distinct
    // prime factors of N
    var disPrimeFact = {};

    // Calculate prime factor of N
    for(var i = 2; i * i <= N; ++i)
    {

        // Calculate distinct
        // prime factor
        while (N % i === 0)
        {

            // Insert i into
            // disPrimeFact
            disPrimeFact[i] = 1;

            // Update N
            N = parseInt(N / i);
        }
    }

    // If N is not equal to 1
    if (N !== 1)
    {

        // Insert N into
        // disPrimeFact
        disPrimeFact[N] = 1;
    }

    // If N contains a single
    // distinct prime factor
    if (Object.keys(disPrimeFact).length === 1)
    {

        // Return single distinct
        // prime factor of N
        for(const [key, value] of Object.entries(
            disPrimeFact))
        {
            return key;
        }
    }

    // If N contains more than
    // one distinct prime factor
    return -1;
}

// Function to count pairs in
// the array whose product
// contains only single distinct
// prime factor
function cntsingleFactorPair(arr, N)
{

    // Stores count of 1s
    // in the array
    var countOf1 = 0;

    // mp[i]: Stores count of array
    // elements whose distinct prime
    // factor is only i
    var mp = {};

    // Traverse the array arr[]
    for(var i = 0; i < N; i++)
    {

        // If current element is 1
        if (arr[i] === 1)
        {
            countOf1++;
            continue;
        }

        // Store distinct
        // prime factor of arr[i]
        var factorValue = singlePrimeFactor(arr[i]);

        // If arr[i] contains more
        // than one prime factor
        if (factorValue === -1)
        {
            continue;
        }

        // If arr[i] contains
        // a single prime factor
        else
        {
            if (mp.hasOwnProperty(factorValue))
                mp[factorValue] = mp[factorValue] + 1;
            else
                mp[factorValue] = 1;
        }
    }

    // Stores the count of pairs whose
    // product of elements contains only
    // a single distinct prime factor
    var res = 0;

    // Traverse the map mp[]
    for(const [key, value] of Object.entries(mp))
    {

        // Stores count of array
        // elements whose prime
        // factor is (it.first)
        var X = value;

        // Update res
        res = parseInt(res + countOf1 * X +
                        (X * (X - 1)) / 2);
    }
    return res;
}

// Driver Code
var arr = [ 1, 2, 3, 4 ];
var N = arr.length;

document.write(cntsingleFactorPair(arr, N));

// This code is contributed by rdtank

</script>
```

**Output:** 

```
4
```

***时间复杂度:** O(N√X)* ，其中 **X** 是给定数组的最大元素。
***辅助空间:** O(N)*
# 数组中的对计数，使得对和 X 的异或的位“与”为 0

> 原文:[https://www . geeksforgeeks . org/数组中对的计数，即对与 x 的按位异或为 0/](https://www.geeksforgeeks.org/count-of-pairs-in-array-such-that-bitwise-and-of-xor-of-pair-and-x-is-0/)

给定一个由 **N** 个正整数和一个正整数 **X** 组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】】**,任务是找出对 **(i，j)** 的数量，使得 **i < j** 和**(arr[i]^arr[j)&x**为 **0** 。

**示例:**

> **输入:** arr[] = {1，3，4，2}，X = 2
> **输出:** 2
> **解释:**
> 以下是给定数组中可能的对:
> 
> 1.  **(0，2):**(arr[0]^arr[2)&x 的值是(1^4) & 2 = 0。
> 2.  **(1，3):**(arr[1]^arr[3)&x 的值为(3^2) & 2 = 0。
> 
> 因此，对的总数是 2。
> 
> **输入:** arr[] = {3，2，5，4，6，7}，X = 6
> T3】输出: 3

**天真方法:**解决给定问题的简单方法是[生成给定数组](https://www.geeksforgeeks.org/find-all-pairs-possible-from-the-given-array/)的所有可能的对，并对那些满足给定标准的对 **(i，j)** 进行计数，即 **i < j** 和**(arr[i]^arr[j)&x**为 **0** ..检查所有对后，打印获得的总数**计数**。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the number of pairs
// that satisfy the given criteria i.e.,
// i < j and (arr[i]^arr[j] )&X is 0
int countOfPairs(int arr[], int N, int X)
{
    // Stores the resultant count
    // of pairs
    int count = 0;

    // Iterate over the range [0, N)
    for (int i = 0; i < N - 1; i++) {

        // Iterate over the range
        for (int j = i + 1; j < N; j++) {

            // Check for the given
            // condition
            if (((arr[i] ^ arr[j]) & X) == 0)
                count++;
        }
    }

    // Return the resultant count
    return count;
}

// Driver Code
int main()
{
    int arr[] = { 3, 2, 5, 4, 6, 7 };
    int X = 6;
    int N = sizeof(arr) / sizeof(arr[0]);
    cout << countOfPairs(arr, N, X);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG
{

// Function to find the number of pairs
// that satisfy the given criteria i.e.,
// i < j and (arr[i]^arr[j] )&X is 0
public static int countOfPairs(int arr[], int N, int X)
{
    // Stores the resultant count
    // of pairs
    int count = 0;

    // Iterate over the range [0, N)
    for (int i = 0; i < N - 1; i++) {

        // Iterate over the range
        for (int j = i + 1; j < N; j++) {

            // Check for the given
            // condition
            if (((arr[i] ^ arr[j]) & X) == 0)
                count++;
        }
    }

    // Return the resultant count
    return count;
}

// Driver Code
public static void main(String args[])
{
    int arr[] = { 3, 2, 5, 4, 6, 7 };
    int X = 6;
    int N = arr.length;
    System.out.println(countOfPairs(arr, N, X));
}
}

// This code is contributed by gfgking.
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the number of pairs
# that satisfy the given criteria i.e.,
# i < j and (arr[i]^arr[j] )&X is 0
def countOfPairs(arr, N, X):

    # Stores the resultant count
    # of pairs
    count = 0

    # Iterate over the range [0, N)
    for i in range(N - 1):

        # Iterate over the range
        for j in range(i + 1, N):

            # Check for the given
            # condition
            if (((arr[i] ^ arr[j]) & X) == 0):
                count += 1

    # Return the resultant count
    return count

# Driver Code
if __name__ == '__main__':

    arr = [ 3, 2, 5, 4, 6, 7 ]
    X = 6
    N = len(arr)

    print(countOfPairs(arr, N, X))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to find the number of pairs
// that satisfy the given criteria i.e.,
// i < j and (arr[i]^arr[j] )&X is 0
static int countOfPairs(int []arr, int N, int X)
{

    // Stores the resultant count
    // of pairs
    int count = 0;

    // Iterate over the range [0, N)
    for(int i = 0; i < N - 1; i++)
    {

        // Iterate over the range
        for(int j = i + 1; j < N; j++)
        {

            // Check for the given
            // condition
            if (((arr[i] ^ arr[j]) & X) == 0)
                count++;
        }
    }

    // Return the resultant count
    return count;
}

// Driver Code
public static void Main()
{
    int []arr = { 3, 2, 5, 4, 6, 7 };
    int X = 6;
    int N = arr.Length;

    Console.Write(countOfPairs(arr, N, X));
}
}

// This code is contributed by SURENDRA_GANGWAR
```

## java 描述语言

```
<script>
       // JavaScript program for the above approach

       // Function to find the number of pairs
       // that satisfy the given criteria i.e.,
       // i < j and (arr[i]^arr[j] )&X is 0
       function countOfPairs(arr, N, X)
       {

           // Stores the resultant count
           // of pairs
           let count = 0;

           // Iterate over the range [0, N)
           for (let i = 0; i < N - 1; i++)
           {

               // Iterate over the range
               for (let j = i + 1; j < N; j++)
               {

                   // Check for the given
                   // condition
                   if (((arr[i] ^ arr[j]) & X) == 0)
                       count++;
               }
           }

           // Return the resultant count
           return count;
       }

       // Driver Code
       let arr = [3, 2, 5, 4, 6, 7];
       let X = 6;
       let N = arr.length;
       document.write(countOfPairs(arr, N, X));

   // This code is contributed by Potta Lokesh

   </script>
```

**Output:** 

```
3
```

***时间复杂度:**O(N<sup>2</sup>)* *****辅助空间:** O(1)***

****高效方法:**上述方法也可以通过观察给定的方程进行优化。因此，要执行**(a[i]^a[j)&x = = 0**，则需要在 x 在其[二进制表示](https://www.geeksforgeeks.org/binary-representations-in-digital-logic/)中设置位的相同位置取消设置**(a[i]^a[j)**答案中的位。**

> **例如，如果 **X = 6 = > 110** ，那么要使**(答案& X) == 0** 其中**答案= a[i]^a[j】**，答案应为 **001** 或 **000** 。因此，要获得答案中的 **0** 位(与 **X** 所具有的置位位位处于相同的位置)，要求在该位置的**a【I】**和**a【j】**中具有与相同位(1^1 = 0 和 0^0 = 0)的[按位异或](https://www.geeksforgeeks.org/tag/xor/)给出的 **0** 相同的位。**

**仔细观察 **X** 与**A【I】**和**A【j】**的关系，发现**X&A【I】= = X&A【j】**。因此，思路是[求有值**arr【I】&X**的数组元素](https://www.geeksforgeeks.org/counting-frequencies-of-array-elements/)的频率，任意两个值相同的数字可以做成一对。按照以下步骤解决问题:**

*   **[初始化无序映射](https://www.geeksforgeeks.org/unordered_map-in-cpp-stl/)，比如 **M** 来存储具有特定值 **arr[i]^X** 的数字计数。**
*   **[使用变量 **i** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，N】**，并增加[无序映射](https://www.geeksforgeeks.org/unordered_map-in-cpp-stl/) **M** 中**arr【I】&X**的值的计数。**
*   **将变量**计数**初始化为 **0** ，以存储成对的结果计数。**
*   **[使用变量 **m** 迭代地图](https://www.geeksforgeeks.org/traversing-a-map-or-unordered_map-in-cpp-stl/) **M** ，并将**(米秒)*(米秒–1)/2**的值添加到变量**计数**中。**
*   **完成上述步骤后，打印**计数**的值作为结果。**

**下面是上述方法的实现:**

## **C++**

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the number of pairs
// that satisfy the given criteria i.e.,
// i < j and (arr[i]^arr[j] )&X is 0
int countOfPairs(int arr[], int N, int X)
{
    // Stores the resultant count
    // of pairs
    int count = 0;

    // Initializing the map M
    unordered_map<int, int> M;

    // Populating the map
    for (int i = 0; i < N; i++) {
        M[(arr[i] & X)]++;
    }

    // Count number of pairs for every
    // element in map using mathematical
    // concept of combination
    for (auto m : M) {
        int p = m.second;

        // As nC2 = n*(n-1)/2
        count += p * (p - 1) / 2;
    }

    // Return the resultant count
    return count;
}

// Driver Code
int main()
{
    int arr[] = { 3, 2, 5, 4, 6, 7 };
    int X = 6;
    int N = sizeof(arr) / sizeof(arr[0]);
    cout << countOfPairs(arr, N, X);
    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to find the number of pairs
// that satisfy the given criteria i.e.,
// i < j and (arr[i]^arr[j] )&X is 0
static int countOfPairs(int[] arr, int N, int X)
{

    // Stores the resultant count
    // of pairs
    int count = 0;

    // Initializing the map M
    HashMap<Integer,
            Integer> M = new HashMap<Integer,
                                     Integer>();

    // Populating the map
    for(int i = 0; i < N; i++)
    {
        if (M.containsKey(arr[i] & X))
            M.put((arr[i] & X),
             M.get(arr[i] & X) + 1);
        else
            M.put(arr[i] & X, 1);
    }

    // Count number of pairs for every
    // element in map using mathematical
    // concept of combination
    for(Integer entry : M.keySet())
    {
        int p = M.get(entry);

        // As nC2 = n*(n-1)/2
        count += p * (p - 1) / 2;
    }

    // Return the resultant count
    return count;
}

// Driver Code
public static void main(String[] args)
{
    int[] arr = { 3, 2, 5, 4, 6, 7 };
    int X = 6;
    int N = arr.length;

    System.out.print(countOfPairs(arr, N, X));
}
}

// This code is contributed by ukasp
```

## **蟒蛇 3**

```
# Python3 program for the above approach

# Function to find the number of pairs
# that satisfy the given criteria i.e.,
# i < j and (arr[i]^arr[j] )&X is 0
def countOfPairs(arr, N, X):

    # Stores the resultant count
    # of pairs
    count = 0

    # Initialize the dictionary M
    M = dict()

    # Populate the map
    for i in range(0, N):
        k = arr[i] & X
        if k in M:
            M[k] += 1
        else:
            M[k] = 1

    # Count number of pairs for every
    # element in map using mathematical
    # concept of combination
    for m in M.keys():
        p = M[m]

        # As nC2 = n*(n-1)/2
        count += p * (p - 1) // 2

    # Return the resultant count
    return count

# Driver Code
if __name__ == '__main__':

    arr = [ 3, 2, 5, 4, 6, 7 ]
    X = 6
    N = len(arr)

    print(countOfPairs(arr, N, X))

# This code is contributed by MuskanKalra1
```

## **C#**

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to find the number of pairs
// that satisfy the given criteria i.e.,
// i < j and (arr[i]^arr[j] )&X is 0
static int countOfPairs(int []arr, int N, int X)
{

    // Stores the resultant count
    // of pairs
    int count = 0;

    // Initializing the map M
    Dictionary<int,int> M = new Dictionary<int,int>();

    // Populating the map
    for (int i = 0; i < N; i++) {
        if(M.ContainsKey(arr[i] & X))
           M[(arr[i] & X)]++;
        else
           M.Add(arr[i] & X,1);
    }

    // Count number of pairs for every
    // element in map using mathematical
    // concept of combination
    foreach(KeyValuePair<int, int> entry in M)
    {
         int p = entry.Value;

        // As nC2 = n*(n-1)/2
        count += p * (p - 1) / 2;
    }

    // Return the resultant count
    return count;
}

// Driver Code
public static void Main()
{
    int []arr = { 3, 2, 5, 4, 6, 7 };
    int X = 6;
    int N = arr.Length;
    Console.Write(countOfPairs(arr, N, X));
}
}

// This code is contributed by ipg2016107.
```

## **java 描述语言**

```
<script>
// Javascript program for the above approach

// Function to find the number of pairs
// that satisfy the given criteria i.e.,
// i < j and (arr[i]^arr[j] )&X is 0
function countOfPairs(arr, N, X)
{

  // Stores the resultant count
  // of pairs
  let count = 0;

  // Initializing the map M
  let M = new Map();

  // Populating the map
  for (let i = 0; i < N; i++) {
    if (M.has(arr[i] & X)) {
      M.set(arr[i] & X, M.get(arr[i] & X) + 1);
    } else {
      M.set(arr[i] & X, 1);
    }
  }

  // Count number of pairs for every
  // element in map using mathematical
  // concept of combination
  for (let m of M) {
    let p = m[1];

    // As nC2 = n*(n-1)/2
    count += (p * (p - 1)) / 2;
  }

  // Return the resultant count
  return count;
}

// Driver Code
let arr = [3, 2, 5, 4, 6, 7];
let X = 6;
let N = arr.length;
document.write(countOfPairs(arr, N, X));

// This code is contributed by gfgking.
</script>
```

****Output:** 

```
3
```** 

*****时间复杂度:**O(N)**T5】
*T8】辅助空间: O(N)******
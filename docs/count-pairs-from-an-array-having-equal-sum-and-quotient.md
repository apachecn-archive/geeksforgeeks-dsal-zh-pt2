# 从具有相等和商的数组中计数对

> 原文:[https://www . geesforgeks . org/从具有等和商的数组中计数对/](https://www.geeksforgeeks.org/count-pairs-from-an-array-having-equal-sum-and-quotient/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，任务是计算有效对 **(i，j)** 的数量，使得**arr[I]+arr[j]= arr[I]/arr[j]**。

**示例:**

> **输入:** arr[] = {-4，-3，0，2，1}
> **输出:** 1
> **解释:**唯一可能的对是满足条件(-4 + 2 = -4 / 2 (= -2))的(0，3)。
> 
> **输入:** arr[] = {1，2，3，4，5}
> **输出:** 0

**天真方法:**简单的方法是[生成给定数组](https://www.geeksforgeeks.org/find-all-pairs-possible-from-the-given-array/)的所有可能的对，并计算其和等于其除的对的数量。检查后，所有对打印可能对的最终计数。

下面是上述方法的实现:

## C++14

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to count all pairs (i, j)
// such that a[i] + [j] = a[i] / a[j]
int countPairs(int a[], int n)
{
    // Stores total count of pairs
    int count = 0;

    // Generate all possible pairs
    for (int i = 0; i < n; i++) {

        for (int j = i + 1; j < n; j++) {

            if (a[j] != 0
                && a[i] % a[j] == 0) {

                // If a valid pair is found
                if ((a[i] + a[j])
                    == (a[i] / a[j]))

                    // Increment count
                    count++;
            }
        }
    }

    // Return the final count
    return count;
}

// Driver Code
int main()
{
    int arr[] = { -4, -3, 0, 2, 1 };
    int N = sizeof(arr) / sizeof(arr[0]);
    cout << countPairs(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
class GFG
{

// Function to count all pairs (i, j)
// such that a[i] + [j] = a[i] / a[j]
static int countPairs(int a[], int n)
{
    // Stores total count of pairs
    int count = 0;

    // Generate all possible pairs
    for (int i = 0; i < n; i++)
    {
        for (int j = i + 1; j < n; j++)
        {
            if (a[j] != 0
                && a[i] % a[j] == 0) {

                // If a valid pair is found
                if ((a[i] + a[j])
                    == (a[i] / a[j]))

                    // Increment count
                    count++;
            }
        }
    }

    // Return the final count
    return count;
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { -4, -3, 0, 2, 1 };
    int N = arr.length;
    System.out.print(countPairs(arr, N));
}
}

// This code is contributed by code_hunt.
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to count all pairs (i, j)
# such that a[i] + [j] = a[i] / a[j]
def countPairs(a, n):

    # Stores total count of pairs
    count = 0

    # Generate all possible pairs
    for i in range(n):
        for j in range(i + 1, n):
            if (a[j] != 0 and a[i] % a[j] == 0):

                # If a valid pair is found
                if ((a[i] + a[j]) == (a[i] // a[j])):

                    # Increment count
                    count += 1

    # Return the final count
    return count

# Driver Code
if __name__ == '__main__':
    arr =[-4, -3, 0, 2, 1]
    N = len(arr)
    print (countPairs(arr, N))

    # This code is contributed by mohit kumar 29.
```

## C#

```
// C# program for the above approach
using System;
class GFG {

  // Function to count all pairs (i, j)
  // such that a[i] + [j] = a[i] / a[j]
  static int countPairs(int[] a, int n)
  {

    // Stores total count of pairs
    int count = 0;

    // Generate all possible pairs
    for (int i = 0; i < n; i++)
    {
      for (int j = i + 1; j < n; j++)
      {
        if (a[j] != 0
            && a[i] % a[j] == 0)
        {

          // If a valid pair is found
          if ((a[i] + a[j])
              == (a[i] / a[j]))

            // Increment count
            count++;
        }
      }
    }

    // Return the final count
    return count;
  }

  // Driver code
  static void Main() {
    int[] arr = { -4, -3, 0, 2, 1 };
    int N = arr.Length;
    Console.WriteLine(countPairs(arr, N));
  }
}

// This code is contributed by divyeshrabadiya07.
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to count all pairs (i, j)
// such that a[i] + [j] = a[i] / a[j]
function countPairs(a, n)
{
    // Stores total count of pairs
    var count = 0;

    // Generate all possible pairs
    for (var i = 0; i < n; i++) {

        for (var j = i + 1; j < n; j++) {

            if (a[j] != 0
                && a[i] % a[j] == 0) {

                // If a valid pair is found
                if ((a[i] + a[j])
                    == (a[i] / a[j]))

                    // Increment count
                    count++;
            }
        }
    }

    // Return the final count
    return count;
}

// Driver Code
var arr = [-4, -3, 0, 2, 1 ];
var N = arr.length;
document.write( countPairs(arr, N));

</script>   
```

**Output:** 

```
1
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(N)*

**有效方法:**上述方法可以通过简化给定的表达式并使用[图](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)来计算满足以下简化条件的对的数量来优化:

> 假设 **X** 和 **Y** 是指数 **i** 和 **j** 中存在的数字，那么需要满足的条件是:
> T9】=>X+Y = X/Y
> T12】=>X = Y<sup>2</sup>/(1–Y)

按照以下步骤解决上述问题:

*   初始化一个变量，比如**计数**，以存储满足要求条件的所有可能对的计数。
*   初始化一个[映射](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)，以存储为每个数组元素获得的上述表达式的值的频率。
*   [使用变量 **i** 遍历给定数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，并执行以下步骤:
    *   如果 **arr[i]** 不等于 **1** 和 **0** ，则计算**arr[I]<sup>2</sup>/(1–arr[I])**，称 **X** 。
    *   将**地图**中 **X** 的频率加到**计数**上。
    *   在**地图**中通过 **1** 增加**arr【I】**的频率。
*   完成上述步骤后，打印**计数**的值作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find number of pairs
// with equal sum and quotient
// from a given array
int countPairs(int a[], int n)
{
    // Store the count of pairs
    int count = 0;

    // Stores frequencies
    map<double, int> mp;

    // Traverse the array
    for (int i = 0; i < n; i++) {

        int y = a[i];

        // If y is neither 1 or 0
        if (y != 0 && y != 1) {

            // Evaluate x
            double x = ((y * 1.0)
                        / (1 - y))
                       * y;

            // Increment count by frequency
            // of x
            count += mp[x];
        }

        // Update map
        mp[y]++;
    }

    // Print the final count
    return count;
}

// Driver Code
int main()
{
    int arr[] = { -4, -3, 0, 2, 1 };
    int N = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    cout << countPairs(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
class GFG
{

// Function to find number of pairs
// with equal sum and quotient
// from a given array
static int countPairs(int a[], int n)
{

    // Store the count of pairs
    int count = 0;

    // Stores frequencies
    HashMap<Double, Integer> mp = new HashMap<Double, Integer>();

    // Traverse the array
    for (int i = 0; i < n; i++)
    {

        double y = a[i];

        // If y is neither 1 or 0
        if (y != 0 && y != 1)
        {

            // Evaluate x
            double x = ((y * 1.0)
                        / (1 - y))
                       * y;

            // Increment count by frequency
            // of x
            if(mp.containsKey(x))
                count += mp.get(x);
        }

        // Update map
        if(mp.containsKey(y)){
            mp.put(y, mp.get(y)+1);
        }
        else{
            mp.put(y, 1);
        }
    }

    // Print the final count
    return count;
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { -4, -3, 0, 2, 1 };
    int N = arr.length;

    // Function Call
    System.out.print(countPairs(arr, N));

}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find number of pairs
# with equal sum and quotient
# from a given array
def countPairs(a, n) :

    # Store the count of pairs
    count = 0

    # Stores frequencies
    mp = {}

    # Traverse the array
    for i in range(n):

        y = a[i]

        # If y is neither 1 or 0
        if (y != 0 and y != 1) :

            # Evaluate x
            x = (((y * 1.0)
                        // (1 - y))
                       * y)

            # Increment count by frequency
            # of x
            count += mp.get(x, 0)

        # Update map
        mp[y]  = mp.get(y, 0) + 1

    # Prthe final count
    return count

# Driver Code

arr = [ -4, -3, 0, 2, 1 ]
N = len(arr)

# Function Call
print(countPairs(arr, N))

# This code is contributed by susmitakundugoaldanga.
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;
class GFG
{

  // Function to find number of pairs
  // with equal sum and quotient
  // from a given array
  static int countPairs(int[] a, int n)
  {

    // Store the count of pairs
    int count = 0;

    // Stores frequencies
    Dictionary<double, int> mp
      = new Dictionary<double, int>();

    // Traverse the array
    for (int i = 0; i < n; i++) {

      int y = a[i];

      // If y is neither 1 or 0
      if (y != 0 && y != 1) {

        // Evaluate x
        double x = ((y * 1.0) / (1 - y)) * y;

        // Increment count by frequency
        // of x
        if (!mp.ContainsKey(x))
          mp[x] = 0;

        count += mp[x];
      }

      // Update map
      if (!mp.ContainsKey(y))
        mp[y] = 0;

      mp[y]++;
    }

    // Print the final count
    return count;
  }

  // Driver Code
  public static void Main()
  {
    int[] arr = { -4, -3, 0, 2, 1 };
    int N = arr.Length;

    // Function Call
    Console.Write(countPairs(arr, N));
  }
}

// This code is contributed by ukasp.
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to find number of pairs
// with equal sum and quotient
// from a given array
function countPairs(a, n)
{

    // Store the count of pairs
    let count = 0;

    // Stores frequencies
    let mp = new Map();

    // Traverse the array
    for (let i = 0; i < n; i++)
    {

        let y = a[i];

        // If y is neither 1 or 0
        if (y != 0 && y != 1)
        {

            // Evaluate x
            let x = ((y * 1.0)
                        / (1 - y))
                       * y;

            // Increment count by frequency
            // of x
            if(mp.has(x))
                count += mp.get(x);
        }

        // Update map
        if(mp.has(y)){
            mp.set(y, mp.get(y)+1);
        }
        else{
            mp.set(y, 1);
        }
    }

    // Print the final count
    return count;
}

// Driver Code

    let arr = [ -4, -3, 0, 2, 1 ];
    let N = arr.length;

    // Function Call
    document.write(countPairs(arr, N));

</script>          
```

**Output:** 

```
1
```

***时间复杂度:** O(N*log N)*
***辅助空间:** O(N)*
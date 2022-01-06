# 从按位“或”大于按位“与”的数组中计数对

> 原文:[https://www . geesforgeks . org/count-pairs-from-from-from-from-from-from-from-from-from-from-from-from-from-from-from-from-from-from-from-from-from-from-from-from-](https://www.geeksforgeeks.org/count-pairs-from-an-array-whose-bitwise-or-is-greater-than-bitwise-and/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/array-data-structure/)**A【】**，任务是计算对 **(i，j)** 的个数，使得 **i < j** ，[按位 OR](https://www.geeksforgeeks.org/bitwise-or-or-of-a-range/) 的**A【I】**和**A【j】的**大于**A【I】的[按位 AND](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)**

**示例:**

> **输入:** A[] = {1，4，7}
> **输出:** 3
> **说明:**
> 有 3 个这样的对:(1，4)、(4，7)、(1，7)。
> 1)1 | 4(= 5)>1&4(= 0)
> 2)4 | 7(= 7)>4&7(= 4)
> 3)1 | 7(= 7)>1&7(= 1)
> 
> **输入:** A[] = {3，3，3}
> **输出:** 0
> **说明:**不存在这样的对。

**简单方法:**最简单的方法是[从给定的数组](https://www.geeksforgeeks.org/find-all-pairs-possible-from-the-given-array/)中生成所有可能的对，对于每个对 **(i，j)** ，如果它满足给定的条件，那么将**计数**增加 **1** 。检查所有对后，打印**计数**的值作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to count the number of
// pairs (i, j) their Bitwise OR is
// greater than Bitwise AND
void countPairs(int A[], int n)
{
    // Store the required answer
    int count = 0;

    // Check for all possible pairs
    for (int i = 0; i < n; i++) {

        for (int j = i + 1; j < n; j++)

            // If the condition satisfy
            // then increment count by 1
            if ((A[i] | A[j])
                > (A[i] & A[j])) {
                count++;
            }
    }

    // Print the answer
    cout << count;
}

// Driver Code
int main()
{
    int A[] = { 1, 4, 7 };
    int N = sizeof(A) / sizeof(A[0]);

    // Function Call
    countPairs(A, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;
class GFG{

  // Function to count the number of
  // pairs (i, j) their Bitwise OR is
  // greater than Bitwise AND
  static void countPairs(int A[], int n)
  {
    // Store the required answer
    int count = 0;

    // Check for all possible pairs
    for (int i = 0; i < n; i++) {

      for (int j = i + 1; j < n; j++)

        // If the condition satisfy
        // then increment count by 1
        if ((A[i] | A[j])
            > (A[i] & A[j])) {
          count++;
        }
    }

    // Print the answer
    System.out.println(count);
  }

  // Driver Code
  public static void main(String args[])
  {
    int A[] = { 1, 4, 7 };
    int N = A.length;

    // Function Call
    countPairs(A, N);
  }
}

// This code is contributed by splevel62.
```

## 蟒蛇 3

```
# Python program to implement
# the above approach

# Function to count the number of
# pairs (i, j) their Bitwise OR is
# greater than Bitwise AND
def countPairs(A, n):

    # Store the required answer
    count = 0;

    # Check for all possible pairs
    for i in range(n):
        for j in range(i + 1, n):

            # If the condition satisfy
            # then increment count by 1
            if ((A[i] | A[j]) > (A[i] & A[j])):
                count += 1;

    # Prthe answer
    print(count);

# Driver Code
if __name__ == '__main__':
    A = [1, 4, 7];
    N = len(A);

    # Function Call
    countPairs(A, N);

    # This code is contributed by 29AjayKumar
```

## C#

```
// C# program to implement
// the above approach
using System;
class GFG
{
  // Function to count the number of
  // pairs (i, j) their Bitwise OR is
  // greater than Bitwise AND
  static void countPairs(int[] A, int n)
  {
    // Store the required answer
    int count = 0;

    // Check for all possible pairs
    for (int i = 0; i < n; i++) {

      for (int j = i + 1; j < n; j++)

        // If the condition satisfy
        // then increment count by 1
        if ((A[i] | A[j])
            > (A[i] & A[j])) {
          count++;
        }
    }

    // Print the answer
    Console.Write(count);
}

// Driver Code
public static void Main()
{
    int[] A = { 1, 4, 7 };
    int N = A.Length;

    // Function Call
    countPairs(A, N);
}
}

// This code is contributed by susmitakundugoaldanga.
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to count the number of
// pairs (i, j) their Bitwise OR is
// greater than Bitwise AND
function countPairs( A, n)
{
    // Store the required answer
    var count = 0;

    // Check for all possible pairs
    for (var i = 0; i < n; i++) {

        for (var j = i + 1; j < n; j++)

            // If the condition satisfy
            // then increment count by 1
            if ((A[i] | A[j])
                > (A[i] & A[j])) {
                count++;
            }
    }

    // Print the answer
    document.write( count);
}

// Driver Code
var A = [ 1, 4, 7 ];
var N = A.length;
// Function Call
countPairs(A, N);

</script>
```

**Output:** 

```
3
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*

**高效途径:**优化上述途径，思路是基于观察到只有 **Ai** 和 **Aj** 不同时，才满足条件 **Ai | Aj > Ai & Aj** 。如果 **Ai** 等于 **Aj** ，那么 **Ai | Aj = Ai & Aj** 。条件 **Ai | Aj < Ai & Aj** 从未满足。因此，这个问题可以通过从可能的对的总数中减去具有相等值的对的数量来解决。按照以下步骤解决问题:

*   初始化一个变量，比如说**计数**，用**N *(N–1)/2**表示可能对的总数。
*   初始化一个 [hashmap](https://www.geeksforgeeks.org/java-util-hashmap-in-java/) ，说 **M** 来存储各个阵元的[频率。](https://www.geeksforgeeks.org/counting-frequencies-of-array-elements/)
*   [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **arr[]** ，对于每个数组元素 **arr[i]** ，将 **M** 中 **arr[i]** 的频率增加 **1** 。
*   现在，[遍历 hashmap](https://www.geeksforgeeks.org/traversing-a-map-or-unordered_map-in-cpp-stl/) **M** ，对于每个键 **K** ，及其对应的值 **X** ，从**计数**中减去**(X *(X–1))/2**的值。
*   完成上述步骤后，打印**计数**的值作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to count the number of
// pairs (i, j) their Bitwise OR is
// greater than Bitwise AND
void countPairs(int A[], int n)
{
    // Total number of pairs
    // possible from the array
    long long count = (n * (n - 1)) / 2;

    // Stores frequency of each array element
    unordered_map<long long, long long> ump;

    // Traverse the array A[]
    for (int i = 0; i < n; i++) {

        // Increment ump[A[i]] by 1
        ump[A[i]]++;
    }

    // Traverse the Hashmap ump
    for (auto it = ump.begin();
         it != ump.end(); ++it) {

        // Subtract those pairs (i, j)
        // from count which has the
        // same element on index i
        // and j (i < j)
        long long c = it->second;
        count = count - (c * (c - 1)) / 2;
    }

    // Print the result
    cout << count;
}

// Driver Code
int main()
{
    int A[] = { 1, 4, 7 };
    int N = sizeof(A) / sizeof(A[0]);

    // Function Call
    countPairs(A, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
class GFG
{

// Function to count the number of
// pairs (i, j) their Bitwise OR is
// greater than Bitwise AND
static void countPairs(int A[], int n)
{
    // Total number of pairs
    // possible from the array
    int count = (n * (n - 1)) / 2;

    // Stores frequency of each array element
    Map<Integer,Integer> mp = new HashMap<>();

    // Traverse the array A[]
    for (int i = 0 ; i < n; i++){
        if(mp.containsKey(A[i])){
            mp.put(A[i], mp.get(A[i])+1);
        }
        else{
            mp.put(A[i], 1);
        }
    }

    // Traverse the Hashmap ump
    for (Map.Entry<Integer,Integer> it : mp.entrySet()){

        // Subtract those pairs (i, j)
        // from count which has the
        // same element on index i
        // and j (i < j)
        int c = it.getValue();
        count = count - (c * (c - 1)) / 2;
    }

    // Print the result
    System.out.print(count);
}

// Driver Code
public static void main(String[] args)
{
    int A[] = { 1, 4, 7 };
    int N = A.length;

    // Function Call
    countPairs(A, N);
}
}

// This code is contributed by shikhasingrajput
```

## 蟒蛇 3

```
# Python 3 program for the above approach
from collections import defaultdict

# Function to count the number of
# pairs (i, j) their Bitwise OR is
# greater than Bitwise AND
def countPairs(A, n):

    # Total number of pairs
    # possible from the array
    count = (n * (n - 1)) // 2

    # Stores frequency of each array element
    ump = defaultdict(int)

    # Traverse the array A[]
    for i in range(n):

        # Increment ump[A[i]] by 1
        ump[A[i]] += 1

    # Traverse the Hashmap ump
    for it in ump.keys():

        # Subtract those pairs (i, j)
        # from count which has the
        # same element on index i
        # and j (i < j)
        c = ump[it]
        count = count - (c * (c - 1)) // 2

    # Print the result
    print(count)

# Driver Code
if __name__ == "__main__":

    A = [1, 4, 7]
    N = len(A)

    # Function Call
    countPairs(A, N)

    # This code is contributed by chitranayal.
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;
class GFG
{

  // Function to count the number of
  // pairs (i, j) their Bitwise OR is
  // greater than Bitwise AND
  static void countPairs(int[] A, int n)
  {

    // Total number of pairs
    // possible from the array
    long count = (n * (n - 1)) / 2;

    // Stores frequency of each array element
    Dictionary<long, long> ump = new Dictionary<long, long>();

    // Traverse the array A[]
    for (int i = 0; i < n; i++)
    {

      // Increment ump[A[i]] by 1
      if(ump.ContainsKey(A[i]))
      {
        ump[A[i]]++;
      }
      else{
        ump[A[i]] = 1;
      }
    }

    // Traverse the Hashmap ump
    foreach(KeyValuePair<long, long> it in ump)
    {

      // Subtract those pairs (i, j)
      // from count which has the
      // same element on index i
      // and j (i < j)
      long c = it.Value;
      count = count - (c * (c - 1)) / 2;
    }

    // Print the result
    Console.WriteLine(count);
  }

  // Driver code
  static void Main() {
    int[] A = { 1, 4, 7 };
    int N = A.Length;

    // Function Call
    countPairs(A, N);
  }
}

// This code is contributed by divyeshrabadiya07.
```

## java 描述语言

```
<script>
// Javascript program for the above approach

  // Function to count the number of
  // pairs (i, j) their Bitwise OR is
  // greater than Bitwise AND
  function countPairs(A, n)
  {

    // Total number of pairs
    // possible from the array
    var count = (n * (n - 1)) / 2;

    // Stores frequency of each array element
    var ump = new Map();

    // Traverse the array A[]
    for (var i = 0; i < n; i++)
    {

      // Increment ump[A[i]] by 1
      if(ump.has(A[i]))
      {
        ump.set(A[i], ump.get(A[i])+1);
      }
      else{
        ump.set(A[i], 1);
      }
    }

    // Traverse the Hashmap ump
    for(var it of ump)
    {

      // Subtract those pairs (i, j)
      // from count which has the
      // same element on index i
      // and j (i < j)
      var c = it[1];
      count = count - (c * (c - 1)) / 2;
    }

    // Print the result
    document.write(count + "<br>");
  }

  // Driver code
    var A = [1, 4, 7];
    var N = A.length;

    // Function Call
    countPairs(A, N);

// This code is contributed by rutvik_56.
</script>
```

**Output:** 

```
3
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)
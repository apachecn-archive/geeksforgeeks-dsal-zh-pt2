# 计算具有偶数和的整数对

> 原文:[https://www . geesforgeks . org/count-对整数有偶数和/](https://www.geeksforgeeks.org/count-pair-of-integers-having-even-sum/)

给定两个整数 **N** 和 **M** ，任务是统计所有可能的整数对 **(i，j)** (1 ≤ i ≤ N，1 ≤ j ≤ M)，使得 **i + j** 为偶数。

**示例:**

> **输入:** N = 6，M = 4
> **输出:** 12
> **说明:**对(1，1)，(1，3)，(2，2)，(2，4)，(3，1)，(3，3)，(4，2)，(4，4)，(5，1)，(5，3)，(6，2)，(6，4)满足要求条件。因此，计数为 12。
> 
> **输入:** N = 2，M = 8
> T3】输出: 8

**天真方法:**解决这个问题最简单的方法是遍历范围**【1，M】**对于该范围内的每个数字，遍历范围**【1，N】**并生成所有可能的对。对于每一个可能的对，检查它的和是否为偶数。如果发现为真，则增加计数。最后，打印获得的计数。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <iostream>
using namespace std;

// Function to count pairs with even sum
int countEvenPairs(int N, int M)
{

    // Stores the count of pairs
    // with even sum
    int count = 0;

    // Traverse the range 1 to N
    for(int i = 1; i <= N; i++)
    {

        // Traverse the range 1 to M
        for(int j = 1; j <= M; j++)
        {

            // Check if the sum of the
            // pair (i, j) is even or not
            if ((i + j) % 2 == 0)
            {

                // Update count
                count++;
            }
        }
    }

    // Return the count
    return count;
}

// Driver Code
int main()
{
    int N = 4;
    int M = 6;

    cout << countEvenPairs(N, M) << endl;

    return 0;
}

// This code is contributed by akhilsaini
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;

class GFG {

    // Function to count pairs with even sum
    public static int countEvenPairs(
        int N, int M)
    {

        // Stores the count of pairs
        // with even sum
        int count = 0;

        // Traverse the range 1 to N
        for (int i = 1; i <= N; i++) {

            // Traverse the range 1 to M
            for (int j = 1; j <= M; j++) {

                // Check if the sum of the
                // pair (i, j) is even or not
                if ((i + j) % 2 == 0) {

                    // Update count
                    count++;
                }
            }
        }

        // Return the count
        return count;
    }

    // Driver Code
    public static void main(String[] args)
    {
        int N = 4;
        int M = 6;
        System.out.print(
            countEvenPairs(N, M));
    }
}
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to count pairs with even sum
def countEvenPairs(N, M):

    # Stores the count of pairs
    # with even sum
    count = 0

    # Traverse the range 1 to N
    for i in range(1, N + 1):

        # Traverse the range 1 to M
        for j in range(1, M + 1):

            # Check if the sum of the
            # pair (i, j) is even or not
            if ((i + j) % 2 == 0):

                # Update count
                count += 1

    # Return the count
    return count

# Driver Code
if __name__ == '__main__':

  N = 4
  M = 6

  print(countEvenPairs(N, M))

# This code is contributed by akhilsaini
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to count pairs with even sum
public static int countEvenPairs(int N, int M)
{

    // Stores the count of pairs
    // with even sum
    int count = 0;

    // Traverse the range 1 to N
    for(int i = 1; i <= N; i++)
    {

        // Traverse the range 1 to M
        for(int j = 1; j <= M; j++)
        {

            // Check if the sum of the
            // pair (i, j) is even or not
            if ((i + j) % 2 == 0)
            {

                // Update count
                count++;
            }
        }
    }

    // Return the count
    return count;
}

// Driver Code
public static void Main()
{
    int N = 4;
    int M = 6;

    Console.WriteLine(
        countEvenPairs(N, M));
}
}

// This code is contributed by akhilsaini
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to count pairs with even sum
function countEvenPairs(N, M)
{

    // Stores the count of pairs
    // with even sum
    var count = 0;

    // Traverse the range 1 to N
    for(var i = 1; i <= N; i++)
    {

        // Traverse the range 1 to M
        for(var j = 1; j <= M; j++)
        {

            // Check if the sum of the
            // pair (i, j) is even or not
            if ((i + j) % 2 == 0)
            {

                // Update count
                count++;
            }
        }
    }

    // Return the count
    return count;
}

// Driver code
var N = 4;
var M = 6;

document.write(countEvenPairs(N, M));

// This code is contributed by Kirti

</script>
```

**Output:** 

```
12
```

***时间复杂度:**O(N<sup>2</sup>)*
***空间复杂度:** O(1)*

**高效方法:**上述方法可以基于以下观察进行优化:

> *   **even number+even number = even number**
> *   **Odd+Odd = Even**

按照以下步骤解决问题:

*   初始化两个变量，比如 **nEven** 和 **nOdd** ，来存储奇数和偶数的计数直到 **N** 。
*   初始化两个变量，比如 **mEven** 和 **mOdd** ，来存储偶数和奇数的计数直到 **M** 。
*   最后，使用以下公式计算所需的对数:

> **计数 = nEven * mEven + nOdd * mOdd**

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to count even pairs
int countEvenPairs(int N, int M)
{

    // Stores count of pairs having even sum
    int count = 0;

    // Stores count of even numbers up to N
    int nEven = floor(N / 2);

    // Stores count of odd numbers up to N
    int nOdd = ceil(N / 2);

    // Stores count of even numbers up to M
    int mEven = floor(M / 2);

    // Stores count of odd numbers up to M
    int mOdd = ceil(M / 2);
    count = nEven * mEven + nOdd * mOdd;

    // Return the count
    return count;
}

// Driver Code
int main()
{
    int N = 4;
    int M = 6;
    cout << countEvenPairs(N, M);
    return 0;
}

// This code is contributed by Dharanendra L V
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;

class GFG {

    // Function to count even pairs
    public static int countEvenPairs(
        int N, int M)
    {

        // Stores count of pairs having even sum
        int count = 0;

        // Stores count of even numbers up to N
        int nEven = (int)Math.floor((double)N / 2);

        // Stores count of odd numbers up to N
        int nOdd = (int)Math.ceil((double)N / 2);

        // Stores count of even numbers up to M
        int mEven = (int)Math.floor((double)M / 2);

        // Stores count of odd numbers up to M
        int mOdd = (int)Math.ceil((double)M / 2);

        count = nEven * mEven + nOdd * mOdd;

        // Return the count
        return count;
    }

    // Driver Code
    public static void main(String[] args)
    {
        int N = 4;
        int M = 6;
        System.out.print(countEvenPairs(N, M));
    }
}
```

## 蟒蛇 3

```
# Python3 program for the above approach
import math

# Function to count even pairs
def countEvenPairs(N, M):

    # Stores count of pairs having even sum
    count = 0;

    # Stores count of even numbers up to N
    nEven = int(math.floor(N / 2));

    # Stores count of odd numbers up to N
    nOdd = int(math.ceil(N / 2));

    # Stores count of even numbers up to M
    mEven = int(math.floor(M / 2));

    # Stores count of odd numbers up to M
    mOdd = int(math.ceil(M / 2));

    count = nEven * mEven + nOdd * mOdd;

    # Return the count
    return count;

# Driver Code
if __name__ == '__main__':
    N = 4;
    M = 6;
    print(countEvenPairs(N, M));

# This code is contributed by 29AjayKumar
```

## C#

```
// C# program for the above approach
using System;

class GFG
{

  // Function to count even pairs
  public static int countEvenPairs(int N, int M)
  {

    // Stores count of pairs having even sum
    int count = 0;

    // Stores count of even numbers up to N
    int nEven = (int)Math.Floor((double)N / 2);

    // Stores count of odd numbers up to N
    int nOdd = (int)Math.Ceiling((double)N / 2);

    // Stores count of even numbers up to M
    int mEven = (int)Math.Floor((double)M / 2);

    // Stores count of odd numbers up to M
    int mOdd = (int)Math.Ceiling((double)M / 2);
    count = nEven * mEven + nOdd * mOdd;

    // Return the count
    return count;
  }

  // Driver Code
  public static void Main(String[] args)
  {
    int N = 4;
    int M = 6;
    Console.Write(countEvenPairs(N, M));
  }
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to count even pairs
function countEvenPairs(N, M)
{

    // Stores count of pairs having even sum
    let count = 0;

    // Stores count of even numbers up to N
    nEven = parseInt(Math.floor(N / 2));

    // Stores count of odd numbers up to N
    nOdd = parseInt(Math.ceil(N / 2));

    // Stores count of even numbers up to M
    mEven = parseInt(Math.floor(M / 2));

    // Stores count of odd numbers up to M
    mOdd = parseInt(Math.ceil(M / 2));

    count = nEven * mEven + nOdd * mOdd;

    // Return the count
    return count;
}

// Driver Code
let N = 4;
let M = 6;

document.write(countEvenPairs(N, M));

// This code is contributed by mohan1240760

</script>
```

**Output:** 

```
12
```

***时间复杂度:**O(1)*
T5**辅助空间:** O(1)
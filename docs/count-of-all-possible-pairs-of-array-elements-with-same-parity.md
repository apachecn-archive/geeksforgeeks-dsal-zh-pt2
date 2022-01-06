# 具有相同奇偶性的所有可能的阵列元素对的计数

> 原文:[https://www . geeksforgeeks . org/具有相同奇偶校验的所有可能数组元素对的计数/](https://www.geeksforgeeks.org/count-of-all-possible-pairs-of-array-elements-with-same-parity/)

给定一个整数数组 **A[]** ，任务是找到配对的总数，使得每对包含偶数或奇数元素。有效对( **A[ i ]** 、 **A[ j ]** )只有在 **i 时才能形成！= j** 。

**示例:**

> **输入:** A[ ] = {1，2，3，1，3}
> **输出:** 6
> **解释:**
> 可能的奇数对= (1，3)、(1，1)、(1，3)、(3，1)、(3，3)、(1，3) = 6
> 可能的偶数对= 0
> 因此，总对= 6 + 0 = 6
> 
> **输入:** A[ ] = {8，2，3，1，4，2 }
> T3】输出 : 7
> **解释:**
> 可能的奇数对= (3，1) = 1
> 可能的偶数对= (8，2)，(8，4)，(8，2)，(2，4)，(2)，(4，2) = 6
> 因此，总对= 6 + 1 = 7

**天真方法:**
最简单的方法是生成所有可能的对。对于每一对，检查两个元素是奇数还是偶数。如果是，增加一个计数器。最终的计数将是所需的答案。

***时间复杂度:** O(N <sup>2</sup> )*

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the answer
int countPairs(int A[], int n)
{
    int count = 0, i, j;

    // Generate all possible pairs
    for(i = 0; i < n; i++)
    {
        for(j = i + 1; j < n; j++)
        {

            // Increment the count if
            // both even or both odd
            if ((A[i] % 2 == 0 &&
                 A[j] % 2 == 0) ||
                (A[i] % 2 != 0 &&
                 A[j] % 2 != 0))
                count++;
        }
    }
    return count;
}

// Driver Code
int main()
{
    int A[] = { 1, 2, 3, 1, 3 };
    int n = sizeof(A) / sizeof(int);

    cout << countPairs(A, n);
}

// This code is contributed by jrishabh99
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for above approach

import java.util.*;

class GFG {

    static int countPairs(
        int[] A, int n)
    {
        int count = 0, i, j;

        // Generate all possible pairs
        for (i = 0; i < n; i++) {
            for (j = i + 1; j < n; j++) {

                // Increment the count if
                // both even or both odd
                if ((A[i] % 2 == 0
                     && A[j] % 2 == 0)
                    || (A[i] % 2 != 0
                        && A[j] % 2 != 0))
                    count++;
            }
        }
        return count;
    }

    // Driver Code
    public static void main(
        String[] args)
    {
        int[] A = { 1, 2, 3, 1, 3 };
        int n = A.length;
        System.out.println(
            countPairs(A, n));
    }
}
```

## 蟒蛇 3

```
# Python3 program for
# the above approach

# Function to return the answer
def countPairs(A, n):

    count = 0

    # Generate all possible pairs
    for i in range (n):
        for j in range (i + 1, n):

            # Increment the count if
            # both even or both odd
            if ((A[i] % 2 == 0 and
                 A[j] % 2 == 0) or
                (A[i] % 2 != 0 and
                 A[j] % 2 != 0)):
                count += 1

    return count

# Driver Code
if __name__ == "__main__":

    A = [1, 2, 3, 1, 3]
    n = len(A)
    print(countPairs(A, n))

# This code is contributed by Chitranayal
```

## C#

```
// C# program for above approach
using System;
class GFG{

static int countPairs(int[] A, int n)
{
    int count = 0, i, j;

    // Generate all possible pairs
    for (i = 0; i < n; i++)
    {
        for (j = i + 1; j < n; j++)
        {

            // Increment the count if
            // both even or both odd
            if ((A[i] % 2 == 0 && A[j] % 2 == 0) ||
                (A[i] % 2 != 0 && A[j] % 2 != 0))
                count++;
        }
    }
    return count;
}

// Driver Code
public static void Main(String[] args)
{
    int[] A = { 1, 2, 3, 1, 3 };
    int n = A.Length;
    Console.Write(countPairs(A, n));
}
}

// This code is contributed by shivanisinghss2110
```

## java 描述语言

```
<script>

// Javascript program for above approach
function countPairs(A, n)
{
    let count = 0, i, j;

    // Generate all possible pairs
    for(i = 0; i < n; i++)
    {
        for(j = i + 1; j < n; j++)
        {

            // Increment the count if
            // both even or both odd
            if ((A[i] % 2 == 0 && A[j] % 2 == 0) ||
                (A[i] % 2 != 0 && A[j] % 2 != 0))
                count++;
        }
    }
    return count;
}

// Driver code
let A = [ 1, 2, 3, 1, 3 ];
let n = A.length;

document.write(countPairs(A, n));

// This code is contributed by rameshtravel07

</script>
```

**Output:** 

```
6
```

**高效方法:**
遍历数组，计数并存储数组中的偶数和奇数，根据各自的计数计算可能的对，并显示它们的总和。

> 设数组中偶数和奇数元素的个数分别为 EC 和 OC。
> 偶对数=(EC *(EC–1))/2
> 奇对数=(OC *(OC–1))/2
> 因此，可能对的总数=((EC *(EC–1))+(OC *(OC–1)))/2

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

int countPairs(int A[], int n)
{

    // Store count of
    // even and odd elements
    int even = 0, odd = 0;

    for(int i = 0; i < n; i++)
    {
        if (A[i] % 2 == 0)
            even++;
        else
            odd++;
    }

    return (even * (even - 1)) / 2 +
             (odd * (odd - 1)) / 2;
}

// Driver code
int main()
{
    int A[] = { 1, 2, 3, 1, 3 };
    int n = sizeof(A) / sizeof(int);

    cout << countPairs(A, n);
}

// This code is contributed by jrishabh99
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

import java.util.*;

class GFG {

    static int countPairs(
        int[] A, int n)
    {
        // Store count of
        // even and odd elements
        int even = 0, odd = 0;

        for (int i = 0; i < n; i++) {

            if (A[i] % 2 == 0)
                even++;
            else
                odd++;
        }

        return (even * (even - 1)) / 2
            + (odd * (odd - 1)) / 2;
    }

    // Driver Program
    public static void main(
        String[] args)
    {

        int[] A = { 1, 2, 3, 1, 3 };
        int n = A.length;
        System.out.println(
            countPairs(A, n));
    }
}
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to return count of pairs
def countPairs(A, n):

    # Store count of
    # even and odd elements
    even, odd = 0, 0

    for i in range(0, n):
        if A[i] % 2 == 0:
            even = even + 1
        else:
            odd = odd + 1

    return ((even * (even - 1)) // 2 +
              (odd * (odd - 1)) // 2)

# Driver code
A = [ 1, 2, 3, 1, 3 ]
n = len(A)

print(countPairs(A, n))

# This code is contributed by jrishabh99
```

## C#

```
// C# program for the above approach
using System;

class GFG{

static int countPairs(int[] A, int n)
{

    // Store count of
    // even and odd elements
    int even = 0, odd = 0;

    for(int i = 0; i < n; i++)
    {
    if (A[i] % 2 == 0)
        even++;
    else
        odd++;
    }

    return (even * (even - 1)) / 2 +
            (odd * (odd - 1)) / 2;
}

// Driver code
public static void Main()
{
    int[] A = { 1, 2, 3, 1, 3 };
    int n = A.Length;

    Console.Write(countPairs(A, n));
}
}

// This code is contributed by nidhi_biet
```

## java 描述语言

```
<script>

    // Javascript program for the above approach

    function countPairs(A, n)
    {

        // Store count of
        // even and odd elements
        let even = 0, odd = 0;

        for(let i = 0; i < n; i++)
        {
            if (A[i] % 2 == 0)
                even++;
            else
                odd++;
        }

        return (even * (even - 1)) / 2 + (odd * (odd - 1)) / 2;
    }

    let A = [ 1, 2, 3, 1, 3 ];
    let n = A.length;

    document.write(countPairs(A, n));

</script>
```

**Output:** 

```
6
```

***时间复杂度:**O(N)*T4】
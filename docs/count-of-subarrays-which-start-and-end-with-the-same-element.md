# 以相同元素开始和结束的子阵列的计数

> 原文:[https://www . geeksforgeeks . org/子数组计数-以相同的元素开始和结束/](https://www.geeksforgeeks.org/count-of-subarrays-which-start-and-end-with-the-same-element/)

给定一个大小为 **N** 的数组 **A** ，其中数组元素包含从 **1 到 N** 的重复值，任务是找出以相同元素开始和结束的子数组的总数。

**示例:**

> **输入:** A[] = {1，2，1，5，2}
> **输出:** 7
> **说明:**
> 给定数组的共 7 个子数组为{1}、{2}、{1}、{5}、{2}、{1，2，1}和{2，1，5，2}以相同元素开始和结束。
> **输入:** A[] = {1，5，6，1，9，5，8，10，8，9}
> **输出:** 14
> **说明:**
> 共 14 个子阵列{1}、{5}、{6}、{1}、{9}、{5}、{8}、{10}、{8}、{9}、{1，5，6，1}、{ 9 }

**天真的方法:**对于数组中的每个元素，如果它也出现在不同的索引中，我们将把结果增加 1。此外，所有 1 尺寸子阵列都是计算结果的一部分。因此，在结果中加上 N。

下面是上述方法的实现:

## C++

```
// C++ program to Count total sub-array
// which start and end with same element

#include <bits/stdc++.h>
using namespace std;

// Function to find total sub-array
// which start and end with same element
void cntArray(int A[], int N)
{
    // initialize result with 0
    int result = 0;

    for (int i = 0; i < N; i++) {

        // all size 1 sub-array
        // is part of our result
        result++;

        // element at current index
        int current_value = A[i];

        for (int j = i + 1; j < N; j++) {

            // Check if A[j] = A[i]
            // increase result by 1
            if (A[j] == current_value) {
                result++;
            }
        }
    }

    // print the result
    cout << result << endl;
}

// Driver code
int main()
{
    int A[] = { 1, 5, 6, 1, 9,
                5, 8, 10, 8, 9 };
    int N = sizeof(A) / sizeof(int);

    cntArray(A, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to Count total sub-array
// which start and end with same element

public class Main {

    // function to find total sub-array
    // which start and end with same element
    public static void cntArray(int A[], int N)
    {
        // initialize result with 0
        int result = 0;

        for (int i = 0; i < N; i++) {

            // all size 1 sub-array
            // is part of our result
            result++;

            // element at current index
            int current_value = A[i];

            for (int j = i + 1; j < N; j++) {

                // Check if A[j] = A[i]
                // increase result by 1
                if (A[j] == current_value) {
                    result++;
                }
            }
        }

        // print the result
        System.out.println(result);
    }

    // Driver code
    public static void main(String[] args)
    {
        int[] A = { 1, 5, 6, 1, 9,
                    5, 8, 10, 8, 9 };
        int N = A.length;
        cntArray(A, N);
    }
}
```

## 蟒蛇 3

```
# Python3 program to count total sub-array
# which start and end with same element

# Function to find total sub-array
# which start and end with same element
def cntArray(A, N):

    # Initialize result with 0
    result = 0

    for i in range(0, N):

        # All size 1 sub-array
        # is part of our result
        result = result + 1

        # Element at current index
        current_value = A[i]

        for j in range(i + 1, N):

            # Check if A[j] = A[i]
            # increase result by 1
            if (A[j] == current_value):
                result = result + 1

    # Print the result
    print(result)
    print("\n")

# Driver code
A = [ 1, 5, 6, 1, 9, 5, 8, 10, 8, 9 ]
N = len(A)

cntArray(A, N)

# This code is contributed by PratikBasu
```

## C#

```
// C# program to Count total sub-array
// which start and end with same element
using System;
class GFG{

// function to find total sub-array
// which start and end with same element
public static void cntArray(int []A, int N)
{
    // initialize result with 0
    int result = 0;

    for (int i = 0; i < N; i++)
    {

        // all size 1 sub-array
        // is part of our result
        result++;

        // element at current index
        int current_value = A[i];

        for (int j = i + 1; j < N; j++)
        {

            // Check if A[j] = A[i]
            // increase result by 1
            if (A[j] == current_value)
            {
                result++;
            }
        }
    }

    // print the result
    Console.Write(result);
}

// Driver code
public static void Main()
{
    int[] A = { 1, 5, 6, 1, 9,
                5, 8, 10, 8, 9 };
    int N = A.Length;
    cntArray(A, N);
}
}

// This code is contributed by Code_Mech
```

## java 描述语言

```
<script>

// Javascript program to Count total sub-array
// which start and end with same element

// Function to find total sub-array
// which start and end with same element
function cntArray(A, N)
{
    // initialize result with 0
    var result = 0;

    for (var i = 0; i < N; i++) {

        // all size 1 sub-array
        // is part of our result
        result++;

        // element at current index
        var current_value = A[i];

        for (var j = i + 1; j < N; j++) {

            // Check if A[j] = A[i]
            // increase result by 1
            if (A[j] == current_value) {
                result++;
            }
        }
    }

    // print the result
    document.write( result );
}

// Driver code
var A = [1, 5, 6, 1, 9,
            5, 8, 10, 8, 9];
var N = A.length;
cntArray(A, N);

// This code is contributed by noob2000.
</script>
```

**Output:** 

```
14
```

***时间复杂度:** O(N <sup>2</sup> )* ，其中 N 是数组的大小
***空间复杂度:** O(1)*

**高效方法:**我们可以通过观察到答案只是依赖于原始数组中数字的**频率来优化上述方法。
*例如*在数组{1，5，6，1，9，5，8，10，8，9}中，1 的频率为 2，贡献答案的子数组分别为{1}、{1}和{1，5，6，1}，共 3 个。
因此，计算数组中每个元素的频率。然后，对于每个元素，用以下公式产生的结果增加计数:**

> ((元素的频率)*(元素的频率+ 1)) / 2

下面是上述方法的实现:

## C++

```
// C++ program to Count total sub-array
// which start and end with same element

#include <bits/stdc++.h>
using namespace std;

// function to find total sub-array
// which start and end with same element
void cntArray(int A[], int N)
{
    // initialize result with 0
    int result = 0;

    // array to count frequency of 1 to N
    int frequency[N + 1] = { 0 };

    for (int i = 0; i < N; i++) {
        // update frequency of A[i]
        frequency[A[i]]++;
    }

    for (int i = 1; i <= N; i++) {
        int frequency_of_i = frequency[i];

        // update result with sub-array
        // contributed by number i
        result += +((frequency_of_i)
                    * (frequency_of_i + 1))
                  / 2;
    }

    // print the result
    cout << result << endl;
}

// Driver code
int main()
{
    int A[] = { 1, 5, 6, 1, 9, 5,
                8, 10, 8, 9 };
    int N = sizeof(A) / sizeof(int);

    cntArray(A, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to Count total sub-array
// which start and end with same element

public class Main {

    // function to find total sub-array which
    // start and end with same element
    public static void cntArray(int A[], int N)
    {
        // initialize result with 0
        int result = 0;

        // array to count frequency of 1 to N
        int[] frequency = new int[N + 1];

        for (int i = 0; i < N; i++) {
            // update frequency of A[i]
            frequency[A[i]]++;
        }

        for (int i = 1; i <= N; i++) {
            int frequency_of_i = frequency[i];

            // update result with sub-array
            // contributed by number i
            result += ((frequency_of_i)
                       * (frequency_of_i + 1))
                      / 2;
        }

        // print the result
        System.out.println(result);
    }

    // Driver code
    public static void main(String[] args)
    {

        int[] A = { 1, 5, 6, 1, 9, 5,
                    8, 10, 8, 9 };
        int N = A.length;
        cntArray(A, N);
    }
}
```

## 蟒蛇 3

```
# Python3 program to count total sub-array
# which start and end with same element

# Function to find total sub-array
# which start and end with same element
def cntArray(A, N):

    # Initialize result with 0
    result = 0

    # Array to count frequency of 1 to N
    frequency = [0] * (N + 1)

    for i in range(0, N):

        # Update frequency of A[i]
        frequency[A[i]] = frequency[A[i]] + 1

    for i in range(1, N + 1):
        frequency_of_i = frequency[i]

        # Update result with sub-array
        # contributed by number i
        result = result + ((frequency_of_i) *
                           (frequency_of_i + 1)) / 2

    # Print the result
    print(int(result))
    print("\n")

# Driver code
A = [ 1, 5, 6, 1, 9, 5, 8, 10, 8, 9 ]
N = len(A)

cntArray(A, N)

# This code is contributed by PratikBasu
```

## C#

```
// C# program to Count total sub-array
// which start and end with same element
using System;
class GFG{

// function to find total sub-array which
// start and end with same element
public static void cntArray(int []A, int N)
{
    // initialize result with 0
    int result = 0;

    // array to count frequency of 1 to N
    int[] frequency = new int[N + 1];

    for (int i = 0; i < N; i++)
    {
        // update frequency of A[i]
        frequency[A[i]]++;
    }

    for (int i = 1; i <= N; i++)
    {
        int frequency_of_i = frequency[i];

        // update result with sub-array
        // contributed by number i
        result += ((frequency_of_i) *
                   (frequency_of_i + 1)) / 2;
    }

    // print the result
    Console.Write(result);
}

// Driver code
public static void Main()
{
    int[] A = { 1, 5, 6, 1, 9, 5,
                8, 10, 8, 9 };
    int N = A.Length;
    cntArray(A, N);
}
}

// This code is contributed by Nidhi_Biet
```

## java 描述语言

```
<script>

// Javascript program to Count total sub-array
// which start and end with same element

   // function to find total sub-array which
    // start and end with same element
    function cntArray(A, N)
    {
        // initialize result with 0
        let result = 0;

        // array to count frequency of 1 to N
        let frequency = Array.from({length: N+1}, (_, i) => 0);

        for (let i = 0; i < N; i++) {
            // update frequency of A[i]
            frequency[A[i]]++;
        }

        for (let i = 1; i <= N; i++) {
            let frequency_of_i = frequency[i];

            // update result with sub-array
            // contributed by number i
            result += ((frequency_of_i)
                       * (frequency_of_i + 1))
                      / 2;
        }

        // prlet the result
        document.write(result);
    }

// Driver Code

    let A = [ 1, 5, 6, 1, 9, 5,
                    8, 10, 8, 9 ];
        let N = A.length;
        cntArray(A, N);

</script>
```

**Output:** 

```
14
```

***时间复杂度:** O(N)* ，其中 N 为阵的大小
***空间复杂度:** O(N)*
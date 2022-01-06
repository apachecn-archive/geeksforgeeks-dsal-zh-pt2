# 从给定数组中计数给定类型的四倍

> 原文:[https://www . geeksforgeeks . org/count-四倍给定类型从给定数组/](https://www.geeksforgeeks.org/count-quadruples-of-given-type-from-given-array/)

## C++

```
// C++ program of the
// above approach

#include <cstring>
#include <iostream>

using namespace std;
const int maxN = 2002;

// lcount[i][j]: Stores the count of
// i on left of index j
int lcount[maxN][maxN];

// rcount[i][j]: Stores the count of
// i on right of index j
int rcount[maxN][maxN];

// Function to count unique elements
// on left and right of any index
void fill_counts(int a[], int n)
{
    int i, j;

    // Find the maximum array element
    int maxA = a[0];

    for (i = 0; i < n; i++) {
        if (a[i] > maxA) {
            maxA = a[i];
        }
    }

    memset(lcount, 0, sizeof(lcount));
    memset(rcount, 0, sizeof(rcount));

    for (i = 0; i < n; i++) {
        lcount[a[i]][i] = 1;
        rcount[a[i]][i] = 1;
    }

    for (i = 0; i <= maxA; i++) {

        // Calculate prefix sum of
        // counts of each value
        for (j = 0; j < n; j++) {
            lcount[i][j] = lcount[i][j - 1]
                           + lcount[i][j];
        }

        // Calculate suffix sum of
        // counts of each value
        for (j = n - 2; j >= 0; j--) {
            rcount[i][j] = rcount[i][j + 1]
                           + rcount[i][j];
        }
    }
}

// Function to count quadruples
// of the required type
int countSubsequence(int a[], int n)
{
    int i, j;
    fill_counts(a, n);
    int answer = 0;
    for (i = 1; i < n; i++) {
        for (j = i + 1; j < n - 1; j++) {

            answer += lcount[a[j]][i - 1]
                      * rcount[a[i]][j + 1];
        }
    }

    return answer;
}

// Driver Code
int main()
{
    int a[7] = { 1, 2, 3, 2, 1, 3, 2 };
    cout << countSubsequence(a, 7);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program of the
// above approach
import java.util.*;
class GFG{

static int maxN = 2002;

// lcount[i][j]: Stores the
// count of i on left of index j
static int [][]lcount =
       new int[maxN][maxN];

// rcount[i][j]: Stores the
// count of i on right of index j
static int [][]rcount =
       new int[maxN][maxN];

// Function to count unique
// elements on left and right
// of any index
static void fill_counts(int a[],
                        int n)
{
  int i, j;

  // Find the maximum
  // array element
  int maxA = a[0];

  for (i = 0; i < n; i++)
  {
    if (a[i] > maxA)
    {
      maxA = a[i];
    }
  }

  for (i = 0; i < n; i++)
  {
    lcount[a[i]][i] = 1;
    rcount[a[i]][i] = 1;
  }

  for (i = 0; i <= maxA; i++)
  {
    // Calculate prefix sum of
    // counts of each value
    for (j = 1; j < n; j++)
    {
      lcount[i][j] = lcount[i][j - 1] +
                     lcount[i][j];
    }

    // Calculate suffix sum of
    // counts of each value
    for (j = n - 2; j >= 0; j--)
    {
      rcount[i][j] = rcount[i][j + 1] +
                     rcount[i][j];
    }
  }
}

// Function to count quadruples
// of the required type
static int countSubsequence(int a[],
                            int n)
{
  int i, j;
  fill_counts(a, n);
  int answer = 0;
  for (i = 1; i < n; i++)
  {
    for (j = i + 1; j < n - 1; j++)
    {
      answer += lcount[a[j]][i - 1] *
                rcount[a[i]][j + 1];
    }
  }

  return answer;
}

// Driver Code
public static void main(String[] args)
{
  int a[] = {1, 2, 3, 2, 1, 3, 2};
  System.out.print(
  countSubsequence(a, a.length));
}
}

// This code is contributed by shikhasingrajput
```

## 蟒蛇 3

```
# Python3 program of the
# above approach

maxN = 2002;

# lcount[i][j]: Stores the
# count of i on left of index j
lcount = [[0 for i in range(maxN)] for j in range(maxN)]

# rcount[i][j]: Stores the
# count of i on right of index j
rcount = [[0 for i in range(maxN)] for j in range(maxN)]

# Function to count unique
# elements on left and right
# of any index
def fill_counts(a, n):

    # Find the maximum
    # array element
    maxA = a[0];

    for i in range(n):
        if (a[i] > maxA):
            maxA = a[i];

    for i in range(n):
        lcount[a[i]][i] = 1;
        rcount[a[i]][i] = 1;

    for i in range(maxA + 1):

        # Calculate prefix sum of
        # counts of each value
        for j in range(1, n):
            lcount[i][j] = lcount[i][j - 1] + lcount[i][j];

        # Calculate suffix sum of
        # counts of each value
        for j in range(n - 2, 0, -1):
            rcount[i][j] = rcount[i][j + 1] + rcount[i][j];

# Function to count quadruples
# of the required type
def countSubsequence(a, n):
    fill_counts(a, n);
    answer = 0;
    for i in range(1, n):
        for j in range(i + 1, n - 1):
            answer += lcount[a[j]][i - 1] * rcount[a[i]][j + 1];

    return answer;

# Driver Code
if __name__ == '__main__':
    a = [1, 2, 3, 2, 1, 3, 2];
    print(countSubsequence(a, len(a)));

# This code contributed by gauravrajput1
```

## C#

```
// C# program of the
// above approach
using System;

class GFG{

static int maxN = 2002;

// lcount[i][j]: Stores the
// count of i on left of index j
static int[, ] lcount = new int[maxN, maxN];

// rcount[i][j]: Stores the
// count of i on right of index j
static int[, ] rcount = new int[maxN, maxN];

// Function to count unique
// elements on left and right
// of any index
static void fill_counts(int[] a, int n)
{
    int i, j;

    // Find the maximum
    // array element
    int maxA = a[0];

    for(i = 0; i < n; i++)
    {
        if (a[i] > maxA)
        {
            maxA = a[i];
        }
    }

    for(i = 0; i < n; i++)
    {
        lcount[a[i], i] = 1;
        rcount[a[i], i] = 1;
    }

    for(i = 0; i <= maxA; i++)
    {

        // Calculate prefix sum of
        // counts of each value
        for(j = 1; j < n; j++)
        {
            lcount[i, j] = lcount[i, j - 1] +
                           lcount[i, j];
        }

        // Calculate suffix sum of
        // counts of each value
        for(j = n - 2; j >= 0; j--)
        {
            rcount[i, j] = rcount[i, j + 1] +
                           rcount[i, j];
        }
    }
}

// Function to count quadruples
// of the required type
static int countSubsequence(int[] a, int n)
{
    int i, j;
    fill_counts(a, n);
    int answer = 0;

    for(i = 1; i < n; i++)
    {
        for(j = i + 1; j < n - 1; j++)
        {
            answer += lcount[a[j], i - 1] *
                      rcount[a[i], j + 1];
        }
    }
    return answer;
}

// Driver Code
public static void Main(string[] args)
{
    int[] a = { 1, 2, 3, 2, 1, 3, 2 };

    Console.Write(countSubsequence(a, a.Length));
}
}

// This code is contributed by chitranayal
```

## java 描述语言

```
<script>
// Javascript program of the
// above approach
let maxN = 2002;

// lcount[i][j]: Stores the
// count of i on left of index j
let lcount = new Array(maxN);

// rcount[i][j]: Stores the
// count of i on right of index j
let rcount = new Array(maxN);
for(let i = 0; i < maxN; i++)
{
    lcount[i] = new Array(maxN);
    rcount[i] = new Array(maxN);
    for(let j = 0; j < maxN; j++)
    {
        lcount[i][j] = 0;
        rcount[i][j] = 0;
    }
}

// Function to count unique
// elements on left and right
// of any index
function fill_counts(a, n)
{
    let i, j;

  // Find the maximum
  // array element
  let maxA = a[0];

  for (i = 0; i < n; i++)
  {
    if (a[i] > maxA)
    {
      maxA = a[i];
    }
  }

  for (i = 0; i < n; i++)
  {
    lcount[a[i]][i] = 1;
    rcount[a[i]][i] = 1;
  }

  for (i = 0; i <= maxA; i++)
  {
    // Calculate prefix sum of
    // counts of each value
    for (j = 1; j < n; j++)
    {
      lcount[i][j] = lcount[i][j - 1] +
                     lcount[i][j];
    }

    // Calculate suffix sum of
    // counts of each value
    for (j = n - 2; j >= 0; j--)
    {
      rcount[i][j] = rcount[i][j + 1] +
                     rcount[i][j];
    }
  }
}

// Function to count quadruples
// of the required type
function countSubsequence(a,n)
{
    let i, j;
  fill_counts(a, n);
  let answer = 0;
  for (i = 1; i < n; i++)
  {
    for (j = i + 1; j < n - 1; j++)
    {
      answer += lcount[a[j]][i - 1] *
                rcount[a[i]][j + 1];
    }
  }

  return answer;
}

// Driver Code
let a = [1, 2, 3, 2, 1, 3, 2];
document.write(countSubsequence(a, a.length));

// This code is contributed by avanitrachhadiya2155
</script>
```

**输出:**

```
5
```

给定一个[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**，任务是从给定数组中找到表格 **a[i] = a[k]** 和**a[j]= a[l]**(0**<= I<j<k<l<= N**)的[四倍数](https://www.geeksforgeeks.org/count-unique-subsequences-of-length-k/)。

**示例:**

> **输入:** arr[] = {1，2，4，2，1，5，2}
> **输出:** 2
> **解释:**四元组{1，2，1，2}在数组中出现两次，索引为{0，1，4，6}和{0，3，4，6}。因此，所需的计数是 2。
> 
> **输入:** arr[] = {1，2，3，2，1，3，2}
> **输出:** 5
> **解释:**四重{1，2，1，2}在数组中的索引{0，1，4，6}和{0，3，4，6}处出现两次。四倍{1，3，1，3}、{3，2，3，2}和{2，3，2，3}各出现一次。因此，所需的计数是 5。

**天真方法:**解决问题最简单的方法是迭代检查[给定数组](https://www.geeksforgeeks.org/print-all-possible-combinations-of-r-elements-in-a-given-array-of-size-n/)中 4 个元素的所有组合，并检查它是否满足给定条件。

下面是上述方法的实现:

## C++

```
// C++ program of the
// above approach

#include <iostream>
using namespace std;

const int maxN = 2002;

// Function to find the count of
// the subsequence of given type
int countSubsequece(int a[], int n)
{
    int i, j, k, l;

    // Stores the count
    // of quadruples
    int answer = 0;

    // Generate all possible
    // combinations of quadruples
    for (i = 0; i < n; i++) {
        for (j = i + 1; j < n; j++) {
            for (k = j + 1; k < n; k++) {
                for (l = k + 1; l < n; l++) {

                    // Check if 1st element is
                    // equal to 3rd element
                    if (a[j] == a[l] &&

                        // Check if 2nd element is
                        // equal to 4th element
                        a[i] == a[k]) {
                        answer++;
                    }
                }
            }
        }
    }
    return answer;
}

// Driver Code
int main()
{
    int a[7] = { 1, 2, 3, 2, 1, 3, 2 };
    cout << countSubsequece(a, 7);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program of the
// above approach
import java.util.*;

class GFG{

// Function to find the count of
// the subsequence of given type
static int countSubsequece(int a[], int n)
{
    int i, j, k, l;

    // Stores the count
    // of quadruples
    int answer = 0;

    // Generate all possible
    // combinations of quadruples
    for(i = 0; i < n; i++)
    {
        for(j = i + 1; j < n; j++)
        {
            for(k = j + 1; k < n; k++)
            {
                for(l = k + 1; l < n; l++)
                {

                    // Check if 1st element is
                    // equal to 3rd element
                    if (a[j] == a[l] &&

                        // Check if 2nd element is
                        // equal to 4th element
                        a[i] == a[k])
                    {
                        answer++;
                    }
                }
            }
        }
    }
    return answer;
}

// Driver code
public static void main(String[] args)
{
    int[] a = { 1, 2, 3, 2, 1, 3, 2 };

    System.out.print(countSubsequece(a, 7));
}
}

// This code is contributed by code_hunt
```

## 蟒蛇 3

```
# Python3 program of the
# above approach
maxN = 2002

# Function to find the count of
# the subsequence of given type
def countSubsequece(a, n):

    # Stores the count
    # of quadruples
    answer = 0

    # Generate all possible
    # combinations of quadruples
    for i in range(n):
        for j in range(i + 1, n):
            for k in range(j + 1, n):
                for l in range(k + 1, n):

                    # Check if 1st element is
                    # equal to 3rd element
                    if (a[j] == a[l] and

                        # Check if 2nd element is
                        # equal to 4th element
                        a[i] == a[k]):
                        answer += 1

    return answer

# Driver Code
if __name__ == '__main__':

    a = [ 1, 2, 3, 2, 1, 3, 2 ]

    print(countSubsequece(a, 7))

# This code is contributed by bgangwar59
```

## C#

```
// C# program of the
// above approach
using System;

class GFG{

// Function to find the count of
// the subsequence of given type
static int countSubsequece(int[] a, int n)
{
    int i, j, k, l;

    // Stores the count
    // of quadruples
    int answer = 0;

    // Generate all possible
    // combinations of quadruples
    for(i = 0; i < n; i++)
    {
        for(j = i + 1; j < n; j++)
        {
            for(k = j + 1; k < n; k++)
            {
                for(l = k + 1; l < n; l++)
                {

                    // Check if 1st element is
                    // equal to 3rd element
                    if (a[j] == a[l] &&

                        // Check if 2nd element is
                        // equal to 4th element
                        a[i] == a[k])
                    {
                        answer++;
                    }
                }
            }
        }
    }
    return answer;
}

// Driver Code
public static void Main()
{
    int[] a = { 1, 2, 3, 2, 1, 3, 2 };

    Console.WriteLine(countSubsequece(a, 7));
}
}

// This code is contributed by susmitakundugoaldanga
```

## java 描述语言

```
<script>
    // Javascript program of the above approach

    // Function to find the count of
    // the subsequence of given type
    function countSubsequece(a, n)
    {
        let i, j, k, l;

        // Stores the count
        // of quadruples
        let answer = 0;

        // Generate all possible
        // combinations of quadruples
        for(i = 0; i < n; i++)
        {
            for(j = i + 1; j < n; j++)
            {
                for(k = j + 1; k < n; k++)
                {
                    for(l = k + 1; l < n; l++)
                    {

                        // Check if 1st element is
                        // equal to 3rd element
                        if (a[j] == a[l] &&

                            // Check if 2nd element is
                            // equal to 4th element
                            a[i] == a[k])
                        {
                            answer++;
                        }
                    }
                }
            }
        }
        return answer;
    }

    let a = [ 1, 2, 3, 2, 1, 3, 2 ];
    document.write(countSubsequece(a, 7));

    // This code is contributed by mukesh07.
</script>
```

**Output:** 

```
5
```

***时间复杂度:**O(N<sup>4</sup>)*
***辅助空间:** O(1)*

**高效方式:**对上述方式进行优化，思路是维护两个[数组](https://www.geeksforgeeks.org/arrays-in-c-cpp/)在每个索引的左右两边存储元素 **X** 的计数。按照以下步骤解决问题:

*   维护两个[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**l count【I】【j】**和**r count【I】【j】**，它们将元素 **i** 的计数存储在小于 **j** 的索引中，而**r count【I】【j】**将元素 **i** 的计数存储在大于 **j** 的索引中。
*   从 1 到 N 迭代嵌套循环，找到 XYXY 类型的所有子序列

```
answer += lcount[a[i]][j-1] * rcount[a[j]][i-1]
```

下面是上述方法的实现:

## C++

```
// C++ program of the
// above approach

#include <cstring>
#include <iostream>

using namespace std;
const int maxN = 2002;

// lcount[i][j]: Stores the count of
// i on left of index j
int lcount[maxN][maxN];

// rcount[i][j]: Stores the count of
// i on right of index j
int rcount[maxN][maxN];

// Function to count unique elements
// on left and right of any index
void fill_counts(int a[], int n)
{
    int i, j;

    // Find the maximum array element
    int maxA = a[0];

    for (i = 0; i < n; i++) {
        if (a[i] > maxA) {
            maxA = a[i];
        }
    }

    memset(lcount, 0, sizeof(lcount));
    memset(rcount, 0, sizeof(rcount));

    for (i = 0; i < n; i++) {
        lcount[a[i]][i] = 1;
        rcount[a[i]][i] = 1;
    }

    for (i = 0; i <= maxA; i++) {

        // Calculate prefix sum of
        // counts of each value
        for (j = 0; j < n; j++) {
            lcount[i][j] = lcount[i][j - 1]
                           + lcount[i][j];
        }

        // Calculate suffix sum of
        // counts of each value
        for (j = n - 2; j >= 0; j--) {
            rcount[i][j] = rcount[i][j + 1]
                           + rcount[i][j];
        }
    }
}

// Function to count quadruples
// of the required type
int countSubsequence(int a[], int n)
{
    int i, j;
    fill_counts(a, n);
    int answer = 0;
    for (i = 1; i < n; i++) {
        for (j = i + 1; j < n - 1; j++) {

            answer += lcount[a[j]][i - 1]
                      * rcount[a[i]][j + 1];
        }
    }

    return answer;
}

// Driver Code
int main()
{
    int a[7] = { 1, 2, 3, 2, 1, 3, 2 };
    cout << countSubsequence(a, 7);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program of the
// above approach
import java.util.*;

class GFG{
static int maxN = 2002;

// lcount[i][j]: Stores the
// count of i on left of index j
static int [][]lcount =
       new int[maxN][maxN];

// rcount[i][j]: Stores the
// count of i on right of index j
static int [][]rcount =
       new int[maxN][maxN];

// Function to count unique
// elements on left and right
// of any index
static void fill_counts(int a[],
                        int n)
{
  int i, j;

  // Find the maximum
  // array element
  int maxA = a[0];

  for (i = 0; i < n; i++)
  {
    if (a[i] > maxA)
    {
      maxA = a[i];
    }
  }

  for (i = 0; i < n; i++)
  {
    lcount[a[i]][i] = 1;
    rcount[a[i]][i] = 1;
  }

  for (i = 0; i <= maxA; i++)
  {
    // Calculate prefix sum of
    // counts of each value
    for (j = 1; j < n; j++)
    {
      lcount[i][j] = lcount[i][j - 1] +
                     lcount[i][j];
    }

    // Calculate suffix sum of
    // counts of each value
    for (j = n - 2; j >= 0; j--)
    {
      rcount[i][j] = rcount[i][j + 1] +
                     rcount[i][j];
    }
  }
}

// Function to count quadruples
// of the required type
static int countSubsequence(int a[],
                            int n)
{
  int i, j;
  fill_counts(a, n);
  int answer = 0;
  for (i = 1; i < n; i++)
  {
    for (j = i + 1; j < n - 1; j++)
    {
      answer += lcount[a[j]][i - 1] *
                rcount[a[i]][j + 1];
    }
  }

  return answer;
}

// Driver Code
public static void main(String[] args)
{
  int a[] = {1, 2, 3, 2, 1, 3, 2};
  System.out.print(
  countSubsequence(a, a.length));
}
}

// This code is contributed by shikhasingrajput
```

## 蟒蛇 3

```
# Python3 program of the
# above approach
maxN = 2002

# lcount[i][j]: Stores the count of
# i on left of index j
lcount = [[0 for i in range(maxN)]
             for j in range(maxN)]

# rcount[i][j]: Stores the count of
# i on right of index j
rcount = [[0 for i in range(maxN)]
             for j in range(maxN)]

# Function to count unique elements
# on left and right of any index
def fill_counts(a, n):

    # Find the maximum array element
    maxA = a[0]

    for i in range(n):
        if (a[i] > maxA):
            maxA = a[i]

    for i in range(n):
        lcount[a[i]][i] = 1
        rcount[a[i]][i] = 1

    for i in range(maxA + 1):

        # Calculate prefix sum of
        # counts of each value
        for j in range(n) :
            lcount[i][j] = (lcount[i][j - 1] +
                            lcount[i][j])

        # Calculate suffix sum of
        # counts of each value
        for j in range(n - 2, -1, -1):
            rcount[i][j] = (rcount[i][j + 1] + 
                            rcount[i][j])

# Function to count quadruples
# of the required type
def countSubsequence(a, n):

    fill_counts(a, n)
    answer = 0

    for i in range(1, n):
        for j in range(i + 1, n - 1):
            answer += (lcount[a[j]][i - 1] *
                       rcount[a[i]][j + 1])

    return answer

# Driver Code
a = [ 1, 2, 3, 2, 1, 3, 2 ]

print(countSubsequence(a, 7))

# This code is contributed by divyesh072019
```

## C#

```
// C# program of the
// above approach
using System;

class GFG{

static int maxN = 2002;

// lcount[i,j]: Stores the
// count of i on left of index j
static int [,]lcount = new int[maxN, maxN];

// rcount[i,j]: Stores the
// count of i on right of index j
static int [,]rcount = new int[maxN, maxN];

// Function to count unique
// elements on left and right
// of any index
static void fill_counts(int []a,
                        int n)
{
    int i, j;

    // Find the maximum
    // array element
    int maxA = a[0];

    for(i = 0; i < n; i++)
    {
        if (a[i] > maxA)
        {
            maxA = a[i];
        }
    }

    for(i = 0; i < n; i++)
    {
        lcount[a[i], i] = 1;
        rcount[a[i], i] = 1;
    }

    for(i = 0; i <= maxA; i++)
    {

        // Calculate prefix sum of
        // counts of each value
        for (j = 1; j < n; j++)
        {
            lcount[i, j] = lcount[i, j - 1] +
                           lcount[i, j];
        }

        // Calculate suffix sum of
        // counts of each value
        for(j = n - 2; j >= 0; j--)
        {
            rcount[i, j] = rcount[i, j + 1] +
                           rcount[i, j];
        }
    }
}

// Function to count quadruples
// of the required type
static int countSubsequence(int []a,
                            int n)
{
    int i, j;
    fill_counts(a, n);

    int answer = 0;

    for(i = 1; i < n; i++)
    {
        for(j = i + 1; j < n - 1; j++)
        {
            answer += lcount[a[j], i - 1] *
                      rcount[a[i], j + 1];
        }
    }
    return answer;
}

// Driver Code
public static void Main(String[] args)
{
    int []a = { 1, 2, 3, 2, 1, 3, 2 };

    Console.Write(
        countSubsequence(a, a.Length));
}
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>
// Javascript program of the
// above approach
let maxN = 2002;

// lcount[i][j]: Stores the
// count of i on left of index j
let lcount = new Array(maxN);

// rcount[i][j]: Stores the
// count of i on right of index j
let rcount = new Array(maxN);

for(let i = 0; i < maxN; i++)
{
    lcount[i] = new Array(maxN);
    rcount[i] = new Array(maxN);
    for(let j = 0; j < maxN; j++)
    {
        lcount[i][j] = 0;
        rcount[i][j] = 0;
    }

}

// Function to count unique
// elements on left and right
// of any index
function fill_counts(a,n)
{
    let i, j;

  // Find the maximum
  // array element
  let maxA = a[0];

  for (i = 0; i < n; i++)
  {
    if (a[i] > maxA)
    {
      maxA = a[i];
    }
  }

  for (i = 0; i < n; i++)
  {
    lcount[a[i]][i] = 1;
    rcount[a[i]][i] = 1;
  }

  for (i = 0; i <= maxA; i++)
  {
    // Calculate prefix sum of
    // counts of each value
    for (j = 1; j < n; j++)
    {
      lcount[i][j] = lcount[i][j - 1] +
                     lcount[i][j];
    }

    // Calculate suffix sum of
    // counts of each value
    for (j = n - 2; j >= 0; j--)
    {
      rcount[i][j] = rcount[i][j + 1] +
                     rcount[i][j];
    }
  }
}

// Function to count quadruples
// of the required type
function countSubsequence(a,n)
{
    let i, j;
  fill_counts(a, n);
  let answer = 0;
  for (i = 1; i < n; i++)
  {
    for (j = i + 1; j < n - 1; j++)
    {
      answer += lcount[a[j]][i - 1] *
                rcount[a[i]][j + 1];
    }
  }

  return answer;
}

// Driver Code
let a=[1, 2, 3, 2, 1, 3, 2];
document.write(countSubsequence(a, a.length));

// This code is contributed by rag2127
</script>
```

**Output:** 

```
5
```

**时间复杂度:**O(N<sup>2</sup>)
T5】辅助空间: O(N <sup>2</sup>
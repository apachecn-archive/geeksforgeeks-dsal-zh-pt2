# 使矩阵所有元素相等的给定类型的最小运算

> 原文:[https://www . geesforgeks . org/给定类型的最小运算使矩阵的所有元素相等/](https://www.geeksforgeeks.org/minimum-operations-of-given-type-to-make-all-elements-of-a-matrix-equal/)

给定一个整数 **K** 和一个由 **N** 行和 **M** 列组成的矩阵，任务是找到使矩阵所有元素相等所需的**最小**运算次数。在一次操作中， **K** 可以添加到矩阵的任何元素中，也可以从矩阵的任何元素中减去。如果不可能打印 **-1** 。

**示例:**

> **输入:** mat[][] = {{2，4}，{22，24}}，K = 2
> **输出:**20
> mat[0][0]= 2+(10 * K)= 22…10 运算
> mat[0][1] = 4 + (9 * K) = 22 … 9 运算
> mat[1][0] = 22 …无运算
> mat[1][1]= 24–K = 22…1
> 
> **输入:** mat[][] = {
> {3，63，42}，
> {18，12，12}，
> {15，21，18}，
> {33，84，24}}，
> K = 3
> **输出:** 63

**方法:**由于我们只允许对任意元素进行 **K** 的加减运算，因此我们很容易推断出所有带有 **K** 的元素的 **mod** 应该相等，因为**x % K =(x+K)% K =(x–K)% K**。
如果不是这样，只需打印 **-1** 。否则，以非递减顺序对矩阵的所有元素进行排序，并找到排序元素的中间值。如果我们将所有元素转换为等于中值，将会出现最少的步数。计算这些步骤并打印结果。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the minimum
// number of operations required
int minOperations(int n, int m, int k,
                  vector<vector<int> >& matrix)
{
    // Create another array to
    // store the elements of matrix
    vector<int> arr(n * m, 0);

    int mod = matrix[0][0] % k;

    for (int i = 0; i < n; ++i) {
        for (int j = 0; j < m; ++j) {
            arr[i * m + j] = matrix[i][j];

            // If not possible
            if (matrix[i][j] % k != mod) {
                return -1;
            }
        }
    }

    // Sort the array to get median
    sort(arr.begin(), arr.end());

    int median = arr[(n * m) / 2];

    // To count the minimum operations
    int minOperations = 0;
    for (int i = 0; i < n * m; ++i)
        minOperations += abs(arr[i] - median) / k;

    // If there are even elements, then there
    // are two medians. We consider the best
    // of two as answer.
    if ((n * m) % 2 == 0)
    {
       int median2 = arr[( (n * m) / 2) - 1];
       int minOperations2 = 0;
       for (int i = 0; i < n * m; ++i)
          minOperations2 += abs(arr[i] - median2) / k;

       minOperations = min(minOperations, minOperations2);
    }

    // Return minimum operations required
    return minOperations;
}

// Driver code
int main()
{
    vector<vector<int> > matrix = { { 2, 4, 6 },
                                    { 8, 10, 12 },
                                    { 14, 16, 18 },
                                    { 20, 22, 24 } };
    int n = matrix.size();
    int m = matrix[0].size();
    int k = 2;
    cout << minOperations(n, m, k, matrix);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{
    // Function to return the minimum
    // number of operations required
    static int minOperations(int n, int m,
                        int k, int matrix[][])
    {
        // Create another array to
        // store the elements of matrix
        int [] arr = new int[n * m];

        int mod = matrix[0][0] % k;

        for (int i = 0; i < n; ++i)
        {
            for (int j = 0; j < m; ++j)
            {
                arr[i * m + j] = matrix[i][j];

                // If not possible
                if (matrix[i][j] % k != mod)
                {
                    return -1;
                }
            }
        }

        // Sort the array to get median
        Arrays.sort(arr);

        int median = arr[(n * m) / 2];

        // To count the minimum operations
        int minOperations = 0;
        for (int i = 0; i < n * m; ++i)
            minOperations += Math.abs(arr[i] - median) / k;

        // If there are even elements, then there
        // are two medians. We consider the best
        // of two as answer.
        if ((n * m) % 2 == 0)
        {
        int median2 = arr[( (n * m) / 2 ) - 1];
        int minOperations2 = 0;
        for (int i = 0; i < n * m; ++i)
            minOperations2 += Math.abs(arr[i] - median2) / k;

        minOperations = Math.min(minOperations, minOperations2);
        }

        // Return minimum operations required
        return minOperations;
    }

    // Driver code
    public static void main(String []args)
    {
        int matrix [][] = { { 2, 4, 6 },
                            { 8, 10, 12 },
                            { 14, 16, 18 },
                            { 20, 22, 24 } };

        int n = matrix.length;
        int m = matrix[0].length;
        int k = 2;
        System.out.println(minOperations(n, m, k, matrix));
    }
}

// This code is contributed by ihritik
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the minimum
# number of operations required
def minOperations(n, m, k, matrix):

    # Create another array to store the
    # elements of matrix
    arr = [0] * (n * m)

    mod = matrix[0][0] % k

    for i in range(0, n):
        for j in range(0, m):
            arr[i * m + j] = matrix[i][j]

            # If not possible
            if matrix[i][j] % k != mod:
                return -1

    # Sort the array to get median
    arr.sort()

    median = arr[(n * m) // 2]

    # To count the minimum operations
    minOperations = 0
    for i in range(0, n * m):
        minOperations += abs(arr[i] - median) // k

    # If there are even elements, then there
    # are two medians. We consider the best
    # of two as answer.
    if (n * m) % 2 == 0:

        median2 = arr[( (n * m) // 2  ) - 1]
        minOperations2 = 0
        for i in range(0, n * m):
            minOperations2 += abs(arr[i] - median2) // k

        minOperations = min(minOperations,
                            minOperations2)

    # Return minimum operations required
    return minOperations

# Driver code
if __name__ == "__main__":

    matrix = [[2, 4, 6],
              [8, 10, 12],
              [14, 16, 18],
              [20, 22, 24]]

    n = len(matrix)
    m = len(matrix[0])
    k = 2
    print(minOperations(n, m, k, matrix))

# This code is contributed by Rituraj Jain
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{
    // Function to return the minimum
    // number of operations required
    static int minOperations(int n, int m,
                        int k, int [,]matrix)
    {

        // Create another array to
        // store the elements of matrix
        int []arr = new int[n * m];

        int mod = matrix[0, 0] % k;

        for (int i = 0; i < n; ++i)
        {
            for (int j = 0; j < m; ++j)
            {
                arr[i * m + j] = matrix[i,j];

                // If not possible
                if (matrix[i,j] % k != mod)
                {
                    return -1;
                }
            }
        }

        // Sort the array to get median
        Array.Sort(arr);

        int median = arr[(n * m) / 2];

        // To count the minimum operations
        int minOperations = 0;
        for (int i = 0; i < n * m; ++i)
            minOperations += Math.Abs(arr[i] - median) / k;

        // If there are even elements, then there
        // are two medians. We consider the best
        // of two as answer.
        if ((n * m) % 2 == 0)
        {
            int median2 = arr[( (n * m) / 2 ) - 1];
            int minOperations2 = 0;
            for (int i = 0; i < n * m; ++i)
                minOperations2 += Math.Abs(arr[i] - median2) / k;

            minOperations = Math.Min(minOperations, minOperations2);
        }

        // Return minimum operations required
        return minOperations;
    }

    // Driver code
    public static void Main()
    {
        int [,]matrix = { { 2, 4, 6 },
                            { 8, 10, 12 },
                            { 14, 16, 18 },
                            { 20, 22, 24 } };

        int n = matrix.GetLength(0);
        int m = matrix.GetLength(1);
        int k = 2;
        Console.WriteLine(minOperations(n, m, k, matrix));
    }
}

// This code is contributed by Ryuga
```

## java 描述语言

```
<script>
    // Javascript implementation of the approach

    // Function to return the minimum
    // number of operations required
    function minOperations(n, m, k, matrix)
    {
        // Create another array to
        // store the elements of matrix
        let arr = new Array(n * m);
        arr.fill(0);

        let mod = matrix[0][0] % k;

        for (let i = 0; i < n; ++i)
        {
            for (let j = 0; j < m; ++j)
            {
                arr[i * m + j] = matrix[i][j];

                // If not possible
                if (matrix[i][j] % k != mod)
                {
                    return -1;
                }
            }
        }

        // Sort the array to get median
        arr.sort(function(a, b){return a - b});

        let median = arr[parseInt((n * m) / 2, 10)];

        // To count the minimum operations
        let minOperations = 0;
        for (let i = 0; i < n * m; ++i)
            minOperations += parseInt(Math.abs(arr[i] - median) / k, 10);

        // If there are even elements, then there
        // are two medians. We consider the best
        // of two as answer.
        if ((n * m) % 2 == 0)
        {
          let median2 = arr[parseInt((n * m) / 2, 10)];
          let minOperations2 = 0;
          for (let i = 0; i < n * m; ++i)
              minOperations2 += parseInt(Math.abs(arr[i] - median2) / k, 10);

          minOperations = Math.min(minOperations, minOperations2);
        }

        // Return minimum operations required
        return minOperations;
    }

    // Driver code
    let matrix = [ [ 2, 4, 6 ],
                   [ 8, 10, 12 ],
                   [ 14, 16, 18 ],
                   [ 20, 22, 24 ] ];

    let n = 4;
    let m = 3;
    let k = 2;
    document.write(minOperations(n, m, k, matrix));

    // This code is contributed by mukesh07.
</script>
```

**Output:** 

```
36
```

**下面是一个同样在输入矩阵中处理负数的实现:**

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the minimum
// number of operations required
int minOperations(int n, int m, int k,
                  vector<vector<int> >& matrix)
{
    // Create another array to
    // store the elements of matrix
    vector<int> arr;

    int mod;

    // will not work for negative elements, so ..
    // adding this
    if (matrix[0][0] < 0) {
        mod = k - (abs(matrix[0][0]) % k);
    }
    else {
        mod = matrix[0][0] % k;
    }

    for (int i = 0; i < n; ++i) {
        for (int j = 0; j < m; ++j) {
            arr.push_back(matrix[i][j]);

            // adding this to handle negative elements too .
            int val = matrix[i][j];
            if (val < 0) {
                int res = k - (abs(val) % k);
                if (res != mod) {
                    return -1;
                }
            }
            else {
                int foo = matrix[i][j];
                if (foo % k != mod) {
                    return -1;
                }
            }
        }
    }

    // Sort the array to get median
    sort(arr.begin(), arr.end());

    int median = arr[(n * m) / 2];

    // To count the minimum operations
    int minOperations = 0;
    for (int i = 0; i < n * m; ++i)
        minOperations += abs(arr[i] - median) / k;

    // If there are even elements, then there
    // are two medians. We consider the best
    // of two as answer.
    if ((n * m) % 2 == 0) {

        // changed here as in case of even elements there will be 2 medians
        int median2 = arr[((n * m) / 2) - 1];

        int minOperations2 = 0;
        for (int i = 0; i < n * m; ++i)
            minOperations2 += abs(arr[i] - median2) / k;

        minOperations = min(minOperations, minOperations2);
    }

    // Return minimum operations required
    return minOperations;
}

// Driver code
int main()
{
    vector<vector<int> > matrix = { { 2, 4, 6 },
                                    { 8, 10, 12 },
                                    { 14, 16, 18 },
                                    { 20, 22, 24 } };
    int n = matrix.size();
    int m = matrix[0].size();
    int k = 2;
    cout << minOperations(n, m, k, matrix);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;
class GFG
{

  // Function to return the minimum
  // number of operations required
  public static int minOperations(int n, int m, int k,
                                  int matrix[][])
  {
    // Create another array to
    // store the elements of matrix
    Vector<Integer> arr = new Vector<>(); 

    int mod;

    // will not work for negative elements, so ..
    // adding this
    if (matrix[0][0] < 0)
    {
      mod = k - (Math.abs(matrix[0][0]) % k);
    }
    else
    {
      mod = matrix[0][0] % k;
    }

    for (int i = 0; i < n; ++i)
    {
      for (int j = 0; j < m; ++j)
      {
        arr.add(matrix[i][j]);

        // adding this to handle
        // negative elements too .
        int val = matrix[i][j];
        if (val < 0)
        {
          int res = k - (Math.abs(val) % k);
          if (res != mod)
          {
            return -1;
          }
        }
        else
        {
          int foo = matrix[i][j];
          if (foo % k != mod)
          {
            return -1;
          }
        }
      }
    }

    // Sort the array to get median
    Collections.sort(arr);     
    int median = arr.get((n * m) / 2);

    // To count the minimum operations
    int minOperations = 0;
    for (int i = 0; i < n * m; ++i)
      minOperations += Math.abs(arr.get(i) - median) / k;

    // If there are even elements, then there
    // are two medians. We consider the best
    // of two as answer.
    if ((n * m) % 2 == 0)
    {

      // changed here as in case of
      // even elements there will be 2 medians
      int median2 = arr.get(((n * m) / 2) - 1);

      int minOperations2 = 0;
      for (int i = 0; i < n * m; ++i)
        minOperations2 += Math.abs(arr.get(i) - median2) / k;

      minOperations = Math.min(minOperations, minOperations2);
    }

    // Return minimum operations required
    return minOperations;
  }

  // Driver code
  public static void main(String[] args)
  {
    int matrix[][] = {
      {2, 4, 6},
      {8, 10, 12},
      {14, 16, 18},
      {20, 22, 24}
    };
    int n = matrix.length;
    int m = matrix[0].length;
    int k = 2;
    System.out.println(minOperations(n, m, k, matrix));
  }
}

// This code is contributed by divyesh072019
```

## 蟒蛇 3

```
# Python3 implementation of the
# above approach

# Function to return the minimum
# number of operations required
def minOperations(n, m, k,
                  matrix):

    # Create another array to
    # store the elements of
    # matrix
    arr = []

    # will not work for negative
    # elements, so .. adding this
    if (matrix[0][0] < 0):
        mod = k - (abs(matrix[0][0]) % k)
    else:
        mod = matrix[0][0] % k

    for i in range(n):
        for j in range(m):
            arr.append(matrix[i][j])

            # adding this to handle
            # negative elements too .
            val = matrix[i][j]

            if (val < 0):
                res = k - (abs(val) % k)
                if (res != mod):
                    return -1
            else:
                foo = matrix[i][j]
                if (foo % k != mod):
                    return -1

    # Sort the array to get median
    arr.sort()

    median = arr[(n * m) // 2]

    # To count the minimum
    # operations
    minOperations = 0
    for i in range(n * m):
        minOperations += abs(arr[i] -
                             median) // k

    # If there are even elements,
    # then there are two medians.
    # We consider the best of two
    # as answer.
    if ((n * m) % 2 == 0):

        # changed here as in case of
        # even elements there will be
        # 2 medians
        median2 = arr[((n * m) //
                        2) - 1]

        minOperations2 = 0
        for i in range(n * m):
            minOperations2 += abs(arr[i] -
                                  median2) / k

        minOperations = min(minOperations,
                            minOperations2)

    # Return minimum operations required
    return minOperations

# Driver code
if __name__ == "__main__":

    matrix = [[2, 4, 6],
              [8, 10, 12],
              [14, 16, 18],
              [20, 22, 24]]
    n = len(matrix)
    m = len(matrix[0])
    k = 2
    print(minOperations(n, m, k, matrix))

# This code is contributed by Chitranayal
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;
class GFG {

    // Function to return the minimum
    // number of operations required
    static int minOperations(int n, int m, int k,
                      List<List<int>> matrix)
    {
        // Create another array to
        // store the elements of matrix
        List<int> arr = new List<int>();

        int mod;

        // will not work for negative elements, so ..
        // adding this
        if (matrix[0][0] < 0) {
            mod = k - (Math.Abs(matrix[0][0]) % k);
        }
        else {
            mod = matrix[0][0] % k;
        }

        for (int i = 0; i < n; ++i) {
            for (int j = 0; j < m; ++j) {
                arr.Add(matrix[i][j]);

                // adding this to handle negative elements too .
                int val = matrix[i][j];
                if (val < 0) {
                    int res = k - (Math.Abs(val) % k);
                    if (res != mod) {
                        return -1;
                    }
                }
                else {
                    int foo = matrix[i][j];
                    if (foo % k != mod) {
                        return -1;
                    }
                }
            }
        }

        // Sort the array to get median
        arr.Sort();

        int median = arr[(n * m) / 2];

        // To count the minimum operations
        int minOperations = 0;
        for (int i = 0; i < n * m; ++i)
            minOperations += Math.Abs(arr[i] - median) / k;

        // If there are even elements, then there
        // are two medians. We consider the best
        // of two as answer.
        if ((n * m) % 2 == 0) {

            // changed here as in case of
            // even elements there will be 2 medians
            int median2 = arr[((n * m) / 2) - 1];

            int minOperations2 = 0;
            for (int i = 0; i < n * m; ++i)
                minOperations2 += Math.Abs(arr[i] - median2) / k;

            minOperations = Math.Min(minOperations, minOperations2);
        }

        // Return minimum operations required
        return minOperations;
    }

  static void Main() {
    List<List<int>> matrix = new List<List<int>>{
        new List<int> {2, 4, 6},
        new List<int> {8, 10, 12},
        new List<int> {14, 16, 18},
        new List<int> {20, 22, 24},
    };
    int n = matrix.Count;
    int m = matrix[0].Count;
    int k = 2;
    Console.Write(minOperations(n, m, k, matrix));
  }
}

// This code is contributed by divyeshrabadiya07.
```

## java 描述语言

```
<script>
// Javascript implementation of the approach

// Function to return the minimum
// number of operations required
function minOperations(n,m,k,matrix)
{
    // Create another array to
    // store the elements of matrix
    let arr = [];

    let mod;

    // will not work for negative elements, so ..
    // adding this
    if (matrix[0][0] < 0)
    {
      mod = k - (Math.abs(matrix[0][0]) % k);
    }
    else
    {
      mod = matrix[0][0] % k;
    }

    for (let i = 0; i < n; ++i)
    {
      for (let j = 0; j < m; ++j)
      {
        arr.push(matrix[i][j]);

        // adding this to handle
        // negative elements too .
        let val = matrix[i][j];
        if (val < 0)
        {
          let res = k - (Math.abs(val) % k);
          if (res != mod)
          {
            return -1;
          }
        }
        else
        {
          let foo = matrix[i][j];
          if (foo % k != mod)
          {
            return -1;
          }
        }
      }
    }

    // Sort the array to get median
    arr.sort(function(a,b){return a-b;});    
    let median = arr[(n * m) / 2];

    // To count the minimum operations
    let minOperations = 0;
    for (let i = 0; i < n * m; ++i)
      minOperations += Math.abs(arr[i] - median) / k;

    // If there are even elements, then there
    // are two medians. We consider the best
    // of two as answer.
    if ((n * m) % 2 == 0)
    {

      // changed here as in case of
      // even elements there will be 2 medians
      let median2 = arr[((n * m) / 2) - 1];

      let minOperations2 = 0;
      for (let i = 0; i < n * m; ++i)
        minOperations2 += Math.abs(arr[i] - median2) / k;

      minOperations = Math.min(minOperations, minOperations2);
    }

    // Return minimum operations required
    return minOperations;
}

// Driver code
let matrix = [[2, 4, 6],
              [8, 10, 12],
              [14, 16, 18],
              [20, 22, 24]];

let n = matrix.length;
let m = matrix[0].length;
let k = 2;
document.write(minOperations(n, m, k, matrix));

// This code is contributed by rag2127
</script>
```

**Output:** 

```
36
```
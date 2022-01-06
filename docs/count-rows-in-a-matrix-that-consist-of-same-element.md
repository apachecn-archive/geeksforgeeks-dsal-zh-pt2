# 计算由相同元素组成的矩阵中的行数

> 原文:[https://www . geeksforgeeks . org/count-由相同元素组成的矩阵中的行数/](https://www.geeksforgeeks.org/count-rows-in-a-matrix-that-consist-of-same-element/)

给定一个矩阵 **mat[][]** ，任务是计算矩阵中由相同元素组成的行数。

**示例:**

> **输入:** mat[][] = {{1，1，1}，{1，2，3}，{5，5，5}}
> **输出:** 2
> 第一行的所有元素和第三行的所有元素都是一样的。
> 
> **输入:** mat[][] = {{1，2}，{4，2 } }
> T3】输出: 0

**方法:**设置**计数= 0** 并开始逐行遍历矩阵，对于特定行，将该行的每个元素添加到[设置](https://www.geeksforgeeks.org/hashset-in-java/)中，并检查**大小(设置)= 1** ，如果**是**，则更新**计数=计数+ 1** 。
遍历完所有行后，打印**计数**的值。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>

using namespace std;

// Function to return the count of all identical rows
int countIdenticalRows(vector< vector <int> > mat)
{
    int count = 0;

    for (int i = 0; i < mat.size(); i++)
    {

        // HashSet for current row
        set<int> hs;

        // Traverse the row
        for (int j = 0; j < mat[i].size(); j++)
        {

            // Add all the values of the row in HashSet
            hs.insert(mat[i][j]);
        }

        // Check if size of HashSet = 1
        if (hs.size() == 1)
            count++;
    }
    return count;
}

// Driver code
int main()
{
    vector< vector <int> > mat = {{ 1, 1, 1 },
                                { 1, 2, 3 },
                                { 5, 5, 5 }};

    cout << countIdenticalRows(mat);
    return 0;
}

// This code is contributed by Rituraj Jain
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.HashSet;

class GFG {

    // Function to return the count of all identical rows
    public static int countIdenticalRows(int mat[][])
    {

        int count = 0;

        for (int i = 0; i < mat.length; i++) {

            // HashSet for current row
            HashSet<Integer> hs = new HashSet<>();

            // Traverse the row
            for (int j = 0; j < mat[i].length; j++) {

                // Add all the values of the row in HashSet
                hs.add(mat[i][j]);
            }

            // Check if size of HashSet = 1
            if (hs.size() == 1)
                count++;
        }

        return count;
    }

    // Driver code
    public static void main(String[] args)
    {
        int mat[][] = { { 1, 1, 1 },
                        { 1, 2, 3 },
                        { 5, 5, 5 } };
        System.out.print(countIdenticalRows(mat));
    }
}
```

## 蟒蛇 3

```
#Function to return the count of all identical rows
def countIdenticalRows(mat):
    count = 0

    for i in range(len(mat)):

        #HashSet for current row
        hs=dict()

        #Traverse the row
        for j in range(len(mat[i])):

            #Add all the values of the row in HashSet
            hs[mat[i][j]]=1

        #Check if size of HashSet = 1
        if (len(hs)== 1):
            count+=1

    return count

#Driver code

mat= [ [ 1, 1, 1 ],
                [ 1, 2, 3 ],
                [ 5, 5, 5 ] ]
print(countIdenticalRows(mat))

#This code is contributed by Mohit kumar 29
```

## C#

```
// C# implementation of
// the above approach
using System;
using System.Collections.Generic;
class GFG
{

    // Function to return the count
    // of all identical rows
    public static int countIdenticalRows(int [,]mat)
    {
        int count = 0;

        for (int i = 0;
                 i < mat.GetLength(0); i++)
        {

            // HashSet for current row
            HashSet<int> hs = new HashSet<int>();

            // Traverse the row
            for (int j = 0;
                     j < mat.GetLength(0); j++)
            {

                // Add all the values
                // of the row in HashSet
                hs.Add(mat[i, j]);
            }

            // Check if size of HashSet = 1
            if (hs.Count == 1)
                count++;
        }
        return count;
    }

    // Driver code
    public static void Main(String[] args)
    {
        int [,]mat = {{ 1, 1, 1 },
                      { 1, 2, 3 },
                      { 5, 5, 5 }};
        Console.WriteLine(countIdenticalRows(mat));
    }
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>
// Javascript implementation of the approach

    // Function to return the count of all identical rows
    function countIdenticalRows(mat)
    {
        let count = 0;

        for (let i = 0; i < mat.length; i++) {

            // HashSet for current row
            let hs = new Set();

            // Traverse the row
            for (let j = 0; j < mat[i].length; j++) {

                // Add all the values of the row in HashSet
                hs.add(mat[i][j]);
            }

            // Check if size of HashSet = 1
            if (hs.size == 1)
                count++;
        }

        return count;
    }

    // Driver code
    let mat= [ [ 1, 1, 1 ],
               [ 1, 2, 3 ],
               [ 5, 5, 5 ] ];

    document.write(countIdenticalRows(mat));

// This code is contributed by avanitrachhadiya2155
</script>
```

**Output:** 

```
2
```

**内存高效方法:**设置**计数= 0** 并开始逐行遍历矩阵，对于特定行，将该行的第一个元素保存在变量**第一个**中，并将所有其他元素与**第一个**进行比较。如果该行的所有其他元素都等于第一个元素，则更新**计数=计数+ 1** 。遍历完所有行后，打印**计数**。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>

using namespace std;

    // Function to return the count of all identical rows
    int countIdenticalRows(int mat[3][3],int r,int c)
    {
        int count = 0;
        for (int i = 0; i < r; i++)
        {

            // First element of current row
            int first = mat[i][0];
            bool allSame = true;

            // Compare every element of the current row
            // with the first element of the row

            for (int j = 1; j < c; j++)
            {

                // If any element is different
                if (mat[i][j] != first)
                {
                    allSame = false;
                    break;
                }
            }

            // If all the elements of the
            // current row were same
            if (allSame)
                count++;
        }
        return count;
    }

    // Driver code
    int main()
    {
        //int mat[3][3] ;
        int mat[][3] = { { 1, 1, 2 },
                        { 2, 2, 2 },
                        { 5, 5, 2 } };

        int row_length = sizeof(mat)/sizeof(mat[0]) ;
        int col_length = sizeof(mat[0])/sizeof(int) ;

        cout << countIdenticalRows(mat, row_length,col_length) << endl;
    return 0;
    }

// This code is contributed by aishwarya.27
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG {

    // Function to return the count of all identical rows
    public static int countIdenticalRows(int mat[][])
    {

        int count = 0;

        for (int i = 0; i < mat.length; i++) {

            // First element of current row
            int first = mat[i][0];
            boolean allSame = true;

            // Compare every element of the current row
            // with the first element of the row
            for (int j = 1; j < mat[i].length; j++) {

                // If any element is different
                if (mat[i][j] != first) {
                    allSame = false;
                    break;
                }
            }

            // If all the elements of the
            // current row were same
            if (allSame)
                count++;
        }

        return count;
    }

    // Driver code
    public static void main(String[] args)
    {
        int mat[][] = { { 1, 1, 2 },
                        { 2, 2, 2 },
                        { 5, 5, 2 } };
        System.out.print(countIdenticalRows(mat));
    }
}
```

## 蟒蛇 3

```
# Python 3 implementation of the approach

# Function to return the count of
# all identical rows
def countIdenticalRows(mat):

    count = 0

    for i in range(len(mat)):

        # First element of current row
        first = mat[i][0]
        allSame = True

        # Compare every element of the current
        # row with the first element of the row
        for j in range(1, len(mat[i])):

            # If any element is different
            if (mat[i][j] != first):
                allSame = False
                break

        # If all the elements of the
        # current row were same
        if (allSame):
            count += 1

    return count

# Driver code
if __name__ == "__main__":

    mat = [[ 1, 1, 2 ],
           [2, 2, 2 ],
           [5, 5, 2 ]]
    print(countIdenticalRows(mat))

# This code is contributed by ita_c
```

## C#

```
// C# implementation of the approach

using System;

class GFG {

    // Function to return the count of all identical rows
    public static int countIdenticalRows(int [,]mat)
    {

        int count = 0;

        for (int i = 0; i < mat.GetLength(0); i++) {

            // First element of current row
            int first = mat[i,0];
            bool allSame = true;

            // Compare every element of the current row
            // with the first element of the row
            for (int j = 1; j < mat.GetLength(1); j++) {

                // If any element is different
                if (mat[i,j] != first) {
                    allSame = false;
                    break;
                }
            }

            // If all the elements of the
            // current row were same
            if (allSame)
                count++;
        }

        return count;
    }

    // Driver code
    public static void Main()
    {
        int [,]mat = { { 1, 1, 2 },
                        { 2, 2, 2 },
                        { 5, 5, 2 } };

        Console.Write(countIdenticalRows(mat));
    }
    // This code is contributed by Ryuga
}
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to return the count of
// all identical rows
function countIdenticalRows(&$mat)
{
    $count = 0;

    for ($i = 0; $i < sizeof($mat); $i++)
    {

        // First element of current row
        $first = $mat[$i][0];
        $allSame = true;

        // Compare every element of the current
        // row with the first element of the row
        for ($j = 1; $j < sizeof($mat[$i]); $j++)
        {

            // If any element is different
            if ($mat[$i][$j] != $first)
            {
                $allSame = false;
                break;
            }
        }

        // If all the elements of the
        // current row were same
        if ($allSame)
            $count++;
    }

    return $count;
}

// Driver code
$mat = array(array(1, 1, 2),
             array(2, 2, 2),
             array(5, 5, 2));

echo(countIdenticalRows($mat));

// This code is contributed by Shivi_Aggarwal
?>
```

## java 描述语言

```
<script>
// Javascript implementation of the approach

// Function to return the count of all identical rows
function countIdenticalRows(mat)
{
    let count = 0;

        for (let i = 0; i < mat.length; i++) {

            // First element of current row
            let first = mat[i][0];
            let allSame = true;

            // Compare every element of the current row
            // with the first element of the row
            for (let j = 1; j < mat[i].length; j++) {

                // If any element is different
                if (mat[i][j] != first) {
                    allSame = false;
                    break;
                }
            }

            // If all the elements of the
            // current row were same
            if (allSame)
                count++;
        }

        return count;
}

// Driver code
let mat = [[ 1, 1, 2 ],
           [2, 2, 2 ],
           [5, 5, 2 ]];

document.write(countIdenticalRows(mat));

// This code is contributed by rag2127
</script>
```

**Output:** 

```
1
```
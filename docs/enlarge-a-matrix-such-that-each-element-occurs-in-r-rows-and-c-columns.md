# 放大矩阵，使每个元素出现在 R 行和 C 列中

> 原文:[https://www . geesforgeks . org/expand-a-matrix-so-每个元素出现在-r-row-and-c-columns/](https://www.geeksforgeeks.org/enlarge-a-matrix-such-that-each-element-occurs-in-r-rows-and-c-columns/)

给定一个大小为 **N x M** 的矩阵 **arr[][]** ，以及两个数字 **R** 和 **C** ，任务是放大该矩阵，使得原始矩阵的每个元素出现在放大矩阵的 **R** 行和 **C** 列中。

**示例:**

> **输入:** arr[][] = {{1，2，3}，{4，5，6}} R = 3，C = 2
> **输出:**
> 1 1 2 2 3 4 4 5 5 6
> 1 2 2 3 3 4 4 5 5 6
> 1 2 3 3 4 5 5 6
> **解释:**
> 原始矩阵的每个元素在放大后的矩阵中出现 3 行 2 列。
> 
> **输入:** arr = {{1，2}}，R = 2，C = 3
> **输出:**
> 1 1 1 2 2 2
> 1 1 2 2
> **说明:**
> 原矩阵的每个元素在放大后的矩阵中出现 2 行 3 列。

**方法:**这个问题可以通过保持行数或列数不变来解决。在本文中，行数是固定的。因此，对于任何 N×M 维的矩阵，最终答案中的行数将是 R.
想法是首先将给定矩阵转换为一维数组(即)[展平给定矩阵](https://www.geeksforgeeks.org/python-numpy-matrix-flatten/)。现在，对于展平矩阵中的每个元素，在最终放大矩阵的 R 行和 C 列中追加值。

下面是上述方法的实现:

## C++

```
// C++ program to enlarge a matrix
// such that each element occurs in
// R rows and C columns
#include <bits/stdc++.h>
using namespace std;

// Function to convert the matrix
// into a 1-D array
vector<int> oneD(vector<vector<int>> &matrix){

    // Variable to store the
    // given matrix
    vector<int> m;

    // Iterating through all the
    // elements of the matrix
    for(int i = 0; i < matrix.size(); ++i)
        for(int j = 0; j < matrix[0].size(); ++j)
            // Adding the element into the
            // defined matrix
            m.push_back(matrix[i][j]);

    return m;
}

// Function to enlarge a matrix
// such that each element occurs
// in R rows and C columns
vector<vector<int>> dimensions(int R, int C, vector<int> matrix) {

    // Initializing the enlarged
    // matrix
    vector<vector<int>> ans(R+1);

    // Variables to iterate over
    // the matrix
    int ctr = 0;
    int r = 0;

    while(ctr < matrix.size()) {

        // To keep the rows in the
        // range [0, R]
        r = r % R;
        int c = 0;
        while(c < C) {            
            // In order to fix the number
            // of columns, the above r
            // statement can be commented 
            // and this can be uncommented
            // c = c % C
               for(int i = 0; i < R; ++i)
                   ans[i].push_back(matrix[ctr]);

               c += 1;
          }
        ctr += 1;
        r += 1;
    }

    return ans;
}

// Driver code
int main() {

    vector<vector<int>> arr = {{1, 2}, {3, 4}};
    int R = 2, C = 3;

    vector<vector<int>> ans = dimensions(R, C, oneD(arr));

    // Print the enlarged matrix
    for(int i = 0; i < ans.size(); ++i) {

        for(int j = 0; j < ans[i].size(); ++j) {
            cout << ans[i][j] << " ";
        }

        cout<<endl;
    }

    return 0;
}

// This code is contributed by Sanjit_Prasad
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to enlarge a matrix
// such that each element occurs in
// R rows and C columns
import java.io.*;
import java.util.*;

class GFG{

// Function to convert the matrix
// into a 1-D array
static ArrayList<Integer>oneD(
    ArrayList<ArrayList<Integer>> matrix)
{

    // Variable to store the
    // given matrix
    ArrayList<Integer> m = new ArrayList<Integer>();

    // Iterating through all the
    // elements of the matrix
    for(int i = 0; i < matrix.size(); ++i)
        for(int j = 0; j < matrix.get(0).size(); ++j)

            // Adding the element into the
            // defined matrix
            m.add(matrix.get(i).get(j));

    return m;
}

// Function to enlarge a matrix
// such that each element occurs
// in R rows and C columns
static ArrayList<ArrayList<Integer>>dimensions(
    int R, int C, ArrayList<Integer> matrix)
{

    // Initializing the enlarged
    // matrix
    ArrayList<ArrayList<Integer>> ans = new ArrayList<>();
    for(int i = 0; i < R; ++i)
    {
        ans.add(new ArrayList<Integer>());
    }

    // Variables to iterate over
    // the matrix
    int ctr = 0;
    int r = 0;

    while (ctr < matrix.size())
    {

        // To keep the rows in the
        // range [0, R]
        r = r % R;
        int c = 0;

        while (c < C)
        {

            // In order to fix the number
            // of columns, the above r
            // statement can be commented
            // and this can be uncommented
            // c = c % C
            for(int i = 0; i < R; ++i)
            {
                ans.get(i).add(matrix.get(ctr));
            }
            c += 1;
        }
        ctr += 1;
        r += 1;
    }
    return ans;
}

// Driver code
public static void main(String[] args)
{

    ArrayList<ArrayList<Integer>> arr = new ArrayList<>();
    arr.add(new ArrayList<Integer>(Arrays.asList(1, 2)));
    arr.add(new ArrayList<Integer>(Arrays.asList(3, 4)));
    int R = 2, C = 3;

    ArrayList<ArrayList<Integer>> ans = new ArrayList<>(
        dimensions(R, C, oneD(arr)));

    // Print the enlarged matrix
    for(int i = 0; i < ans.size(); ++i)
    {
        System.out.print("[");
        for(int j = 0; j < ans.get(i).size(); ++j)
        {
            System.out.print(ans.get(i).get(j) + ", ");
        }
        System.out.print("]\n");
    }
}
}

// This code is contributed by akhilsaini
```

## 蟒蛇 3

```
# Python program to enlarge a matrix
# such that each element occurs in
# R rows and C columns

# Function to convert the matrix
# into a 1-D array
def oneD(matrix):

    # Variable to store the
    # given matrix
    m = []

    # Iterating through all the
    # elements of the matrix
    for i in range(len(matrix)):
        for j in range(len(matrix[0])):

            # Adding the element into the
            # defined matrix
            m.append(matrix[i][j])

    return m[:]

# Function to enlarge a matrix
# such that each element occurs
# in R rows and C columns
def dimensions(R, C, matrix):

    # Initializing the enlarged
    # matrix
    ans = [[]] * R

    # Variables to iterate over
    # the matrix
    ctr = 0
    r = 0

    while(ctr < len(matrix)):

        # To keep the rows in the
        # range [0, R]
        r = r % R
        c = 0
        while(c < C):

            # In order to fix the number
            # of columns, the above r
            # statement can be commented 
            # and this can be uncommented
            # c = c % C
            ans[r].append(matrix[ctr])

            c+= 1

        ctr += 1
        r+= 1

    return ans

# Driver code
if __name__ == '__main__':

    arr = [[1, 2], [3, 4]]
    R, C = 2, 3

    ans = dimensions(R, C, oneD(arr))

    # Print the enlarged matrix
    for i in ans:
        print(i)
```

## C#

```
// C# program to enlarge a matrix
// such that each element occurs in
// R rows and C columns
using System;
using System.Collections;
using System.Collections.Generic;

class GFG{

// Function to convert the matrix
// into a 1-D array
static List<int> oneD(List<List<int> > matrix)
{

    // Variable to store the
    // given matrix
    List<int> m = new List<int>();

    // Iterating through all the
    // elements of the matrix
    for(int i = 0; i < matrix.Count; ++i)
        for(int j = 0; j < matrix[0].Count; ++j)

            // Adding the element into the
            // defined matrix
            m.Add(matrix[i][j]);

    return m;
}

// Function to enlarge a matrix
// such that each element occurs
// in R rows and C columns
static List<List<int>> dimensions(int R, int C,
                                  List<int> matrix)
{

    // Initializing the enlarged
    // matrix
    List<List<int> > ans = new List<List<int> >();
    for(int i = 0; i < R; ++i)
    {
        ans.Add(new List<int>());
    }

    // Variables to iterate over
    // the matrix
    int ctr = 0;
    int r = 0;

    while (ctr < matrix.Count)
    {

        // To keep the rows in the
        // range [0, R]
        r = r % R;
        int c = 0;

        while (c < C)
        {

            // In order to fix the number
            // of columns, the above r
            // statement can be commented
            // and this can be uncommented
            // c = c % C
            for(int i = 0; i < R; ++i)
            {
                ans[i].Add(matrix[ctr]);
            }
            c += 1;
        }
        ctr += 1;
        r += 1;
    }
    return ans;
}

// Driver code
public static void Main()
{

    List<List<int>> arr = new List<List<int>>();
    arr.Add(new List<int>() { 1, 2 });
    arr.Add(new List<int>() { 3, 4 });
    int R = 2, C = 3;

    List<List<int>> ans = new List<List<int>>(
        dimensions(R, C, oneD(arr)));

    // Print the enlarged matrix
    for(int i = 0; i < ans.Count; ++i)
    {
        Console.Write("[");
        for(int j = 0; j < ans[i].Count; ++j)
        {
            Console.Write(ans[i][j] + ", ");
        }
        Console.Write("]\n");
    }
}
}

// This code is contributed by akhilsaini
```

## java 描述语言

```
<script>

// JavaScript program to enlarge a matrix
// such that each element occurs in
// R rows and C columns

// Function to convert the matrix
// into a 1-D array
function oneD(matrix){

    // Variable to store the
    // given matrix
    let m = new Array();

    // Iterating through all the
    // elements of the matrix
    for(let i = 0; i < matrix.length; ++i)
        for(let j = 0; j < matrix[0].length; ++j)
            // Adding the element into the
            // defined matrix
            m.push(matrix[i][j]);

    return m;
}

// Function to enlarge a matrix
// such that each element occurs
// in R rows and C columns
function dimensions(R, C, matrix) {

    // Initializing the enlarged
    // matrix
    let ans = new Array();

    for(let i = 0;  i < R + 1; i++){
        ans.push([])
    }

    // Variables to iterate over
    // the matrix
    let ctr = 0;
    let r = 0;

    while(ctr < matrix.length) {

        // To keep the rows in the
        // range [0, R]
        r = r % R;
        let c = 0;
        while(c < C) {           
            // In order to fix the number
            // of columns, the above r
            // statement can be commented
            // and this can be uncommented
            // c = c % C
            for(let i = 0; i < R; ++i)
                ans[i].push(matrix[ctr]);

            c += 1;
        }
        ctr += 1;
        r += 1;
    }

    return ans;
}

// Driver code

    let arr = [[1, 2], [3, 4]];
    let R = 2, C = 3;

    let ans = dimensions(R, C, oneD(arr));

    // Print the enlarged matrix
     for (let i of ans){
         if(i.length)
        document.write("[" + i + "]<br>")
     }

// This code is contributed by _saurabh_jaiswal

</script>
```

**Output:** 

```
[1, 1, 1, 2, 2, 2, 3, 3, 3, 4, 4, 4]
[1, 1, 1, 2, 2, 2, 3, 3, 3, 4, 4, 4]
```
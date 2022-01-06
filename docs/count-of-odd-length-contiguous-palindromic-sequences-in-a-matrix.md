# 矩阵中奇数长度连续回文序列的计数

> 原文:[https://www . geeksforgeeks . org/奇数长度连续回文序列矩阵计数/](https://www.geeksforgeeks.org/count-of-odd-length-contiguous-palindromic-sequences-in-a-matrix/)

给定一个大小为 **MxN** 的矩阵 **arr[][]** ，任务是找出该矩阵中奇数长度的连续回文序列的数量。

**示例:**

```
Input: arr[][] = { { 2, 1, 2 },
                   { 1, 1, 1 },
                   { 2, 1, 2 }}
Output: 15
Explanation
Contigiuos Palindromic sequences of odd length are:
Row 1: (2), (1), (2), (2, 1, 2) => n(R1) = 4
Row 2: (1), (1), (1), (1, 1, 1) => n(R2) = 4
Row 3: (2), (1), (2), (2, 1, 2) => n(R3) = 4
Column 1: (2, 1, 2) => n(C1) = 1
Column 2: (1, 1, 1) => n(C2) = 1
Column 3: (2, 1, 2) => n(C3) = 1
Therefore, 
Total count = n(R1) + n(R2) + n(R3)
              + n(C1) + n(C2) + n(C3)
            = 15

Input: arr[][] = { { 1, 1, 1, 1, 1 },
                   { 1, 1, 1, 1, 1 },
                   { 1, 1, 1, 1, 1 },
                   { 1, 1, 1, 1, 1 },
                   { 1, 1, 1, 1, 1 } }
Output: 65 
```

**进场:**

1.创建一个变量计数来存储矩阵中连续回文序列的总数

2.由于[矩阵](https://www.geeksforgeeks.org/matrix/)中的每个元素都是长度为 1 的[连续回文序列](https://www.geeksforgeeks.org/longest-palindromic-subsequence-dp-12/)，将矩阵中元素的总数加到计数中，即，

```
count += (M*N)
```

3.然后，对于长度> 1 的序列，

*   遍历矩阵的每个元素，通过将元素与其左右两边的其他元素进行比较，计算每行中回文序列的数量
*   同样，通过将元素与其上面和下面的其他元素进行比较，计算每列中回文序列的数量。

1.  如果找到，将找到的回文序列计数增加 1。
2.  在末尾打印计算出的回文序列数

下面是上述方法的实现:

## C++

```
// C++ code to Count the odd length contiguous
// Palindromic sequences in the matrix

#include <bits/stdc++.h>
using namespace std;

#define MAX 10

// Function to count the number of
// contiguous palindromic sequences in the matrix
int countPalindromes(int n, int m, int matrix[MAX][MAX])
{
    // Add the total number of elements
    // in the matrix to the count
    int count = n * m;

    // Length of possible sequence to be checked
    // for palindrome horizontally and vertically
    int length_of_sequence_row;
    int length_of_sequence_column;

    // Iterate through each element of the matrix
    // and count the number of palindromic
    // sequences in each row and column
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < m; j++) {

            // Find the possible length of sequences
            // that can be a palindrome
            length_of_sequence_row
                = min(j, m - 1 - j);
            length_of_sequence_column
                = min(i, n - i - 1);

            // From i, check if the sequence
            // formed by elements to its
            // left and right is
            // palindrome or not
            for (int k = 1; k <= length_of_sequence_row; k++) {

                // if the sequence [i, j-k] to [i, j+k]
                // is a palindrome,
                // increment the count by 1
                if (matrix[i][j - k] == matrix[i][j + k]) {
                    count++;
                }
                else {
                    break;
                }
            }

            // From i, check if the sequence
            // formed by elements to its
            // above and below is
            // palindrome or not
            for (int k = 1; k <= length_of_sequence_column; k++) {

                // if the sequence [i-k, j] to [i+k, j]
                // is a palindrome,
                // increment the count by 1
                if (matrix[i - k][j] == matrix[i + k][j]) {
                    count++;
                }
                else {
                    break;
                }
            }
        }
    }

    // Return the total count
    // of the palindromic sequences
    return count;
}

// Driver code
int main(void)
{
    int m = 3, n = 3;
    int matrix[MAX][MAX] = { { 2, 1, 2 },
                             { 1, 1, 1 },
                             { 2, 1, 2 } };

    cout << countPalindromes(n, m, matrix)
         << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to Count the odd length contiguous
// Palindromic sequences in the matrix
class GFG
{

static final int MAX = 10;

// Function to count the number of
// contiguous palindromic sequences in the matrix
static int countPalindromes(int n, int m, int matrix[][])
{
    // Add the total number of elements
    // in the matrix to the count
    int count = n * m;

    // Length of possible sequence to be checked
    // for palindrome horizontally and vertically
    int length_of_sequence_row;
    int length_of_sequence_column;

    // Iterate through each element of the matrix
    // and count the number of palindromic
    // sequences in each row and column
    for (int i = 0; i < n; i++)
    {
        for (int j = 0; j < m; j++)
        {

            // Find the possible length of sequences
            // that can be a palindrome
            length_of_sequence_row
                = Math.min(j, m - 1 - j);
            length_of_sequence_column
                = Math.min(i, n - i - 1);

            // From i, check if the sequence
            // formed by elements to its
            // left and right is
            // palindrome or not
            for (int k = 1; k <= length_of_sequence_row; k++)
            {

                // if the sequence [i, j-k] to [i, j+k]
                // is a palindrome,
                // increment the count by 1
                if (matrix[i][j - k] == matrix[i][j + k])
                {
                    count++;
                }
                else
                {
                    break;
                }
            }

            // From i, check if the sequence
            // formed by elements to its
            // above and below is
            // palindrome or not
            for (int k = 1; k <= length_of_sequence_column; k++)
            {

                // if the sequence [i-k, j] to [i+k, j]
                // is a palindrome,
                // increment the count by 1
                if (matrix[i - k][j] == matrix[i + k][j])
                {
                    count++;
                }
                else
                {
                    break;
                }
            }
        }
    }

    // Return the total count
    // of the palindromic sequences
    return count;
}

// Driver code
public static void main(String []args)
{
    int m = 3, n = 3;
    int matrix[][] = { { 2, 1, 2 },
                        { 1, 1, 1 },
                        { 2, 1, 2 } };

    System.out.print(countPalindromes(n, m, matrix)
        +"\n");

}
}

// This code is contributed by 29AjayKumar
`
```

## 蟒蛇 3

```
# Python code to Count the odd length contiguous
# Palindromic sequences in the matrix
MAX = 10;

# Function to count the number of
# contiguous palindromic sequences in the matrix
def countPalindromes(n, m, matrix):

    # Add the total number of elements
    # in the matrix to the count
    count = n * m;

    # Length of possible sequence to be checked
    # for palindrome horizontally and vertically
    length_of_sequence_row = 0;
    length_of_sequence_column = 0;

    # Iterate through each element of the matrix
    # and count the number of palindromic
    # sequences in each row and column
    for i in range(n):
        for j in range(m):

            # Find the possible length of sequences
            # that can be a palindrome
            length_of_sequence_row = min(j, m - 1 - j);
            length_of_sequence_column = min(i, n - i - 1);

            # From i, check if the sequence
            # formed by elements to its
            # left and right is
            # palindrome or not
            for k in range(1, length_of_sequence_row + 1):

                # if the sequence [i, j-k] to [i, j+k]
                # is a palindrome,
                # increment the count by 1
                if (matrix[i][j - k] == matrix[i][j + k]):
                    count += 1;
                else:
                    break;

            # From i, check if the sequence
            # formed by elements to its
            # above and below is
            # palindrome or not
            for k in range(1, length_of_sequence_column + 1):

                # if the sequence [i-k, j] to [i+k, j]
                # is a palindrome,
                # increment the count by 1
                if (matrix[i - k][j] == matrix[i + k][j]):
                    count += 1;
                else:
                    break;

    # Return the total count
    # of the palindromic sequences
    return count;

# Driver code
if __name__ == '__main__':
    m = 3;
    n = 3;
    matrix = [ 2, 1, 2 ],[ 1, 1, 1 ],[ 2, 1, 2 ];

    print(countPalindromes(n, m, matrix));

# This code is contributed by 29AjayKumar
```

## C#

```
// C# code to Count the odd length contiguous
// Palindromic sequences in the matrix
using System;

class GFG
{

    static int MAX = 10;

    // Function to count the number of
    // contiguous palindromic sequences in the matrix
    static int countPalindromes(int n, int m, int [,]matrix)
    {
        // Add the total number of elements
        // in the matrix to the count
        int count = n * m;

        // Length of possible sequence to be checked
        // for palindrome horizontally and vertically
        int length_of_sequence_row;
        int length_of_sequence_column;

        // Iterate through each element of the matrix
        // and count the number of palindromic
        // sequences in each row and column
        for (int i = 0; i < n; i++)
        {
            for (int j = 0; j < m; j++)
            {

                // Find the possible length of sequences
                // that can be a palindrome
                length_of_sequence_row
                    = Math.Min(j, m - 1 - j);
                length_of_sequence_column
                    = Math.Min(i, n - i - 1);

                // From i, check if the sequence
                // formed by elements to its
                // left and right is
                // palindrome or not
                for (int k = 1; k <= length_of_sequence_row; k++)
                {

                    // if the sequence [i, j-k] to [i, j+k]
                    // is a palindrome,
                    // increment the count by 1
                    if (matrix[i, j - k] == matrix[i, j + k])
                    {
                        count++;
                    }
                    else
                    {
                        break;
                    }
                }

                // From i, check if the sequence
                // formed by elements to its
                // above and below is
                // palindrome or not
                for (int k = 1; k <= length_of_sequence_column; k++)
                {

                    // if the sequence [i-k, j] to [i+k, j]
                    // is a palindrome,
                    // increment the count by 1
                    if (matrix[i - k, j] == matrix[i + k, j])
                    {
                        count++;
                    }
                    else
                    {
                        break;
                    }
                }
            }
        }

        // Return the total count
        // of the palindromic sequences
        return count;
    }

    // Driver code
    public static void Main()
    {
        int m = 3, n = 3;
        int [,]matrix = { { 2, 1, 2 },
                            { 1, 1, 1 },
                            { 2, 1, 2 } };

        Console.WriteLine(countPalindromes(n, m, matrix) );
    }
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>
// Javascript code to Count the odd length contiguous
// Palindromic sequences in the matrix

let MAX = 10

// Function to count the number of
// contiguous palindromic sequences in the matrix
function countPalindromes(n, m, matrix) {
    // Add the total number of elements
    // in the matrix to the count
    let count = n * m;

    // Length of possible sequence to be checked
    // for palindrome horizontally and vertically
    let length_of_sequence_row;
    let length_of_sequence_column;

    // Iterate through each element of the matrix
    // and count the number of palindromic
    // sequences in each row and column
    for (let i = 0; i < n; i++) {
        for (let j = 0; j < m; j++) {

            // Find the possible length of sequences
            // that can be a palindrome
            length_of_sequence_row
                = Math.min(j, m - 1 - j);
            length_of_sequence_column
                = Math.min(i, n - i - 1);

            // From i, check if the sequence
            // formed by elements to its
            // left and right is
            // palindrome or not
            for (let k = 1; k <= length_of_sequence_row; k++) {

                // if the sequence [i, j-k] to [i, j+k]
                // is a palindrome,
                // increment the count by 1
                if (matrix[i][j - k] == matrix[i][j + k]) {
                    count++;
                }
                else {
                    break;
                }
            }

            // From i, check if the sequence
            // formed by elements to its
            // above and below is
            // palindrome or not
            for (let k = 1; k <= length_of_sequence_column; k++) {

                // if the sequence [i-k, j] to [i+k, j]
                // is a palindrome,
                // increment the count by 1
                if (matrix[i - k][j] == matrix[i + k][j]) {
                    count++;
                }
                else {
                    break;
                }
            }
        }
    }

    // Return the total count
    // of the palindromic sequences
    return count;
}

// Driver code

let m = 3, n = 3;
let matrix = [[2, 1, 2],
[1, 1, 1],
[2, 1, 2]];

document.write(countPalindromes(n, m, matrix) + "<br>");
</script>
```

**Output:** 

```
15
```

**时间复杂度:** O(n*m*max(n，m))
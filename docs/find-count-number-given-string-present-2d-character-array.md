# 2D 字符数组中给定字符串个数的计数

> 原文:[https://www . geesforgeks . org/find-count-number-given-string-present-2d-character-array/](https://www.geeksforgeeks.org/find-count-number-given-string-present-2d-character-array/)

给定一个二维字符数组和一个字符串，我们需要在二维字符数组中找到给定的字符串，使得单个字符可以从左到右、从右到左、从上到下或从下到上呈现。

**示例:**

```
Input : a ={
            {D,D,D,G,D,D},
            {B,B,D,E,B,S},
            {B,S,K,E,B,K},
            {D,D,D,D,D,E},
            {D,D,D,D,D,E},
            {D,D,D,D,D,G}
           }
        str= "GEEKS"
Output :2

Input : a = {
            {B,B,M,B,B,B},
            {C,B,A,B,B,B},
            {I,B,G,B,B,B},
            {G,B,I,B,B,B},
            {A,B,C,B,B,B},
            {M,C,I,G,A,M}
            }
        str= "MAGIC"

Output :3
```

我们讨论了更简单的问题[来找出一个单词是否存在于矩阵](https://www.geeksforgeeks.org/search-a-word-in-a-2d-grid-of-characters/)中。
为了统计所有事件，我们遵循简单的暴力方法。遍历矩阵的每个字符，并把每个字符作为要查找的字符串的开始，尝试在所有可能的方向上进行搜索。每当找到一个单词时，增加计数，遍历矩阵后，计数的值将是字符串在字符矩阵中存在的次数。

**算法:**
1-逐个字符遍历矩阵，取一个字符作为字符串开始
2-对于每个字符，递归查找所有四个方向的字符串
3-如果找到一个字符串，我们增加计数
4-当我们完成一个字符作为开始时，我们对下一个字符重复相同的过程
5-计算每个字符的计数总和
6-最终计数将是答案

## C++14

```
// C++ code for finding count
// of string in a given 2D
// character array.
#include <bits/stdc++.h>
using namespace std;

#define ARRAY_SIZE(a) (sizeof(a) / sizeof(*a))

// utility function to search
// complete string from any
// given index of 2d char array
int internalSearch(string needle, int row,
                   int col, string hay[],
                   int row_max, int col_max, int xx)
{
    int found = 0;

    if (row >= 0 && row <= row_max && col >= 0 &&
        col <= col_max && needle[xx] == hay[row][col])
    {
        char match = needle[xx];
        xx += 1;

        hay[row][col] = 0;

        if (needle[xx] == 0)
        {
            found = 1;
        }
        else
        {

            // through Backtrack searching
            // in every directions
            found += internalSearch(needle, row,
                                    col + 1, hay,
                                    row_max, col_max,xx);
            found += internalSearch(needle, row, col - 1,
                                    hay, row_max, col_max,xx);
            found += internalSearch(needle, row + 1, col,
                                    hay, row_max, col_max,xx);
            found += internalSearch(needle, row - 1, col,
                                    hay, row_max, col_max,xx);
        }
        hay[row][col] = match;
    }
    return found;
}

// Function to search the string in 2d array
int searchString(string needle, int row, int col,
                  string str[], int row_count,
                                int col_count)
{
    int found = 0;
    int r, c;

    for (r = 0; r < row_count; ++r)
    {
        for (c = 0; c < col_count; ++c)
        {
            found += internalSearch(needle, r, c, str,
                                    row_count - 1,
                                    col_count - 1, 0);
        }
    }
    return found;
}

// Driver code
int main()
{
    string needle = "MAGIC";
    string input[] = { "BBABBM",
                       "CBMBBA",
                       "IBABBG",
                       "GOZBBI",
                       "ABBBBC",
                       "MCIGAM" };
    string str[ARRAY_SIZE(input)];
    int i;
    for (i = 0; i < ARRAY_SIZE(input); ++i)
    {
        str[i] = input[i];
    }

    cout << "count: " << searchString(needle, 0, 0, str,
                                      ARRAY_SIZE(str),
                                      str[0].size()) << endl;
    return 0;
}

// This code is contributed by SHUBHAMSINGH8410
```

## C

```
// C code for finding count
// of string in a given 2D
// character array.
#include <stdio.h>
#include <string.h>
#include <stdlib.h>

#define ARRAY_SIZE(a) (sizeof(a) / sizeof(*a))

// utility function to search
// complete string from any
// given index of 2d char array
int internalSearch(char *needle, int row,
                   int col, char **hay,
                   int row_max, int col_max)
{
    int found = 0;

    if (row >= 0 && row <= row_max && col >= 0 &&
        col <= col_max && *needle == hay[row][col])
        {

        char match = *needle++;

        hay[row][col] = 0;

        if (*needle == 0) {
            found = 1;
        } else {

            // through Backtrack searching
            // in every directions
            found += internalSearch(needle, row,
                                    col+1, hay,
                                    row_max, col_max);
            found += internalSearch(needle, row, col-1,
                                    hay, row_max, col_max);
            found += internalSearch(needle, row+1, col,
                                    hay, row_max, col_max);
            found += internalSearch(needle, row-1, col,
                                    hay, row_max, col_max);
        }

        hay[row][col] = match;
    }

    return found;
}

// Function to search the string in 2d array
int searchString(char *needle, int row, int col,
                 char **str, int row_count, int col_count)
{
    int found = 0;
    int r, c;

    for (r = 0; r < row_count; ++r) {
        for (c = 0; c < col_count; ++c) {
            found += internalSearch(needle, r, c, str,
                            row_count - 1, col_count - 1);
        }
    }

    return found;
}

// Driver code
int main(void){

    char needle[] = "MAGIC";
    char *input[] = {
        "BBABBM",
        "CBMBBA",
        "IBABBG",
        "GOZBBI",
        "ABBBBC",
        "MCIGAM"
    };
    char *str[ARRAY_SIZE(input)];
    int i;
    for (i = 0; i < ARRAY_SIZE(input); ++i) {
        str[i] = malloc(strlen(input[i]));
        strcpy(str[i], input[i]);
    }

    printf("count: %d\n", searchString(needle, 0, 0,
              str, ARRAY_SIZE(str), strlen(str[0])));

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code for finding count
// of string in a given 2D
// character array.
import java.util.*;

class GFG{

// Utility function to search
// complete string from any
// given index of 2d char array
static int internalSearch(String needle, int row,
                          int col, String hay[],
                          int row_max, int col_max,
                          int xx)
{
    int found = 0;

    if (row >= 0 && row <= row_max && col >= 0 &&
        col <= col_max && xx < needle.length() &&
        needle.charAt(xx) == hay[row].charAt(col))
    {
        char match = needle.charAt(xx);
        xx += 1;

        hay[row] = hay[row].substring(0, col) + "0" +
                   hay[row].substring(col + 1);

        if (xx == needle.length())
        {
            found = 1;
        }
        else
        {

            // Through Backtrack searching
            // in every directions
            found += internalSearch(needle, row,
                                    col + 1, hay,
                                    row_max, col_max,xx);
            found += internalSearch(needle, row, col - 1,
                                    hay, row_max, col_max,xx);
            found += internalSearch(needle, row + 1, col,
                                    hay, row_max, col_max,xx);
            found += internalSearch(needle, row - 1, col,
                                    hay, row_max, col_max,xx);
        }

        hay[row] = hay[row].substring(0, col) +
           match + hay[row].substring(col + 1);
    }
    return found;
}

// Function to search the string in 2d array
static int searchString(String needle, int row, int col,
                        String str[], int row_count,
                                      int col_count)
{
    int found = 0;
    int r, c;

    for(r = 0; r < row_count; ++r)
    {
        for(c = 0; c < col_count; ++c)
        {
            found += internalSearch(needle, r, c, str,
                                    row_count - 1,
                                    col_count - 1, 0);
        }
    }
    return found;
}

// Driver code
public static void main(String args[])
{
    String needle = "MAGIC";
    String input[] = { "BBABBM", "CBMBBA",
                       "IBABBG", "GOZBBI",
                       "ABBBBC", "MCIGAM" };
    String str[] = new String[input.length];
    int i;
    for(i = 0; i < input.length; ++i)
    {
        str[i] = input[i];
    }

    System.out.println("count: " +
              searchString(needle, 0, 0, str,
                           str.length,
                           str[0].length()));
}
}

// This code is contributed by adityapande88
```

## 蟒蛇 3

```
# Python code for finding count
# of string in a given 2D
# character array.

# utility function to search
# complete string from any
# given index of 2d array
def internalSearch(ii, needle, row, col, hay,
                    row_max, col_max):

    found = 0
    if (row >= 0 and row <= row_max and
        col >= 0 and col <= col_max and
        needle[ii] == hay[row][col]):
        match = needle[ii]
        ii += 1
        hay[row][col] = 0
        if (ii == len(needle)):
            found = 1
        else:

            # through Backtrack searching
            # in every directions
            found += internalSearch(ii, needle, row,
                               col + 1, hay, row_max, col_max)
            found += internalSearch(ii, needle, row,
                               col - 1, hay, row_max, col_max)
            found += internalSearch(ii, needle, row + 1,
                               col, hay, row_max, col_max)
            found += internalSearch(ii, needle, row - 1,
                               col, hay, row_max, col_max)
        hay[row][col] = match
    return found

# Function to search the string in 2d array
def searchString(needle, row, col,strr,
                row_count, col_count):
    found = 0
    for r in range(row_count):
        for c in range(col_count):
            found += internalSearch(0, needle, r, c,
                        strr, row_count - 1, col_count - 1)

    return found

# Driver code

needle = "MAGIC"
inputt = ["BBABBM","CBMBBA","IBABBG",
            "GOZBBI","ABBBBC","MCIGAM"]

strr = [0] * len(inputt)

for i in range(len(inputt)):
    strr[i] = list(inputt[i])

print("count: ", searchString(needle, 0, 0, strr,
                        len(strr), len(strr[0])))

# This code is contributed by SHUBHAMSINGH10
```

**Output**

```
count: 3

```
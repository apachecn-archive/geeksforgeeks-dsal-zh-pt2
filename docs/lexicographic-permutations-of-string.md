# 按排序(字典顺序)顺序打印所有排列

> 原文:[https://www . geeksforgeeks . org/词典-字符串排列/](https://www.geeksforgeeks.org/lexicographic-permutations-of-string/)

给定一个字符串，按排序顺序打印它的所有排列。例如，如果输入字符串是“ABC”，那么输出应该是“ABC、ACB、北汽、BCA、CAB、CBA”。

我们已经讨论了一个在帖子中打印所有排列的程序，但是这里我们必须以递增的顺序打印排列。

以下是按字典顺序打印排列的步骤
**1。**按非递减顺序对给定字符串进行排序并打印。第一个排列总是按非递减顺序排序的字符串。
T4【2】。开始生成下一个更高的排列。这样做，直到下一个更高的排列是不可能的。如果我们得到一个排列，其中所有字符都按非递增顺序排序，那么这个排列就是最后一个排列。

**生成下一个更高排列的步骤:**
**1。**取之前打印的排列，找到其中最右边的字符，比它的下一个字符小。让我们称这个角色为“第一角色”。
**2。**现在找到‘第一个角色’的上限。上限是“第一个字符”右边的最小字符，大于“第一个字符”。让我们称天花板角色为“第二角色”。
**3。**交换以上 2 步找到的两个字符。
**4。**对‘第一个字符’原始索引后的子串进行排序(非递减顺序)。

让我们考虑字符串“ABCDEF”。让先前打印的排列为“DCFEBA”。排序顺序中的下一个排列应该是“DEABCF”。让我们理解以上步骤，找到下一个排列。“第一个字符”将是“C”。“第二个字符”将是“E”。在交换了这两个之后，我们得到了“DEFCBA”。最后一步是对“第一个字符”的字符原始索引后的子字符串进行排序。最后，我们得到“DEABCF”。

下面是算法的实现。

## C++

```
// C++ Program to print all permutations
// of a string in sorted order.
#include <bits/stdc++.h>
using namespace std;

/* Following function is needed for library function qsort(). Refer
http://www.cplusplus.com/reference/clibrary/cstdlib/qsort/ */
int compare (const void *a, const void * b)
{ return ( *(char *)a - *(char *)b ); }

// A utility function two swap two characters a and b
void swap (char* a, char* b)
{
    char t = *a;
    *a = *b;
    *b = t;
}

// This function finds the index of the smallest character
// which is greater than 'first' and is present in str[l..h]
int findCeil (char str[], char first, int l, int h)
{
    // initialize index of ceiling element
    int ceilIndex = l;

    // Now iterate through rest of the elements and find
    // the smallest character greater than 'first'
    for (int i = l+1; i <= h; i++)
    if (str[i] > first && str[i] < str[ceilIndex])
            ceilIndex = i;

    return ceilIndex;
}

// Print all permutations of str in sorted order
void sortedPermutations ( char str[] )
{
    // Get size of string
    int size = strlen(str);

    // Sort the string in increasing order
    qsort( str, size, sizeof( str[0] ), compare );

    // Print permutations one by one
    bool isFinished = false;
    while ( ! isFinished )
    {
        // print this permutation
        cout << str << endl;

        // Find the rightmost character which is
        // smaller than its next character.
        // Let us call it 'first char'
        int i;
        for ( i = size - 2; i >= 0; --i )
        if (str[i] < str[i+1])
            break;

        // If there is no such character, all are
        // sorted in decreasing order, means we
        // just printed the last permutation and we are done.
        if ( i == -1 )
            isFinished = true;
        else
        {
            // Find the ceil of 'first char' in
            // right of first character.
            // Ceil of a character is the smallest
            // character greater than it
            int ceilIndex = findCeil( str, str[i], i + 1, size - 1 );

            // Swap first and second characters
            swap( &str[i], &str[ceilIndex] );

            // Sort the string on right of 'first char'
            qsort( str + i + 1, size - i - 1, sizeof(str[0]), compare );
        }
    }
}

// Driver program to test above function
int main()
{
    char str[] = "ABCD";
    sortedPermutations( str );
    return 0;
}

// This is code is contributed by rathbhupendra
```

## C

```
// Program to print all permutations of a string in sorted order.
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

/* Following function is needed for library function qsort(). Refer
http://www.cplusplus.com/reference/clibrary/cstdlib/qsort/ */
int compare (const void *a, const void * b)
{ return ( *(char *)a - *(char *)b ); }

// A utility function two swap two characters a and b
void swap (char* a, char* b)
{
    char t = *a;
    *a = *b;
    *b = t;
}

// This function finds the index of the smallest character
// which is greater than 'first' and is present in str[l..h]
int findCeil (char str[], char first, int l, int h)
{
    // initialize index of ceiling element
    int ceilIndex = l;

    // Now iterate through rest of the elements and find
    // the smallest character greater than 'first'
    for (int i = l+1; i <= h; i++)
    if (str[i] > first && str[i] < str[ceilIndex])
            ceilIndex = i;

    return ceilIndex;
}

// Print all permutations of str in sorted order
void sortedPermutations ( char str[] )
{
    // Get size of string
    int size = strlen(str);

    // Sort the string in increasing order
    qsort( str, size, sizeof( str[0] ), compare );

    // Print permutations one by one
    bool isFinished = false;
    while ( ! isFinished )
    {
        // print this permutation
        printf ("%s \n", str);

        // Find the rightmost character which is smaller than its next
        // character. Let us call it 'first char'
        int i;
        for ( i = size - 2; i >= 0; --i )
        if (str[i] < str[i+1])
            break;

        // If there is no such character, all are sorted in decreasing order,
        // means we just printed the last permutation and we are done.
        if ( i == -1 )
            isFinished = true;
        else
        {
            // Find the ceil of 'first char' in right of first character.
            // Ceil of a character is the smallest character greater than it
            int ceilIndex = findCeil( str, str[i], i + 1, size - 1 );

            // Swap first and second characters
            swap( &str[i], &str[ceilIndex] );

            // Sort the string on right of 'first char'
            qsort( str + i + 1, size - i - 1, sizeof(str[0]), compare );
        }
    }
}

// Driver program to test above function
int main()
{
    char str[] = "ABCD";
    sortedPermutations( str );
    return 0;
}
```

**输出:**

```
ABCD
ABDC
....
....
DCAB
DCBA
```

上述程序时间复杂度的上限是 O(n^2 x n！).我们可以优化上述算法的步骤 4，以找到下一个置换。我们可以反转子阵列，而不是在“第一个字符”后对子阵列进行排序，因为我们在交换后得到的子阵列总是以非递增的顺序进行排序。这种优化使得时间复杂度为 O(n×n！).请参见以下优化代码。

## C++

```
#include <bits/stdc++.h>
using namespace std;

// An optimized version that uses reverse instead of sort for
// finding the next permutation

// A utility function to reverse a string str[l..h]
void reverse(char str[], int l, int h)
{
    while (l < h)
    {
        swap(&str[l], &str[h]);
        l++;
        h--;
    }
}

// Print all permutations of str in sorted order
void sortedPermutations ( char str[] )
{
    // Get size of string
    int size = strlen(str);

    // Sort the string in increasing order
    qsort( str, size, sizeof( str[0] ), compare );

    // Print permutations one by one
    bool isFinished = false;
    while ( ! isFinished )
    {
        // print this permutation
        cout << str << endl;

        // Find the rightmost character which
        // is smaller than its next character.
        // Let us call it 'first char'
        int i;
        for ( i = size - 2; i >= 0; --i )
        if (str[i] < str[i+1])
            break;

        // If there is no such character, all
        // are sorted in decreasing order,
        // means we just printed the last
        // permutation and we are done.
        if ( i == -1 )
            isFinished = true;
        else
        {
            // Find the ceil of 'first char' in
            // right of first character.
            // Ceil of a character is the
            // smallest character greater than it
            int ceilIndex = findCeil( str, str[i], i + 1, size - 1 );

            // Swap first and second characters
            swap( &str[i], &str[ceilIndex] );

            // reverse the string on right of 'first char'
            reverse( str, i + 1, size - 1 );
        }
    }
}

// This code is contributed by rathbhupendra
```

## C

```
// An optimized version that uses reverse instead of sort for
// finding the next permutation

// A utility function to reverse a string str[l..h]
void reverse(char str[], int l, int h)
{
   while (l < h)
   {
       swap(&str[l], &str[h]);
       l++;
       h--;
   }
}

// Print all permutations of str in sorted order
void sortedPermutations ( char str[] )
{
    // Get size of string
    int size = strlen(str);

    // Sort the string in increasing order
    qsort( str, size, sizeof( str[0] ), compare );

    // Print permutations one by one
    bool isFinished = false;
    while ( ! isFinished )
    {
        // print this permutation
        printf ("%s \n", str);

        // Find the rightmost character which is smaller than its next
        // character. Let us call it 'first char'
        int i;
        for ( i = size - 2; i >= 0; --i )
           if (str[i] < str[i+1])
              break;

        // If there is no such character, all are sorted in decreasing order,
        // means we just printed the last permutation and we are done.
        if ( i == -1 )
            isFinished = true;
        else
        {
            // Find the ceil of 'first char' in right of first character.
            // Ceil of a character is the smallest character greater than it
            int ceilIndex = findCeil( str, str[i], i + 1, size - 1 );

            // Swap first and second characters
            swap( &str[i], &str[ceilIndex] );

            // reverse the string on right of 'first char'
            reverse( str, i + 1, size - 1 );
        }
    }
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
import java.util.*;

// An optimized version that uses reverse instead of sort
// for finding the next permutation
class GFG
{

    // A utility function two swap two characters a and b
    static void swap(char[] str, int i, int j)
    {
        char t = str[i];
        str[i] = str[j];
        str[j] = t;
    }

    // A utility function to reverse a string str[l..h]
    static void reverse(char str[], int l, int h)
    {
        while (l < h) {
            swap(str, l, h);
            l++;
            h--;
        }
    }

    // This function finds the index of the smallest
    // character which is greater than 'first' and is
    // present in str[l..h]
    static int findCeil(char str[], char first, int l,
                        int h)
    {
        // initialize index of ceiling element
        int ceilIndex = l;

        // Now iterate through rest of the elements and find
        // the smallest character greater than 'first'
        for (int i = l + 1; i <= h; i++)
            if (str[i] > first && str[i] < str[ceilIndex])
                ceilIndex = i;

        return ceilIndex;
    }

    // Print all permutations of str in sorted order
    static void sortedPermutations(char str[])
    {
        // Get size of string
        int size = str.length;

        // Sort the string in increasing order
        Arrays.sort(str);

        // Print permutations one by one
        boolean isFinished = false;
        while (!isFinished) {
            // print this permutation
            System.out.println(str);

            // Find the rightmost character which is
            // smaller than its next character.
            // Let us call it 'first char'
            int i;
            for (i = size - 2; i >= 0; --i)
                if (str[i] < str[i + 1])
                    break;

            // If there is no such character, all are
            // sorted in decreasing order, means we
            // just printed the last permutation and we are
            // done.
            if (i == -1)
                isFinished = true;
            else {
                // Find the ceil of 'first char' in
                // right of first character.
                // Ceil of a character is the smallest
                // character greater than it
                int ceilIndex = findCeil(str, str[i], i + 1,
                                         size - 1);

                // Swap first and second characters
                swap(str, i, ceilIndex);

                // reverse the string on right of 'first
                // char'
                reverse(str, i + 1, size - 1);
            }
        }
    }

    // Driver program to test above function
    public static void main(String[] args)
    {
        char str[] = "ABCD".toCharArray();
        sortedPermutations(str);
    }
}

// This code is contributed by Swarn Pallav Bhaskar
```

## 蟒蛇 3

```
# An optimized version that uses reverse
# instead of sort for finding the next
# permutation

# A utility function to reverse a
# string str[l..h]
def reverse(str, l, h):

    while (l < h) :
        str[l], str[h] = str[h], str[l]
        l += 1
        h -= 1

    return str

def findCeil(str, c, k, n):

    ans = -1
    val = c

    for i in range(k, n + 1):
        if str[i] > c and str[i] < val:
            val = str[i]
            ans = i

    return ans

# Print all permutations of str in sorted order
def sortedPermutations(str):

    # Get size of string
    size = len(str)

    # Sort the string in increasing order
    str = ''.join(sorted(str))

    # Print permutations one by one
    isFinished = False

    while (not isFinished):

        # Print this permutation
        print(str)

        # Find the rightmost character which
        # is smaller than its next character.
        # Let us call it 'first char' 
        for i in range(size - 2, -1, -1):
            if (str[i] < str[i + 1]):
                break

        # If there is no such character, all
        # are sorted in decreasing order,
        # means we just printed the last
        # permutation and we are done.
        if (i == -1):
            isFinished = True
        else:

            # Find the ceil of 'first char' in
            # right of first character.
            # Ceil of a character is the
            # smallest character greater than it
            ceilIndex = findCeil(str, str[i], i + 1,
                                           size - 1)

            # Swap first and second characters
            str[i], str[ceilIndex] =  str[ceilIndex], str[i]

            # Reverse the string on right of 'first char'
            str = reverse(str, i + 1, size - 1)

# This code is contributed by rohan07
```

当字符重复时，上述程序打印重复排列。我们可以通过跟踪前面的排列来避免它。打印时，如果当前排列与之前排列相同，我们不会打印。
本文由**阿施·巴恩瓦尔**编辑，GeeksforGeeks 团队审核。如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。
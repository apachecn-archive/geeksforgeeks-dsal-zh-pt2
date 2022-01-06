# 使用数组元素制作字母

> 原文:[https://www . geesforgeks . org/make-alphabets-use-elements-array/](https://www.geeksforgeeks.org/make-alphabets-using-elements-array/)

给定一个正整数数组，找出我们可以用数组元素组成的所有字母。
**例:**

```
Input : arr[] = {6, 5}
Output : A
In this example, we can take 6 and 5
as 65 that gives us A.

Input : arr[] = {5, 6, 6}
Output : A B
Here we can take 6 and 5 as 65 to make A. 
And 6 and 6 as 66 to make B.

Input : arr[] = {1, 0, 1, 0}
Output: d e n
Here we can take 1, 0 and 0 as 100 to make d.
1, 0 and 1 as 101 to make e. And 
1, 1, and 0 as 110 to make n.
```

**方法:**
方法是迭代一个从 char A 到 Z 的循环，检查数组中是否存在它们的 ASCII 值的两位数(A 的 ASCII 值是 65，A 的 ASCII 值的位数是 6 和 5)。为此，我们必须计算数组中每个元素的频率。和小字母一样。
以下是上述办法的实施情况。

## C++

```
// CPP program to find all the capital characters
// we can make from the given array.
#include <bits/stdc++.h>
using namespace std;

// Function returns all the capital characters
//  we can make.
string findCharacters(int arr[], int n)
{
    string ans = "";
    int brr[10] = { 0 };

    // Calculating the frequency of the elements.
    for (int i = 0; i < n; i++)
        brr[arr[i]]++;

    // Checking for capital alphabets.
    for (char ch = 'A'; ch <= 'Z'; ch++)
    {

        // Storing one digit in x and other in y.
        int x = ch / 10;
        int y = ch % 10;
        brr[x]--;
        brr[y]--;

        // If both the digits exist.
        if (brr[x] >= 0 && brr[y] >= 0)
        {

            // Putting in the result
            ans += ch;
            ans += ' ';
        }
        brr[x]++;
        brr[y]++;
    }

    // Checking for alphabets a, b and c.
    for (char ch = 'a'; ch <= 'c'; ch++)
    {
        int x = ch / 10;
        int y = ch % 10;
        brr[x]--;
        brr[y]--;

        // If all the digits exist.
        if (brr[x] >= 0 && brr[y] >= 0)
        {

            // Putting in the result
            ans += ch;
            ans += ' ';
        }
        brr[x]++;
        brr[y]++;
    }

    // Checking for d to z.
    for (char ch = 'd'; ch <= 'z'; ch++)
    {
        int x = (ch / 10) / 10;
        int y = (ch / 10) % 10;
        int z = ch % 10;
        brr[x]--;
        brr[y]--;
        brr[z]--;

        // If all the digits exist.
        if (brr[x] >= 0 && brr[y] >= 0 && brr[z] >= 0)
        {

            // Putting in the result
            ans += ch;
            ans += ' ';
        }
        brr[x]++;
        brr[y]++;
        brr[z]++;
    }

    return ans;
}

// Driver function
int main()
{
    int arr[] = { 5, 6, 6 }, n;
    n = sizeof(arr) / sizeof(arr[0]);
    cout << findCharacters(arr, n) << endl;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find all the capital characters
// we can make from the given array.
import java.util.*;
import java.lang.*;

public class GeeksforGeeks
{

    // Function returns all the capital characters we can make.
    public static String findCharacters(int arr[], int n)
    {
        String ans = "";
        int[] brr = new int[10];

        // Calculating the frequency of the elements.
        for (int i = 0; i < n; i++)
            brr[arr[i]]++;

        for (char ch = 'A'; ch <= 'Z'; ch++)
        {

            // Storing one digit in x and other in y.
            int x = ch / 10;
            int y = ch % 10;
            brr[x]--;
            brr[y]--;

            // If both the digits exist.
            if (brr[x] >= 0 && brr[y] >= 0)
            {

                // Putting in the result
                ans += ch;
                ans += ' ';
            }
            brr[x]++;
            brr[y]++;
        }

        // Checking for alphabets a, b and c.
        for (char ch = 'a'; ch <= 'c'; ch++)
        {
            int x = ch / 10;
            int y = ch % 10;
            brr[x]--;
            brr[y]--;

            // If all the digits exist.
            if (brr[x] >= 0 && brr[y] >= 0)
            {

                // Putting in the result
                ans += ch;
                ans += ' ';
            }
            brr[x]++;
            brr[y]++;
        }

        // Checking for d to z.
        for (char ch = 'd'; ch <= 'z'; ch++)
        {
            int x = (ch / 10) / 10;
            int y = (ch / 10) % 10;
            int z = ch % 10;
            brr[x]--;
            brr[y]--;
            brr[z]--;

            // If all the digits exist.
            if (brr[x] >= 0 && brr[y] >= 0 && brr[z] >= 0)
            {

                // Putting in the result
                ans += ch;
                ans += ' ';
            }
            brr[x]++;
            brr[y]++;
            brr[z]++;
        }

        return ans;
    }

    // Driver function
    public static void main(String argc[])
    {
        int arr[] = { 5, 6, 6 }, n;
        n = 3;
        System.out.println(findCharacters(arr, n));
    }
}
```

## 计算机编程语言

```
# Python3 program to find all the capital characters
# we can make from the given array.

# Function returns all the capital characters
# we can make.
def findCharacters(arr, n):
    ans = ""
    brr = [0] * 10

    # Calculating the frequency of the elements.
    for i in range(n):
        brr[arr[i]] += 1

    # Checking for capital alphabets.
    for ch in range(ord('A'), ord('Z') + 1):

        # Storing one digit in x and other in y.
        x = ch // 10
        y = ch % 10
        brr[x] -= 1
        brr[y] -= 1

        # If both the digits exist.
        if (brr[x] >= 0 and brr[y] >= 0):

            # Putting in the result
            ans += chr(ch)
            ans += ' '
        brr[x] += 1
        brr[y] += 1

    # Checking for alphabets a, b and c.
    for ch in range(ord('a'), ord('c') + 1):
        x = ch // 10
        y = ch % 10
        brr[x] -= 1
        brr[y] -= 1

        # If all the digits exist.
        if (brr[x] >= 0 and brr[y] >= 0):

            # Putting in the result
            ans += chr(ch)
            ans += ' '
        brr[x] += 1
        brr[y] += 1

    # Checking for d to z.
    for ch in range(ord('d'), ord('z') + 1):
        x = (ch // 10) // 10
        y = (ch // 10) % 10
        z = ch % 10
        brr[x] -= 1
        brr[y] -= 1
        brr[z] -= 1

        # If all the digits exist.
        if (brr[x] >= 0 and brr[y] >= 0 and brr[z] >= 0):

            # Putting in the result
            ans += chr(ch)
            ans += ' '
        brr[x] += 1
        brr[y] += 1
        brr[z] += 1

    return ans

# Driver function
arr = [5, 6, 6]
n = len(arr)
print(findCharacters(arr, n))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program to find all the capital
// characters we can make from the given array.
using System;

class GeeksforGeeks
{
    // Function returns all the capital
    // characters we can make.
    public static String findCharacters(int []arr, int n )
    {
        String ans = "";
        int []brr = new int[10];

        // Calculating the frequency of the elements.
        for (int i = 0; i < n; i++)
            brr[arr[i]]++;

        for (char ch = 'A'; ch <= 'Z'; ch++)
        {
            // Storing one digit in x and other in y.
            int x = ch / 10;
            int y = ch % 10;
            brr[x]--;
            brr[y]--;

            // If both the digits exist.
            if (brr[x] >= 0 && brr[y] >= 0)
            {
                // Putting in the result
                ans += ch;
                ans += ' ';
            }
            brr[x]++;
            brr[y]++;
        }

        // Checking for alphabets a, b and c.
        for (char ch = 'a'; ch <= 'c'; ch++)
        {
            int x = ch / 10;
            int y = ch % 10;
            brr[x]--;
            brr[y]--;

            // If all the digits exist.
            if (brr[x] >= 0 && brr[y] >= 0)
            {

                // Putting in the result
                ans += ch;
                ans += ' ';
            }
            brr[x]++;
            brr[y]++;
        }

        // Checking for d to z.
        for (char ch = 'd'; ch <= 'z'; ch++)
        {
            int x = (ch / 10) / 10;
            int y = (ch / 10) % 10;
            int z = ch % 10;
            brr[x]--;
            brr[y]--;
            brr[z]--;

            // If all the digits exist.
            if (brr[x] >= 0 && brr[y] >= 0 && brr[z] >= 0)
            {
                // Putting in the result
                ans += ch;
                ans += ' ';
            }
            brr[x]++;
            brr[y]++;
            brr[z]++;
        }

        return ans;
    }

    // Driver function
    public static void Main()
    {
        int []arr = {5, 6, 6};
        int n = 3;
        Console.Write(findCharacters(arr, n));
    }
}

// This code is contributed by nitin mittal.
```

## java 描述语言

```
<script>

// JavaScript program to find
// all the capital characters
// we can make from the given array.

    // Function returns all the capital
    // characters we can make.
    function findCharacters(arr,n)
    {
        let ans = "";
        let brr = new Array(10);
        for(let i=0;i<brr.length;i++)
        {
            brr[i]=0;
        }

        // Calculating the frequency of the elements.
        for (let i = 0; i < n; i++)
            brr[arr[i]]++;

        for (let ch = 'A'.charCodeAt(0);
        ch <= 'Z'.charCodeAt(0); ch++)
        {

            // Storing one digit in x and other in y.
            let x = Math.floor(ch / 10);
            let y = ch % 10;
            brr[x]--;
            brr[y]--;

            // If both the digits exist.
            if (brr[x] >= 0 && brr[y] >= 0)
            {

                // Putting in the result
                ans += String.fromCharCode(ch);
                ans += ' ';
            }
            brr[x]++;
            brr[y]++;
        }

        // Checking for alphabets a, b and c.
        for (let ch = 'a'.charCodeAt(0);
        ch <= 'c'.charCodeAt(0); ch++)
        {
            let x = Math.floor(ch / 10);
            let y = ch % 10;
            brr[x]--;
            brr[y]--;

            // If all the digits exist.
            if (brr[x] >= 0 && brr[y] >= 0)
            {

                // Putting in the result
                ans += String.fromCharCode(ch);
                ans += ' ';
            }
            brr[x]++;
            brr[y]++;
        }

        // Checking for d to z.
        for (let ch = 'd'.charCodeAt(0);
        ch <= 'z'.charCodeAt(0); ch++)
        {
            let x = Math.floor((ch / 10) / 10);
            let y = (ch / 10) % 10;
            let z = ch % 10;
            brr[x]--;
            brr[y]--;
            brr[z]--;

            // If all the digits exist.
            if (brr[x] >= 0 && brr[y] >= 0 &&
            brr[z] >= 0)
            {

                // Putting in the result
                ans += String.fromCharCode(ch);
                ans += ' ';
            }
            brr[x]++;
            brr[y]++;
            brr[z]++;
        }

        return ans;
    }

    // Driver function
    let arr=[5, 6, 6 ];
    let n = 3;
    document.write(findCharacters(arr, n));

// This code is contributed by patel2127

</script>
```

**输出:**

```
A B
```

**时间复杂度:** O(n)
# 索引对(I，j)的计数，使得删除第个字符后的字符串等于删除第个字符后的字符串

> 原文:[https://www . geesforgeks . org/index-pairs-I-j-so-string-deleting-with-character-等于 string-deleting-jth-character/](https://www.geeksforgeeks.org/count-of-index-pairs-i-j-such-that-string-after-deleting-ith-character-is-equal-to-string-after-deleting-jth-character/)

给定一个由 **N 个**字符组成的[字符串](https://www.geeksforgeeks.org/string-data-structure/) **字符串**，任务是计算 **(i，j)** 的有效无序对的计数，使得删除 **i <sup>th</sup>** 字符后的字符串等于删除**j<sup>th</sup>T15】字符后的字符串。**

**示例:**

> **输入:** str = "aabb"
> **输出:** 2
> **说明:**删除第一个元素后的字符串为“abb”，删除第二个元素后的字符串为“abb”。同样，删除第三个元素后的字符串为“aab”，删除第四个元素后的字符串为“aab”。因此，(I，j)的有效对的数量是 2，即(1，2)和(3，4)。
> 
> **输入:**str = " aaaaa "
> T3】输出: 15

**方法:**给定的问题可以使用以下观察结果来解决:

> *   如果 **S <sub>i</sub> = S <sub>j</sub>** ，那么**S<sub>I</sub>= S<sub>I+1</sub>= S<sub>I+2</sub>……= S<sub>j</sub>**必须成立。
> *   Similarly, if **S <sub>I</sub> = S <sub>J</sub>** , then **STR [I] = STR [I+1] = STR [I+2] … = STR [J]** must also hold.

因此，利用上述观察，[双指针技术](https://www.geeksforgeeks.org/two-pointers-technique/)可用于计算[字符串](https://www.geeksforgeeks.org/string-data-structure/) **字符串**中的区间 **(l，r)** ，使得**字符串【l】= str[l+1]…= str[r]**，对于每个有效的 **(l，r)** ，有效对的计数将为**<sup>r–l</sup>C<sub>2</sub>**

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the count of valid
// pairs (i, j) such that string after
// deleting ith character is equal to
// string after deleting jth character
int countValidPairs(string str, int N)
{

    // Stores the required count
    int ans = 0;

    // Loop to iterate the given array
    for (int l = 0, r; l < N; l = r) {

        // initial end point
        r = l;

        // Loop to calculate the range
        // [l, r] such that all characters
        // from l to r are equal
        while (r < N && str[l] == str[r]) {
            r++;
        }

        // Update the answer
        ans += ((r - l) * (r - l - 1)) / 2;
    }

    // Return Answer
    return ans;
}

// Driver Code
int main()
{
    string str = "aaaaaa";
    cout << countValidPairs(str, str.length());

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
public class GFG
{

// Function to find the count of valid
// pairs (i, j) such that string after
// deleting ith character is equal to
// string after deleting jth character
static int countValidPairs(String str, int N)
{

    // Stores the required count
    int ans = 0;

    // Loop to iterate the given array
    for (int l = 0, r; l < N; l = r) {

        // initial end point
        r = l;

        // Loop to calculate the range
        // [l, r] such that all characters
        // from l to r are equal
        Character c1 = str.charAt(l);
        Character c2 = str.charAt(r);
        while (r < N && c1.equals(c2)) {
            r++;
        }

        // Update the answer
        ans += ((r - l) * (r - l - 1)) / 2;
    }

    // Return Answer
    return ans;
}

// Driver Code
public static void main(String args[])
{
    String str = "aaaaaa";
    System.out.print(countValidPairs(str, str.length()));
}
}

// This code is contributed by Samim Hossain Mondal.
```

## 蟒蛇 3

```
# Python program for the above approach

# Function to find the count of valid
# pairs (i, j) such that string after
# deleting ith character is equal to
# string after deleting jth character
def countValidPairs(str, N):

    # Stores the required count
    ans = 0;

    # Loop to iterate the given array
    l = 0;
    r = None;

    while(l < N):
        # initial end point
        r = l;

        # Loop to calculate the range
        # [l, r] such that all characters
        # from l to r are equal
        while (r < N and str[l] == str[r]):
            r += 1

        # Update the answer
        ans += ((r - l) * (r - l - 1)) // 2;

        l = r;

    # Return Answer
    return ans;

# Driver Code
str = "aaaaaa";
print(countValidPairs(str, len(str)));

# This code is contributed by Saurabh Jaiswal
```

## C#

```
// C# program for the above approach
using System;
class GFG
{

// Function to find the count of valid
// pairs (i, j) such that string after
// deleting ith character is equal to
// string after deleting jth character
static int countValidPairs(string str, int N)
{

    // Stores the required count
    int ans = 0;

    // Loop to iterate the given array
    for (int l = 0, r; l < N; l = r) {

        // initial end point
        r = l;

        // Loop to calculate the range
        // [l, r] such that all characters
        // from l to r are equal
        char c1 = str[l];
        char c2 = str[r];
        while (r < N && c1.Equals(c2)) {
            r++;
        }

        // Update the answer
        ans += ((r - l) * (r - l - 1)) / 2;
    }

    // Return Answer
    return ans;
}

// Driver Code
public static void Main()
{
    string str = "aaaaaa";
    Console.Write(countValidPairs(str, str.Length));

}
}

// This code is contributed by Samim Hossain Mondal.
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to find the count of valid
// pairs (i, j) such that string after
// deleting ith character is equal to
// string after deleting jth character
function countValidPairs(str, N)
{

    // Stores the required count
    let ans = 0;

    // Loop to iterate the given array
    for (let l = 0, r; l < N; l = r) {

        // initial end point
        r = l;

        // Loop to calculate the range
        // [l, r] such that all characters
        // from l to r are equal
        while (r < N && str[l] == str[r]) {
            r++;
        }

        // Update the answer
        ans += ((r - l) * (r - l - 1)) / 2;
    }

    // Return Answer
    return ans;
}

// Driver Code
let str = "aaaaaa";
document.write(countValidPairs(str, str.length));

// This code is contributed by Samim Hossain Mondal.
</script>
```

**Output**

```
15
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)
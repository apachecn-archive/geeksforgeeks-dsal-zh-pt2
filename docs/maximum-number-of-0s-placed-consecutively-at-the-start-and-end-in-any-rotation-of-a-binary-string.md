# 在二进制字符串的任何一次旋转的开始和结束连续放置的 0 的最大数量

> 原文:[https://www . geesforgeks . org/二进制字符串任意旋转开始和结束时连续放置 0 的最大数量/](https://www.geeksforgeeks.org/maximum-number-of-0s-placed-consecutively-at-the-start-and-end-in-any-rotation-of-a-binary-string/)

给定大小为 **N** 的[二进制字符串](https://www.geeksforgeeks.org/tag/binary-string/) **S** ，任务是最大化给定字符串 **S** 的任意[旋转开始和结束时出现的连续 **0** s 的计数总和。](https://www.geeksforgeeks.org/generate-rotations-given-string/)

**示例:**

> **输入:** S = "1001"
> **输出:** 2
> **解释:**
> 字符串所有可能的旋转都是:
> 【1001】:开始时计数为 0 = 0；结尾= 0。总和= 0 + 0 = 0。
> “0011”:开始时计数为 0 = 2；结尾= 0。总和= 2+0 = 2
> “0110”:开始时的 0 计数= 1；结尾= 1。总和= 1 + 1 = 2。
> “1100”:开始时计数为 0 = 0；结尾= 2。总和= 0 + 2 = 2
> 因此，最大可能总和为 2。
> 
> **输入:** S = "01010"
> **输出:** 2
> **解释:**
> 字符串所有可能的旋转为:
> 【01010】:开始时的 0 计数= 1；结尾= 1。总和= 1+1 = 1
> “10100”:开始时的 0 计数= 0；结尾= 2。总和= 0+2 = 2
> “01001”:开始时的 0 计数= 1；结尾= 0。总和= 1+0 = 1
> “10010”:开始时的 0 计数= 0；结尾= 1。总和= 0+1 = 1
> “00101”:开始时的 0 计数= 2；结尾= 0。总和= 2+0=2
> 因此，最大可能总和为 2。

**天真方法:**最简单的想法是[生成给定字符串](https://www.geeksforgeeks.org/generate-rotations-given-string/)的所有旋转，对于每个旋转，计算字符串开头和结尾出现的 0 的数量，并计算它们的总和。最后，打印得到的最大和。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the maximum sum of
// consecutive 0s present at the start
// and end of a string present in any
// of the rotations of the given string
void findMaximumZeros(string str, int n)
{
    // Check if all the characters
    // in the string are 0
    int c0 = 0;

    // Iterate over characters
    // of the string
    for (int i = 0; i < n; ++i) {
        if (str[i] == '0')
            c0++;
    }

    // If the frequency of '1' is 0
    if (c0 == n) {

        // Print n as the result
        cout << n;
        return;
    }

    // Concatenate the string
    // with itself
    string s = str + str;

    // Stores the required result
    int mx = 0;

    // Generate all rotations of the string
    for (int i = 0; i < n; ++i) {

        // Store the number of consecutive 0s
        // at the start and end of the string
        int cs = 0;
        int ce = 0;

        // Count 0s present at the start
        for (int j = i; j < i + n; ++j) {
            if (s[j] == '0')
                cs++;
            else
                break;
        }

        // Count 0s present at the end
        for (int j = i + n - 1; j >= i; --j) {
            if (s[j] == '0')
                ce++;
            else
                break;
        }

        // Calculate the sum
        int val = cs + ce;

        // Update the overall
        // maximum sum
        mx = max(val, mx);
    }

    // Print the result
    cout << mx;
}

// Driver Code
int main()
{
    // Given string
    string s = "1001";

    // Store the size of the string
    int n = s.size();

    findMaximumZeros(s, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to find the maximum sum of
// consecutive 0s present at the start
// and end of a string present in any
// of the rotations of the given string
static void findMaximumZeros(String str, int n)
{

    // Check if all the characters
    // in the string are 0
    int c0 = 0;

    // Iterate over characters
    // of the string
    for(int i = 0; i < n; ++i)
    {
        if (str.charAt(i) == '0')
            c0++;
    }

    // If the frequency of '1' is 0
    if (c0 == n)
    {

        // Print n as the result
        System.out.print(n);
        return;
    }

    // Concatenate the string
    // with itself
    String s = str + str;

    // Stores the required result
    int mx = 0;

    // Generate all rotations of the string
    for(int i = 0; i < n; ++i)
    {

        // Store the number of consecutive 0s
        // at the start and end of the string
        int cs = 0;
        int ce = 0;

        // Count 0s present at the start
        for(int j = i; j < i + n; ++j)
        {
            if (s.charAt(j) == '0')
                cs++;
            else
                break;
        }

        // Count 0s present at the end
        for(int j = i + n - 1; j >= i; --j)
        {
            if (s.charAt(j) == '0')
                ce++;
            else
                break;
        }

        // Calculate the sum
        int val = cs + ce;

        // Update the overall
        // maximum sum
        mx = Math.max(val, mx);
    }

    // Print the result
    System.out.print(mx);
}

// Driver Code
public static void main(String[] args)
{

    // Given string
    String s = "1001";

    // Store the size of the string
    int n = s.length();

    findMaximumZeros(s, n);
}
}

// This code is contributed by susmitakundugoaldanga
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the maximum sum of
# consecutive 0s present at the start
# and end of a string present in any
# of the rotations of the given string
def findMaximumZeros(st, n):

    # Check if all the characters
    # in the string are 0
    c0 = 0

    # Iterate over characters
    # of the string
    for i in range(n):
        if (st[i] == '0'):
            c0 += 1

    # If the frequency of '1' is 0
    if (c0 == n):

        # Print n as the result
        print(n)
        return

    # Concatenate the string
    # with itself
    s = st + st

    # Stores the required result
    mx = 0

    # Generate all rotations of the string
    for i in range(n):

        # Store the number of consecutive 0s
        # at the start and end of the string
        cs = 0
        ce = 0

        # Count 0s present at the start
        for j in range(i, i + n):
            if (s[j] == '0'):
                cs += 1
            else:
                break

        # Count 0s present at the end
        for j in range(i + n - 1, i - 1, -1):
            if (s[j] == '0'):
                ce += 1
            else:
                break

        # Calculate the sum
        val = cs + ce

        # Update the overall
        # maximum sum
        mx = max(val, mx)

    # Print the result
    print(mx)

# Driver Code
if __name__ == "__main__":

    # Given string
    s = "1001"

    # Store the size of the string
    n = len(s)

    findMaximumZeros(s, n)

    # This code is contributed by ukasp.
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to find the maximum sum of
// consecutive 0s present at the start
// and end of a string present in any
// of the rotations of the given string
static void findMaximumZeros(string str, int n)
{

    // Check if all the characters
    // in the string are 0
    int c0 = 0;

    // Iterate over characters
    // of the string
    for(int i = 0; i < n; ++i)
    {
        if (str[i] == '0')
            c0++;
    }

    // If the frequency of '1' is 0
    if (c0 == n)
    {

        // Print n as the result
        Console.Write(n);
        return;
    }

    // Concatenate the string
    // with itself
    string s = str + str;

    // Stores the required result
    int mx = 0;

    // Generate all rotations of the string
    for(int i = 0; i < n; ++i)
    {

        // Store the number of consecutive 0s
        // at the start and end of the string
        int cs = 0;
        int ce = 0;

        // Count 0s present at the start
        for(int j = i; j < i + n; ++j)
        {
            if (s[j] == '0')
                cs++;
            else
                break;
        }

        // Count 0s present at the end
        for(int j = i + n - 1; j >= i; --j)
        {
            if (s[j] == '0')
                ce++;
            else
                break;
        }

        // Calculate the sum
        int val = cs + ce;

        // Update the overall
        // maximum sum
        mx = Math.Max(val, mx);
    }

    // Print the result
    Console.Write(mx);
}

// Driver Code
public static void Main(string[] args)
{

    // Given string
    string s = "1001";

    // Store the size of the string
    int n = s.Length;

    findMaximumZeros(s, n);
}
}

// This code is contributed by AnkThon
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to find the maximum sum of
// consecutive 0s present at the start
// and end of a string present in any
// of the rotations of the given string
function findMaximumZeros(str, n)
{
    // Check if all the characters
    // in the string are 0
    var c0 = 0;

    var i;
    // Iterate over characters
    // of the string
    for (i = 0; i < n; ++i) {
        if (str[i] == '0')
            c0++;
    }

    // If the frequency of '1' is 0
    if (c0 == n) {

        // Print n as the result
        document.write(n);
        return;
    }

    // Concatenate the string
    // with itself
    var s = str + str;

    // Stores the required result
    var mx = 0;
    var j;

    // Generate all rotations of the string
    for (i = 0; i < n; ++i) {

        // Store the number of consecutive 0s
        // at the start and end of the string
        var cs = 0;
        var ce = 0;

        // Count 0s present at the start
        for (j = i; j < i + n; ++j) {
            if (s[j] == '0')
                cs++;
            else
                break;
        }

        // Count 0s present at the end
        for (j = i + n - 1; j >= i; --j) {
            if (s[j] == '0')
                ce++;
            else
                break;
        }

        // Calculate the sum
        var val = cs + ce;

        // Update the overall
        // maximum sum
        mx = Math.max(val, mx);
    }

    // Print the result
    document.write(mx);
}

    // Driver Code
    // Given string
    var s = "1001";

    // Store the size of the string
    var n = s.length;

    findMaximumZeros(s, n);

</script>
```

**Output:** 

```
2
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(N)*

**有效方法:**想法是在给定的字符串中找到[连续 0 的最大数量。另外，求字符串开始和结束处连续的 **0** 的和，然后打印出其中的最大值。
按照以下步骤解决问题:](https://www.geeksforgeeks.org/maximum-consecutive-ones-or-zeros-in-a-binary-array/)

*   检查 **S** 串中的[频率是否等于 **0** 。如果发现为真，打印 **N** 的值作为结果。](https://www.geeksforgeeks.org/c-program-to-find-the-frequency-of-characters-in-a-string/)
*   否则，请执行以下步骤:
    *   将给定字符串中连续 0 的最大数量[存储在一个变量中，比如 **X** 。](https://www.geeksforgeeks.org/maximum-consecutive-ones-or-zeros-in-a-binary-array/)
    *   初始化两个变量，**开始**为 **0** ，**结束**为 **N-1** 。
    *   当 **S【开始】**不等于“ **1** 时，将 **cnt** 和 **start** 的值增加 **1** 。
    *   当 **S【结束】**不等于“ **1** 时，增加 **cnt** 的值，减少**end****1**。
    *   打印 **X** 和**CNT**T5 的[最大值作为结果。](https://www.geeksforgeeks.org/stdmax-in-cpp/)

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the maximum sum of
// consecutive 0s present at the start
// and end of any rotation of the string str
void findMaximumZeros(string str, int n)
{
    // Stores the count of 0s
    int c0 = 0;
    for (int i = 0; i < n; ++i) {
        if (str[i] == '0')
            c0++;
    }

    // If the frequency of '1' is 0
    if (c0 == n) {

        // Print n as the result
        cout << n;
        return;
    }

    // Stores the required sum
    int mx = 0;

    // Find the maximum consecutive
    // length of 0s present in the string
    int cnt = 0;

    for (int i = 0; i < n; i++) {
        if (str[i] == '0')
            cnt++;
        else {
            mx = max(mx, cnt);
            cnt = 0;
        }
    }

    // Update the overall maximum sum
    mx = max(mx, cnt);

    // Find the number of 0s present at
    // the start and end of the string
    int start = 0, end = n - 1;
    cnt = 0;

    // Update the count of 0s at the start
    while (str[start] != '1' && start < n) {
        cnt++;
        start++;
    }

    // Update the count of 0s at the end
    while (str[end] != '1' && end >= 0) {
        cnt++;
        end--;
    }

    // Update the maximum sum
    mx = max(mx, cnt);

    // Print the result
    cout << mx;
}

// Driver Code
int main()
{
    // Given string
    string s = "1001";

    // Store the size of the string
    int n = s.size();

    findMaximumZeros(s, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to find the maximum sum of
// consecutive 0s present at the start
// and end of any rotation of the string str
static void findMaximumZeros(String str, int n)
{

    // Stores the count of 0s
    int c0 = 0;
    for(int i = 0; i < n; ++i)
    {
        if (str.charAt(i) == '0')
            c0++;
    }

    // If the frequency of '1' is 0
    if (c0 == n)
    {

        // Print n as the result
        System.out.print(n);
        return;
    }

    // Stores the required sum
    int mx = 0;

    // Find the maximum consecutive
    // length of 0s present in the string
    int cnt = 0;

    for(int i = 0; i < n; i++)
    {
        if (str.charAt(i) == '0')
            cnt++;
        else
        {
            mx = Math.max(mx, cnt);
            cnt = 0;
        }
    }

    // Update the overall maximum sum
    mx = Math.max(mx, cnt);

    // Find the number of 0s present at
    // the start and end of the string
    int start = 0, end = n - 1;
    cnt = 0;

    // Update the count of 0s at the start
    while (str.charAt(start) != '1' && start < n)
    {
        cnt++;
        start++;
    }

    // Update the count of 0s at the end
    while (str.charAt(end) != '1' && end >= 0)
    {
        cnt++;
        end--;
    }

    // Update the maximum sum
    mx = Math.max(mx, cnt);

    // Print the result
    System.out.println(mx);
}

// Driver Code
public static void main (String[] args)
{

    // Given string
    String s = "1001";

    // Store the size of the string
    int n = s.length();

    findMaximumZeros(s, n);
}
}

// This code is contributed by sanjoy_62
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the maximum sum of
# consecutive 0s present at the start
# and end of any rotation of the string str
def findMaximumZeros(string, n):

    # Stores the count of 0s
    c0 = 0

    for i in range(n):
        if (string[i] == '0'):
            c0 += 1

    # If the frequency of '1' is 0
    if (c0 == n):

        # Print n as the result
        print(n, end = "")
        return

    # Stores the required sum
    mx = 0

    # Find the maximum consecutive
    # length of 0s present in the string
    cnt = 0

    for i in range(n):
        if (string[i] == '0'):
            cnt += 1
        else:
            mx = max(mx, cnt)
            cnt = 0

    # Update the overall maximum sum
    mx = max(mx, cnt)

    # Find the number of 0s present at
    # the start and end of the string
    start = 0
    end = n - 1
    cnt = 0

    # Update the count of 0s at the start
    while (string[start] != '1' and start < n):
        cnt += 1
        start += 1

    # Update the count of 0s at the end
    while (string[end] != '1' and  end >= 0):
        cnt += 1
        end -= 1

    # Update the maximum sum
    mx = max(mx, cnt)

    # Print the result
    print(mx, end = "")

# Driver Code
if __name__ == "__main__":

    # Given string
    s = "1001"

    # Store the size of the string
    n = len(s)

    findMaximumZeros(s, n)

# This code is contributed by AnkThon
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to find the maximum sum of
// consecutive 0s present at the start
// and end of any rotation of the string str
static void findMaximumZeros(string str, int n)
{

    // Stores the count of 0s
    int c0 = 0;
    for(int i = 0; i < n; ++i)
    {
        if (str[i] == '0')
            c0++;
    }

    // If the frequency of '1' is 0
    if (c0 == n)
    {

        // Print n as the result
         Console.Write(n);
        return;
    }

    // Stores the required sum
    int mx = 0;

    // Find the maximum consecutive
    // length of 0s present in the string
    int cnt = 0;

    for(int i = 0; i < n; i++)
    {
        if (str[i] == '0')
            cnt++;
        else
        {
            mx = Math.Max(mx, cnt);
            cnt = 0;
        }
    }

    // Update the overall maximum sum
    mx = Math.Max(mx, cnt);

    // Find the number of 0s present at
    // the start and end of the string
    int start = 0, end = n - 1;
    cnt = 0;

    // Update the count of 0s at the start
    while (str[start] != '1' && start < n)
    {
        cnt++;
        start++;
    }

    // Update the count of 0s at the end
    while (str[end] != '1' && end >= 0)
    {
        cnt++;
        end--;
    }

    // Update the maximum sum
    mx = Math.Max(mx, cnt);

    // Print the result
    Console.Write(mx);
}

// Driver Code
static public void Main ()
{

    // Given string
    string s = "1001";

    // Store the size of the string
    int n = s.Length;

    findMaximumZeros(s, n);
}
}

// This code is contributed by avijitmondal1998
```

## java 描述语言

```
<script>
//Javascript program for
//the above approach

// Function to find the maximum sum of
// consecutive 0s present at the start
// and end of any rotation of the string str
function findMaximumZeros(str, n)
{
    // Stores the count of 0s
    var c0 = 0;
    for (var i = 0; i < n; ++i) {
        if (str[i] == '0')
            c0++;
    }

    // If the frequency of '1' is 0
    if (c0 == n) {

        // Print n as the result
        document.write( n);
        return;
    }

    // Stores the required sum
    var mx = 0;

    // Find the maximum consecutive
    // length of 0s present in the string
    var cnt = 0;

    for (var i = 0; i < n; i++) {
        if (str[i] == '0')
            cnt++;
        else {
            mx = Math.max(mx, cnt);
            cnt = 0;
        }
    }

    // Update the overall maximum sum
    mx = Math.max(mx, cnt);

    // Find the number of 0s present at
    // the start and end of the string
    var start = 0, end = n - 1;
    cnt = 0;

    // Update the count of 0s at the start
    while (str[start] != '1' && start < n) {
        cnt++;
        start++;
    }

    // Update the count of 0s at the end
    while (str[end] != '1' && end >= 0) {
        cnt++;
        end--;
    }

    // Update the maximum sum
    mx = Math.max(mx, cnt);

    // Print the result
    document.write( mx);
}

var s = "1001";
// Store the size of the string
var n = s.length;

findMaximumZeros(s, n);

// This code is contributed by SoumikMondal
</script>
```

**Output:** 

```
2
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)
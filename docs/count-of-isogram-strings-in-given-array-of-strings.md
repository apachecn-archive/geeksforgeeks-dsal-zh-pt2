# 给定字符串数组中等值线字符串的计数

> 原文:[https://www . geeksforgeeks . org/给定字符串数组中的字符串计数/](https://www.geeksforgeeks.org/count-of-isogram-strings-in-given-array-of-strings/)

给定一个包含 **N** 弦的数组 **arr[]** ，任务是找到弦的**计数**，它们是 [**等值线图**](https://www.geeksforgeeks.org/check-string-isogram-not/) 。如果字符串中没有字母出现多次，则该字符串是一个等值线图。

**示例:**

> **输入:**arr[]= {“ABCD”、“derg”、“erty”}
> **输出:** 3
> **解释:**所有给定的字符串都是等值线图。在所有字符串中，没有字符
> 出现不止一次。因此计数为 3
> 
> **输入:**arr[]= {“agka”、“lkmn”}
> **输出:** 1
> **说明:**只有字符串“lkmn”是等值线图。在字符串“agka”
> 中，字符“a”出现了两次。因此计数为 1。

**进场:** [**【贪婪的 T4】**](http://www.geeksforgeeks.org/greedy-algorithms/) 进场可以用来解决这个问题。遍历给定字符串数组中的每个字符串，检查它是否是等值线。为此，请执行以下步骤:

*   遍历字符串数组，并对每个字符串执行以下步骤:
*   创建字符的**频率图**。
*   任何字符的频率**大于 1** 的地方，跳过当前字符串，**移动到下一个**字符串。
*   如果没有字符的频率超过 1，则**将**答案的计数增加 1。
*   遍历所有字符串时，返回存储在答案中的计数。

下面是上述方法的实现:

## C++

```
#include <bits/stdc++.h>
using namespace std;

// Function to check
// if a string is an isogram
bool isIsogram(string s)
{
    // Loop to check
    // if string is isogram or not
    vector<int> freq(26, 0);
    for (char c : s) {
        freq++;
        if (freq > 1) {
            return false;
        }
    }
    return true;
}

// Function to count the number of isograms
int countIsograms(vector<string>& arr)
{
    int ans = 0;

    // Loop to iterate the string array
    for (string x : arr) {
        if (isIsogram(x)) {
            ans++;
        }
    }
    return ans;
}

// Driver Code
int main()
{
    vector<string> arr = { "abcd", "derg", "erty" };

    // Count of isograms in string array arr[]
    cout << countIsograms(arr) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.ArrayList;

class GFG {

    // Function to check
    // if a String is an isogram
    static boolean isIsogram(String s) {

        // Loop to check
        // if String is isogram or not
        int[] freq = new int[26];
        for (int i = 0; i < 26; i++) {
            freq[i] = 0;
        }

        for (char c : s.toCharArray()) {
            freq++;
            if (freq > 1) {
                return false;
            }
        }
        return true;
    }

    // Function to count the number of isograms
    static int countIsograms(ArrayList<String> arr) {
        int ans = 0;

        // Loop to iterate the String array
        for (String x : arr) {
            if (isIsogram(x)) {
                ans++;
            }
        }
        return ans;
    }

    // Driver Code
    public static void main(String args[]) {
        ArrayList<String> arr = new ArrayList<String>();

        arr.add("abcd");
        arr.add("derg");
        arr.add("erty");

        // Count of isograms in String array arr[]
        System.out.println(countIsograms(arr));
    }
}

// This code is contributed by gfgking
```

## 蟒蛇 3

```
# Function to check
# if a string is an isogram
def isIsogram(s):

    # Loop to check
    # if string is isogram or not
    freq = [0]*(26)
    for c in s:
        freq[ord(c) - ord('a')] += 1
        if (freq[ord(c) - ord('a')] > 1):
            return False

    return True

# Function to count the number of isograms
def countIsograms(arr):
    ans = 0

    # Loop to iterate the string array
    for x in arr:
        if (isIsogram(x)):
            ans += 1

    return ans

# Driver Code
if __name__ == "__main__":

    arr = ["abcd", "derg", "erty"]

    # Count of isograms in string array arr[]
    print(countIsograms(arr))

    # This code is contributed by ukasp.
```

## C#

```
// C# program for the above approach
using System;
using System.Collections;

class GFG
{

// Function to check
// if a string is an isogram
static bool isIsogram(string s)
{

    // Loop to check
    // if string is isogram or not
    int []freq = new int[26];
    for(int i = 0; i < 26; i++) {
        freq[i] = 0;
    }

    foreach (char c in s) {
        freq++;
        if (freq > 1) {
            return false;
        }
    }
    return true;
}

// Function to count the number of isograms
static int countIsograms(ArrayList arr)
{
    int ans = 0;

    // Loop to iterate the string array
    foreach (string x in arr) {
        if (isIsogram(x)) {
            ans++;
        }
    }
    return ans;
}

// Driver Code
public static void Main()
{
    ArrayList arr = new ArrayList();

    arr.Add("abcd");
    arr.Add("derg");
    arr.Add("erty");

    // Count of isograms in string array arr[]
    Console.WriteLine(countIsograms(arr));
}
}

// This code is contributed by Samim Hossain Mondal.
```

## java 描述语言

```
<script>

    // Function to check
    // if a string is an isogram
    const isIsogram = (s) => {

        // Loop to check
        // if string is isogram or not
        let freq = new Array(26).fill(0);
        for (let c in s) {
            freq[s.charCodeAt(c) - "0".charCodeAt(0)]++;
            if (freq > 1) {
                return false;
            }
        }
        return true;
    }

    // Function to count the number of isograms
    const countIsograms = (arr) => {
        let ans = 0;

        // Loop to iterate the string array
        for (let x in arr) {
            if (isIsogram(x)) {
                ans++;
            }
        }
        return ans;
    }

    // Driver Code
    let arr = ["abcd", "derg", "erty"];

    // Count of isograms in string array arr[]
    document.write(countIsograms(arr));

    // This code is contributed by rakeshsahni

</script>
```

**Output**

```
3
```

**时间复杂度:** O(N*M)，其中 N 是数组的大小，M 是最长字符串的大小
T3】辅助空间: O(1)
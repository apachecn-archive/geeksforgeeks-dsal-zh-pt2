# 第一个数组中小于第二个数组中每个字符串的字符串数

> 原文:[https://www . geesforgeks . org/第一个数组中的字符串数小于第二个数组中的每个字符串数/](https://www.geeksforgeeks.org/count-of-strings-in-the-first-array-which-are-smaller-than-every-string-in-the-second-array/)

给定两个数组 **A[]** 和 **B[]** ，分别由 **N** 和 **M** 串组成。如果 **S1** 中最小字符的出现频率小于 **S2** 中最小字符的出现频率，则称字符串 **S1** 小于字符串 **S2** 。任务是计算每一个 **i** 的 **A[]** 中小于 **B[i]** 的弦数。

**示例:**

> **输入:**A[]= {“AAA”、“aa”、“BDC”}，B[]= {“cccccch”、“cccd”}
> **输出:**3 2
> “cccccch”最小字符的频率为 4，A[]中的所有字符串
> 最小字符的频率均小于 4。
> “cccd”的最小字符频率为 3，只有“aa”和“BDC”
> 的最小字符频率小于 3。
> 
> **输入:**A[]= {“abca”、“jji”}，B[]= {“jhkki”、“aaaa”、“极客”}
> T3】输出: 0 2 1

一种**天真的**方法是取 **B[]** 中的每一根弦，然后计算 **A[]** 中满足条件的弦数。
一种有效的**方法是使用[二分搜索法](https://www.geeksforgeeks.org/binary-search/)和如下所述的一些预先计算来解决它:**

*   首先统计每个字符串最小字符的出现频率，并存储在[向量](https://www.geeksforgeeks.org/vector-in-cpp-stl/) / [数组](https://www.geeksforgeeks.org/array-data-structure/)中。
*   按升序对向量/数组进行排序。
*   现在对于 **B[i]** 中的每个字符串，找到最小字符的频率。
*   使用 C++中的[下界](https://www.geeksforgeeks.org/upper_bound-and-lower_bound-for-vector-in-cpp-stl/)函数，或者在向量/数组中做一个[二分搜索法](https://www.geeksforgeeks.org/binary-search/)，为每个 **B[i]** 找到频率小于最小字符频率的数字计数。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;
#define MAX 26
// Function to count the number of smaller
// strings in A[] for every string in B[]
vector<int> findCount(string a[], string b[], int n, int m)
{

    // Count the frequency of all characters
    int freq[MAX] = { 0 };

    vector<int> smallestFreq;

    // Iterate for all possible strings in A[]
    for (int i = 0; i < n; i++) {
        string s = a[i];
        memset(freq, 0, sizeof freq);

        // Increase the frequency of every character
        for (int j = 0; j < s.size(); j++) {
            freq[s[j] - 'a']++;
        }

        // Check for the smallest character's frequency
        for (int j = 0; j < MAX; j++) {

            // Get the smallest character frequency
            if (freq[j]) {

                // Insert it in the vector
                smallestFreq.push_back(freq[j]);
                break;
            }
        }
    }

    // Sort the count of all the frequency of the smallest
    // character in every string
    sort(smallestFreq.begin(), smallestFreq.end());

    vector<int> ans;

    // Iterate for every string in B[]
    for (int i = 0; i < m; i++) {
        string s = b[i];

        // Hash set every frequency 0
        memset(freq, 0, sizeof freq);

        // Count the frequency of every character
        for (int j = 0; j < s.size(); j++) {
            freq[s[j] - 'a']++;
        }

        int frequency = 0;

        // Find the frequency of the smallest character
        for (int j = 0; j < MAX; j++) {
            if (freq[j]) {
                frequency = freq[j];
                break;
            }
        }

        // Count the number of strings in A[]
        // which has the frequency of the smaller
        // character less than the frequency of the
        // smaller character of the string in B[]
        int ind = lower_bound(smallestFreq.begin(),
                              smallestFreq.end(), frequency)
                  - smallestFreq.begin();

        // Store the answer
        ans.push_back(ind);
    }

    return ans;
}

// Function to print the answer
void printAnswer(string a[], string b[], int n, int m)
{

    // Get the answer
    vector<int> ans = findCount(a, b, n, m);

    // Print the number of strings
    // for every answer
    for (auto it : ans) {
        cout << it << " ";
    }
}

// Driver code
int main()
{
    string A[] = { "aaa", "aa", "bdc" };
    string B[] = { "cccch", "cccd" };
    int n = sizeof(A) / sizeof(A[0]);
    int m = sizeof(B) / sizeof(B[0]);

    printAnswer(A, B, n, m);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;
class GFG
{
    static int MAX = 26;

    // Function to count the number of smaller
    // strings in A[] for every String in B[]
    static Vector<Integer> findCount(String a[],
                                     String b[],
                                     int n, int m)
    {

        // Count the frequency of all characters
        int []freq = new int[MAX];

        Vector<Integer> smallestFreq = new Vector<Integer>();

        // Iterate for all possible strings in A[]
        for (int i = 0; i < n; i++)
        {
            String s = a[i];
            Arrays.fill(freq, 0);

            // Increase the frequency of every character
            for (int j = 0; j < s.length(); j++)
            {
                freq[s.charAt(j) - 'a']++;
            }

            // Check for the smallest character's frequency
            for (int j = 0; j < MAX; j++)
            {

                // Get the smallest character frequency
                if (freq[j] > 0)
                {

                    // Insert it in the vector
                    smallestFreq.add(freq[j]);
                    break;
                }
            }
        }

        // Sort the count of all the frequency of
        // the smallest character in every string
        Collections.sort(smallestFreq);

        Vector<Integer> ans = new Vector<Integer>();

        // Iterate for every String in B[]
        for (int i = 0; i < m; i++)
        {
            String s = b[i];

            // Hash set every frequency 0
            Arrays.fill(freq, 0);

            // Count the frequency of every character
            for (int j = 0; j < s.length(); j++)
            {
                freq[s.charAt(j) - 'a']++;
            }

            int frequency = 0;

            // Find the frequency of the smallest character
            for (int j = 0; j < MAX; j++)
            {
                if (freq[j] > 0)
                {
                    frequency = freq[j];
                    break;
                }
            }

            // Count the number of strings in A[]
            // which has the frequency of the smaller
            // character less than the frequency of the
            // smaller character of the String in B[]
            int [] array = new int[smallestFreq.size()];
            int k = 0;
            for(Integer val:smallestFreq)
            {
                array[k] = val;
                k++;
            }

            int ind = lower_bound(array, 0,
                                  smallestFreq.size(),
                                  frequency);

            // Store the answer
            ans.add(ind);
        }
        return ans;
    }

    static int lower_bound(int[] a, int low,
                           int high, int element)
    {
        while(low < high)
        {
            int middle = low + (high - low) / 2;
            if(element > a[middle])
                low = middle + 1;
            else
                high = middle;
        }
        return low;
    }

    // Function to print the answer
    static void printAnswer(String a[], String b[],
                            int n, int m)
    {

        // Get the answer
        Vector<Integer> ans = findCount(a, b, n, m);

        // Print the number of strings
        // for every answer
        for (Integer it : ans)
        {
            System.out.print(it + " ");
        }
    }

    // Driver code
    public static void main(String[] args)
    {
        String A[] = { "aaa", "aa", "bdc" };
        String B[] = { "cccch", "cccd" };
        int n = A.length;
        int m = B.length;

        printAnswer(A, B, n, m);
    }
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation of the approach
from bisect import bisect_left as lower_bound

MAX = 26

# Function to count the number of smaller
# strings in A for every in B
def findCount(a, b, n, m):

    # Count the frequency of all characters
    freq=[0 for i in range(MAX)]

    smallestFreq=[]

    # Iterate for all possible strings in A
    for i in range(n):
        s = a[i]

        for i in range(MAX):
            freq[i]=0

        # Increase the frequency of every character
        for j in range(len(s)):
            freq[ord(s[j]) - ord('a')]+= 1

        # Check for the smallest character's frequency
        for j in range(MAX):

            # Get the smallest character frequency
            if (freq[j]):

                # Insert it in the vector
                smallestFreq.append(freq[j])
                break

    # Sort the count of all the frequency of the smallest
    # character in every string
    smallestFreq=sorted(smallestFreq)

    ans=[]

    # Iterate for every in B
    for i in range(m):
        s = b[i]

        # Hash set every frequency 0
        for i in range(MAX):
            freq[i]=0

        # Count the frequency of every character
        for j in range(len(s)):
            freq[ord(s[j]) - ord('a')]+= 1

        frequency = 0

        # Find the frequency of the smallest character
        for j in range(MAX):
            if (freq[j]):
                frequency = freq[j]
                break

        # Count the number of strings in A
        # which has the frequency of the smaller
        # character less than the frequency of the
        # smaller character of the in B
        ind = lower_bound(smallestFreq,frequency)

        # Store the answer
        ans.append(ind)

    return ans

# Function to print the answer
def printAnswer(a, b, n, m):

    # Get the answer
    ans = findCount(a, b, n, m)

    # Print the number of strings
    # for every answer
    for it in ans:
        print(it,end=" ")

# Driver code

A = ["aaa", "aa", "bdc"]
B = ["cccch", "cccd"]
n = len(A)
m = len(B)

printAnswer(A, B, n, m)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;   
public class GFG
{
    static int MAX = 26;

    // Function to count the number of smaller
    // strings in A[] for every String in B[]
    static List<int> findCount(String []a,
                                     String []b,
                                     int n, int m)
    {

        // Count the frequency of all characters
        int []freq = new int[MAX];

        List<int> smallestFreq = new List<int>();

        // Iterate for all possible strings in A[]
        for (int i = 0; i < n; i++)
        {
            String s = a[i];
            for (int l = 0; l < freq.Length; l++)
                freq[l]=0;

            // Increase the frequency of every character
            for (int j = 0; j < s.Length; j++)
            {
                freq[s[j] - 'a']++;
            }

            // Check for the smallest character's frequency
            for (int j = 0; j < MAX; j++)
            {

                // Get the smallest character frequency
                if (freq[j] > 0)
                {

                    // Insert it in the vector
                    smallestFreq.Add(freq[j]);
                    break;
                }
            }
        }

        // Sort the count of all the frequency of
        // the smallest character in every string
        smallestFreq.Sort();

        List<int> ans = new List<int>();

        // Iterate for every String in B[]
        for (int i = 0; i < m; i++)
        {
            String s = b[i];

            // Hash set every frequency 0
            for (int l = 0; l < freq.Length; l++)
                freq[l]=0;

            // Count the frequency of every character
            for (int j = 0; j < s.Length; j++)
            {
                freq[s[j] - 'a']++;
            }

            int frequency = 0;

            // Find the frequency of the smallest character
            for (int j = 0; j < MAX; j++)
            {
                if (freq[j] > 0)
                {
                    frequency = freq[j];
                    break;
                }
            }

            // Count the number of strings in A[]
            // which has the frequency of the smaller
            // character less than the frequency of the
            // smaller character of the String in B[]
            int [] array = new int[smallestFreq.Count];
            int k = 0;
            foreach (int val in smallestFreq)
            {
                array[k] = val;
                k++;
            }

            int ind = lower_bound(array, 0,
                                  smallestFreq.Count,
                                  frequency);

            // Store the answer
            ans.Add(ind);
        }
        return ans;
    }

    static int lower_bound(int[] a, int low,
                           int high, int element)
    {
        while(low < high)
        {
            int middle = low + (high - low) / 2;
            if(element > a[middle])
                low = middle + 1;
            else
                high = middle;
        }
        return low;
    }

    // Function to print the answer
    static void printAnswer(String []a, String []b,
                            int n, int m)
    {

        // Get the answer
        List<int> ans = findCount(a, b, n, m);

        // Print the number of strings
        // for every answer
        foreach (int it in ans)
        {
            Console.Write(it + " ");
        }
    }

    // Driver code
    public static void Main(String[] args)
    {
        String []A = { "aaa", "aa", "bdc" };
        String []B = { "cccch", "cccd" };
        int n = A.Length;
        int m = B.Length;

        printAnswer(A, B, n, m);
    }
}
// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>

// JavaScript implementation of the approach
const MAX = 26;

// Function to count the number of smaller
// strings in A[] for every String in B[]
function findCount(a, b, n, m)
{
    // Count the frequency of all characters
    var freq = new Array(MAX).fill(0);

    var smallestFreq = [];

    // Iterate for all possible strings in A[]
    for(var i = 0; i < n; i++)
    {
        var s = a[i];
        for(var l = 0; l < freq.length; l++)
            freq[l] = 0;

        // Increase the frequency of every character
        for(var j = 0; j < s.length; j++)
        {
            freq[s[j].charCodeAt(0) -
                  "a".charCodeAt(0)]++;
        }

        // Check for the smallest character's frequency
        for(var j = 0; j < MAX; j++)
        {

            // Get the smallest character frequency
            if (freq[j] > 0)
            {

                // Insert it in the vector
                smallestFreq.push(freq[j]);
                break;
            }
        }
    }

    // Sort the count of all the frequency of
    // the smallest character in every string
    smallestFreq.sort();

    var ans = [];

    // Iterate for every String in B[]
    for(var i = 0; i < m; i++)
    {
        var s = b[i];

        // Hash set every frequency 0
        for(var l = 0; l < freq.length; l++)
            freq[l] = 0;

        // Count the frequency of every character
        for(var j = 0; j < s.length; j++)
        {
            freq[s[j].charCodeAt(0) -
                  "a".charCodeAt(0)]++;
        }

        var frequency = 0;

        // Find the frequency of the smallest character
        for(var j = 0; j < MAX; j++)
        {
            if (freq[j] > 0)
            {
                frequency = freq[j];
                break;
            }
        }

        // Count the number of strings in A[]
        // which has the frequency of the smaller
        // character less than the frequency of the
        // smaller character of the String in B[]
        var array = new Array(smallestFreq.length).fill(0);
        var k = 0;

        for(const val of smallestFreq)
        {
            array[k] = val;
            k++;
        }

        var ind = lower_bound(
            array, 0, smallestFreq.length, frequency);

        // Store the answer
        ans.push(ind);
    }
    return ans;
}

function lower_bound(a, low, high, element)
{
    while (low < high)
    {
        var middle = low + parseInt((high - low) / 2);
        if (element > a[middle])
            low = middle + 1;
        else
            high = middle;
    }
    return low;
}

// Function to print the answer
function printAnswer(a, b, n, m)
{
    // Get the answer
    var ans = findCount(a, b, n, m);

    // Print the number of strings
    // for every answer
    for(const it of ans)
    {
        document.write(it + " ");
    }
}

// Driver code
var A = [ "aaa", "aa", "bdc" ];
var B = [ "cccch", "cccd" ];
var n = A.length;
var m = B.length;

printAnswer(A, B, n, m);

// This code is contributed by rdtank

</script>
```

**Output:** 

```
3 2
```
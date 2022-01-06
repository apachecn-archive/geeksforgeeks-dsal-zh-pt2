# 对一个数组中至少有一个公共数字的对进行计数

> 原文:[https://www . geesforgeks . org/count-pairs-array-至少一位数-common/](https://www.geeksforgeeks.org/count-pairs-array-least-one-digit-common/)

给定一组 N 个数字。找出 I 和 j 对的数量，使得 i < j and A <sub>i</sub> 和 A <sub>j</sub> 至少有一个公共数字(例如(11，19)有 1 个公共数字，但(36，48)没有公共数字)

**示例:**

> **输入:** A[] = { 10，12，24 }
> **输出:** 2
> **解释:**两个有效对是(10，12)和(12，24)，它们至少有一个数字是相同的

**方法 1(蛮力)**解决这个问题的一个简单方法就是运行两个嵌套循环，并考虑所有可能的对。我们可以通过提取第一个数字的每个数字，并尝试在提取的第二个数字中找到它，来检查这两个数字是否至少有一个公共数字。如果我们简单地将它们转换成字符串，任务会变得容易得多。

下面是上述方法的实现:

## C++

```
// CPP Program to count pairs in an array
// with some common digit
#include <bits/stdc++.h>

using namespace std;

// Returns true if the pair is valid,
// otherwise false
bool checkValidPair(int num1, int num2)
{
    // converting integers to strings
    string s1 = to_string(num1);
    string s2 = to_string(num2);

    // Iterate over the strings and check
    // if a character in first string is also
    // present in second string, return true
    for (int i = 0; i < s1.size(); i++)
        for (int j = 0; j < s2.size(); j++)
            if (s1[i] == s2[j])
                return true;

    // No common digit found
    return false;
}

// Returns the number of valid pairs
int countPairs(int arr[], int n)
{
    int numberOfPairs = 0;

    // Iterate over all possible pairs
    for (int i = 0; i < n; i++)
        for (int j = i + 1; j < n; j++)
            if (checkValidPair(arr[i], arr[j]))
                numberOfPairs++;

    return numberOfPairs;
}

// Driver Code to test above functions
int main()
{
    int arr[] = { 10, 12, 24 };
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << countPairs(arr, n) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to count
// pairs in an array
// with some common digit
import java.io.*;

class GFG
{

    // Returns true if the pair
    // is valid, otherwise false
    static boolean checkValidPair(int num1,
                                  int num2)
    {
        // converting integers
        // to strings
        String s1 = Integer.toString(num1);
        String s2 = Integer.toString(num2);

        // Iterate over the strings
        // and check if a character
        // in first string is also
        // present in second string,
        // return true
        for (int i = 0; i < s1.length(); i++)
            for (int j = 0; j < s2.length(); j++)
                if (s1.charAt(i) == s2.charAt(j))
                    return true;

        // No common
        // digit found
        return false;
    }

    // Returns the number
    // of valid pairs
    static int countPairs(int []arr, int n)
    {
        int numberOfPairs = 0;

        // Iterate over all
        // possible pairs
        for (int i = 0; i < n; i++)
            for (int j = i + 1; j < n; j++)
                if (checkValidPair(arr[i], arr[j]))
                    numberOfPairs++;

        return numberOfPairs;
    }

    // Driver Code
    public static void main(String args[])
    {
        int []arr = new int[]{ 10, 12, 24 };
        int n = arr.length;
        System.out.print(countPairs(arr, n));
    }
}

// This code is contributed
// by manish shaw.
```

## 蟒蛇 3

```
# Python3 Program to count pairs in
# an array with some common digit

# Returns true if the pair is
# valid, otherwise false
def checkValidPair(num1, num2) :

    # converting integers to strings
    s1 = str(num1)
    s2 = str(num2)

    # Iterate over the strings and check if
    # a character in first string is also
    # present in second string, return true
    for i in range(len(s1)) :
        for j in range(len(s2)) :
            if (s1[i] == s2[j]) :
                return True;

    # No common digit found
    return False;

# Returns the number of valid pairs
def countPairs(arr, n) :

    numberOfPairs = 0

    # Iterate over all possible pairs
    for i in range(n) :
        for j in range(i + 1, n) :
            if (checkValidPair(arr[i], arr[j])) :
                numberOfPairs += 1

    return numberOfPairs

# Driver Code
if __name__ == "__main__" :
    arr = [ 10, 12, 24 ]
    n = len(arr)
    print(countPairs(arr, n))

# This code is contributed by Ryuga
```

## C#

```
// C# Program to count pairs in an array
// with some common digit
using System;

class GFG {

    // Returns true if the pair is valid,
    // otherwise false
    static bool checkValidPair(int num1, int num2)
    {
        // converting integers to strings
        string s1 = num1.ToString();
        string s2 = num2.ToString();

        // Iterate over the strings and check
        // if a character in first string is also
        // present in second string, return true
        for (int i = 0; i < s1.Length; i++)
            for (int j = 0; j < s2.Length; j++)
                if (s1[i] == s2[j])
                    return true;

        // No common digit found
        return false;
    }

    // Returns the number of valid pairs
    static int countPairs(int []arr, int n)
    {
        int numberOfPairs = 0;

        // Iterate over all possible pairs
        for (int i = 0; i < n; i++)
            for (int j = i + 1; j < n; j++)
                if (checkValidPair(arr[i], arr[j]))
                    numberOfPairs++;

        return numberOfPairs;
    }

    // Driver Code to test above functions
    static void Main()
    {
        int []arr = new int[]{ 10, 12, 24 };
        int n = arr.Length;
        Console.WriteLine(countPairs(arr, n));
    }
}

// This code is contributed by manish shaw.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program to count pairs in an array
// with some common digit

// Returns true if the pair is valid,
// otherwise false
function checkValidPair($num1, $num2)
{
    // converting integers to strings
    $s1 = (string)$num1;
    $s2 = (string)$num2;

    // Iterate over the strings and check
    // if a character in first string is also
    // present in second string, return true
    for ($i = 0; $i < strlen($s1); $i++)
        for ($j = 0; $j < strlen($s2); $j++)
            if ($s1[$i] == $s2[$j])
                return true;

    // No common digit found
    return false;
}

// Returns the number of valid pairs
function countPairs(&$arr, $n)
{
    $numberOfPairs = 0;

    // Iterate over all possible pairs
    for ($i = 0; $i < $n; $i++)
        for ($j = $i + 1; $j < $n; $j++)
            if (checkValidPair($arr[$i],
                               $arr[$j]))
                $numberOfPairs++;

    return $numberOfPairs;
}

// Driver Code
$arr = array(10, 12, 24 );
$n = sizeof($arr);
echo (countPairs($arr, $n));

// This code is contributed
// by Shivi_Aggarwal
?>
```

## java 描述语言

```
<script>

// Javascript Program to count pairs in an array
// with some common digit

// Returns true if the pair is valid,
// otherwise false
function checkValidPair(num1, num2)
{
    // converting integers to strings
    var s1 = num1.toString();
    var s2 = num2.toString();

    var i,j;
    // Iterate over the strings and check
    // if a character in first string is also
    // present in second string, return true
    for(i = 0; i < s1.length; i++)
        for(j = 0; j < s2.length; j++)
            if (s1[i] == s2[j])
                return true;

    // No common digit found
    return false;
}

// Returns the number of valid pairs
function countPairs(arr, n)
{
    var numberOfPairs = 0;

    // Iterate over all possible pairs
    for(i = 0; i < n; i++)
      for(j = i + 1; j < n; j++)
         if(checkValidPair(arr[i], arr[j]))
            numberOfPairs++;

    return numberOfPairs;
}

// Driver Code to test above functions
    var arr = [10, 12, 24];
    var n = arr.length;;
    document.write(countPairs(arr, n));

</script>
```

**Output**

```
2
```

**时间复杂度:** O(N <sup>2</sup> )其中 N 是数组的大小。

**方法 2(位屏蔽):**解决这个问题的有效方法是为特定数字中出现的每个数字创建位屏蔽。因此，如果我们有一个 111111111111 的掩码，那么数字中的每个数字。

```
Digits -  0  1  2  3  4  5  6  7  8  9
          |  |  |  |  |  |  |  |  |  |
Mask   -  1  1  1  1  1  1  1  1  1  1 

Here 1 denotes that the corresponding ith digit is set. 
For e.g. 1235 can be represented as
Digits -         0  1  2  3  4  5  6  7  8  9
                 |  |  |  |  |  |  |  |  |  |
Mask for 1235 -  0  1  1  1  0  1  0  0  0  0
```

现在我们只需要提取一个数字的每个数字，并设置相应的位 **(1 < < i <sup>th</sup> 数字)**并将整个数字存储为掩码。仔细分析表明，掩码的最大值是十进制的 1023(包含从 0 到 9 的所有数字)。由于同一组数字可以存在于多个数字中，因此我们需要维护一个频率数组来存储掩码值的计数。

> 让两个掩码 I 和 j 的频率分别为 freq <sub>i</sub> 和 freq <sub>j</sub> ，
> 如果(I 和 j)返回 true，则意味着 i <sub>th</sub> 和 j <sub>th</sub> 掩码包含至少一个公共设置位，这又意味着构建这些掩码的数字也包含一个公共数字
> ，然后，
> 递增答案
> ans+= freq<sub>I</sub>* freq<sub>= j]
> ans+=(freq<sub>I</sub>*(freq<sub>I</sub>–1))/2[如果 j == i ]</sub>

下面是这种有效方法的实现:

## C++

```
// CPP Program to count pairs in an array with
// some common digit
#include <bits/stdc++.h>
using namespace std;

// This function calculates the mask frequencies
// for every present in the array
void calculateMaskFrequencies(int arr[], int n,
                 unordered_map<int, int>& freq)
{
    // Iterate over the array
    for (int i = 0; i < n; i++) {

        int num = arr[i];

        // Creating an empty mask
        int mask = 0;

        // Extracting every digit of the number
        // and updating corresponding bit in the
        // mask
        while (num > 0) {
            mask = mask | (1 << (num % 10));
            num /= 10;
        }

        // Update the frequency array
        freq[mask]++;
    }
}

// Function return the number of valid pairs
int countPairs(int arr[], int n)
{
    // Store the mask frequencies
    unordered_map<int, int> freq;

    calculateMaskFrequencies(arr, n, freq);

    long long int numberOfPairs = 0;

    // Considering every possible pair of masks
    // and calculate pairs according to their
    // frequencies
    for (int i = 0; i < 1024; i++) {
        numberOfPairs += (freq[i] * (freq[i] - 1)) / 2;
        for (int j = i + 1; j < 1024; j++) {

            // if it contains a common digit
            if (i & j)
                numberOfPairs += (freq[i] * freq[j]);
        }
    }
    return numberOfPairs;
}

// Driver Code to test above functions
int main()
{
    int arr[] = { 10, 12, 24 };
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << countPairs(arr, n) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to count pairs in an array with
// some common digit
import java.io.*;
import java.util.*;
class GFG
{

  // Store the mask frequencies
  public static Map<Integer, Integer> freq = new HashMap<Integer, Integer>();

  // This function calculates the mask frequencies
  // for every present in the array
  public static void calculateMaskFrequencies(int[] arr,int n)
  {

    // Iterate over the array
    for(int i = 0; i < n; i++)
    {
      int num = arr[i];

      // Creating an empty mask
      int mask = 0;

      // Extracting every digit of the number
      // and updating corresponding bit in the
      // mask
      while(num > 0)
      {
        mask = mask | (1 << (num % 10));
        num /= 10;
      }

      // Update the frequency array
      if(freq.containsKey(mask))
      {
        freq.put(new Integer(mask), freq.get(mask) + 1);
      }
      else
      {
        freq.put(new Integer(mask), 1);
      }
    }
  }

  // Function return the number of valid pairs
  public static int countPairs(int[] arr, int n)
  {
    calculateMaskFrequencies(arr, n);
    int numberOfPairs = 0;

    // Considering every possible pair of masks
    // and calculate pairs according to their
    // frequencies
    for(int i = 0; i < 1024; i++)
    {
      int x = 0;
      if(freq.containsKey(i))
      {
        x = freq.get(i);

      }
      numberOfPairs += ((x) * (x - 1)) / 2;
      for(int j = i + 1; j < 1024; j++)
      {
        int y = 0;

        // if it contains a common digit
        if((i & j) != 0)
        {
          if(freq.containsKey(j))
          {
            y = freq.get(j);
          }
          numberOfPairs += x * y;
        }
      }
    }
    return numberOfPairs;
  }

  // Driver Code
  public static void main (String[] args)
  {
    int[] arr = {10, 12, 24};
    int n = arr.length;       
    System.out.println(countPairs(arr, n));
  }
}

// This code is contributed by avanitrachhadiya2155
```

## 蟒蛇 3

```
# Python3 Program to count pairs in an array
# with some common digit

# This function calculates the mask frequencies
# for every present in the array
def calculateMaskFrequencies(arr, n, freq):

    # Iterate over the array
    for i in range(n):

        num = arr[i]

        # Creating an empty mask
        mask = 0

        # Extracting every digit of the number
        # and updating corresponding bit in the
        # mask
        while (num > 0):
            mask = mask | (1 << (num % 10))
            num //= 10

        # Update the frequency array
        freq[mask] = freq.get(mask, 0) + 1

# Function return the number of valid pairs
def countPairs(arr, n):

    # Store the mask frequencies
    freq = dict()

    calculateMaskFrequencies(arr, n, freq)

    numberOfPairs = 0

    # Considering every possible pair of masks
    # and calculate pairs according to their
    # frequencies
    for i in range(1024):

        x = 0

        if i in freq.keys():
            x = freq[i]

        numberOfPairs += (x * (x - 1)) // 2

        for j in range(i + 1, 1024):

            y = 0

            if j in freq.keys():
                y = freq[j]

            # if it contains a common digit
            if (i & j):
                numberOfPairs += (x * y)

    return numberOfPairs

# Driver Code
arr = [10, 12, 24]
n = len(arr)
print(countPairs(arr, n))

# This code is contributed by mohit kumar
```

## C#

```
// C# Program to count pairs in an array with
// some common digit
using System;
using System.Collections.Generic;

public class GFG
{

    // Store the mask frequencies
    static Dictionary<int, int> freq =  new Dictionary<int, int>();

    // This function calculates the mask frequencies
    // for every present in the array
    public static void calculateMaskFrequencies(int[] arr,int n)
    {

        // Iterate over the array
        for(int i = 0; i < n; i++)
        {
            int num = arr[i];

            // Creating an empty mask
            int mask = 0;

            // Extracting every digit of the number
            // and updating corresponding bit in the
            // mask
            while(num > 0)
            {
                mask = mask | (1 << (num % 10));
                num /= 10;
            }

            // Update the frequency array
            if(freq.ContainsKey(mask))
            {
                freq[mask]++;
            }
            else
            {
                freq.Add(mask, 1);
            }
        }

    }
    public static int countPairs(int[] arr, int n)
    {
        calculateMaskFrequencies(arr, n);
        int numberOfPairs = 0;

        // Considering every possible pair of masks
        // and calculate pairs according to their
        // frequencies
        for(int i = 0; i < 1024; i++)
        {
            int x = 0;
            if(freq.ContainsKey(i))
            {
                x = freq[i];

            }
            numberOfPairs += ((x) * (x - 1)) / 2;
            for(int j = i + 1; j < 1024; j++)
            {
                int y = 0;

                // if it contains a common digit
                if((i & j) != 0)
                {  
                    if(freq.ContainsKey(j))
                    {
                        y = freq[j];
                    }
                    numberOfPairs += x * y;
                }
            }
        }
        return numberOfPairs;

    }

    // Driver Code
    static public void Main ()
    {
        int[] arr = {10, 12, 24};
        int n = arr.Length;       
        Console.WriteLine(countPairs(arr, n));
    }
}

// This code is contributed by rag2127
```

## java 描述语言

```
<script>
// Javascript Program to count pairs in an array with
// some common digit

// Store the mask frequencies
let freq = new Map();

// This function calculates the mask frequencies
  // for every present in the array
function calculateMaskFrequencies(arr,n)
{
    // Iterate over the array
    for(let i = 0; i < n; i++)
    {
      let num = arr[i];

      // Creating an empty mask
      let mask = 0;

      // Extracting every digit of the number
      // and updating corresponding bit in the
      // mask
      while(num > 0)
      {
        mask = mask | (1 << (num % 10));
        num = Math.floor(num/10);
      }

      // Update the frequency array
      if(freq.has(mask))
      {
        freq.set((mask), freq.get(mask) + 1);
      }
      else
      {
        freq.set((mask), 1);
      }
    }
}

// Function return the number of valid pairs
function countPairs(arr,n)
{
    calculateMaskFrequencies(arr, n);
    let numberOfPairs = 0;

    // Considering every possible pair of masks
    // and calculate pairs according to their
    // frequencies
    for(let i = 0; i < 1024; i++)
    {
      let x = 0;
      if(freq.has(i))
      {
        x = freq.get(i);

      }
      numberOfPairs += Math.floor((x) * (x - 1)) / 2;
      for(let j = i + 1; j < 1024; j++)
      {
        let y = 0;

        // if it contains a common digit
        if((i & j) != 0)
        {
          if(freq.has(j))
          {
            y = freq.get(j);
          }
          numberOfPairs += x * y;
        }
      }
    }
    return numberOfPairs;
}

// Driver Code
let arr=[10, 12, 24];
let n = arr.length;
document.write(countPairs(arr, n));

// This code is contributed by unknown2108
</script>
```

**Output**

```
2
```

**时间复杂度:** O(N + 1024 * 1024)，其中 N 为数组的大小。